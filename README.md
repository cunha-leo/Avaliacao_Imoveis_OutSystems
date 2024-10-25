# App Avaliação de Imóveis em OutSystems

Aplicação em OutSystems Reactive de Avaliações de Imóveis

## Índice

* [1ª Parte - Título da Parte 1](#documentação-da-1ª-parte)
* [2ª Parte - Título da Parte 2](#documentação-da-2ª-parte)
* [3ª Parte - Em Construção : Clique aqui](/Assets/Parte%203/Parte%203.md)

-----------------------------------

## Documentação da 1ª Parte

* Entendendo o projeto através do template
* Criando o projeto em dois módulos Web e Services
* Entendendo a separação de responsabilidades
* Criando a arquitetura do banco de dados

### Mockups e Template das Telas

Antes de começar a implementação, iniciamos com entendimento dos mockup das telas utilizando o **Drawio** e a importância de ter uma template visual e os benefícios que pode trazer.

Esse planejamento visual ajudou a garantir que todos os elementos fossem claramente definidos antes da implementação e trazendo clareza da aplicabilidade.

As telas incluem:

* Tela de Login
  ![Figura do Mockup - Tela de Login](/Template/img/mockup-tela-login.png)
  
* Dashboard
  ![Figura do Mockup - Dashboard](/Template/img/mockup-dashboard.png)
  
* Cadastro de Imóvel
  ![Figura do Mockup - Cadastro de Imóvel](/Template/img/mockup-cadastro-imovel.png)

* Avaliar Imóvel
  ![Figura do Mockup - Avaliar Imóvel](/Template/img/mockup-avaliar-imovel.png)

* Pop-up Avaliar Imóvel
  ![Figura do Mockup - Pop-up Avaliar Imóvel](/Template/img/mockup-popup-avaliar-imovel.png)

* Minhas Avaliações
  ![Figura do Mockup - Minhas Avaliações](/Template/img/mockup-minhas-avaliacoes.png)

* Meus Imóveis
  ![Figura do Mockup - Meus Imóveis](/Template/img/mockup-meus-imoveis.png)

* Imóveis que já morei
  ![Figura do Mockup - Imóveis que já morei](/Template/img/mockup-imoveis-que-ja-morei.png)

### Estrutura do Projeto

O projeto foi dividido em dois módulos principais:

1. **Módulo AAR\_Services (Service)**:
   * Responsável pela lógica de backend, incluindo a arquitetura do banco de dados, os relacionamentos e as ações CRUD.

   * O módulo foi configurado para ser **público**, permitindo que outros módulos acessem suas funcionalidades como leitura.

   * A arquitetura de entidades foi projetada para ser clara e garantir a integridade dos dados. O diagrama de entidade (ER) criei para facilitar a minha visualização, segue o mesmo é uma previa de cada tabela, abaixo:

     ![Diagrama ER](./Assets/Parte%201/img/Data/ER/ER01.png)

   * **Criamos o diagrama ER**:
     ![Diagrama ER](./Assets/Parte%201/img/Data/ER/ER01.png)

   **Tabelas Criadas**:

   * **Tabela Immobile**: Contém os dados dos imóveis cadastrados, como CEP, endereço, cidade, proprietário, entre outros.
     ![Diagrama ER](./Assets/Parte%201/img/Data/Table/ER_Immobile.png)

   * **Tabela Rating**: Armazena as avaliações dos imóveis, incluindo informações como tempo de locação, recomendações e observações dos usuários.
     ![Diagrama ER](./Assets/Parte%201/img/Data/Table/ER_Rating.png)
  
   * **Tabela TypeExperience**: Armazena os tipos de experiência relacionados aos imóveis. Possui registros como **Excelente, Bom, Neutro, Ruim, Péssimo**.
     ![Tabela TypeExperience](./Assets/Parte%201/img/Data/Table/ER_TypeExperience.png)

   * **Tabela TypeImmobile**: Armazena os tipos de imóvel disponíveis (ex.: Casa, Apartamento, Loja). Possui registros como **Casa, Apartamento, Loja**.
     ![Tabela TypeImmobile](./Assets/Parte%201/img/Data/Table/ER_TypeImmobile.png)

   * **Tabela UserxImmobile**: Relaciona usuários aos imóveis, indicando propriedades e ocupação. São tabelas auxiliares que armazenam os tipos de experiência, tipos de imóvel, e a relação entre usuários e imóveis.
     ![Tabela UserxImmobile](./Assets/Parte%201/img/Data/Table/ER_UserxImmobile.png)

   * **Tabela User**: Utiliza a entidade padrão do sistema OutSystems para armazenar informações dos usuários, como data de criação e última alteração.
     ![Tabela User](./Assets/Parte%201/img/Data/Table/ER_User.png)

2. **Módulo AAR\_WEB**:
   * Responsável pelo front-end e pelas telas da aplicação.

   * Foi adicionado como dependência ao **AAR\_WEB**, como leitura, para garantir a segurança e centralizar toda a lógica de servidor no módulo **AAR\_Services**.

   * No módulo web/reactive, podemos observar as abas completas, incluindo **Triggers, Interface, Logic, e Data**.  

     ![Estrutura do Módulo AAR_WEB](./Assets/Parte%201/img/Model/estrutura-aar-web.png)

### Conclusão

Essa primeira etapa do projeto incluiu a configuração inicial dos módulos e a criação das entidades do banco de dados, além da definição da interface do usuário. Utilizamos uma abordagem modular que facilita a manutenção e a segurança dos dados, separando a lógica de servidor do front-end.

Na próxima etapa, vamos nos concentrar em finalizar a estruturação das telas no módulo **AAR\_WEB**, garantindo que todas as funcionalidades estejam alinhadas ao objetivo do projeto.

-----------------------------------

## Documentação da 2ª Parte

* Criação Tela de Login e Cadastro Imóveis e suas lógicas

### Tela de Login

* Aqui podemos observar ao lado direito que, por padrão, a tela de Login da própria OutSystems vem com:
  ![Tela de Login](./Assets/Parte%202/img/Tela%20Login/Login01.png)

#### 4 Variáveis Locais

* **Username**: Consumida no Input **E-mail**
  ![Var Username](./Assets/Parte%202/img/Tela%20Login/Var_Username.png)

* **Password**: Consumida no Input **Senha**
  ![Var Password](./Assets/Parte%202/img/Tela%20Login/Var_Password.png)

* **IsExecuting**: Utilizada para informar execução de algo na ClientAction **OnInitialize**
  ![Var IsExecuting](./Assets/Parte%202/img/Tela%20Login/Var_IsExecuting.png)

* **Remember**: Consumida no Input de Checkbox **Lembrar-me**
  ![Var Remember](./Assets/Parte%202/img/Tela%20Login/Var_Remember.png)

#### 3 Client Actions

* **ForgotPassword**: Para recuperar a senha
  ![ForgotPassword](./Assets/Parte%202/img/Tela%20Login/Client/ForgotPassword.png)

* **Login**: Usado no botão **Entrar**
  ![Login](./Assets/Parte%202/img/Tela%20Login/Client/Login.png)

  * A lógica Login recebendo o **Variavel local IsExecuting** como True, que será após clicar no botão
    ![IsExecuting](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-IsExecuting.png)

  * Após, segui para a ServerAction **DoLogin**, que é a ServerAction usada no Login
    * Que receberá as variáveis locais: Username, Password, Remember
    * A ServerAction é chamada para persistir os dados e saber se realmente salvou no banco de dados
    * E chamar a ServerAction padrão de Login da OutSystems dentro de User
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin.png)
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin01.png)
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin02.png)
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)

  * Após, irá **remover** uma mensagem de feedback ao Logar
    * Ou seja, será removida qualquer possível mensagem que apareça após realizar o login.

  * Após, **redirecionará**
    * O usuário será redirecionado para a tela principal
      ![Redirect](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)

