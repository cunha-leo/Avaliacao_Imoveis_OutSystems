# Parte 2

## Tela de Login

![[{D53FDF15-2A06-4A07-A791-4F0424A539B1}.png]]

- Aqui podemos observar ao lado direito que, por padrão, a tela de Login da própria OutSystems vem com:

  ![[{723353FD-1C7F-4909-80E7-9955A852D676}.png]]

### 4 Variáveis Locais

- **Username**: Consumida no Input "E-mail"

  ![[{79E4873B-702F-45BB-94AF-18EFEC2D7048}.png]]

- **Password**: Consumida no Input "Senha"

  ![[{54F5D1FC-704A-4299-9F5E-AF0F27355CEF}.png]]

- **IsExecuting**: Utilizada para informar execução de algo na ClientAction "OnInitialize"

- **Remember**: Consumida no Input de Checkbox "Lembrar-me"

  ![[{47B828D1-C66E-41BE-98C1-E12451444BA4}.png]]

### 3 Client Actions

- **ForgotPassword**: Para recuperar a senha

  ![[{05673F07-C706-49C3-9C2E-C20268464EF8}.png]]

- **Login**: Usado no botão "Entrar"

  ![[{D0F964F1-EE9B-46A5-A5BB-3267C4D60BE5}.png]]

  - A lógica é receber o **IsExecuting** como True, que será após clicar no botão

    ![[{F189A230-90BC-416F-A76F-04B592D5685A}.png]]

  - Após, irá para a ServerAction "DoLogin", que é a ServerAction de Login
    - Que receberá as variáveis locais: Username, Password, Remember
    - A ServerAction é chamada para persistir meus dados no banco de dados e saber se realmente salvou no banco de dados
    - E chamar a ServerAction padrão de Login da OutSystems dentro de User

      ![[{87DA3446-B4E7-465E-880D-C1E365DEE899}.png]]
      ![[{A33DACCF-EEA9-4CFA-A936-78F7EC1435D6}.png]]

  - Após, irá **remover** uma mensagem de feedback após Login
    - Ou seja, será removida qualquer possível mensagem que apareça após realizar o login.

  - Após, **redirecionará**
    - O usuário será redirecionado para a tela principal

      ![[{BCC69033-AB42-4950-B5EA-BDF1499262C1}.png]]
      ![[{6A22498A-7965-415E-B71F-B683D93CF2DA}.png]]

- **OnInitialize**:
  - Usado para realizar alguma ação após o carregamento da tela
    - Como padrão, no caso da imagem abaixo

      ![[{3542E58E-7069-4D8A-8AF5-89B29B0A2C42}.png]]

  - Usado para receber a variável local "IsExecuting" para implementar a ação
    - Nesse caso, o padrão está como False, ou seja, quando iniciar esta tela, por padrão, não inicialize nenhuma ação

      ![[{9B2C5CF3-95A5-4AF3-A31B-19077A60D00C}.png]]

----------------------------------------------------------

### Mudando as ações de Autentication para o caminho correto

- Isso se dá porque a lógica de servidor deve ficar no módulo **ARR_Service**
  - Então, basta recortar da **ARR_WEB** e colocar na **AAR_Service**, aba **Logic**, e **Publicar**

    ![[{0EA506EF-DF36-4FBA-8F8F-B1B7C0E8E13D}.png]]

  - Deve deixar público antes de publicar, dessa forma podemos acessar no outro módulo as mesmas

    ![[{7AE3728C-4FEF-47D6-9C7C-C44483123CB7}.png]]

  - Agora temos que apontar
    - Achamos as dependências, buscamos o módulo, clicamos, adicionamos e "Apply"
    - Após aplicar, os erros irão sumir

      ![[Pasted image 20241017140112.png]]
      ![[{34F8ED1D-83FF-4DA8-8026-3FA1AA2CE03F}.png]]

----------------------------------------------------------

## Tela de Cadastro de Imóveis

### Módulo ARR_WEB

![[{CA41BF37-3B0F-444C-B36E-6822F3775D5A}.png]]

