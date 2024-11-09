# Parte 3 : Criando Telas e lógica de Login e Cadastro de Imoveis

- Ajustes de labels
- Utilizando componente da Forge (api)
- Deixando aplicação mais segura com AccessKey
- Eventos OnChange
- Evento OnScroolingEnd
- Gerando AccessKey randômico
- Utilizando Widget List ao invés de TableList
- Join entre tabelas
- Tela Meus imóveis
- Tela Avaliar Imóveis

## Start

## Gerando AccessKey randômico

- Até o momento SE para edição ou ações que é mostrada na URL, está esposto o ID passado isso trás vulnerabilidade e brechas para ser burlado o sistema
- Por médida de segurança, vamos colocar o AccessKey que mascara esse ID, dando mais segurança e evitando contra vunerabilidades na aplicação

    ![Tela de Login](..//Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey.png)

### Access Key ARR_SERVICES

- Vamos Iremos iniciar no as alterações no servidor, conforme verifica na imagem abaixo até o momento temos a ServerAction (**Immobile_CreateOrUpdate**) que possui um parametro de entrada que é a propria tabela Immobile e o parametro de saida é o Output (*Success, Message, AccessKey, Id*)

- Porém o nosso (**CreateImmobile**) no fluxo não está recebendo ainda o **AccesKey**, porque não foi atriuido ainda a nossa tabela.

    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey01.png)

#### Criando o Access Key

- 1º Temos que criar um atributo na tabela Immobile na aba **Data**
  - Esse atributo irá com o tipo **Text** porque receberá uma **HASH**

  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey02.png)
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey03.png)

- 2º Uma vez criado o atributo, retornamos para o nosso fluxo da ServerAction (**Immobile_CreateOrUpdate**)
  - Na (**CreateImmobile**) Já estará disponivel a AccessKey
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey04.png)
  - E agora irei pedir para toda vez que criar um registro **novo** preencher a **Access Key**

- 3º Usando uma função da Systems padrão para configurar a AccessKey
  - Dessa forma é necessário busca-la nas dependências, para isso
    - Clicamos em dependências e atribuimos a ServerAction (**GenerateGuid**)
    - Toda vez que esta função for chamada será retornada uma hash pelo parametro de saida(retorno) da ServerAction do sistema
    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey05.png)

- 4º Uma vez que adicionamos a  ServerAction (**GenerateGuid**)
  - Podmeos agora retornar ao fluxo da ServerAction (**Immobile_CreateOrUpdate**) e atribuirmos a função ao atributo AccesKey do parametro de entrada que adicionamos a tabela Immobile.
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey06.png)
  - Agora No fluxo, toda vez que crio um Id novo ou imovel ele gerará um AccessKey
    - Posteriormente iremos para ARR_WEB onde será trocado na url ao em vez do ID a nossa AccessKey já com a hash.

- 5º Publicar e irmos então para ARR_WEB

### Access Key ARR_WEB

- Uma vez que finalizamos a parte do **ARR_SERVICES** temos que adicionar essas novas atualizaçãoes a nossa dependencia no ARR_WEB
  - Ao abrir já verificamos o ARR_Services flegado, dessa forma apenas clicamos no botão *Refresh all* e após *Apply* e publicamos
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey07.png)

- 1º A tela **ImmobileDetail** está esperando como parametro de entrada um **Immobile Identifier** é esse valor que retorna o ID do usuário, é aqui que vamos tratar a vulnerabilidade com **AccesKey**
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey08.png)
- Iremos substituir o parametro de entrada para o AccessKey
  - Seu *DataType* será *Text*, pois agora será esperado uma **hash** e não mais um ID
  - Não será necessário ser mandatorio, pois não tem a necessidade de mostrar o parametro vazio, somente no Update que será passado.
  - Ainda terei que alterar o GET onde pego essas informações e na minha lista
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey09.png)

- 2º Alterando nosso **GetImmobileBy**
  - Clicando nele já deparamos com um eror informando que estava sendo feito uma comparação de Identificador com Data types diferentes isso, porque mudamos o parametro de entrada de Id para Access Key, dessa forma temos que alterar também no nosso filtro do Get, como na imagem abaixo.
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey10.png)

- 3º Alterando o filtro do GetImmobileBy
  - Quando falamos que estamos buscando um | Immobile.AccessKey = AccessKey | ou seja uma busca unica o MaxRecord deve ser de 1 registro e não o padrão de 50.
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey11.png)

