# App Avaliação de Imóveis em OutSystems

Aplicação em OutSystems Reactive de Avaliações de Imóveis

## Índice - PT

- [1ª Parte - Título da Parte 1](#documentação-da-1ª-parte)
- [2ª Parte - Título da Parte 2](#documentação-da-2ª-parte)
- [3ª Parte - Título da Parte 3](#documentação-da-3ª-parte)
- [4ª Parte - Título da Parte 4](#documentação-da-4ª-parte)
- [5ª Parte - Título da Parte 5](#documentação-da-5ª-parte)

## Readme in English - EN

If you are an English reader, visit the link below:

- [Click here documentation](/README-EN.md)

## Readme en Español - ES

Si eres un lector en español entra en el seguinte enlace:

- [Haga clic aquí](/README-ES.md)

-----------------------------------

## Documentação da 1ª Parte

- Entendendo o projeto através do template
- Criando o projeto em dois módulos Web e Services
- Entendendo a separação de responsabilidades
- Criando a arquitetura do banco de dados

### Mockups e Template das Telas

Antes de começar a implementação, iniciamos com o entendimento dos mockups das telas utilizando o **Drawio** e a importância de ter uma template visual, com os benefícios que pode trazer.

Esse planejamento visual ajudou a garantir que todos os elementos fossem claramente definidos antes da implementação, trazendo clareza à aplicabilidade.

As telas incluem:

- Tela de Login  
  ![Figura do Mockup - Tela de Login](./Template/img/mockup-tela-login.png)
- Dashboard  
  ![Figura do Mockup - Dashboard](./Template/img/mockup-dashboard.png)
- Cadastro de Imóvel  
  ![Figura do Mockup - Cadastro de Imóvel](./Template/img/mockup-cadastro-imovel.png)
- Avaliar Imóvel  
  ![Figura do Mockup - Avaliar Imóvel](./Template/img/mockup-avaliar-imovel.png)
- Pop-up Avaliar Imóvel  
  ![Figura do Mockup - Pop-up Avaliar Imóvel](./Template/img/mockup-popup-avaliar-imovel.png)
- Minhas Avaliações  
  ![Figura do Mockup - Minhas Avaliações](./Template/img/mockup-minhas-avaliacoes.png)
- Meus Imóveis  
  ![Figura do Mockup - Meus Imóveis](./Template/img/mockup-meus-imoveis.png)
- Imóveis que já morei  
  ![Figura do Mockup - Imóveis que já morei](./Template/img/mockup-imoveis-que-ja-morei.png)

### Estrutura do Projeto

1. **Módulo AAR_Services (Service)**:
   - Responsável pela lógica de backend, incluindo a arquitetura do banco de dados, os relacionamentos e as ações CRUD.
   - O módulo foi configurado para ser **público**, permitindo que outros módulos acessem suas funcionalidades como leitura.
   - A arquitetura de entidades foi projetada para ser clara e garantir a integridade dos dados.  
     O diagrama de entidade (ER) foi criado para facilitar a visualização e segue abaixo uma prévia de cada tabela:
     ![Diagrama ER](./Assets/Parte%201/img/Data/ER/ER01.png)
   - **Criamos o diagrama ER**:  
     ![Diagrama ER](./Assets/Parte%201/img/Data/ER/ER01.png)
   - **Tabelas Criadas**:
     - **Tabela Immobile**: Contém os dados dos imóveis cadastrados, como CEP, endereço, cidade, proprietário, entre outros.  
       ![Diagrama ER](./Assets/Parte%201/img/Data/Table/ER_Immobile.png)
     - **Tabela Rating**: Armazena as avaliações dos imóveis, incluindo informações como tempo de locação, recomendações e observações dos usuários.  
       ![Diagrama ER](./Assets/Parte%201/img/Data/Table/ER_Rating.png)
     - **Tabela TypeExperience**: Armazena os tipos de experiência relacionados aos imóveis. Possui registros como **Excelente, Bom, Neutro, Ruim, Péssimo**.  
       ![Tabela TypeExperience](./Assets/Parte%201/img/Data/Table/ER_TypeExperience.png)
     - **Tabela TypeImmobile**: Armazena os tipos de imóvel disponíveis (ex.: Casa, Apartamento, Loja). Possui registros como **Casa, Apartamento, Loja**.  
       ![Tabela TypeImmobile](./Assets/Parte%201/img/Data/Table/ER_TypeImmobile.png)
     - **Tabela UserxImmobile**: Relaciona usuários aos imóveis, indicando propriedades e ocupação.  
       São tabelas auxiliares que armazenam os tipos de experiência, tipos de imóvel e a relação entre usuários e imóveis.  
       ![Tabela UserxImmobile](./Assets/Parte%201/img/Data/Table/ER_UserxImmobile.png)
     - **Tabela User**: Utiliza a entidade padrão do sistema OutSystems para armazenar informações dos usuários, como data de criação e última alteração.  
       ![Tabela User](./Assets/Parte%201/img/Data/Table/ER_User.png)
2. **Módulo AAR_WEB**:
   - Responsável pelo front-end e pelas telas da aplicação.
   - Foi adicionado como dependência ao **AAR_WEB**, com acesso somente leitura, para garantir a segurança e centralizar toda a lógica de servidor no módulo **AAR_Services**.
   - No módulo web/reactive, é possível observar as abas completas, incluindo **Triggers, Interface, Logic, e Data**.  
     ![Estrutura do Módulo AAR_WEB](./Assets/Parte%201/img/Model/estrutura-aar-web.png)

### Conclusão

Essa primeira etapa do projeto incluiu a configuração inicial dos módulos e a criação das entidades do banco de dados, além da definição da interface do usuário.  
Utilizamos uma abordagem modular que facilita a manutenção e a segurança dos dados, separando a lógica de servidor do front-end.

Na próxima etapa, vamos nos concentrar em finalizar a estruturação das telas no módulo **AAR_WEB**, garantindo que todas as funcionalidades estejam alinhadas ao objetivo do projeto.

-----------------------------------

## Documentação da 2ª Parte

- Criação da Tela de Login e Cadastro de Imóveis e suas lógicas

### Tela de Login

- Aqui podemos observar, à direita, que por padrão a tela de Login da própria OutSystems vem com:  
  ![Tela de Login](./Assets/Parte%202/img/Tela%20Login/Login01.png)

#### 4 Variáveis Locais

- **Username**: Consumida no Input **E-mail**  
  ![Var Username](./Assets/Parte%202/img/Tela%20Login/Var_Username.png)
- **Password**: Consumida no Input **Senha**  
  ![Var Password](./Assets/Parte%202/img/Tela%20Login/Var_Password.png)
- **IsExecuting**: Utilizada para informar a execução de algo na ClientAction **OnInitialize**  
  ![Var IsExecuting](./Assets/Parte%202/img/Tela%20Login/Var_IsExecuting.png)
- **Remember**: Consumida no Input de Checkbox **Lembrar-me**  
  ![Var Remember](./Assets/Parte%202/img/Tela%20Login/Var_Remember.png)

#### 3 Client Actions

- **ForgotPassword**: Para recuperar a senha  
  ![ForgotPassword](./Assets/Parte%202/img/Tela%20Login/Client/ForgotPassword.png)
- **Login**: Usado no botão **Entrar**  
  ![Login](./Assets/Parte%202/img/Tela%20Login/Client/Login.png)
  - A lógica do Login recebe a variável local **IsExecuting** como True após o clique:  
    ![IsExecuting](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-IsExecuting.png)
  - Em seguida, a ServerAction **DoLogin** é chamada:
    - Recebe as variáveis locais: Username, Password, Remember.
    - Persiste os dados e verifica se foram salvos no banco.
    - Chama a ServerAction padrão de Login da OutSystems (dentro de User).  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin01.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin02.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)
  - Após, remove uma mensagem de feedback ao logar.
  - Por fim, redireciona o usuário para a tela principal:  
    ![Redirect](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)
- **OnInitialize**:
  - Executa ações após o carregamento da tela (como na imagem abaixo):  
    ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize01.png)
  - Utiliza a variável local "IsExecuting" (padrão False, sem ação inicial).  
    ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize.png)

-----------------------------------

### Mudando as ações de Autenticação para o caminho correto

- A lógica de servidor deve residir no módulo **ARR_Service**:
  - Recorte a ação da **ARR_WEB** e cole na **AAR_Service**, na aba **Logic**, e publique.  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin.png)
  - Torne a ação pública antes de publicar, para que seja acessível de outros módulos.  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin01.png)
  - Aponte as dependências (busque o módulo, clique, adicione e “Apply”).  
    Os erros desaparecerão:  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin02.png)

