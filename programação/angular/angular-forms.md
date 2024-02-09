<div align='justify'>

## FORMULÁRIOS DO ANGULAR

>[angular.io](https://angular.io/guide/reactive-forms)
>
>02 Fevereiro 2024

#### REATIVOS

Os formulários reativos podem ser acessados de forma síncrona. Cada alteração em um campo retorna um novo estado do formulário, isso permite uma maior integridade dos dados, garantindo que eles são consistentes.

#### FORMCONTROL

É a unidade básica de controle dos inputs, e está diretamente vinculado a eles.

Para criar um formControl:

```ts
fc = new FormControl('');
```
Para acessar seu valor:
```ts
fc.value;
```
Para setar um valor:
```ts
fc.setValue('Exemplo');
```

#### FORMGROUP
O formGroup contém vários formControls. Nada mais é que um formulário que agrupa vários tipos diferentes de formControls. O FormGroup também permite detectar as alterações de um único campo (FormControl) e emitir um novo status.

Para criar um formGroup:

```ts
fg = new FormGroup({
   firstName: new FormControl(''),
   lastName: new FormControl(''),
});
```
Exemplo em HTML:

```html
<form [formGroup]="fg" (ngSubmit)="onSubmit()">
   <label for="first-name">First Name: </label>
   <input id="first-name" type="text" formControlName="firstName">
   <label for="first-name">First Name: </label>
   <input id="first-name" type="text" formControlName="firstName">
   <button type="submit" [disabled]="!fb.valid">Submit</button>
</form>
```

Para colocar um formGroup dentro de outro formGroup:
- typescript

```ts
fg = new FormGroup({
   firstName: new FormControl(''),
   lastName: new FormControl(''),
   address: new FormGroup({
        street: new FormControl(''),
        city: bew FormControl(''),
   }),
});
```

- html
```html
<div formGroupName="address">
   <h2>Address</h2>
   <label for="street">Street: </label>
   <input id="street" type="text" formControlName="street">
   <label for="city">City: </label>
   <input id="city" type="text" formControlName="city">
</div>
```

Update em vários campos ao mesmo tempo:
```ts
this.fg.patchValue({
   firstName: 'Nancy',
   address: {
       street: '123 Drew Street',
   },
});
```
#### FORMBUILDER

Para tornar a construção de formulários menos repetitiva, e sem precisar instanciar novos formcontrols o tempo todo, o angular fornece o formBuilder, um serviço que acelera a construção de formulários reativos. 

Ele possui três apenas serviço: `control()` `group()` e `array()`.

Como o FormBuilder é um serviço, é necessário importá-lo no construtor para ser injetado:

constructor(private formBuilder: FormBuilder) {}

Depois é possível construir um formGroup da seguinte forma:

```ts
fg = this.formBuilder.group({
   firstName: [''],
   lastName: [''],
   address: this.formBuilder.group({
       street: [''],
       city: [''],
   }),
});
```
#### VALIDATORS

A validação é usada para garantir que a entrada do usuário esteja completa e correta.

Por exemplo, para adicionar uma validação no campo firstName:

```ts
fg = this.formBuilder.group({
   firstName: ['', Validators.required],
   lastName: [''],
   address: this.formBuilder.group({
       street: [''],
       city: [''],
   }),
});
```

Para checar o status do formulário


```ts
fg.status
```
Automaticamente o botão de submit vinculado ao formulário será desativado.

#### FORMARRAY

Quando você quer um formulário dinâmico, ou seja uma quantidade desconhecida de campos (você não sabe antecipadamente), e as vezes sem nem saber o nome desses formControls, é uma boa opção utilizar o formArray.

É comum utilizar um método getter para recuperar o valor do formArray, porque como ele é criado dentro de um formGroup, nós não teriamos acesso direto a variável fora desse escopo (do escopo do formGroup).

Para utilizar o formArray (aliases):

```ts
fg = this.formBuilder.group({
   firstName: ['', Validators.required],
   lastName: [''],
   address: this.formBuilder.group({
       street: [''],
       city: [''],
   }),
   aliases:
       this.formBuilder.array([this.formBuilder.control('')]),
});
```

Para poder acessar o formArray, é necessário criar um getter:
```ts
get aliases() {
   return this.fg.get('aliases') as FormArray;
}
```
Para inserir um novo formControl dentro do formArray:
```ts
addAlias() {
   this.aliases.push(this.formBuilder.control(''));
}
```
Por fim, para utilizar um formArray dinamicamente em um HTML:

```html
<div formArrayName="aliases">
   <h2>Aliases</h2>
   <button type="button" (click)="addAlias()">+ Add another alias</button>
   <div *ngFor="let alias of aliases.controls; let i=index">
       <label for="alias-{{ i }}">Alias:</label>
       <input id="alias-{{ i }}" type="text" [formControlName]="i">
   </div>
</div>
```

</div>