- 4º Por padrão as linhas de registros do nosso **Immobile List** ao clicar vai para página de edição daquele registro especifico, porém mudamos o nosso parametro de entrada para Access Key, dessa forma aqui também deve ser alterado.
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey12.png)
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey13.png)
![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey14.png)

------------------------------

## Utilizando componente da Forge (api) CEP

- ✨ **IMPLEMENTANDO O CEP**:
  - 🛠️ Criando ação **OnChange** para quando o usuário clicar no campo **CEP**.
  - ✏️ Quando começar a alterar o campo **CEP**, cairá em um evento de **OnChange**:
    - 🌐 Onde chama um serviço. Se aquele **CEP** existe:
      - 🏢 SE existir, ele vai preencher automaticamente o logradouro, bairro e cidade.
      - 🚫 SE não existir, ele vai mostrar uma mensagem de erro.

### Baixando o Componente na Forge (ViaCEP)

- Baixar o componente viaCEP - Endereços
  - Clicar na ABA **Forge** e procurar por **ViaCEP**
  - Uma vez encontrada apenas instale no studio
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP.png)

### Aplicando ARR_WEB

- 1º Esse componente é uma aplicaçõa separada o ViaCEP, dessa forma eu preciso referenciar ele dentro do meu código como eu faço com o ARR_Service
  - Clicando no plug de tomada e adicionando ele ao meu projeto
  - Ele possui uma ServerAction (**CEP**) com um parametro de entrada (CEP) e um parametro de saída (Output)
    - O Output possui um campo de retorno (CEP), através de uma **Structure** e campos de retorno (CEP, Logradouro, Complemento, Bairro, Localidade, Uf, Ibge, ...,Erro)
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP01.png)
  - Após aplicar já o verei na ABA **Logic**
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP02.png)

- 2º Trabalhando em cima da tela

  - Indo no meu campo Input **CEP** criarei uma ação OnChange que quando esse campo for alterado, irá rodar uma trigger e dentro dessa ação vai estar a ação do CEP
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP03.png)
  ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP04.png)

- 3º Aplicando a lógica:
  - Add um **IF**, SE CEP > 7, ou seja se ele tiver 8 caracteres ou mais
    - Vou no meu serviço de **ViaCEP** e ver se eu consigo pegar alguma informação baseado no CEP que ele me passou

    ```Js
        Length(GetImmobileByAccessKey.List.Current.Immobile.CEP) > 7
    ```

    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP05.png)

    - SE for satisfeita a condição ele irá chamar o ViaCEP
      - Para isso basta apenas eu arrastar da ABA Logic > Via_Services > Via_CEP : CEP
      - E ligar na minha condição e assim ele irá chamar o serviço e pegar as informações do CEP
    - Na parte de parametros como na imagem ira esperar um CEP, aqui e o mesmo que eu coloquei na condição então seleciono ele.
      - Aqui até o momento ele está referenciando no serviço de CEP mais ainda não está fazendo nada

    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP06.png)
    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP07.png)

    - Agora deve configurar os campos de Input para receber os valores automaticamente do meu serviço ViaCEP
      - **1º** Preciso validar se ele recebeu as informações desse serviço
        - SE Cep > 7 = FALSE (PARA)
        - SE Cep > 7 = TRUE ele chama meu serviço **ViaCEP**
          - onde é esperado como parametro um CEP, neste caso usamos o mesmo da condição (If)
        .....
        - **2º** validamos **O retorno do serviço CEP**
          - SE o retorno do serviço CEP.Output.Erro = True (PARA)
          - SE o retorno do serviço CEP.Output.Erro = FALSE
            - Ou seja se ele deu erro ele irá chamar o Asign
        ....
          - **3º** Preenchemos o **Assign**
            - Onde o valor do atributo da **GetImmobileByAccessesKey** recebe os Outputs da estrutura do serviço CEP.Output

    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)
    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP10.png)
    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP11.png)
    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP12.png)

    - **Digitando o CEP** no campo Input agora ele aciona meu serviõ viaCEP, valida se é maior do que 7 caracteres e caso seja satisfeito ele retorna preenchendo automaticamente os campos [logradouro, bairro, cidade, complemento(caso encontre)]
    ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)

    - **4º** Limpando campos caso haja alteração no Input **CEP**
      - Isso é necessário pois se alterarmos o campo do CEP novamente ele precisa ter uma ação que limpe os campos caso ele não ache o CEP ou seja SE a busca do CEP.Output.Erro for True ele limpa os campos
      - Dessa forma criei um asign recebendo os atributos porém com valor vazio
      ![Tela de Login](../Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP13.png)

    ⚠️**APRENDIZADO:** A partir de **Onchange** eu consigo buscar qualquer informação ou fazer qualquer tipo de manipulação dentro da minha aplicação, baseado em informações que eu tenha preenchido anteriormente.
    - Nessa aplicação foi a partir deu preencher um campo o CEP em preenchi automaticamente varios outros.
    - Serve para aplicar de diversas formas e diversas situações

