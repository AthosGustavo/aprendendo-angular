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



</details>