-----------------------------------

## Tela de Cadastro de Imóveis

### Módulo ARR_WEB

- Exemplo de tela:
  ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela.png)
- A partir da aba **Data**, arraste para o **MainFlow**:
  - As duas telas são criadas:  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela01.png)
  - **Immobiles**: Tela de Listagem  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela02.png)
  - **ImmobileDetail**: Tela de registro
    - Remova o IF padrão (que indica "Cadastrar" ou "Editar") e substitua por uma Expression:
      - Se ImmobileId for nulo, exiba "Cadastrar"; senão, "Editar" concatenado com "Imóvel":

        ```javascript
        If(ImmobileId = NullIdentifier(), "Cadastrar", "Editar") + " Imóvel"
        ```

    - Remova o Form dentro da Column1 para que ele expanda:  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela03.png)  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela04.png)
    - Arraste o **Adaptive/Columns2** para dentro do Form, dividindo as colunas:  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela05.png)
    - O layout ajustado fica assim:  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela06.png)
    - Troque o checkbox por radioGroup para melhor visualização:
      - Configure o Label como None (não vinculado) e ajuste a posição dos botões.  
        ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela07.png)
    - Verifique a ClientAction **SaveDetail** para a persistência dos dados:  
      ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail.png)
      - Nota: A persistência ainda não está ativa:  
        ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail01.png)
      - Visualmente, a tela ficou assim:  
        ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail02.png)