------------------------------

## Tela Meus Imóveis

- Tela de Listagem de Imóveis
  - Iniciando assim, vamos reaproveitar a mesma para criar a tela de listagem de imóveis

  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis01.png)

- Realizando a alteraçõa inicial mais proximo do nosso template
  - **1º** Alteramos o nome da página
  - **2º** Retiramos o link de Casa pois será no logradouro para edição
  - **3º** Editamos as posições das colunas
  - **4º** Renomeamos o botão de criação para **Cadastrar Imóvel**
  - **5º** Adiconamos o link de edição na coluna **Logradouro**
  - **6º** Adiconamos a coluna de **Ação** com ícone de **Delete**
  - **7º** Adiconamos a coluna de **Cadastro**

  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis02.png)

- configurar as **Expressions** para receber os valores das colunas.
  - **1º** **Avaliações** - Recebe o valor do atributo correto
    - A ideia dessa coluna e realizar a somatoria de avaliações do endereço especifico.
    - Então terei que alterar meu Get(Aggregate) para realizar essa soma.
    - Começando a alterar o **GetImoveis**(Aggregate)
      - Criando um join para chamar a tabela avaliações
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis03.png)
      - Foi feito o Join e já está relacionado
        - Ao apertar **Source** e escolher a tabela já é feita a relação de tabelas
        - Uma coisa importantes a relação de ligação está como **With or without** que significa que ele buscara tanta os registros de que tenha **Avaliação** e o que não tem.
        - **With or without** Busca ambos registros com ou sem
        - **With** Busca registro preenchidos
        - **Only With** Busca apenas os registros que tenham a avaliação

        - Para realizar a avaliação lá na frente e verificar corretamente os dados da nossa listagem com a avaliação sem repetir registros realizamos o **group by** e o **count**
        - **Group by** agrupamos os dados de CEP, Id:Imomoble, Street, Street_Number, CreatedAt,Label:TypeMobile, AccessKey
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis06.png)
        - **Count** é para contar a quantidade de registros agrupados
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis05.png)
        - Olha que interessante uma vez que eu realizei o agrupamento e o count ele agora deixou de olhar para toda a estrutura e nosso Get agora mostra apenas os campos agrupados.
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis08.png)
        - Também retiramos a reordenação de cada coluna
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis09.png)
        - Agora vamos abrir as expresison e substituir pelos valores do novo Get os cmapos dos agrupamentos
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis10.png)
        - **Até o momento ficou assim**
      ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis11.png)
- Conseguimos finalizar a primeira parte dessa tela agora vamos realizar alguns ajustes:
  - **1º** Vamos ajustar a formatação do **Criado em** com a função da OutSystems **DateFormate()**
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis12.png)
  - **2º** Vamos ajustar a ação do nosso **Search**
    - Ocorreu que o campo de busca nao estava retornando os registro como veio criado, porque estava apenas pegando o CEP, como temos ainda somente dois registros  de CEP, vamos alterar para pegar o CEP e o Logradouro
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis13.png)

