angular, validator, validation

# Angular Validation


## Availabe Keywords

- valid
- invalid
- dirty
- pristine
- touched
- untouched


CSS classes automatically applied:
- ng-valid / ng-invalid
- ng-dirty / ng-pristine
- ng-toched / ng-untouched



#### Example in `Template Driven Form`:

`myComp.component.html`:
```html
<form #loginFomr="ngForm" (ngSubmit)="verify()">
    <label for="uName">User Name</label>
    <input 
        type="text"
        id="uName"
        [(ngModel)]="userName"
        name="userName"
        #uName="ngModel"
    >
    <!-- validation -->
    <div [hidden]="uName.valid || uName.pristine">
        User name is required
    </div> 
    <button type="submit">Login</button>
</form>
```
## Validation in Reactive Forms

`myComp.component.ts`
```ts
export class MyComp {
    myForm: FormGroup
    constructor(private fb: FormBuilder) {}
    @NgOnInit() {
        this.myForm = this.fb.group({
            name: ['', [
                Validators.required,
            ]],
            quantity: [1, [
                Validators.required,
                Validators.min(1),
                Validators.max(3)
            ]]
            number: ['', [
                Validators.required,
                Validators.pattern("[0-9]{3}")
            ]]
            address: this.fb.group({
                zip: [],
                city: []
            })
        })
    }
}
```

`myComp.component.html`
```html
<form [formGroup]="myForm" (ngSumbit)="verify()">
    <label>number</label>
    <input type="text" formControlName="number">
    <!-- validation -->
    <p *ngIf="myForm.controls['number'].errors![        
    required']">Required</p>