### Módulo: ARR_Services

#### Tela Cadastrar Imóvel e Editar Imóvel

- Persistência dos dados na Tela "Cadastrar Imóvel":
  - Crie uma pasta com o nome da Tabela correspondente.
  - Crie a ação para persistir os dados.

- **Server Action: Immobile_CreateOrUpdate**  
  ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate.png)
  - A ação espera:
    - **Parâmetro de Entrada**: Immobile  
      (Para persistir a Tabela Immobile, use o parâmetro Immobile.)
    - **Parâmetro de Saída**: Output  
      - Crie uma Structure para o Output:  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate01.png)
      - Defina os atributos:
        - Success (padrão false)  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate03.png)
        - Message  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate04.png)
        - AccessKey  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate05.png)
        - Id (Long Integer)  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate06.png)
      - Após criar a Structure, defina o Parâmetro de Saída:  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate07.png)
  - Crie o fluxo da ServerAction:  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate08.png)
  - **Validação Inicial:**  
    - Verifique se o usuário é igual a NullIdentifier():  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate09.png)
  - Se **Immobile.Id** for nulo (novo registro):
    - Se Sim: Execute **CreateImmobile**
    - Se Não: Execute **UpdateImmobile**  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate10.png)
    - Caso seja um novo registro, preencha os campos **CreatedBy** e **CreatedAt** antes de persistir:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate11.png)
    - No Source, remova o Immobile e adicione os campos individualmente:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate12.png)
    - > ⚠️ **ATENÇÃO:** Utilize os valores do parâmetro de entrada para os campos, exceto **CreatedBy** (use GetUserId()) e **CreatedAt** (use CurrDateTime()).  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate13.png)  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate14.png)  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate15.png)
    - Os campos **CreatedBy** e **CreatedAt** são os únicos que não usam o valor do parâmetro de entrada.
      - **CreatedBy:** Função GetUserId()
      - **CreatedAt:** Função CurrDateTime()  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate16.png)
    - Observação:
      - Em **UpdateImmobile**: Atribua diretamente o parâmetro de entrada.  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate19.png)
      - Em **CreateImmobile**: Atribua os campos individualmente, estilizando o CreatedBy com GetUserId().  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.png)
  - Atribuição dos parâmetros de saída:
    - **1º:** Crie um Assign para o CreateImmobile, onde Output.Id recebe o ID do CreateImmobile.  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.1.png)
    - **2º:** Crie um Assign para o UpdateImmobile, onde Output.Id recebe o ID do registro atualizado.  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate22.png)  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate23.png)
