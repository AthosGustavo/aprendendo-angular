# aprendendo-angular

<details>
  <summary>Montagem de ambiente</summary>
  
  # Montagem de ambietne
  *A montagem de ambiente foi feita com base no angular 14*
  
   - Comando para baixar a cli do angular `npm install -g @angular/cli@14.0.3`
   - Comando para criar um projeto `ng new nome-projeto`
   - Comando para habilitar o localhost `ng serve`
   - Comando para criar um componente com arquivos de css,ts e testes `ng generate component nomePasta/nomeComponente`

  `ng new my-app --no-standalone --routing --ssr=false`
  
</details>

<details>
  <summary>Escopo de classe e declaração de funções e variáveis</summary>

  # Escopo de classe e declaração de funções e variáveis

  ### Dicas
  
 - **Obs 1:Dentro do escopo global da classe, nao se usa `let`, `const` e `var` para declarar variáveis.
Os atributos da classe devem ser declarados semelhantes a forma que é declarado no Java e as variáveis com as palavras chaves devem ser declaradas dentro do escopo de uma função.**
   - O motivo disso se dar, porque o escopo da classe deve ser usado para declarar atributos que sejam da classe e esses atributos não podem ser declarados com essas palavras chaves.As palavras let,const e var servem para declarar valores apenas em escopo escopos locais.


  - **Obs 2:A palavra-chave `function` não pode ser usada para declarar métodos diretamente dentro de uma classe no TypeScript**
     - `Formas de declara um método em uma classe`
     - ```javascript
       // Forma clássica
       // Possíveis problemas ao usar this para referênciar atributos da classe
       class MyClass {
          myMethod(): void {
           console.log("Este é um método padrão");
          }
        }
       ```
     - ```javascript
       // Declarar métodos com arrow function garante que o this do método seja sempre vinculado à instância da classe

       class MyClass {
         myMethod = (): void => {
           console.log("Método declarado como arrow function");
        };
       }
       ```
  - **Obs 3:Ao declarar a função com a palavra `function` a palavra this perde o seu
  comportamento padrão, é como o this apontasse para dentro da função e não mais para classe.**

  - **Obs 4: Qualque método ou atributo que seja da classe e que está sendo acessado dentro de um método
da classe, deve ser usada a palavra `this`.**
  
</details>
<details>
  <summary>Método construtor</summary>

  # Método construtor

  ## Como usar o método construtor

  ### Usando o método construtor para instanciar classes e atribuir a uma propriedade da classe atual
  ```javascript
  export class MeuComponente {
    mensagem: string;

    constructor(servico: MeuServico) {
      // Aqui, 'servico' é uma instância do seu serviço MeuServico
      this.mensagem = servico.obterMensagem();
    }
  }
  ```
  ```javascript
  export class BotaoComponent {
    constructor(private httpClient: HttpClient){}
    chamaApi():void{
      this.httpClient
    }
  }
  ```

  ### Usando o método construtor para injeção de dependências
  
</details>