- Vamos criar a partir da ABA **Data** e arrastamos para o nosso **MainFlow**

  ![[{A45E5F34-DB36-4758-A6EB-D74CAC40751F}.png]]

- Criamos então arrastando as duas telas

  ![[{629597CA-A402-48BA-98B0-49ECBD9D97CA}.png]]

  - **Immobiles**: Que é a tela de Listagem

    ![[{65C356ED-7DD6-4251-8BA9-DBE7446E50A0}.png]]

  - **ImmobileDetail**: Que é a de registro
    - Retiramos o IF que vem por padrão, que mostra se "true" Cadastrar ou "else" Editar, e colocamos no lugar uma **Expression**, que tem a seguinte validação:
      - SE o ImmobileId for igual a vazio ou se ele não existe, Cadastrar, se não, Editar e concatenar com Imóvel.

      ```Js
      If(ImmobileId = NullIdentifier(),"Cadastrar","Editar")+" Imóvel"
      ```

    - Vamos tirar agora o Form de dentro da Column1, para que ele expanda

      ![[{7A66B95C-BBAA-4629-A73C-50889631E146}.png]]
      ![[{5D1AB96D-387D-46EE-B4CE-B01BB95DBCC0}.png]]

    - Arrastando o **Adaptive/Columns2** para dentro do **Form** e dividindo as colunas

      ![[{27534316-374B-43B0-9216-7C579213C229}.png]]

    - Ajustado ficou assim:

      ![[{80FB56C6-7E17-4D87-BBB9-594459A3552D}.png]]

    - Foi trocado **checkbox** por **radioGroup**, dessa forma ficou mais visual
      - O **Label** deixamos como **None** para não pegar nenhuma propriedade, pois nesse caso é um **True** ou **False** no Radio, não sendo necessário amarrar ao Label
      - Alteramos também o lado dos botões

      ![[{AD72C59F-568D-481F-8487-1936FBD8476E}.png]]

    - Verificando a **ClientAction** "**SaveDetail**" da tela **ImmobileDetail** se os dados estão persistindo corretamente

      ![[{1370F55E-1801-4DFB-9A91-1F74D2DCE8AD}.png]]

      - Aqui ainda não está fazendo a persistência dos dados

        ![[{AC650FC3-D469-4275-9EA8-443ABF186342}.png]]

      - Mostrando como a tela está ficando visualmente

        ![[{160CFB40-C228-4733-AFD5-C01B5CF8108E}.png]]

### Módulo: ARR_Services

#### Tela Cadastrar Imóvel e Editar Imóvel

- Persistindo os dados da Tela: Cadastrar Imóvel
  - Criamos uma pasta somente com o nome da Tabela que criamos para a tela
  - Aqui vamos criar a ação que irá persistir os dados