* **OnInitialize**:
  * Usado para realizar alguma ação após o carregamento da tela
    * Como padrão, no caso da imagem abaixo
      ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize01.png)

  * Usado para receber a variável local "IsExecuting" para implementar a ação
    * Nesse caso, o padrão está como False, ou seja, quando iniciar esta tela, por padrão, não inicialize nenhuma ação
      ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize.png)

-----------------------------------

### Mudando as ações de Autentication para o caminho correto

* Isso se dá porque a lógica de servidor deve ficar no módulo **ARR_Service**
  * Então, basta recortar da **ARR_WEB** e colocar na **AAR_Service**, aba **Logic**, e **Publicar**
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin.png)

  * Deve deixar público antes de publicar, dessa forma podemos acessar no outro módulo as mesmas
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin01.png)

  * Agora temos que apontar
    * Achamos as dependências, buscamos o módulo, clicamos, adicionamos e "Apply"
    * Após aplicar, os erros irão sumir
      ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin02.png)

-----------------------------------

## Tela de Cadastro de Imóveis

### Módulo ARR_WEB

![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela.png)

* Vamos criar a partir da ABA **Data** e arrastamos para o nosso **MainFlow**
  * Criamos então arrastando as duas telas
  ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela01.png)

  * **Immobiles**: Que é a tela de Listagem
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela02.png)

  * **ImmobileDetail**: Que é a de registro
    * Retiramos o **IF** que vem por padrão, que mostra se **true** Cadastrar ou **else** Editar, e colocamos no lugar uma **Expression**, que tem a seguinte validação:
      * SE o ImmobileId for igual a vazio ou se ele não existe, Cadastrar, se não, Editar e concatenar com Imóvel.

      ```Js
      If(ImmobileId = NullIdentifier(),"Cadastrar","Editar")+" Imóvel"
      ```

    * Vamos tirar agora o Form de dentro da Column1, para que ele expanda
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela03.png)
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela04.png)

    * Arrastando o **Adaptive/Columns2** para dentro do **Form** e dividindo as colunas
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela05.png)

    * Ajustado ficou assim:
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela06.png)

    * Foi trocado **checkbox** por **radioGroup**, dessa forma ficou mais visual
      * O **Label** deixamos como **None** para não pegar nenhuma propriedade, pois nesse caso é um **True** ou **False** no Radio, não sendo necessário amarrar ao Label
      * Alteramos também o lado dos botões
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela07.png)

    * Verificando a **ClientAction** **SaveDetail** da tela **ImmobileDetail** se os dados estão persistindo corretamente
      ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail.png)

      * Aqui ainda não está fazendo a persistência dos dados
        ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail01.png)

      * Mostrando como a tela está ficando visualmente
        ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail02.png)

