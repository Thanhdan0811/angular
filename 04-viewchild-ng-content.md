1. ViewChild
@ViewChild(Reference || TypeComponent, {read: Type, static: true | false}) variable : Type = initialvalue;
Read : Type => xác định type cần thao tác NativeElement or HTMLElement.
Static : true => sẽ có thể lấy reference ở ngOnInit
Ta có thể dùng lifeCycle ngAfterViewInit để lấy reference. Ở lifeCycle này ko nên chỉnh sửa value nếu ko sẽ lỗi.
2. ViewChildren
@ViewChildren(TypeComponent || Reference, {read: ElementRef}) vars : QueryList<TypeCOmponent>;
QueryList chứa tất cả thông tin về list càn query.
Read sẽ trả về type cần đọc, html hay là component.

3. Content Projection - ng-content.
Truyền nội dung giữa 2 tag vào component children , được gán vào tag ng-content trong component children.
<ng-content select=”selector (h1, .class…)”></ng-content>
<child-component> <h1 selector or just h1>Hello</h1>  </child-component>
<ng-content></ng-content> đăt ở cuối để hiển thị ng-content mặc định.
3.1 Content Child Decorator : 
@ContentChild(reference or selectType, {read: ElementRef})  var : Type;
Sẽ chỉ lấy tham chiếu đến content được truyền vào ở <ng-content></ng-content>
 Tương tự có thể lấy trong ngAfterViewInit()

3.2 @ContentChildren() 
=> Tương tự như @ContenChild() vars: QueryList<ElementRef>; nhưng là sẽ lấy nhiều phần tử giống nhau.


4. Angular Template.

================
<ng-template  #blankImage>
	<p>No Images is available yet</p>
</ng-template>

<ng-content select=”course-image” *ngIf=”course.imageUrl; else blankImage” ></ng-content>
=================

Ng-template sẽ ko hiện ở DOM.

Cách tạo biến chỉ hiển thị triong ng-template.

=================

<ng-template #blankImage let-courseName=”description”>
	<p>  {{ courseName }} has no Image yet </p>
 </ng-template>

<ng-container *ngTemplateOutlet=”blankImage; context: { description: course.description }” > </ng-container>

=================

Ng-container sẽ nhận template vào và truyền description vào với tên là courseName.

Angular template còn có thể được xem như là Component Inputs.





=================

Component cha : 

<ng-template #blankImage let-courseName=”description”>
	<p>  {{ courseName }} has no Image yet </p>
 </ng-template>

<component-child  [noImageTpl]=”blankImage”></component-child>

Trong component-child : 

@Input() noImageTpl : TemplateRef<any>;

<ng-content select=”course-image” *ngIf=”course.url; else noImage” ></ng-content>

 <ng-template #noImage >
	<ng-container *ngTemplateOutlet=”noImageTpl; context: { description :  course.description }” ></ng-container>
</ng-template>

=================
https://medium.com/12-developer-labors/why-we-cant-inject-teplaterref-into-a-directive-b4c50e2bb0a4