- Server Action: **Immobile_CreateOrUpdate**

  ![[{337488EF-60A9-4657-AEC5-17F01AB070A5}.png]]

  - A Server Action vai estar esperando:
    - **Parâmetro de Entrada**: **Immobile**
      - No caso, quero persistir a minha **Tabela Immobile**
      - Dessa forma foi criada uma ação dentro do servidor chamada **Immobile_CreateOrUpdate**
      - Para atualizar ou criar, precisamos da estrutura dela, por isso o **parâmetro de entrada** > **Immobile**
    - **Parâmetro de Saída**: **Output**
      - Agora precisamos de um parâmetro de saída para retornar as informações
      - Dessa forma, optamos por criar uma **Structure**

        ![[{45327C6C-BCB5-4B2E-84C4-DC0D59F7089E}.png]]

      - Criando Atributos para a **Structure Output**:
        - **Success**: Retornará se foi sucesso ou não, com valor padrão como **false**

          ![[{B205BB0F-5299-479D-93F5-16B73B40881E}.png]]

        - **Message**: De acordo com o retorno

          ![[{20338010-363B-46E2-A09C-BF103BAE6B6B}.png]]

        - **AccessKey**

          ![[{3F4141B9-91A0-42BF-ACF3-3E5F91584160}.png]]

        - **Id**: Será **Long Integer**, porque não é um retorno definido de uma tela ou tabela; será utilizado como atributo de retorno em várias Server Actions

          ![[{B53F52B8-30EC-41D0-96BD-42D8324643E8}.png]]

      - Uma vez criada a **Structure**, podemos criar o **Parâmetro de Saída**:

        ![[{EA49FAFF-D244-452A-A86C-795930978A2F}.png]]

  - Criando o Fluxo da **Server Side** (Server Action)

    ![[{CD6EE122-092B-4CB6-AC19-4CE2FC0809C2}.png]]

  - **1ª Coisa**: Validar se estou **Criado Por** ou **Criado Como**
    - Você é igual a **NullIdentifier()**

      ![[{6D8519CA-CE9E-4786-9FCD-BC359C43FC7E}.png]]

  - SE **Immobile.Id** = **NullIdentifier()** [Novo registro?]
    - SE Sim: **CreateImmobile**
    - SE Não: **UpdateImmobile**

      ![[Pasted image 20241017163504.png]]

    - Caso Sim: Temos que preencher, antes de persistir os dados, os campos **Criado Por (CreatedBy)** e **Criado Como (CreatedAt)**

      ![[{832C02B8-AB1C-4240-881B-56B2E920C31D}.png]]

    - Como é somente um registro pontual, posso vir no **Source**, tirar o **Immobile** e adicionar os campos pontualmente neste momento.

      ![[{BF8B5A39-8134-4BAA-B3CE-60A01E839EA5}.png]]

    - > ⚠️ **ATENÇÃO**: Se atente aos campos, sempre colocamos o que vem do parâmetro de **ENTRADA** aqui.

      ![[{53509CE9-1D8F-4B05-AE67-187C0A4D8DF4}.png]]
      ![[{82D1201F-7E3A-4E40-8018-F68E1F0AF95F}.png]]
      ![[Pasted image 20241017164737.png]]

    - São os dois únicos campos que não vão selecionar a opção que vem do parâmetro de entrada.
      - Aqui em **CreatedBy**: Passamos uma função chamada:
        - **GetUserId()**:
          - Ela traz o ID do usuário logado atualmente na aplicação
          - Salvando o Id desse usuário como criador
      - Aqui também temos o **CreatedAt**: Passamos uma função chamada:
        - **CurrDateTime()**:
          - Ela pega a hora atual e persiste na minha tabela

        ![[{A4405A7A-EDCB-45BC-AA2C-88039F651894}.png]]

    - Uma observação: o campo **CreatedAt**, anteriormente, passamos o **CurrDateTime()** no próprio atributo da tabela. Dessa forma, não há necessidade de passar algo aqui, então ficará assim:

      ![[{8CFD1ECC-E6D1-43A1-B22F-E876E758CA79}.png]]
      ![[{2F35E776-E3D9-490F-987F-CB2505BD5896}.png]]

  - **Observação Interessante**:
    - Podemos criar a validação de criação ou update de duas formas e utilizamos um exemplo diferente em cada.
    - Em **UpdateImmobile**:
      - Escolhemos atribuir no **Source** diretamente apenas o **Parâmetro de Entrada** PAI
      - Dessa forma, todos os atributos do **Source** vêm junto

        ![[{8B9DB717-A15A-45FB-88EF-B41F230A88E4}.png]]

    - Em **CreateImmobile**:
      - Escolhemos tirar o parâmetro PAI (**Immobile**) e adicionamos um por um e estilizamos o atributo **CreateBy**, passando a função **GetUserId()**

        ![[{936DAC75-EA3C-4B2C-8356-ADFF4F6590A7}.png]]

  - Começando a inserir os parâmetros de saída
    - **1º**: Criamos um **Assign** para o **CreateImmobile**
      - Adicionamos os parâmetros de entrada e seus respectivos valores
      - A diferença é o **Output.Id**, que recebe o parâmetro do Id da função **CreateImmobile**

      ![[{34F8C418-3D0B-4DCD-A7FB-7BF37FAF42EA}.png]]

    - **2º**: Criamos um **Assign** para o **UpdateImmobile**
      - Adicionamos os parâmetros de entrada e seus respectivos valores
      - A diferença é o **Output.Id**, que recebe o próprio atributo **Id** dele, pois já é um user, dessa forma, atualizando-o
      - Porque nesse momento não estou criando um novo, estou simplesmente atualizando-o

      ![[{A2168CC7-B24E-4826-9C53-F75F65A6603B}.png]]
      ![[{5F5EAECA-6AC9-478C-B012-233D584F125A}.png]]