- >❗ **EXCEÇÃO:**  
  - Adicione uma exceção ao fluxo, escolhendo "Todas as Exceptions":  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate24.png)
  - Em um Assign, configure:
    - Output.Success = False
    - Output.Message = AllExceptions.ExceptionMessage  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate25.png)
  - Na exceção AllExceptions, o fluxo aborta (Abort Transcription = Yes).  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate26.png)

### Módulo: ARR_WEB

- Remova os elementos não utilizados:
  - Exclua o Aggregate **GetUsers**:  
    - ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate27.png)  
    - ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate28.png)
- Crie o fluxo da **Client Action: SaveDetail**:
  - Valide se o formulário é inválido (False):  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate29.png)
  - Se válido, chame a ServerAction Immobile_CreateOrUpdate (passando o parâmetro Immobile):  
    - ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate30.png)  
    - ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate31.png)
  - Utilize um IF para verificar a persistência:
    - Se falso, exiba mensagem de ERRO (Output.Message):  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate32.png)
    - Se verdadeiro, exiba mensagem de SUCESSO e redirecione para a tela de listagem **Immobiles**:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate35.png)
    - Finalize com REDIRECT:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate36.png)
- Valide em tela a persistência (observação: o CEP ainda está fictício; usaremos uma API para o CEP):  
  ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate37.png)

### PRÓXIMA ETAPA

- ✨ **IMPLEMENTANDO O CEP**:
  - 🛠️ Crie uma ação **OnChange** para o campo **CEP**.
  - ✏️ Quando o campo **CEP** for alterado, um evento OnChange chamará um serviço que, se o CEP existir, preenche automaticamente logradouro, bairro e cidade.

-----------------------------------

## Documentação da 3ª Parte

- Criando Telas e lógica de Login e Cadastro de Imóveis:
  - Ajustes de labels
  - Utilização de componente da Forge (api)
  - Segurança da aplicação com AccessKey
  - Eventos OnChange
  - Evento OnScroolingEnd
  - Geração de AccessKey randômico
  - Utilização de Widget List ao invés de TableList
  - Join entre tabelas
  - Tela Meus Imóveis
  - Tela Avaliar Imóveis

## Start

## Gerando AccessKey randômico

- Atualmente, a edição ou ações exibidas na URL expõem o ID, o que gera vulnerabilidade.
- Para segurança, será utilizado o AccessKey, que mascara o ID.  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey.png)

### Access Key ARR_SERVICES

- No módulo Services, a ServerAction (**Immobile_CreateOrUpdate**) possui no Output os parâmetros (*Success, Message, AccessKey, Id*).
- Porém, o fluxo (**CreateImmobile**) ainda não recebe o **AccessKey** pois não foi atribuído à tabela.  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey01.png)

#### Criando o Access Key

- 1º Crie um atributo na tabela Immobile na aba **Data**:
  - O atributo deve ser do tipo **Text** (para receber uma HASH).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey02.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey03.png)
- 2º No fluxo da ServerAction (**Immobile_CreateOrUpdate**), na ação **CreateImmobile**, a AccessKey estará disponível.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey04.png)
- 3º Utilize uma função do sistema para gerar a AccessKey:
  - Nas dependências, adicione a ServerAction (**GenerateGuid**).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey05.png)
- 4º Retorne ao fluxo da ServerAction (**Immobile_CreateOrUpdate**) e atribua a função ao atributo AccessKey do Immobile.  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey06.png)
  - Assim, cada novo registro gerará um AccessKey para ser utilizado no ARR_WEB no lugar do ID.
- 5º Publique e vá para o ARR_WEB.

### Access Key ARR_WEB

- No ARR_WEB, atualize as dependências (Refresh all → Apply → Publicar).  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey07.png)
- 1º A tela **ImmobileDetail** espera um parâmetro de entrada (**Immobile Identifier**); substitua-o por **AccessKey**:
  - DataType: **Text** (para receber uma hash).
  - Não precisa ser obrigatório.
  - Também altere o GET e a lista.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey08.png)
- 2º Altere o **GetImmobileBy**:
  - O filtro deve comparar **Immobile.AccessKey** com o parâmetro **AccessKey**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey10.png)