### Módulo: ARR_Services

#### Tela Cadastrar Imóvel e Editar Imóvel

* Persistindo os dados da Tela: Cadastrar Imóvel
  * Criamos uma pasta somente com o nome da Tabela que criamos para a tela
  * Aqui vamos criar a ação que irá persistir os dados

* Server Action: **Immobile_CreateOrUpdate**
  ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate.png)

  * A Server Action vai estar esperando:
    * **Parâmetro de Entrada**: **Immobile**
      * No caso, quero persistir a minha **Tabela Immobile**
      * Dessa forma foi criada uma ação dentro do servidor chamada **Immobile_CreateOrUpdate**
      * Para atualizar ou criar, precisamos da estrutura dela, por isso o **parâmetro de entrada** > **Immobile**
    * **Parâmetro de Saída**: **Output**
      * Agora precisamos de um parâmetro de saída para retornar as informações
      * Dessa forma, optamos por criar uma **Structure**
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate01.png)

      * Criando Atributos para a **Structure Output**:
        * **Success**: Retornará se foi sucesso ou não, com valor padrão como **false**
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate03.png)

        * **Message**: De acordo com o retorno
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate04.png)

        * **AccessKey**
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate05.png)

        * **Id**: Será **Long Integer**, porque não é um retorno definido de uma tela ou tabela; será utilizado como atributo de retorno em várias Server Actions
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate06.png)

      * Uma vez criada a **Structure**, podemos criar o **Parâmetro de Saída**:
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate07.png)

  * Criando o Fluxo da **Server Side** (Server Action)
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate08.png)

  * **1ª Coisa**: Validar se estou **Criado Por** ou **Criado Como**
    * Você é igual a **NullIdentifier()**
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate09.png)

  * SE **Immobile.Id** = **NullIdentifier()** [Novo registro?]
    * SE Sim: **CreateImmobile**
    * SE Não: **UpdateImmobile**
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate10.png)

    * Caso Sim: Temos que preencher, antes de persistir os dados, os campos **Criado Por (CreatedBy)** e **Criado Como (CreatedAt)**
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate11.png)

    * Como é somente um registro pontual, posso vir no **Source**, tirar o **Immobile** e adicionar os campos pontualmente neste momento.
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate12.png)

    * > ⚠️ **ATENÇÃO**: Se atente aos campos, sempre colocamos o que vem do parâmetro de **ENTRADA** aqui.
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate13.png)
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate14.png)
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate15.png)

    * São os dois únicos campos que não vão selecionar a opção que vem do parâmetro de entrada.
      * Aqui em **CreatedBy**: Passamos uma função chamada:
        * **GetUserId()**:
          * Ela traz o ID do usuário logado atualmente na aplicação
          * Salvando o Id desse usuário como criador
      * Aqui também temos o **CreatedAt**: Passamos uma função chamada:
        * **CurrDateTime()**:
          * Ela pega a hora atual e persiste na minha tabela
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate16.png)

    * Uma observação: o campo **CreatedAt**, anteriormente, passamos o **CurrDateTime()** no próprio atributo da tabela. Dessa forma, não há necessidade de passar algo aqui, então ficará assim:
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate17.png)
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate18.png)

  * **Observação Interessante**:
    * Podemos criar a validação de criação ou update de duas formas e utilizamos um exemplo diferente em cada.
    * Em **UpdateImmobile**:
      * Escolhemos atribuir no **Source** diretamente apenas o **Parâmetro de Entrada** PAI
      * Dessa forma, todos os atributos do **Source** vêm junto
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate19.png)

    * Em **CreateImmobile**:
      * Escolhemos tirar o parâmetro PAI (**Immobile**) e adicionamos um por um e estilizamos o atributo **CreateBy**, passando a função **GetUserId()**
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.png)

  * Começando a inserir os parâmetros de saída
    * **1º**: Criamos um **Assign** para o **CreateImmobile**
      * Adicionamos os parâmetros de entrada e seus respectivos valores
      * A diferença é o **Output.Id**, que recebe o parâmetro do Id da função **CreateImmobile**
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.1.png)

    * **2º**: Criamos um **Assign** para o **UpdateImmobile**
      * Adicionamos os parâmetros de entrada e seus respectivos valores
      * A diferença é o **Output.Id**, que recebe o próprio atributo **Id** dele, pois já é um user, dessa forma, atualizando-o
      * Porque nesse momento não estou criando um novo, estou simplesmente atualizando-o
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate22.png)
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate23.png)

