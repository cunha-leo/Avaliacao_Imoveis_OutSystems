# Parte 4 : Pop-up de Avaliação e Tela Minhas Avaliações, Imóveis que já Morei e Ajustes Gerais

- Ajustes no menu
- Modal de avaliação
- Persistência de dados
- Tela Minhas Avaliações
- Tela Imóveis que já morei
- Ajustes gerais

## Criando Modal de Avaliação

![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao01.png)

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
        - **Output.Succes** (False)
        - **Output.Message** ("Avaliação atualizada com sucesso")
        - **Output.Id** (Rating.Id) -> O Id da tabela Rating do nosso **Source**
    - 4º Ambos encerram aqui se der Sucesso em criar ou atualizar
    - 5º Criando o fluxo de Exceção **AllExceptions**
      - 1º Se ocorrer um erro ou situação que não cobre o fluxo anterior, ele irá executar o nosso **AllExceptions**
      - 2º O mesmo irá passar o erro para o nosso **Output**:
        - **Output.Succes** (False)
        - **Output.Message** (AllExceptions.ExceptionMessage) -> Vai receber a propria ação de Erro, tornando dinamico.
        - Fim.

    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao02.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao03.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao04.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao05.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao06.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao07.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao08.png)
    ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao09.png)

- **2º** Criando o Pop-up(Modal) no **Modulo ARR_WEB**
  *1º* Add Componente a tela de Avaliação de Imóvel
  *2º* Esse componente espera uma **váriavel local** para validar a hora que **Abre** e **Fecha**
  ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao10.png)
  *3º* Add a váriavel local **ShowPopupRating** que está setada como Bollean e Default(false), pois queremos que ao entrar nessa página a mesma esteja desativada, somente abrirá quando acionarmos.
  ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao11.png)
  *4º* Atribuirmos a vparivel local ao Popup, dessa forma agora o mesmo já recebe a variavel e podemos então criar o fluxo de **ClientAction** para abrir e fechar.
  ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao12.png)
  *5º* Criando o **ClientAction** para abrir e fechar o popup, para fazer esse passo lembra que colocamos a variável como padrão (False), ou seja será ativado a partir do inverso desse default.
  - Vamos criar o **ClientAction** de **OnClick** no Container de **Card de Avaliação**, pois como está dinamico uma vez que eu aplique no container cada card chamará essa ação.
  - Então a ativação será atraves de um click no Card dos Imoveis, dessa forma no componente a opções de evento onde vamos adicionar o **O tipo de evento(on click)** e o **Handler(ShowPopupRating)** no caso que recebe a nossa variável local.
  ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao13.png)
  - A ação criada **ShowPopupRating**, que a lógica será um **not** + variavel local
  - O que explicamos que a variavel esta como default False ou seja o (not) irá realizar o inverso dela que será (True)
  ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao14.png)
  *6º* Vamos implementar agora o nosso **ModalAvaliacao(Popup)** na tela
    - Criamos uma váriavel local para receber nossa tabela **Rating** que será usada no **Formulário** após arrastamos para nosso **Widget Tree** para o formulário dentro do popupp, que será as informações que vamos trabalhar.
   ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao15.png)
    - Ajustamos nossa estrutura onde **Título e Subtitulo** recebe uma expression que depois vamos colocar para que sempre que for um apartamento ou caso mude e também o icone que vira depois.
    - Ajustamos os campos do formulário, para que fique o de acordo com nosso mockup
    - Criamos os botões de **Cancelar** que recebe a ação **ShowRating** para fechar o popup, que é a negativa (not) da variavel local default (False) ou seja se estiver fechado abrirá se estiver aberto fechará e o botão **Save** ainda sem fluxo.
   ![Parte 4](..//Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao16.png)
