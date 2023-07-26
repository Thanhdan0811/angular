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

# Submit 

```
  <form class="form" #form="ngForm" (ngSubmit)="onSubmitForm(form, $event)" [ngFormOptions]="{updateOn: 'blur'}">
  </form>

``` 

- ngForm là tham chiếu đến directive ngForm (xem exportAs của đirective.)

# group input 

```
        <div ngModelGroup="address">
            <div class="form-field">
                <label for="name">Address Number 1</label>
                <input [(ngModel)]="userInfo.addressNumber1" name="addressNumber1" type="text" id="addressNumber1">
            </div>
            <div class="form-field">
                <label for="name">Address Number 2</label>
                <input [(ngModel)]="userInfo.addressNumber2" name="addressNumber2" type="text" id="addressNumber2">
            </div>
        </div>


  => {
    "first-name": "",
    "last-name": "",
    "address": {
        "addressNumber1": "",
        "addressNumber2": ""
    }
}

```

- Để tạo group input ta dùng directive : ngModelGroup="anyName" 
- Chú ý là phải nằm trong form.

# Control Statuses
- là các class biểu hiện trạng thái của form-control. 
- class ng-untouched và ng-touched : khi focus vào và ko focus nữa.
- class ng-pristine (chưa thay đổi gì) và ng-dirty (value của input đã bị thay đổi.)
- class ng-valid sẽ hiện khi value pass validator, ng-invalid sẽ ngược lại.
- class ng-pending khi mà có async validator.
- class ng-submitted ở form khi mà form đã được click submit.
- state của form sẽ phụ thuộc vào state của child và child group.
  * Ví dụ : khi mà 1 chilđ input có touched thì form cũng sẽ có class ng-touched.
- tương tự với group form control, chỉ cần 1 child có status thì cha cũng sẽ cập nhât.

- style css mẫu : 

```
  .ng-valid.ng-dirty:not([ngModelGroup]):not(form) {  .... }

```