- 3º No filtro do **GetImmobileBy**, defina o MaxRecord como 1 (busca única).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey11.png)
- 4º Na lista de imóveis, altere o parâmetro de entrada para **AccessKey**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey12.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey13.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey14.png)

-----------------------------------

## Utilizando componente da Forge (api) CEP

- ✨ **IMPLEMENTANDO O CEP**:
  - 🛠️ Crie uma ação **OnChange** para o campo **CEP**.
  - ✏️ Ao alterar o campo **CEP**, o evento OnChange chamará um serviço que:
    - Se o CEP existir, preenche logradouro, bairro e cidade automaticamente.
    - Caso contrário, exibe uma mensagem de erro.

### Baixando o Componente na Forge (ViaCEP)

- Baixe o componente ViaCEP - Endereços:
  - Na aba **Forge**, procure por **ViaCEP** e instale-o no Studio.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP.png)

### Aplicando ARR_WEB

- 1º O componente ViaCEP é uma aplicação separada; adicione-o como dependência ao ARR_WEB.
  - Ele possui uma ServerAction (**CEP**) que recebe um parâmetro (CEP) e retorna um Output com os dados do endereço.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP01.png)
  - Após aplicar, ele aparecerá na aba **Logic**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP02.png)
- 2º Na tela, no campo Input **CEP**, crie uma ação OnChange que acione uma trigger para chamar o serviço CEP.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP03.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP04.png)
- 3º Aplicando a lógica:
  - Adicione um IF: se o comprimento do CEP for maior que 7 (ou seja, 8 caracteres ou mais):

    ```js
    Length(GetImmobileByAccessKey.List.Current.Immobile.CEP) > 7
    ```

  - Se falso, finalize; se verdadeiro, chame a API ViaCEP para obter os dados do CEP.
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP05.png)
  - Arraste a ação **Via_CEP : CEP** da aba Logic, configure os parâmetros e conecte à condição.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP06.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP07.png)
  - Configure os campos de Input para receber os valores do Output do CEP:
    - 1º Valide se o serviço retornou dados.
    - 2º Se CEP.Output.Erro for True, finalize.
    - 3º Caso contrário, use um Assign para preencher os campos de endereço.  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP10.png)  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP11.png)  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP12.png)
    - 4º Crie um Assign para limpar os campos caso haja alteração no CEP e o serviço retorne erro.  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP13.png)
    - ⚠️ **APRENDIZADO:** O OnChange permite buscar e manipular dados com base no valor preenchido.

-----------------------------------

## Tela Meus Imóveis

- Tela de Listagem de Imóveis:
  - Inicialmente, reutilize a tela para criar a listagem de imóveis.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis01.png)
- Ajustes iniciais (para se aproximar do template):
  - 1º Altere o nome da página.
  - 2º Remova o link "Casa" (será usado no logradouro para edição).
  - 3º Edite as posições das colunas.
  - 4º Renomeie o botão para **Cadastrar Imóvel**.
  - 5º Adicione o link de edição na coluna **Logradouro**.
  - 6º Adicione a coluna de **Ação** com ícone de **Delete**.
  - 7º Adicione a coluna de **Cadastro**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis02.png)
- Configuração das **Expressions**:
  - 1º **Avaliações**: exibe a soma das avaliações do endereço.
    - Altere o Aggregate (GetImoveis) para fazer o join com a tabela de avaliações e agrupar os dados:
      - Crie um join:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis03.png)
      - O join pode ser configurado como **With or Without** para trazer registros com ou sem avaliação.
      - Utilize **Group by** e **Count** para agrupar e contar:
        - Group by (ex.: CEP, Id, Street, Street_Number, CreatedAt, TypeMobile, AccessKey)  
          ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis06.png)
        - Count dos registros:  
          ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis05.png)
      - O Aggregate passa a mostrar apenas os campos agrupados:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis08.png)
      - Retire a reordenação das colunas:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis09.png)
      - Atualize as Expressions com os novos valores do Aggregate:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis10.png)
      - Resultado final:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis11.png)
  - 2º Ajuste a formatação do campo **Criado em** utilizando a função DateFormate():  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis12.png)
  - 3º Ajuste a ação do **Search** para buscar por CEP e Logradouro:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis13.png)
