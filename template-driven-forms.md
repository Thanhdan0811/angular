# Template-Driven Forms
- Muốn dùng cần import : FormsModule
- FormsModule sẽ thêm vào các directives cho form tag, 
- ta có thể ko áp directives cho form tag bằng cách thêm vào atrribute là : ngNoForm

```
selector : form:not([ngNoForm]):not([formGroup]),ng-form,[ngForm]

```

# ngFomOptions and ngModelOptions

```
  <form class="form" [ngFormOptions]="{updateOn: 'blur'}">
      <input 
          [(ngModel)]="userInfo.firstName" 
          [ngModelOptions]="{
              name: 'first-name',
              updateOn: 'change'
          }"
          name="first-name" 
          type="text" 
          id="name"
      >
  </form>


```
- ngForm sẽ được get ở form tag.
- ngModelOptions sẽ nhận vào 1 object có 3 properties : name (như property name của input tag) , updateOn (change, blur, submit), standalone (true, false)
- ngFormOptions sẽ nhận vào 1 object chỉ có 11 property là : updateOn (change, blur, submit) sẽ update value khi ứng với tên event được chọn.

# Standalone ngModel
- khi 1 ngModelOptions có property là standalone : true 
- Thì ngModel sẽ không được register trong ngForm.
- Trường hợp dùng standalone : nhớ khi nào cần thì dùng :v
- Note : khi ta dùng 1 ngModel bên ngoài form thì nó sẽ được xem như là standalone ngModel.
