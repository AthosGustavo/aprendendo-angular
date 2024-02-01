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
   
  - 1- Declara o dado a ser transmitido na classe pai
  - 2- Declara a variável  que ira receber o valor na classe na classe filho com o decorator @Input
  - 3- na tag do componente filho, faça a vinculação de propriedades `[propFilho]="propPai"`
  - 4- `@Input` decorator usado para definir que uma propriedade pode receber dados externos
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
    <summary>Renderizamento</summary>
    
  # Renderizamento
  ## Renderizamento condicial
  ### Renderizamento condicional com ngIf
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