- Criando a Ação **DELETE**:
  - 1º Crie uma ClientAction (no módulo ARR_WEB) vazia inicialmente.
  - 2º Crie a ServerAction no módulo ARR_Server:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete01.png)
  - 3º Na aba **Data**, arraste a ação de Delete da tabela Immobile para a ServerAction, adicionando o parâmetro ID.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete02.png)
  - 4º Configure o Output do CRUD:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete03.png)
  - 5º Crie o fluxo de exceção (AllExceptions):  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete05.png)
  - 6º No módulo ARR_WEB, configure o fluxo que chama a ServerAction e exibe as mensagens de sucesso ou erro:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete01.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete02.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete03.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete04.png)

## CRIANDO TELA DE AVALIAÇÕES

- **1º** Organize a Tela de Avaliação utilizando um componente **List** (Main Content > List > Container > Content\CardsSectioned).  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel01.png)
- **2º** Crie um Aggregate específico para esta tela:
  - Relacione a tabela **Immobile** com **UserXImmobile** (para trazer os imóveis em que o usuário já morou).
  - Relacione **Immobile** com **TypeImmobile** (usando join Only With).
  - Relacione **Immobile** com **Rating** (usando join With or Without).
  - Agrupe as informações e conte as avaliações:
    - Group by: Immobile.Id, Immobile.Street, Immobile.Street_Number, TypeImmobile.Label, Immobile.AccessKey  
    - Count: Rating.Id  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel03.png)
- **3º** Adicione o Aggregate ao Source:
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel04.png)
  - Atualize as Expressions e estilize o Container:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel05.png)
  - Crie um Group By em **TypeImmobile.Id** para exibir ícones conforme o tipo de imóvel:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel06.png)
  - Crie um IF para exibir o ícone de acordo com o **TypeImmobile**:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel07.png)
- **4º** Implemente o scroll infinito para carregar mais registros conforme o usuário rola:
  - Configure o evento **On Scroll Ending** do componente List com uma Client Action "New Infinite Scroll Client Action".  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel08.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel09.png)
  - A Client Action "ScrollEnding" utiliza uma variável local **MaxRecords** para definir quantos registros serão exibidos inicialmente.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel10.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel11.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel12.png)

-----------------------------------

## Documentação da 4ª Parte

- Pop-up de Avaliação, Tela Minhas Avaliações, Imóveis que já morei e Ajustes Gerais:
  - Ajustes no menu
  - Modal de avaliação
  - Persistência de dados
  - Tela Minhas Avaliações
  - Tela Imóveis que já morei
  - Ajustes gerais

### Criando Modal de Avaliação

- Exibição do modal:  
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao01.png)
- **1º** No módulo ARR_SERVICES, crie a ServerAction **Rating_CreateOrUpdate**:
  - Fluxo:
    - Se for um novo registro, utilize o CRUD "CreatingRating" e, via Assign, defina:
      - Output.Succes = True  
      - Output.Message = "Avaliação criada com sucesso"  
      - Output.Id = CreateRating.Id
    - Caso contrário, utilize o CRUD "UpdateRating" e defina:
      - Output.Succes = True  
      - Output.Message = "Avaliação atualizada com sucesso"  
      - Output.Id = Rating.Id
    - Ambos os fluxos se encerram com sucesso.
    - Em caso de exceção, via AllExceptions, defina:
      - Output.Succes = False  
      - Output.Message = AllExceptions.ExceptionMessage  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao02.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao03.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao04.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao05.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao06.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao07.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao08.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao09.png)
- **2º** No módulo ARR_WEB, crie o Pop-up (Modal) de Avaliação:
  - Adicione um componente para o popup e uma variável local **ShowPopupRating** (Boolean, default False).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao10.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao11.png)
  - Atribua a variável ao Popup.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao12.png)
  - Crie uma ClientAction (ex: **ShowPopupRating**) para inverter o valor da variável (para abrir/fechar o popup).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao13.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao14.png)
  - Crie uma variável local para armazenar a tabela **Rating** a ser usada no formulário do popup.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao15.png)
  - Ajuste a estrutura do popup (título, subtítulo, campos do formulário) conforme o mockup.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao16.png)