<details>
  <summary>Componentes</summary>

  # Componentes
  ## Criando um componente
   - Para criar um componente,basta executar o comando `ng generate component nomePasta/nomeComponente`
   - Serão criados um arquivo de css,html,arquivo de testes e o arquivo para lógica.
     ![Captura de tela de 2024-02-01 11-11-53](https://github.com/AthosGustavo/aprendendo-angular/assets/112649935/89ac442d-2af3-4266-9f02-a6a192dce39c)

  ### Arquivo input.component.component.ts
  ![Captura de tela de 2024-02-01 11-14-31](https://github.com/AthosGustavo/aprendendo-angular/assets/112649935/f4862d50-af40-47fc-a647-fc216b95ae66)

  #### @Component
   - Usado para configurar os atributos do componente

  #### selector
   - seletor angular usado para associar o componente a um elemento específico no template.
   - Ao incorporar este componente em um template, a tag usada seria `<app-input-component></app-input-component>`

  #### standalone
   - booleano que indica se o componente é independete ou se faz parte de um módulo mais amplo

  #### imports
   - lista de módulos que este componente pode importar

  #### templateUrl
   - caminho para o arquivo html do componente

  #### styleUrls
   - lista de caminhos para arquivos ou aquivo css do componente

  ### Passo a passo de como criar um componente
   - 1 - No arquivo input.component.html declare a tag html referente ao input
   - 2 - No arquivo app.component.html, declare o seletor que identifica o componente `<app-input></app-input>`
     
  ### Interpolação de dados
   - Interpolando variáveis em tags html
  ```javascript
  //interpolacao.component.html

  <p>Meu nome é: {{nome}}</p>
  ```
  ```javascript
  //interpolacao.component.ts

  import { Component } from '@angular/core';

  @Component({
    selector: 'app-inerpolacao',
    templateUrl: './inerpolacao.component.html',
    styleUrl: './inerpolacao.component.css'
  })
  export class InerpolacaoComponent {

    nome: string = 'Athos';
  }

  ```
  ```javascript
  //app.component.html
  
  <app-inerpolacao></app-inerpolacao>
  ```
  <details>
    <summary>Compartilhamento de dados</summary>

   # Compartilhamento de dados
   ### Passo a passo
  - 1- Uma propriedade `X` é declarada na classe filha com o decorator `@Input`
  - 2- Essa propriedade `X` é colocada no html do componente filho
  - 3- A propriedade recebe um valor externamente no componente pai
  - 4- No componente pai, declare a tag `selector` filho dentro da tag pai e passe os valores   `[propFilho]="valor"` 
  - 5- `@Input` decorator usado para definir que uma propriedade pode receber dados externos

  *EXEMPLO 2*
  - 1- Declara o dado a ser transmitido na classe pai
  - 2- Declara a variável  que ira receber o valor na classe na classe filho com o decorator @Input
  - 3- na tag do componente filho, faça a vinculação de propriedades `[propFilho]="propPai"`
  - 4- `@Input` decorator usado para definir que uma propriedade pode receber dados externos
  - 
  ```javascript
  // componente-pai.component.ts
  import { Component } from '@angular/core';

   @Component({
     selector: 'app-componente-pai',
    templateUrl: './componente-pai.component.html',
     styleUrls: ['./componente-pai.component.css']
   })
   export class ComponentePaiComponent {
     heranca: string = 'Dados herdados';
   }
   ```
   ```javascript
   // componente-filho.component.ts
   import { Component, Input } from '@angular/core';

  @Component({
     selector: 'app-componente-filho',
     templateUrl: './componente-filho.component.html',
     styleUrls: ['./componente-filho.component.css']
   })
   export class ComponenteFilhoComponent {
     @Input() dadosHerdados: string = '';
   }

   ```
   ```javascript
   <!-- componente-pai.component.html -->
   <app-componente-filho [dadosHerdados]="herança"></app-componente-filho>
   ```
    
    
  </details>
  
  <details>
    <summary>Eventos</summary>

  # Eventos

  #### click
   - A função é chamada na tag html
  *SINTAXE DE DECLARAÇÃO DE EVENTO*
  `<button (evento)="nomeFuncao()"></button>`
  

  ```javascript
  // botao.component.html
  <button (click)="btnFuncao">Clique</button>
  ```
  ```javascript
  // app.component.ts

  import { Component } from '@angular/core';

  @Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
  })
  export class AppComponent {
    mostrarElemento: boolean = true;

    btnFuncao():void{
      this.mostrarElemento = false;
    }
  }

  ```   
  ```javascript
  <!-- app.component.html -->
  <h1>Bem-vindo ao meu aplicativo Angular!</h1>

  <p *ngIf="mostrarElemento">Este elemento será exibido se mostrarElemento for verdadeiro.</p>
  ```
  
  </details>

  <details>
    <summary>Renderização</summary>
    
  # Renderização
  ### Renderização com ngFor
   - Renderizando listas
  
  ```javascript
  // app.component.ts

  import { Component } from '@angular/core';

  @Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
  })
  export class AppComponent {
    nomes=['athos','gustavo','fabricio'];
  }

  ```
  ```javascript
  <!-- app.component.html -->
  <h1>Meus nomes</h1>

  <ul>
    <li*ngFor="let nome of nomes">
      Nome:{{nome}}
    </li>
  </ul>
  ```
  
  ### Renderização condicional com ngIf
  #### Diretiva ngIf
   - Usada no Angular para exibir ou ocultar elementos HTML com base em uma expressão condicional.
   - ngIf adiciona e remove elementos do DOM com base em uma condicional
  ```javascript
  // app.component.ts

  import { Component } from '@angular/core';

  @Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
  })
  export class AppComponent {
    mostrarElemento: boolean = true;
  }

  ```   
  ```javascript
  <!-- app.component.html -->
  <h1>Bem-vindo ao meu aplicativo Angular!</h1>

  <p *ngIf="mostrarElemento">Este elemento será exibido se mostrarElemento for verdadeiro.</p>
  ```
  </details>

</details>

<details>
  <summary>Formulários</summary>
  
  # Formulários

  ## Propriedades de comunicação entre template e componente
   - `template` representa o arquivo .html do componente
   - `componente` representa o arquivo .ts

  ### Property Binding
   - "property binding" é um recurso que permite vincular uma propriedade de um elemento do componente a uma expressão no modelo (template).

  #### Vinculando propriedades no fluxo componente -> template
  *SÍNTAXE*
  ```html
  [propTagHtml] = "propComponente"    // `A propriedade html recebe o valor da propriedade do componente`
  ```
  *Vinculando valor de tag a uma propriedade componente*
  ```html
  <p>{{pessoa.nome}}</p>
  ```
  ### Event binding, template -> componente

  ### Two way data-binding
   - A propriedade "Two-way data binding" (ligação de dados bidirecional) é um recurso que permite a sincronização automática de dados entre o modelo (template) e o componente. Em outras palavras, ela permite que as alterações feitas no modelo sejam refletidas no componente e vice-versa,
   
  #### Diretiva ngModel
   - O ngModule é uma diretiva que permite vincular o valor digitado em um input em uma variável, qualquer alteração de valor feita no input será refletida na variável.
  
  *SINTAXE*
  ```html
  [(ngModule)]="nomeVariavel"
  ```
   - Para usar o ngModel, é necessário fazer a importação do pacote `FormsModule` no arquivo `app.module.ts` e declarar o `FormModule` na propriedade de imports.
  ![Captura de tela de 2024-02-02 12-22-57](https://github.com/AthosGustavo/aprendendo-angular/assets/112649935/1d2f6a7c-f6fb-4f8a-8079-a8900d73b28a)

  *EXEMPLO*
  ```html
  <div>
    <label>Nome</label>
    <input [(ngModel)]="nome" placeholder="Digite o seu nome">
    <button (click)="salvarNome()">Salvar</button>
  </div>
  ```
  ```javascript
  import { Component } from '@angular/core';

  @Component({
    selector: 'app-data-binding',
    templateUrl: './data-binding.component.html',
    styleUrl: './data-binding.component.css'
  })
  export class DataBindingComponent {
    nome: string = '';
    listaNomes:string [] = [];
  
    salvarNome():void {
      console.log(this.nome);
    }
  }

  ```
 <details>
   <summary>Propagação de eventos</summary>

   ### Click

   - As variáveis passadas para o método infoLogin no template são reconhecidas devido a declaração da diretiva ngModule
   
   ```html
   <div>
    <label>Email</label>
    <input name="email" [(ngModel)]="email" placeholder="Digite o seu e-mail"type="text">
    <label>Senha</label>
    <input name="senha" [(ngModel)]="senha" placeholder="Digite a sua senha"type="password">
    <button (click)="infoLogin(email,senha)">Entrar</button>
    <p>Esqueci minha senha</p>
  </div>
   ```
   ```javascript
   export class LoginComponent implements OnInit {
     public email: string;
     public senha: string;

     constructor() { }

     ngOnInit(): void {
     }

     infoLogin = (email: string, senha: string) => {
      console.log(email);
      console.log(senha)
     }

   }
   ```
   
 </details>

 ### EventEmmitter
  *Componente filho passando dados para componente pai*

  *LÓGICA*
   - No componente filho é chamada a uma função `emit` por meio da instância da classe `EventEmmitter`, a função `emit` permite transmitir um valor para uma propriedade do componente pai, no caso, o parâmetro de uma função.
   - Além disso, na instância da classe, sinalizamos a variável com o decorator `@OutPut`, pois indica que uma informação será lançada para fora do componente.

  ```javascript
  import { Component, OnInit, EventEmitter, Output } from '@angular/core';

  @Component({
    selector: 'app-input-filho',
    templateUrl: './input-filho.component.html',
    styleUrls: ['./input-filho.component.css']
  })
  export class InputFilhoComponent implements OnInit {
    constructor() { }

    ngOnInit() {
    }
  
    @Output() componenteFilhoEmite = new EventEmitter();

    valor:number = 0;
    somar():void{
      this.valor++;
      this.componenteFilhoEmite.emit(this.valor);
    }
    subtrair():void{
      this.valor--;
      this.componenteFilhoEmite.emit(this.valor);
    }

  }

  ```
  ```javascript
  <div>
    <app-input-filho (componenteFilhoEmite)="componentePaiRecebe($event)"></app-input-filho>
    <p>{{contadorExibido}}</p>
  </div>
  ```

   - No componente pai, declaramos a função `componentePaiRecebe(event)` e assim capturamos o valor emitido pelo componente filho.
  ```javascript
    import { Component, Input, OnInit } from '@angular/core';

    @Component({
      selector: 'app-componente-pai',
      templateUrl: './componente-pai.component.html',
      styleUrls: ['./componente-pai.component.css']
    })
    export class ComponentePaiComponent implements OnInit {

    constructor() { }

    ngOnInit() {
    }
    @Input() contadorExibido:string;
    componentePaiRecebe(event):void{
      this.contadorExibido=event;
    }

  }

  ```

  ### @ViewChild
   - O decorator `@ViewChild` permite acessar o DOM de uma tag HTML
   - *SINTAXE*: `@ViewChild('#idTag') nomeVariavel:ElementRef`
   - Por meio deste decorator é possível obter propriedades do DOM

  *EXEMPLO*
  ```javascript
  @ViewChild('minhaDiv') inputNome: ElementRef;
    console.log(this.inputNome.nativeElement.value);
  ```
<details>
  <summary>Formulário Reativo</summary>

 # Formulário Reativo

 *IMPORTAÇÕES*
  - `import { FormGroup, FormBuilder, Validators } from '@angular/forms';`
  - `ReactiveFormsModule` deve ser importado em `app.module` e em `imports`
 
 ### FormGroup
 - classe que representa um grupo de controles em um formulário reativo.
 
 ### Controllers
 - Representam os inputs
 
 ### FormBuilder
 - classe que fornece métodos para simplificar a criação de instancias de FormGroup.
 - Ao inves de criar manualmente a instancia de um FormGroup, o FormBuilder ajuda a definir a estrutura do formulario de maneira simples.

 *EXEMPLO: CONSTRUINDO UM FORMULÁRIO*
 ```javascript
  formulario!: FormGroup;

    constructor(
      private formBuilder: FormBuilder,
    ){}

    ngOnInit(): void {
     this.formulario = this.formBuilder.group({
     numero: [''],
     nome:['']
   })
 }
 ```
 ```javascript
 numero: [valor inicial do input,[array para adicionar validações]]
 ```
 ## Declarando o formulpario reativo no html
  - A propriedade `[formGroup]` deve ser declarada en tag `form` e deve receber como valor a variável do tipo `FormGroup`.

 ```html
 <form [formGroup]="formulario" (ngSubmit)="enviarFormulario()">
  <input type="number" formControlName="numero" placeholder="Digite o seu número"/>
  <input type="text" formControlName="nome" placeholder="Digite o seu nome"/>
  <button type="submit">Enviar</button>
</form>
 ```
## Adicionando validação aos inputs

*IMPORTAÇÕES*
 - `import { FormGroup, FormBuilder, Validators } from '@angular/forms';`

```javascript
numero: ['',[Validators.required, Validators.minLength(11), Validators.maxLength(11)]],
nome:['',[Validators.required,Validators.minLength(4)]]
```

*OBS*:Em algumas versões do Angular, para declarar mais de uma validação, é necessário declarar as validações dentro do método `Validators.compose([])`

### Verificando a validade dos inputs e emitindo mensagens de erro

#### Propriedade invalid
 - invalid é um método do objeto controller que retorna `true` se o controler estiver inválido e `false` se ele estiver válido.

#### Propriedade dirty
 - Se o usuário interagir com o controler e digitar qualquer coisa, o controler é considerado `dirty`,caso contrário, se o valor do controler permanecer limpo, o controler é considerado `pristine`

#### Propriedade touched
 - Indica se o controle foi tocado pelo usuário, é semelhante a um evento ´onBlur´ ou ´focusOut´

`<div *ngIf="nome && nome.invalid && (nome.dirty || nome.touched)" class="error-message">`

*EXEMPLO DE UM FORMULÁRIO VALIDADO*
```html
<form [formGroup]="formulario" (ngSubmit)="enviarFormulario()">
  <div>
    <label for="nome">Nome:</label>
    <input type="text" id="nome" formControlName="nome" placeholder="Digite seu nome">
    <div *ngIf="nome && nome.invalid && (nome.dirty || nome.touched)" class="error-message">
      <p *ngIf="nome.errors && nome.errors['required']">O nome é obrigatório.</p>
      <p *ngIf="nome.errors && nome.errors['minlength']">O nome deve ter no mínimo 4 caracteres.</p>
    </div>
  </div>
  <div>
    <label for="numero">Número de Celular:</label>
    <input type="text" id="numero" formControlName="numero" placeholder="Digite o número de celular">
    <div *ngIf="numero && numero.invalid && (numero.dirty || numero.touched)" class="error-message">
      <p *ngIf="numero.errors && numero.errors['required']">O número de celular é obrigatório.</p>
      <p *ngIf="numero.errors && numero.errors['minlength'] || numero.errors && numero.errors['maxlength']">O número de celular deve ter 11 dígitos.</p>
    </div>
  </div>
  <button type="submit">Enviar</button>
</form>

```
```javascript
import { Component } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from '@angular/forms';

@Component({
  selector: 'app-formulario-reativo',
  templateUrl: './formulario-reativo.component.html',
  styleUrl: './formulario-reativo.component.css'
})
export class FormularioReativoComponent {

  formulario!: FormGroup;


  constructor(
    private formBuilder: FormBuilder,
  ){}

  ngOnInit(): void {
    this.formulario = this.formBuilder.group({
      numero: ['',[Validators.required, Validators.minLength(11), Validators.maxLength(11)]],
      nome:['',[Validators.required,Validators.minLength(4)]]
    })
  }

  get nome(){
    return this.formulario!.get('nome')
  }
  get numero(){
    return this.formulario!.get('numero')
  }


  enviarFormulario():void{
    //console.log(this.formulario.get('numero'));

    if (this.formulario.valid){
      console.log('Formulário enviado!')
      console.log(`Nome:${this.formulario.value['nome']}`);
      console.log(`Nome:${this.formulario.value['numero']}`);

    }else{
      console.log('Formulário inválido');
    }
  }
}

```
</details>

</details>
<details>
  <summary>Interfaces</summary>

  # Interface
   - No Angular, as interface são usadas para representar entidades do back-end.Se no back-end existir uma entidade chamada pessoa com os atributos nome, idade e altura, esses atributos serão tipados e representados por meio de uma interface.

  *EXEMPLO*
  ```javascript
  // user.model.ts
  export interface User {
    id: number;
    name: string;
    email: string;
  }
  ```
 
  

  
</details>

<details>
  <summary>Service</summary>

  # Service

*Em Angular, os serviços são frequentemente usados como dependências.
Quando você declara um serviço como um provedor no módulo ou no próprio
componente, o Angular gerencia a criação e a injeção dessas dependências
automaticamente.Ao injetar uma dependência (como um serviço) em um componente,
você está dizendo ao Angular para fornecer uma instância dessa dependência
quando o componente for criado.*

   - É aqui que ficam as requisições para as APIs
   - Comando para criar a pasta service `bg generate service services/<nome>`
</details>


<details>
  <summary>Requisições</summary>

  # Requisições

  ## pacote HttpClient
   - A instância da classe HttpCLient retorna métodos HTTP `varHttpClient.post<tipoRetorno>`
   - Os métodos http aceitam em seu parâmetro a `url` e o dado a ser enviado.
   - Importação no arquivo app.module.ts:`import { HttpClientModule } from '@angular/common/http';`
   - Declaração do módulo em `imports:[HttpClientModule]`

  *EXEMPLOS*
  ```javascript
  this.varHttpClient.get<TipoDoDado>(url);
  this.varHttpClient.post<TipoDoDado>(url, corpoDoPedido);
  this.varHttpClient.put<TipoDoDado>(url, corpoDoPedido);
  this.varHttpClient.delete<TipoDoDado>(url);
  ```

  #### Método GET
  ```javascript
  private urlApi:string = "https://api.github.com/users/AthosGustavo/repos";

  constructor(private httpClient: HttpClient){}

  getRepositorios(): Observable<any[]>{
    return this.httpClient.get<any[]>(this.urlApi);
  }
  ```
  ```javascript
  export class BotaoComponent implements OnInit {
    constructor(private servicoApi: ServicoApiService){}

    ngOnInit(): void {
      this.servicoApi.getRepositorios().subscribe({
        next:(response) => {
          console.log(response)
        },
        error:(error) => {
          console.error(error)
        }
      });
    }
  }
  ```
  ### Observable
   - Observable é um tipo de retorno presente em operações assincronas como requisições HTTP
   - O tipo pode retornar um erro e um valor,a exemplo de uma promisse

  ### subscribe
   - O tipo Observable retorna um método chamada subscribe e esse método é um tipo de notificação que retorna um valor.


</details>
