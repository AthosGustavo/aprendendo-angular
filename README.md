# aprendendo-angular

<details>
  <summary>Montagem de ambiente</summary>
  
  # Montagem de ambietne
  *A montagem de ambiente foi feita com base no angular 14*
  
   - Comando para baixar a cli do angular `npm install -g @angular/cli`
   - Comando para criar um projeto `ng new nome-projeto`
   - Comando para habilitar o localhost `ng serve`
   - Comando para criar um componente com arquivos de css,ts e testes `ng generate component nomePasta/nomeComponente`

  `ng new my-app --no-standalone --routing --ssr=false`
  
</details>

<details>
  <summary>Escopo de classe e declaração de funções e variáveis</summary>

  # Escopo de classe e declaração de funções e variáveis

  ### Tips

  - Obs 1:*Ao declarar a função com a palavra `function` a palavra this perde o seu
  comportamento padrão, é como o this apontasse para dentro da função e não mais para classe.*

  - Obs 2:*Dentro do escopo global da classe, nao se usa `let`, `const` e `var` para declarar métodos.
Essas palavras são usadas fora da classe e dentro de métodos que estão dentro da classe.*

  - Obs 3:*Qualque método ou atributo que seja da classe e que está sendo acessado dentro de um método
da classe, deve ser usada a palavra `this`.*
  
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
   - A instância da classe HttpCLient retorna métodos HTTP `varvarHttpClientClient.post<tipoRetorno>`
   - Os métodos http aceitam em seu parâmetro a `url` e o dado a ser enviado.

  *EXEMPLOS*
  ```javascript
  this.varHttpClient.get<TipoDoDado>(url);
  this.varHttpClient.post<TipoDoDado>(url, corpoDoPedido);
  this.varHttpClient.put<TipoDoDado>(url, corpoDoPedido);
  this.varHttpClient.delete<TipoDoDado>(url);
  ```
  ### Observable
   - Observable é um tipo de retorno presente em operações assincronas como requisições HTTP
   - O tipo pode retornar um erro e um valor,a exemplo de uma promisse

  ### subscribe
   - O tipo Observable retorna um método chamada subscribe e esse método é um tipo de notificação que retorna um valor.


</details>