- Ajustes adicionais:
  - 1º Troque o input de checkbox por um **Radio group** para as recomendações.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao17.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao18.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao19.png)
  - 2º Altere o campo "Observação" para um **textArea** e defina o Label como "None".  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao20.png)
  - 3º Configure o Título e descrição do popup para serem dinâmicos, utilizando variáveis locais (por exemplo, "TypeImmobile" e "ImmobileAddress") que são atribuídas na ação **ShowPopupRating**.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao21.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao22.png)
  - 4º Capture o ID da avaliação ao clicar, utilizando a variável local Rating.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao24.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao25.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao23.png)
  - 5º Para persistir os dados do popup, crie a ClientAction **SaveOnClick** que:
    - Chama a ServerAction **Rating_CreateOrUpdate**.
    - Utiliza um IF para verificar se o Output indica sucesso ou erro e exibe a mensagem correspondente.
    - Se for sucesso, limpe as variáveis locais e feche o popup (atribuindo ShowPopupRating = False).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao26.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao27.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao28.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao29.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao30.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao31.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao32.png)
  - 6º Em **Rating_CreateOrUpdate** (módulo Services), configure os campos **CreatedAt** (CurrDateTime()) e **CreatedBy** (GetUserId()).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao33.png)
    - Atualize as dependências no módulo Web.  
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao34.png)
  - 7º Crie a tela "MyRating" para listar as avaliações do usuário:
    - Utilize a tabela Immobile com join na tabela **Rating**.
    - Adicione um filtro para que somente as avaliações do usuário logado sejam exibidas:

      ```js
      Rating.CreatedBy = GetUserId()
      ```

    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao35.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao36.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao37.png)
    - Organize as colunas (Endereço, CEP, Avaliações, Recomendações, Data) e formate datas com DateTimeToDate().
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao38.png)
    - Crie um campo "Search" para buscar avaliações por rua ou CEP:
      - Crie uma variável local "SearchRating" (Texto).
      - Configure a ação OnChange (ex: "SearchOnChange") para atualizar a lista se o comprimento do texto for >= 3 ou igual a 0:

        ```js
        Length(SearchRatings) >= 3 or Length(SearchRatings) = 0
        ```

      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao42.png)  
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao40.png)  
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao41.png)
      - No Aggregate, crie um filtro utilizando LIKE para os campos rua e CEP.  
        ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao39.png)

-----------------------------------

## Documentação da 5ª Parte

- **Nesta Parte:**
  - Ajustes no menu
  - Evento de editar (tela minhas avaliações)
  - Tela de Dashboard
  - Consumo de dados de gráficos do módulo Services
  - Manipulação dos dados dos gráficos
  - Adição de atributo em Aggregate
  - Uso de Switch
  - Tela Imóveis que já morei
  - Ajustes gerais

### Ajustando menu

- Configure o menu com nomes padronizados para facilitar a navegação.  
  ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao43.png)

-----------------------------------

### Criando a tela do Dashboard

- O dashboard exibirá gráficos com métricas importantes.
- 1º No módulo Services, na aba "Logic", crie uma pasta para ações de servidor do Dashboard.  
  ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao44.png)
- 2º Crie uma ServerAction para cada gráfico.  
  ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao45.png)
  - As ações devem ser públicas.  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao46.png)
- 3º Criando a ServerAction do Rating (Avaliações):
  - I - Arraste um Aggregate e adicione a tabela **Rating**.
  - II - Crie um join (Only With) com a tabela **TypeExperience**.
    - Realize um Count em Rating.ID e agrupe por TypeExperience.Label.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao47.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao48.png)
  - 4º Passe os dados para uma estrutura compatível com gráficos, utilizando **DataPoint**.
    - Adicione 2 parâmetros de saída:
      - Output: estrutura com mensagem e sucesso.
      - Um parâmetro do tipo List of DataPoint.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao50.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao51.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao52.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao53.png)
  - 5º Estruture o fluxo da ServerAction (Rating):
    - I - Crie o Aggregate com os joins e configure os parâmetros de saída.
    - II - Utilize a ação ListAppendAll para transferir os dados do Aggregate para o DataPoint.
    - III - Em um Assign, defina:
      - Output.Success = True  
      - Output.Message = "Dados coletados com sucesso"
    - IV - Configure o fluxo de exceção (AllExceptions):
      - Output.Success = False  
      - Output.Message = AllExceptions.ExceptionMessage  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao54.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao55.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao56.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao57.png)