* >❗ **EXCEÇÃO**: pois esses **Assign** não vão dar False até aqui ou ❌ **ERRO** até aqui.

  * Aplicando:
    * Adicionar Exceção ao Fluxo
      * Decidimos colocar Todas as Exceptions
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate24.png)

    * Preenchendo o **Assign**:
      * **Output.Success = False**
        * Para englobar erros que saem fora do contexto ao lado
      * **Output.Message = AllExceptions.ExceptionMessage**
        * Recebe a própria mensagem da **AllExceptions > ExceptionMessage** de forma automática
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate25.png)

    * **AllExceptions**, a exceção CASO for acionada:
      * Significa que houve um erro e não conseguiu completar o fluxo
      * Caso observe, o **Abort Transcription** está **Yes**
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate26.png)

-----------------------------------

### Módulo: ARR_WEB

* Começando a retirar o que não vamos usar
  * Neste caso, excluímos o Aggregate **GetUsers**
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate27.png)
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate28.png)

* Criando o fluxo da **Client Action: SaveDetail**
  * Primeiro será validado se o formulário é **False**
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate29.png)

  * Se o **Form** for **True**:
    * Irá chamar a **ServerAction** criada **Immobile_CreateOrUpdate**
      * Nela, receberá em **Action > Immobile** a listagem criada como parâmetro de entrada
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate30.png)
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate31.png)

    * **IF** que valida se a persistência dos dados foi realizada com sucesso ou não:
      * **❌ SE Não**: Receberá uma mensagem de ❌ **ERRO** pegando o parâmetro de saída
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate32.png)

      * **✅ SE Sim**: Receberá uma mensagem de ✅ **SUCESSO** do parâmetro de saída
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate35.png)

    * Finaliza com 🔄 **REDIRECT** para a tela 🏠 **Immobiles** de listagem
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate36.png)

* Validando em tela se os dados estão persistindo:
  * Está ok até aqui, mas o **CEP** ainda está fictício, faremos correções e usaremos uma API para o **CEP**
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate37.png)

### PRÓXIMA ETAPA

* ✨ **IMPLEMENTANDO O CEP**:
  * 🛠️ Criando ação **OnChange** para quando o usuário clicar no campo **CEP**.
  * ✏️ Quando começar a alterar o campo **CEP**, cairá em um evento de **OnChange**:
    * 🌐 Onde chama um serviço. Se aquele **CEP** existe:
      * 🏢 SE existir, ele vai preencher automaticamente o logradouro, bairro e cidade.

-----------------------------------
