# App Avaliação de Imóveis em OutSystems

Aplicação em OutSystems Reactive de Avaliações de Imóveis

## Índice - PT

* [1ª Parte - Título da Parte 1](#documentação-da-1ª-parte)
* [2ª Parte - Título da Parte 2](#documentação-da-2ª-parte)
* [3ª Parte - Título da Parte 3](#documentação-da-3ª-parte)
* [4ª Parte - Título da Parte 4](#documentação-da-4ª-parte)
* [5ª Parte - Em criação ...](#documentação-da-5ª-parte)

## Readme in English - EN

If you are an English reader, visit the link below:

* [Click here documentation](/README-EN.md)

## Readme en Español - ES

Si eres un lector en español entra en el seguinte enlace:

* [Haga clic aquí](/README-ES.md)

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
  ![Figura do Mockup - Tela de Login](./Template/img/mockup-tela-login.png)
  
* Dashboard  
  ![Figura do Mockup - Dashboard](./Template/img/mockup-dashboard.png)
  
* Cadastro de Imóvel  
  ![Figura do Mockup - Cadastro de Imóvel](./Template/img/mockup-cadastro-imovel.png)

* Avaliar Imóvel  
  ![Figura do Mockup - Avaliar Imóvel](./Template/img/mockup-avaliar-imovel.png)

* Pop-up Avaliar Imóvel  
  ![Figura do Mockup - Pop-up Avaliar Imóvel](./Template/img/mockup-popup-avaliar-imovel.png)

* Minhas Avaliações  
  ![Figura do Mockup - Minhas Avaliações](./Template/img/mockup-minhas-avaliacoes.png)

* Meus Imóveis  
  ![Figura do Mockup - Meus Imóveis](./Template/img/mockup-meus-imoveis.png)

* Imóveis que já morei  
  ![Figura do Mockup - Imóveis que já morei](./Template/img/mockup-imoveis-que-ja-morei.png)

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

      ```javascript
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

## Documentação da 3ª Parte

## Criando Telas e lógica de Login e Cadastro de Imoveis

* Ajustes de labels
* Utilizando componente da Forge (api)
* Deixando aplicação mais segura com AccessKey
* Eventos OnChange
* Evento OnScroolingEnd
* Gerando AccessKey randômico
* Utilizando Widget List ao invés de TableList
* Join entre tabelas
* Tela Meus imóveis
* Tela Avaliar Imóveis

## Start

## Gerando AccessKey randômico

* Até o momento SE para edição ou ações que é mostrada na URL, está esposto o ID passado isso trás vulnerabilidade e brechas para ser burlado o sistema
* Por médida de segurança, vamos colocar o AccessKey que mascara esse ID, dando mais segurança e evitando contra vunerabilidades na aplicação

  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey.png)

### Access Key ARR_SERVICES

* Iremos iniciar as alterações no servidor, conforme verificamos na imagem abaixo até o momento temos a ServerAction (**Immobile_CreateOrUpdate**) que possui um parametro de entrada que é a propria tabela Immobile e o parametro de saida é o Output (*Success, Message, AccessKey, Id*)

* Porém o nosso (**CreateImmobile**) no fluxo não está recebendo ainda o **AccesKey**, porque não foi atribuido ainda a nossa tabela.

    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey01.png)

#### Criando o Access Key

* 1º Temos que criar um atributo na tabela Immobile na aba **Data**
  * Esse atributo irá com o tipo **Text** porque receberá uma **HASH**

  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey02.png)
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey03.png)

* 2º Uma vez criado o atributo, retornamos para o nosso fluxo da ServerAction (**Immobile_CreateOrUpdate**)
  * Na (**CreateImmobile**) Já estará disponivel a AccessKey
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey04.png)
  * E agora irei pedir para toda vez que criar um registro **novo** preencher a **Access Key**

* 3º Usando uma função da Systems padrão para configurar a AccessKey
  * Dessa forma é necessário busca-la nas dependências, para isso
    * Clicamos em dependências e atribuimos a ServerAction (**GenerateGuid**)
    * Toda vez que esta função for chamada será retornada uma hash pelo parametro de saida(retorno) da ServerAction do sistema
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey05.png)

* 4º Uma vez que adicionamos a  ServerAction (**GenerateGuid**)
  * Podmeos agora retornar ao fluxo da ServerAction (**Immobile_CreateOrUpdate**) e atribuirmos a função ao atributo AccesKey do parametro de entrada que adicionamos a tabela Immobile.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey06.png)
  * Agora No fluxo, toda vez que crio um Id novo ou imovel ele gerará um AccessKey
    * Posteriormente iremos para ARR_WEB onde será trocado na url ao em vez do ID a nossa AccessKey já com a hash.

* 5º Publicar e irmos então para ARR_WEB

### Access Key ARR_WEB

* Uma vez que finalizamos a parte do **ARR_SERVICES** temos que adicionar essas novas atualizaçãoes a nossa dependencia no ARR_WEB
  * Ao abrir já verificamos o ARR_Services flegado, dessa forma apenas clicamos no botão *Refresh all* e após *Apply* e publicamos
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey07.png)

* 1º A tela **ImmobileDetail** está esperando como parametro de entrada um **Immobile Identifier** é esse valor que retorna o ID do usuário, é aqui que vamos tratar a vulnerabilidade com **AccesKey**
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey08.png)
* Iremos substituir o parametro de entrada para o AccessKey
  * Seu *DataType* será *Text*, pois agora será esperado uma **hash** e não mais um ID
  * Não será necessário ser mandatorio, pois não tem a necessidade de mostrar o parametro vazio, somente no Update que será passado.
  * Ainda terei que alterar o GET onde pego essas informações e na minha lista
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey09.png)

* 2º Alterando nosso **GetImmobileBy**
  * Clicando nele já deparamos com um eror informando que estava sendo feito uma comparação de Identificador com Data types diferentes isso, porque mudamos o parametro de entrada de Id para Access Key, dessa forma temos que alterar também no nosso filtro do Get, como na imagem abaixo.
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey10.png)

* 3º Alterando o filtro do GetImmobileBy
  * Quando falamos que estamos buscando um | Immobile.AccessKey = AccessKey | ou seja uma busca unica o MaxRecord deve ser de 1 registro e não o padrão de 50.
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey11.png)

* 4º Por padrão as linhas de registros do nosso **Immobile List** ao clicar vai para página de edição daquele registro especifico, porém mudamos o nosso parametro de entrada para Access Key, dessa forma aqui também deve ser alterado.
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey12.png)
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey13.png)
![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey14.png)

-----------------------------------

## Utilizando componente da Forge (api) CEP

* ✨ **IMPLEMENTANDO O CEP**:
  * 🛠️ Criando ação **OnChange** para quando o usuário clicar no campo **CEP**.
  * ✏️ Quando começar a alterar o campo **CEP**, cairá em um evento de **OnChange**:
    * 🌐 Onde chama um serviço. Se aquele **CEP** existe:
      * 🏢 SE existir, ele vai preencher automaticamente o logradouro, bairro e cidade.
      * 🚫 SE não existir, ele vai mostrar uma mensagem de erro.

### Baixando o Componente na Forge (ViaCEP)

* Baixar o componente viaCEP - Endereços
  * Clicar na ABA **Forge** e procurar por **ViaCEP**
  * Uma vez encontrada apenas instale no studio
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP.png)

### Aplicando ARR_WEB

* 1º Esse componente é uma aplicaçõa separada o ViaCEP, dessa forma eu preciso referenciar ele dentro do meu código como eu faço com o ARR_Service
  * Clicando no plug de tomada e adicionando ele ao meu projeto
  * Ele possui uma ServerAction (**CEP**) com um parametro de entrada (CEP) e um parametro de saída (Output)
    * O Output possui um campo de retorno (CEP), através de uma **Structure** e campos de retorno (CEP, Logradouro, Complemento, Bairro, Localidade, Uf, Ibge, ...,Erro)
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP01.png)
  * Após aplicar já o verei na ABA **Logic**
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP02.png)

* 2º Trabalhando em cima da tela

  * Indo no meu campo Input **CEP** criarei uma ação OnChange que quando esse campo for alterado, irá rodar uma trigger e dentro dessa ação vai estar a ação do CEP
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP03.png)
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP04.png)

* 3º Aplicando a lógica:
  * Add um **IF**, SE o input CEP > 7, ou seja se ele tiver 8 caracteres ou mais
	```Js
	Length(GetImmobileByAccessKey.List.Current.Immobile.CEP) > 7
	```
    * SE False ele finaliza, pois tem menos de 8 caracteres
    * Se True chamo minha API de serviço **ViaCEP** e verifico se eu consigo pegar alguma informação baseado no CEP digitado no Input

  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP05.png)

    * SE for satisfeita a condição ele irá chamar o ViaCEP
      * Para isso basta apenas eu arrastar da ABA Logic > Via_Services > Via_CEP : CEP
      * E ligar na minha condição e assim ele irá chamar o serviço e pegar as informações do CEP
    * Na parte de parametros como na imagem ira esperar um CEP, aqui e o mesmo que eu coloquei na condição então seleciono ele.
      * Aqui até o momento ele está referenciando no serviço de CEP mais ainda não está fazendo nada

    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP06.png)
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP07.png)

    * Agora deve configurar os campos de Input para receber os valores automaticamente do meu serviço ViaCEP
      * **1º** Preciso validar se ele recebeu as informações desse serviço (1º IF)
        * SE Cep > 7 = FALSE (PARA)
        * SE Cep > 7 = TRUE ele chama meu serviço **ViaCEP**
          * onde é esperado como parametro um CEP, neste caso usamos o mesmo da condição (If)
        ```Js
        Length(GetImmobileByAccessKey.List.Current.Immobile.CEP) > 7
        ```
        .....
        * **2º** validamos **O retorno do serviço CEP**  (2º IF)
        ```Js
        CEP.Output.Erro = True
        ```
          * SE o retorno do serviço CEP.Output.Erro = True (PARA)
          * SE o retorno do serviço CEP.Output.Erro = FALSE
            * Ou seja se ele deu erro ele irá chamar o Asign
        ....
          * **3º** Preenchemos o **Assign**
            * Onde o valor do atributo da **GetImmobileByAccessesKey** recebe os Outputs da estrutura do serviço CEP.Output

    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP10.png)
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP11.png)
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP12.png)

    * **Digitando o CEP** no campo Input agora ele aciona meu serviõ viaCEP, valida se é maior do que 7 caracteres e caso seja satisfeito ele retorna preenchendo automaticamente os campos [logradouro, bairro, cidade, complemento(caso encontre)]
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)

    * **4º** Limpando campos caso haja alteração no Input **CEP**
      * Isso é necessário pois se alterarmos o campo do CEP novamente ele precisa ter uma ação que limpe os campos caso ele não ache o CEP ou seja SE a busca do CEP.Output.Erro for True ele limpa os campos
      * Dessa forma criei um asign recebendo os atributos porém com valor vazio
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP13.png)

    ⚠️**APRENDIZADO:** A partir de **Onchange** eu consigo buscar qualquer informação ou fazer qualquer tipo de manipulação dentro da minha aplicação, baseado em informações que eu tenha preenchido anteriormente.
    * Nessa aplicação foi a partir deu preencher um campo o CEP em preenchi automaticamente varios outros.
    * Serve para aplicar de diversas formas e diversas situações

-----------------------------------

## Tela Meus Imóveis

* Tela de Listagem de Imóveis
  * Iniciando assim, vamos reaproveitar a mesma para criar a tela de listagem de imóveis

  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis01.png)

* Realizando a alteraçõa inicial mais proximo do nosso template
  * **1º** Alteramos o nome da página
  * **2º** Retiramos o link de Casa pois será no logradouro para edição
  * **3º** Editamos as posições das colunas
  * **4º** Renomeamos o botão de criação para **Cadastrar Imóvel**
  * **5º** Adiconamos o link de edição na coluna **Logradouro**
  * **6º** Adiconamos a coluna de **Ação** com ícone de **Delete**
  * **7º** Adiconamos a coluna de **Cadastro**

  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis02.png)

* configurar as **Expressions** para receber os valores das colunas.
  * **1º** **Avaliações** - Recebe o valor do atributo correto
    * A ideia dessa coluna e realizar a somatoria de avaliações do endereço especifico.
    * Então terei que alterar meu Get(Aggregate) para realizar essa soma.
    * Começando a alterar o **GetImoveis**(Aggregate)
      * Criando um join para chamar a tabela avaliações
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis03.png)
      * Foi feito o Join e já está relacionado
        * Ao apertar **Source** e escolher a tabela já é feita a relação de tabelas
        * Uma coisa importantes a relação de ligação está como **With or without** que significa que ele buscara tanta os registros de que tenha **Avaliação** e o que não tem.
        * **With or without** Busca ambos registros com ou sem
        * **With** Busca registro preenchidos
        * **Only With** Busca apenas os registros que tenham a avaliação

        * Para realizar a avaliação lá na frente e verificar corretamente os dados da nossa listagem com a avaliação sem repetir registros realizamos o **group by** e o **count**
        * **Group by** agrupamos os dados de CEP, Id:Imomoble, Street, Street_Number, CreatedAt,Label:TypeMobile, AccessKey
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis06.png)
        * **Count** é para contar a quantidade de registros agrupados
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis05.png)
        * Olha que interessante uma vez que eu realizei o agrupamento e o count ele agora deixou de olhar para toda a estrutura e nosso Get agora mostra apenas os campos agrupados.
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis08.png)
        * Também retiramos a reordenação de cada coluna
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis09.png)
        * Agora vamos abrir as expresison e substituir pelos valores do novo Get os cmapos dos agrupamentos
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis10.png)
        * **Até o momento ficou assim**
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis11.png)
* Conseguimos finalizar a primeira parte dessa tela agora vamos realizar alguns ajustes:
  * **1º** Vamos ajustar a formatação do **Criado em** com a função da OutSystems **DateFormate()**
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis12.png)
  * **2º** Vamos ajustar a ação do nosso **Search**
    * Ocorreu que o campo de busca nao estava retornando os registro como veio criado, porque estava apenas pegando o CEP, como temos ainda somente dois registros  de CEP, vamos alterar para pegar o CEP e o Logradouro
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis13.png)

* Criando a Ação **DELETE**
  * 1º Criamos uma *ClientAction* no modulo **ARR_WEB** vazia por enquanto
  * 2º Vamos criar a **ServerAction** no modulo **ARR_Server**
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete01.png)
  * 3º Vou na ABA **Data** acho a ação de Delete da tabela Immobile e arrasto para minha **ServerAction** é adicionio o meu parametro de entrada ID para o Crud de Delete.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete02.png)
  * 4º Passo meu **Output** ou seja a saida desse retorno do CRUD.
    * Ambos os fluxos não passamos o ID nem o AccessKey de Output
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete03.png)
  * 5º Passo criar o **Fluxo de Exceção**
    * Nele podemos ver que o nosso fluxo de **TRUE** está ok e nosso **FALSE**
      * Recebe uma **AllExpetions** que terá um **Asign** de *Output.Succes = True* e *Output.Message = AllExceptions.ExceptionMessage* ou seja caso der erro é informado erro pela **AllExpetions**.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete05.png)
  * 6º Voltamos para o Mudulo **AAR_WEB** para agora receber o retorno da **ServerAction**, realizamos o Fluxo onde
    * 1. Chamamos a **ServerAction immobile_Delete** que passa como parametro o nosso Id.
    * 2. **SE** a **ServerAction** returnou **TRUE**, Recebera uma mensagem de **SUCESSO** **SE NÃO** recebera uma mensagem de **ERRO**, ambas do nosso retorno do **Output.Message da ServerAction** é após encerrerá.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete01.png)
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete02.png)
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete03.png)
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete04.png)

## CRIANDO TELA DE AVALIAÇÕES

* **1º** Para inicar organizamos a Tela de Avaliação com um **List** para ficar ajustado usamos
  * No Main Content > List > Container > Content\CardsSectioned
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel01.png)

* **2º** Iremos mostrar os Imóveis disponiveis para avaliar, para isso vamos criar um Aggregated para essa tela em especifico.
  * 1. Fazemos uma relação com a tabela **Immobile** com a **UserXImmobile**
    * Será a tabela usada para relacionar o usuário com os imoveis que ele já morou e com o **join(With or Whithout)**.
    * Ou seja trará os dados da *Immobile* mesmo se não haver dados relacionados a *UserxImmobile*

  * 2. Fazemos uma relação com a tabela **Immobile** com a **TypeImmobile**
    * Neste caso a ligação é **join(Only Whith**) trará de qualquer forma porque não há como cadatsrar um imóvel sem o seu tipo.

  * 3. Fazemos uma relação com **Immobile** com a **Rating**
    * Para trazer as informações das avaliações, agrupar e contar pelas mesmas.
    * Usamos o **join(With or Whithout**) também.

  * 4. Realizmos os agrupamentos de informação e a contagem por Id do (Rating).
    * **Grup By** :
      * Immobile.Id
      * Immobile.Street
      * Immobile.Street_Number
      * TypeImmobile.Label
      * Immobile.AccessKey
    * **Count** :
      * Rating.Id

    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel03.png)

* **3º**Agora vamos adicionar o nosso **Aggregat** ao nosso **Source**
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel04.png)
  * 1. Após adicionamos nosso Source atraves das nossas **Expressions** de acordo com retorno de cada informação como na imagem abaixo.
  * 2. Também estilizamos um pouco mais nosso **Container** dando um espaçamento de margens e centralização do conteudo.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel05.png)
  * 3. Vamos Criar um *Group By* no do *TypeImmobile.Id* para que quando a informação daquele lista for Casa apareça um icone de casa e se for apartamento irá aparecer apartamento.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel06.png)
  * 4. Agora vamos criar um **If** para mostrar o icone de acordo com o **TypeImmobile**
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel07.png)

* **4º** Vamos criar um scroll infinito que ao rolar as avaliações el sempre vai carregando mais a cada vez que eu rolar para baixo enquanto tiver imoveis.
  * 1. Ao selecionar o component **List** ele por padrão possui os campos de tipos de **Envents** selecione o Event **On Scroll Ending** é após selecione a opção **New Infinite Scroll Cliente Action**
    * Será criado automaticamente uma **Cliente Action** de Scroll
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel08.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel09.png)
    * Ele criou uma ação **ScrollEnding** aonde ele está esperando um **número** para incrementar a partir da variável **Incrementrecords** que é se você vai mostrar 5 agora traga mais 2, 3 ... e também criou uma **Variavel Local** -> **MaxRecords** a primeira vez que abrir a tela mostrará a partir de quantos na tela
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel10.png)
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel11.png)
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel12.png)

## Documentação da 4ª Parte

## Pop-up de Avaliação e Tela Minhas Avaliações, Imóveis que já Morei e Ajustes Gerais

- Ajustes no menu
- Modal de avaliação
- Persistência de dados
- Tela Minhas Avaliações
- Tela Imóveis que já morei
- Ajustes gerais

## Criando Modal de Avaliação

![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao01.png)

- **1º** Iniciamos o **Modulo ARR_SERVECE** Onde será criado a **Server Action: Rating_CreateOrUpdate**

  - Será o fluxo de persistência dos dados do nosso **Modal Avaliação**
  - Lembrando que essa **Server Action: Rating_CreateOrUpdate** deve estar como **Public**
    - Para que o modulo **ARR_WEB** o receba
  - O mesmo irá consumir a tabela **Rating**.
  - Foi criado uma pasta na Aba **Logic > Rating > Rating_CreateOrUpdate** Onde é a nossa server action de persistência.
  - *Fluxo* bem parecido com anterior:
    - 1º O fluxo inicia > Após uma condição *If(É um novo record?)*
    - 2º Se for um novo record, ele irá armazenar esse registro no nosso **CRUD(CreatingRating)**
      - Como **Source** receberá nossa tabela **Rating**
      - Passaremos Nosso **Output** atraves do **Asign** com:
        - **Output.Succes** (True)
        - **Output.Message** ("Avaliação criada com sucesso")
        - **Output.Id** (CreateRating.Id) -> O Id de saida do **CreateRating**
    - 3º Se não for um novo record, ele irá atualizar o registro no nosso **CRUD(UpdateRating)**
      - Como **Source** receberá nossa tabela **Rating**
      - Passaremos Nosso **Output** atraves do **Asign** com:
        - **Output.Succes** (True)
        - **Output.Message** ("Avaliação atualizada com sucesso")
        - **Output.Id** (Rating.Id) -> O Id da tabela Rating do nosso **Source**
    - 4º Ambos encerram aqui se der Sucesso em criar ou atualizar
    - 5º Criando o fluxo de Exceção **AllExceptions**
      - 1º Se ocorrer um erro ou situação que não cobre o fluxo anterior, ele irá executar o nosso **AllExceptions**
      - 2º O mesmo irá passar o erro para o nosso **Output**:
        - **Output.Succes** (False)
        - **Output.Message** (AllExceptions.ExceptionMessage) -> Vai receber a propria ação de Erro, tornando dinamico.
        - Fim.

    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao02.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao03.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao04.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao05.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao06.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao07.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao08.png)
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao09.png)

- **2º** Criando o Pop-up(Modal) no **Modulo ARR_WEB**
  *1º* Add Componente a tela de Avaliação de Imóvel
  *2º* Esse componente espera uma **váriavel local** para validar a hora que **Abre** e **Fecha**
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao10.png)
  *3º* Add a váriavel local **ShowPopupRating** que está setada como Bollean e Default(false), pois queremos que ao entrar nessa página a mesma esteja desativada, somente abrirá quando acionarmos.
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao11.png)
  *4º* Atribuirmos a varivel local ao Popup, dessa forma agora o mesmo já recebe a variavel e podemos então criar o fluxo de **ClientAction** para abrir e fechar.
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao12.png)
  *5º* Criando o **ClientAction** para abrir e fechar o popup, para fazer esse passo lembra que colocamos a variável como padrão (False), ou seja será ativado a partir do inverso desse default.
  - Vamos criar o **ClientAction** de **OnClick** no Container de **Card de Avaliação**, pois como está dinamico uma vez que eu aplique no container cada card chamará essa ação.
  - Então a ativação será atraves de um click no Card dos Imoveis, dessa forma no componente a opções de evento onde vamos adicionar o **O tipo de evento(on click)** e o **Handler(ShowPopupRating)** no caso que recebe a nossa variável local.
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao13.png)
  - A ação criada **ShowPopupRating**, que a lógica será um **not** + variavel local
  - O que explicamos que a variavel esta como default False ou seja o (not) irá realizar o inverso dela que será (True)
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao14.png)
  *6º* Vamos implementar agora o nosso **ModalAvaliacao(Popup)** na tela
    - Criamos uma váriavel local para receber nossa tabela **Rating** que será usada no **Formulário** após arrastamos para nosso **Widget Tree** para o formulário dentro do popup, que será as informações que vamos trabalhar.
   ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao15.png)
    - Ajustamos nossa estrutura onde **Título e Subtitulo** recebe uma expression que depois vamos colocar para que sempre que for um apartamento ou caso mude e também o icone que vira depois.
    - Ajustamos os campos do formulário, para que fique o de acordo com nosso mockup
    - Criamos os botões de **Cancelar** que recebe a ação **ShowRating** para fechar o popup, que é a negativa (not) da variavel local default (False) ou seja se estiver fechado abrirá se estiver aberto fechará e o botão **Save** ainda sem fluxo.
   ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao16.png)
- Uma vez que criamos o form do Modal até aqui, vamos realizar alguns ajustes para que a tela fique mais fluida.
	- 1º - Vamos trocar o input de checkbox das recomendações para um "Radio group" que nos dará a opção de sim ou não.
	![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao17.png)
	![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao18.png)
	![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao19.png)
	- 2º - Vamos alterar o campo de "Observação" que está com Input, porém o mais adequado é um "textArea".
		- Lembrando que sempre que trocar um input ou checkbox ocorrerá um erro com Label, pois sempre vem vinculado ao input, desta maneira temos que altera-lo também, em alguns campos como textarea é onde usamos radiogroup não são necessários o vinculo neste caso então podemos colocar o Label como "None".
	![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao20.png)
	- 3º - Alterando o Título e descrição do popup para retornar se é casa ou apartamento e o endereço, de forma dinâmica antes de persistir nossos dados.
		- Antes colocamos essas duas expressions como vazia com um dafault de valor padrão
	![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao21.png)
	- Para deixar dinâmico vamos ter que criar duas variáveis locais "TypeImmobile" e "ImmobileAddress" e atribui-las a nossa ação "ShowPopupRating" através do Asign,
   	essa função é usada para que quando clicarmos em um card ela abrirá com formulário de avaliação com algumas informações setadas.
		- Ambas as variáveis locais devem ser do tipo texto 
		![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao22.png)
		- Como vemos na figura abaixo estamos preenchendo o Asign com 4 tipo de informações.
			- 1º - recebemos o parâmetro de entrada "ShowPopupRating" que abrirá o popup toda vez que for clicada o mesmo se iniciara com valor
     			False e a condição será "not ShowPopupRating".
			- 2º - Atribuímos nossa variável local "TypeImmobile" que é o título do nosso popup que trará se é casa ou apartamento a lógica foi:
			```Js
			If(GetImmobiles.List.Current.TypeImmobileId = Entities.TypeImmobile.Casa, "Casa", "Apartamento")
			```
			- 3º  - Atribuímos nossa variável local "ImmobileAddress" que é a descrição do nosso popup que trará a rua e o número a lógica do imóvel foi:
```Js
If(GetImmobiles.List.Current.TypeImmobileId = Entities.TypeImmobile.Casa, "Casa", "Apartamento")
```
		
- 4º - Pegaremos nossa variável local Rating selecionaremos o nosso ID e receberemos de valor o ID atual que esta sendo clicado.
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao24.png)
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao25.png)
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao23.png)
	- 4º - Persistindo os dados do "Popup" 
		- Vamos agora criar a lógica para persistir os dados ao clicar no botão "Salvar", através da Client Action "SaveOnClick" que já atribuímos ao botão
    		"Salvar" porém não havíamos criado a lógica.
			- 1º - Vamos inserir a Server Action "Rating_CreateOrUpdate" que criamos anteriormente no modulo server, uma vez que clicar no botão salvar
     			do nosso popup avaliações ele ira chamar a server action.
			- 2º - Colocamos um IF que validara SE a persistência de dados foi sucesso ou não.
				- SE **sim** ele retornara uma mensagem de **Sucesso** do nosso retorno da estrutura "Outupt.Success" que atribuímos a server action
					- Após a persistência ter sido sucesso chamamos um Asign para limpar nossas variáveis locais que atribuímos para pré-carregar
       					as informações do título, descrição e ID do nosso popup
					- Uma vez limpo chamamos outro Asign "ClosePopup" que ira chamar o parametro de entrada "ShowPopupRating" passando valor False
					- E finalizamos com END
				- SE **não** ele ele retornara uma mensagem de **Erro** do nosso retorno da estrutura "Outupt.Success" que atribuímos a server action
					- Apenas atribuímos um Asign vazio para deixar a estrutura mais visualmente agradável, não é necessária
					- E finalizamos com END
				- Segue abaixo cada parte da lógica acima: necessário 
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao26.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao27.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao28.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao29.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao30.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao31.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao32.png)
	- 5º - Vamos atribuir ao criar um novo dado no "Reating" o nosso Created At e Created By.
		- Para isso temos que ir para o Modulo de **SERVICES** pois e nele que iremos atribuir os mesmos.
		- Vamos ir no nosso fluxo da Server Action "Reting_CreateOrUpdate" no Source.
			- Onde está sendo atribuído a tabela **Rating** vamos atribuir campo por campo para configurar os campos "Created At" e "Created By"
		 ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao33.png)
		- Atribuindo funções para Created At [CurrDateTime()] e Created By[GetUserId()]
			- Essa alteração no modulo Services agora após salvar, iremos para o modulo Web atualizar as dependências para que reflita.
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao34.png)
		- Criando a tela "MyRating" onde após confirmar o Popup da anterior ira persistir e irá aparecer para a pessoa suas avaliações nessa tela.
			- 1º - Após criar a screen, puxamos da **Aba Data**, a tabela Immobile 
				- Com ela já veio a relação entre Immobile, TypeImmobile, User
			- 2º - Criamos um Join com a tabela **Rating** pois é nela que está as nossas avaliações.
				- Realizamos o **join** com a ligação (**Only with**) neste caso é necessário porque se não iria trazer todas os registros tendo ou não avaliações e queremos neste caso só trazer os dados caso contenha registros.
				- Criamos um filtro para resolver a questão de visibilidade ou seja o usuário logado só pode ver suas próprias avaliações, dessa forma criamos um filtro.
				```JS
				Rating.CreatedBy = GetUserId()
				```
			- 3º - A implementação da lógica foi: 
				- Vai na tabela de **imóveis** e traga o registro que possui **avaliações** e essas avaliações precisa ser exatamente relacionado ao ID de quem está logado no sistema, o usuário só verá os registros de avaliações dele.
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao35.png)
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao36.png)
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao37.png)
			
		- Uma vez que ajustamos a tela de "Minhas Avaliações" vamos organizar a tabela que será composta por:
			- 1º Endereço: 
			```JS
			Street + GetImmobiles.List.Current.Immobile.Street+", "+GetImmobiles.List.Current.Immobile.Street_Number
			```
			- 2º CEP : 
			```JS
			GetImmobiles.List.Current.Immobile.CEP
			```
			- 3º Avaliações: 
			```JS
			GetImmobiles.List.Current.TypeExperience.Label
			```
			- 4º Recomendações: 
			```JS
			If(GetImmobiles.List.Current.Rating.Recommend,"Sim","Não")
			```
			- 5º Quando
			```JS
			DateTimeToDate(GetImmobiles.List.Current.Immobile.CreatedAt)
			```
			![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao38.png)
		-  Criando o campo "Search" para pesquisar a avaliação.
			- A pesquisa será pelo **nome da rua** ou **Cep**
			- 1º - Adicionamos um Input Serach
			- 2º - Colocamos um placeholder para facilitar o entendimento do usuário.
			- 3º -  Criamos uma variável local "SearchRating" como text, que será nossa variável que capturará o valor que digitarmos.
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao42.png)
			- 4º Criamos no Input uma ação On Change: **SearchOnChange**, que será um delimitador de caracteres ou seja só será atualizado o campo de busca SE ao digitar no campo Search for >= 3 ou = 0 caracteres. Após será atualizado a tabela através de um refresh
				- Ao digitar no Input de pesquisa:
					- 1º - Iniciará a ação OnChange
					- 2º - Verificará se 
				```JS 
				Length(SearchRatings) >= 3 or Length(SearchRatings) = 0
				```
				- 3º - SE for **False** finaliza ou SE for **True** atualiza os dados da tabela
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao40.png)
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao41.png)
			- 5º Criamos o filtro no Agrregatte: GetImmobile que fará um like no campo Search da **rua** e **cep**
				![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao39.png)

-----------------------------------

## Documentação da 5ª Parte

## **Nesta Parte:**

- Ajustes no menu
- Evento de editar (tela minhas avaliações)
- Tela de Dashboard
- Como trazer dados de gráficos do módulo service
- Como manipular dados dos gráfico
- Adicionando atributo em aggregate
- Trabalhando com Switch
- Tela Imóveis que já morei
- Ajustes gerais

### Ajustando menu

- Ajustando o menu
	- Foi configurado com os nomes adequados para entendimento da navegação mais fluida
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao43.png)

-----------------

### Criando a tela do Dashboard

- A ideia desse dashboard é ter alguns gráficos que nos mostrará algumas métricas importantes.
	- Também criarmos a lógica desses gráficos no modulo de Services e consumi-los e estiliza-los no módulo Web.
- 1º - Acessando o Módulo Services, vamos até a aba "Logic" e vamos criar uma pasta para as ações de servidor especificas para o Dashboard como fizemos anteriormente com as demais.
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao44.png)
- 2º - Vamos criar uma Server Action para cada gráfico 
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao45.png)
	- Ambas as ações devem ser públicas para que eu possa consumir depois no módulo Web.
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao46.png)
- 3º - Criando a Server Action do Rating(Avaliações)
	- 1º - Arrastar um Aggregate para o fluxo 
	- 2º - Adicionamos a tabela Rating que sera nossa principal
	- 3º - Criamos um join (Only With) a tabela TypeExperience
		- Aqui fazemos isso porque a ideia é que seja contado a quantidade de avaliações por tipo, por exemplo 3 avaliações boas, 4 ruins ...
		- Para isso além do Join é preciso realizar um **Count** na **Rating.ID** para realizar a contagem e agrupar a **TypeExperience.Label** para trazer a contagem por tipo de avaliação.
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao47.png)
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao48.png)
	- 4º - Agora eu preciso passar esses dados de uma forma que o gráfico entenda, porque não estamos passando esse aggregate direto na tela no módulo Web.
		- Dessa forma para passar vou precisar de uma estrutura determinada que é o **Datapoint** do gráfico 
		- Para isso vamos puxar essa dependência dentro do módulo service
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao49.png)
		- Uma observação a OutSystems trabalha com os modelos de gráficos da **Highcharts** dessa maneira caso tenha algum gráfico lá que possa interessar é provável que possa ser importado para a OutSystems. 
		- Seleciono a dependência que eu quero e aplico 
			- Após isso irei inserir 2 **parâmetros de saída**
				- 1º -  Será **Output** que é nossa estrutura de retorno das mensagem e sucesso
				- 2º - Vamos adicionar o parâmetro de saída, referente ao DataPoint que adicionamos.
					- Para isso temos que primeiro clicar em Add Parâmetro de saída
					- Depois clicar na seta do campo **Data Type** selecionar o tipo **List** e só depois rolar para baixo e selecionar **DataPoint**
					- Isso deve ser feito porque por padrão o parâmetro de saída vem como somente record só que queremos vários datapoints ou seja uma **Lista de Dados**
				![Parte 5](./Assets/Parte%205/img/ModalAvaliacao50.png)
				![Parte 5](./Assets/Parte%205/img/ModalAvaliacao51.png)
				![Parte 5](./Assets/Parte%205/img/ModalAvaliacao52.png)
				![Parte 5](./Assets/Parte%205/img/ModalAvaliacao53.png)
	- 5º - Vamos estruturar agora a lógica do fluxo da Server Action (Ratting)
		- 1º - Criamos nosso Aggregate, realizamos os joins e configuramos nossos parâmetros de saída
		- 2º - Agora vamos arrastar a **Run Server Action** digitar List -> que retornará a função **ListAppendAll** que permite passar os valores vindo do nosso Aggregate para o nosso DataPoint
		- 3º - Uma vez setada o **ListAppendAll** vamos adicionar um Asign que receberá o nosso **Output** caso retorne sucesso e finaliza.
			- Output.Success = True
			- Output.Massage = "Dados coletados com sucesso"
		- 4º - Criando a lógica de exceção através do **AllExpections** -> vamos inserir um **Asign** que receberá e finaliza ao final
			- Output.Success = False
			- Output.Massage = AllExcepetion.ExcepetionMessage (receberá a mensagem de erro da propria **AllExpections**)
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao54.png)
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao55.png)
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao56.png)
		![Parte 5](./Assets/Parte%205/img/ModalAvaliacao57.png)
- 4º - Criando a Server Action do ImmobileRegister
	- Da mesma forma que criamos a ServerAction anterior vamos crear a **ImmobileRegister** a ideia e obter a quantidade de IDs por Data de criação de Immobile 
	- 1º - Vamos adicionar os paremetros de entrada o Output e o Source neste serão o mesmo da anterior.
	- 2º - Vamos criar o fluxo:
		- a) Arraste a tabela **Immobile da aba Data** após isso vamos abrir e realizar a seguinte ação:
			- Count -> Immobile.Id
			- GroupBy CreatedAt -> Immobile.CreatedAt
		- b) Após isso temos que carregar nosso **DataPoint** para que seja consumido no módulo Web e posterior criar o gráfico, preenchendo os campos através do **ListAppendAll** com:
			- List -> DataPoint
			- SourceList -> GetImmobiles.List
				- Value -> Count
				- Label -> CreatedAt
		- c) Uma vez preenchido o ListAppendAll, vamos preencher nosso **Assign**
			- Output.Succes -> True
			- Output.Massage -> "Dados coletados com sucesso"
		- d) Vamos criar a lógica de Exceção que será a mesma da Server Action anterior através do **AllExpections** -> vamos inserir um **Asign** que receberá e finaliza ao final
			- Output.Success = False
			- Output.Massage = AllExcepetion.ExcepetionMessage (receberá a mensagem de erro da propria **AllExpections**)
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao58.png)
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao59.png)
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao60.png)
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao61.png)
	![Parte 5](./Assets/Parte%205/img/ModalAvaliacao62.png)
- 5º - Vamos para o **Módulo Web** para consumir o que criamos no módulo server.
	- Sempre após alteração no Server publique após vá para o módulo WEB agora e clique na tomada de conexão que é a atualização de dependência, aplique e salve.
	- 
-------------

## EM CRIAÇÃO ..... EM BREVE PARTE 5