- 4º Criando a ServerAction do ImmobileRegister:
  - De forma semelhante à ação de Rating, crie uma ação para contar registros de Immobile por data de criação.
  - I - Adicione os parâmetros.
  - II - No fluxo:
    - Arraste a tabela **Immobile**.
    - Realize um Count em Immobile.Id e agrupe por Immobile.CreatedAt.
    - Utilize ListAppendAll para preencher os DataPoints (Value = Count, Label = CreatedAt).
    - Em um Assign, defina:
      - Output.Success = True  
      - Output.Message = "Dados coletados com sucesso"
    - Configure o fluxo de exceção de forma semelhante.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao58.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao59.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao60.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao61.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao62.png)
- 5º No módulo Web, atualize as dependências e crie os gráficos:
  - Crie uma tela chamada **Dashboard**.
  - Adicione título e subtítulo.
  - No Widget Tree, crie um Card com um layout de 3 colunas:
    - Em Column1, adicione um componente **PieChart**.
    - Em Column2, adicione um componente **LineChart**.
  - Na aba Interface > Elements, crie “Fetch Data from Other Source” para os gráficos:
    - Clique com o botão direito na tela Dashboard e selecione "Fetch Data from Other Source".
    - No fluxo, arraste as ServerActions para RatingGraph e ImmobileRegisterGraph.
    - Em um Assign, defina:
      - Para RatingGraph: DataPointList = RatingGraph.DataPoint
      - Para ImmobileRegisterGraph: DataPointList = ImmobileRegister.DataPoint
    - Configure os Outputs de cada Fetch como List of DataPoint.
    - Nos componentes de gráfico, defina a propriedade DataPointList utilizando os Outputs:
      - PieChart: RatingGraph.DataPointList
      - LineChart: ImmobileRegisterGraph.DataPointList  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao64.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao66.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao67.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao76.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao68.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao69.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao70.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao71.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao72.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao73.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao74.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao75.png)

-----------------------------------

### Criando a tela do "Imóveis que já morei"

- Nesta tela, o objetivo é utilizar um atributo calculado no Aggregate.
  - Configure o Dashboard como tela principal.
  - Crie uma Screen chamada **ImmobileLived**.
  - No Aggregate desta Screen:
    - Adicione a tabela **Immobile** e realize um Join com a tabela **UserXImmobile**.
    - Exiba os campos: Imóvel, CEP, Endereço + Número.
    - Adicione um Switch para indicar se o usuário já morou na residência.
      - Crie um novo atributo (New Attribute) no Aggregate com a fórmula:

        ```js
        CreatedAt <> NullDate()
        ```

  - Vincule o atributo ao componente Switch.
- No módulo Services, crie a lógica para o Switch:
  - Crie 3 ServerActions:
    - **UserXimmobile_CreateOrUpdate**: para criar ou atualizar o registro.
    - **UserxImmobile_Delete**: para deletar o registro.
    - **StatusChange**: para determinar, com base no status, se cria ou deleta o registro.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao84.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao85.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao87.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao86.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao88.png)
- No módulo Web, atualize as dependências e configure o Switch:
  - No componente Switch, defina a variável local para receber o valor do atributo (ex.: `GetImmobiles.List.Current.Check`).
  - Configure o evento OnChange para chamar a ClientAction (ex.: "SwitchOnChange"), que invoca a ServerAction **StatusChange** com os parâmetros necessários.  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao97.png)
  - Na ClientAction "SwitchOnChange", trate o retorno:
    - Se Output.Success for True, exiba mensagem de Sucesso.
    - Se não, exiba mensagem de Erro.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao98.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao99.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao100.png)
- Por fim, crie um Input Search para a tabela:
  - Crie uma variável local "SearchImmobile" (Texto).
  - No Aggregate, limite o Max.Record para 10 e crie um filtro para buscar por CEP e Endereço.  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao101.png)  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao102.png)  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao103.png)