- >❗ **EXCEÇÃO**: pois esses **Assign** não vão dar False até aqui ou ❌ **ERRO** até aqui.

  - Aplicando:
    - Adicionar Exceção ao Fluxo
      - Decidimos colocar Todas as Exceptions

        ![[{83EB1D1F-9085-4AA4-A3D2-14EBCD29F97E}.png]]

    - Preenchendo o **Assign**:
      - **Output.Success = False**
        - Para englobar erros que saem fora do contexto ao lado
      - **Output.Message = AllExceptions.ExceptionMessage**
        - Recebe a própria mensagem da **AllExceptions > ExceptionMessage** de forma automática

        ![[{BF583B92-32CC-489C-8979-2C9B2665C1E7}.png]]

    - **AllExceptions**, a exceção CASO for acionada:
      - Significa que houve um erro e não conseguiu completar o fluxo
      - Caso observe, o **Abort Transcription** está **Yes**

        ![[{0B6B0075-0427-4CD3-81BA-C69BF744DC2A}.png]]

----------------------------------------------------------

### Módulo: ARR_WEB

- Começando a retirar o que não vamos usar
  - Neste caso, excluímos a tabela **GetUsers**

    ![[{06301CF7-FB46-42EB-BCFD-429B3D4BAF88}.png]]
    ![[{571952B5-A404-409F-A562-D48DBC47834C}.png]]

- Criando o fluxo da **Client Action: SaveDetail**
  - Primeiro será validado se o formulário é **False**

    ![[{57CF1217-6AA7-4845-A9E7-AC60388A9916}.png]]

  - Se o **Form** for **True**:
    - Irá chamar a **ServerAction** criada **Immobile_CreateOrUpdate**
      - Nela, receberá em **Action > Immobile** a listagem criada como parâmetro de entrada

        ![[{21BDBD82-B8B8-497F-A536-E02A54176C18}.png]]
        ![[{54E9F377-BEBE-411B-A172-C41FB2C939B6}.png]]

    - **IF** que valida se a persistência dos dados foi realizada com sucesso ou não:
      - **❌ SE Não**: Receberá uma mensagem de ❌ **ERRO** pegando o parâmetro de saída

        ![[{82F4010A-77C5-427D-8864-03A61FF8B863}.png]]

      - **✅ SE Sim**: Receberá uma mensagem de ✅ **SUCESSO** do parâmetro de saída

        ![[{5E514C37-4356-4F05-BA17-DAEC02C64FDB}.png]]

    - Finaliza com 🔄 **REDIRECT** para a tela 🏠 **Immobiles** de listagem

      ![[{DF87A210-95C4-4477-8B36-71C7CA9FABD0}.png]]

- Validando em tela se os dados estão persistindo:
  - Está ok até aqui, mas o **CEP** ainda está fictício, faremos correções e usaremos uma API para o **CEP**

    ![[{A8774242-DD44-4866-A33E-66EF871767FB}.png]]
    ![[{632EC737-D432-4565-AF45-8D10E5E7E6E6}.png]]

- ✨ **IMPLEMENTANDO O CEP**:
  - 🛠️ Criando ação **OnChange** para quando o usuário clicar no campo **CEP**.
  - ✏️ Quando começar a alterar o campo **CEP**, cairá em um evento de **OnChange**:
    - 🌐 Onde chama um serviço. Se aquele **CEP** existe:
      - 🏢 SE existir, ele vai preencher automaticamente o logradouro, bairro e cidade.

----------------------------------------------------------

#### Tela de Meus Imóveis

![[{F9DA79F0-8B1C-496C-8CD4-43B2371CAC08}.png]]

#### Próxima aula

![[{104119AE-A341-480A-ABEB-24B6F21C1920}.png]]