- Criando a Ação **DELETE**
  - 1º Criamos uma *ClientAction* no modulo **ARR_WEB** vazia por enquanto
  - 2º Vamos criar a **ServerAction** no modulo **ARR_Server**
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete01.png)
  - 3º Vou na ABA **Data** acho a ação de Delete da tabela Immobile e arrasto para minha **ServerAction** é adicionio o meu parametro de entrada ID para o Crud de Delete.
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete02.png)
  - 4º Passo meu **Output** ou seja a saida desse retorno do CRUD.
    - Ambos os fluxos não passamos o ID nem o AccessKey de Output
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete03.png)
  - 5º Passo criar o **Fluxo de Exceção**
    - Nele podemos ver que o nosso fluxo de **TRUE** está ok e nosso **FALSE**
      - Recebe uma **AllExpetions** que terá um **Asign** de *Output.Succes = True* e *Output.Message = AllExceptions.ExceptionMessage* ou seja caso der erro é informado erro pela **AllExpetions**.
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete05.png)
  - 6º Voltamos para o Mudulo **AAR_WEB** para agora receber o retorno da **ServerAction**, realizamos o Fluxo onde
    - 1. Chamamos a **ServerAction immobile_Delete** que passa como parametro o nosso Id.
    - 2. **SE** a **ServerAction** returnou **TRUE**, Recebera uma mensagem de **SUCESSO** **SE NÃO** recebera uma mensagem de **ERRO**, ambas do nosso retorno do **Output.Message da ServerAction** é após encerrerá.
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete01.png)
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete02.png)
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete03.png)
  ![Tela de Login](../Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete04.png)

## CRIANDO TELA DE AVALIAÇÕES

- **1º** Para inicar organizamos a Tela de Avaliação com um **List** para ficar ajustado usamos
  - No Main Content > List > Container > Content\CardsSectioned
  ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel01.png)

- **2º** Iremos mostrar os Imóveis disponiveis para avaliar, para isso vamos criar um Aggregated para essa tela em especifico.
  - 1. Fazemos uma relação com a tabela **Immobile** com a **UserXImmobile**
    - Será a tabela usada para relacionar o usuário com os imoveis que ele já morou e com o **join(With or Whithout)**.
    - Ou seja trará os dados da *Immobile* mesmo se não haver dados relacionados a *UserxImmobile*

  - 2. Fazemos uma relação com a tabela **Immobile** com a **TypeImmobile**
    - Neste caso a ligação é **join(Only Whith**) trará de qualquer forma porque não há como cadatsrar um imóvel sem o seu tipo.

  - 3. Fazemos uma relação com **Immobile** com a **Rating**
    - Para trazer as informações das avaliações, agrupar e contar pelas mesmas.
    - Usamos o **join(With or Whithout**) também.

  - 4. Realizmos os agrupamentos de informação e a contagem por Id do (Rating).
    - **Grup By** :
      - Immobile.Id
      - Immobile.Street
      - Immobile.Street_Number
      - TypeImmobile.Label
      - Immobile.AccessKey
    - **Count** :
      - Rating.Id

    ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel03.png)

- **3º**Agora vamos adicionar o nosso **Aggregat** ao nosso **Source**
  ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel04.png)
  - 1. Após adicionamos nosso Source atraves das nossas **Expressions** de acordo com retorno de cada informação como na imagem abaixo.
  - 2. Também estilizamos um pouco mais nosso **Container** dando um espaçamento de margens e centralização do conteudo.
  ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel05.png)
  - 3. Vamos Criar um *Group By* no do *TypeImmobile.Id* para que quando a informação daquele lista for Casa apareça um icone de casa e se for apartamento irá aparecer apartamento.
  ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel06.png)
  - 4. Agora vamos criar um **If** para mostrar o icone de acordo com o **TypeImmobile**
  ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel07.png)

- **4º** Vamos criar um scroll infinito que ao rolar as avaliações el sempre vai carregando mais a cada vez que eu rolar para baixo enquanto tiver imoveis.
  - 1. Ao selecionar o component **List** ele por padrão possui os campos de tipos de **Envents** selecione o Event **On Scroll Ending** é após selecione a opção **New Infinite Scroll Cliente Action**
    - Será criado automaticamente uma **Cliente Action** de Scroll
    ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel08.png)  
    ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel09.png)
    - Ele criou uma ação **ScrollEnding** aonde ele está esperando um **número** para incrementar a partir da variável **Incrementrecords** que é se você vai mostrar 5 agora traga mais 2, 3 ... e também criou uma **Variavel Local** -> **MaxRecords** a primeira vez que abrir a tela mostrará a partir de quantos na tela
    ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel10.png)
    ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel11.png)
    ![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel12.png)

## **REVISÃO**

![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel14.png)

## EM CRIAÇÃO ..... EM BREVE PARTE 4

![Tela de Login](../Parte%203/img/Tela%20Avaliações/Avaliar_Imovel13.png)
