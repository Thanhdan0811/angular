
# Suibject and BehaviorSubject.


# asyncSubject and ReplaySubject.

- AsyncSubject : only get lasst value emit after call complete.
```
const subject = new AsyncSubject();
const series$ = subject.asObservable();

series$.subscribe(val => console.log("first : ", val));

subject.next(1);
subject.next(2);
subject.next(3);

subject.complete();

setTimeout( () => {
    series$.subsribe(val => console.log("second : ", val));
} ,3000);

/*
=>   first : 3
      second : 3  
*/

```

- ReplaySubject : send all value had been emit. not link to observable completion
```
const subject = new ReplaySubject();
const series$ = subject.asObservable();

series$.subscribe(val => console.log("first : ", val));

subject.next(1);
subject.next(2);
subject.next(3);

// subject.complete();

setTimeout( () => {
    series$.subsribe(val => console.log("second : ", val));

    subject.next(4);

} ,3000);

/*
=>   first : 1
=>   first : 2
=>   first : 3
      second : 1  
      second : 2  
      second : 3
    first : 4
    second : 4
*/

```

# Store Service Design.
- Idea: Create a share service to store data from call api.
```
/// store.service.ts
@Injectable({
  provideIn: 'root'  
})
export class StoreService {

  private subject = new BehaviorSubject<Course[]>([]);

  courses$: Observable<Course[]> = this.subject.asObservable();
  
}


/// Home Component


constructor() {}

```

