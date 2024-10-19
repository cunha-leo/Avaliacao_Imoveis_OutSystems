# Projeto Aplicativo Avaliação de Imóveis

## Índice

- 1ª Parte: Configuração Inicial e Estruturação dos Módulos

## Documentação da 1ª Parte - Projeto Aplicativo Avaliação de Imóveis

### Mockups e Template das Telas

Antes de começar a implementação, iniciamos com entendimento dos mockup das telas utilizando o **Drawio** e a importancia de ter uma template visual e os beneficios que pode trazer.

Esse planejamento visual ajudou a garantir que todos os elementos fossem claramente definidos antes da implementação e trazendo clareza da aplicabilidade.

As telas incluem:

- Tela de Login
  ![Figura do Mockup - Tela de Login](/Template/img/mockup-tela-login.png)
  
- Dashboard
  ![Figura do Mockup - Dashboard](/Template/img/mockup-dashboard.png)
  
- Cadastro de Imóvel
  ![Figura do Mockup - Cadastro de Imóvel](/Template/img/mockup-cadastro-imovel.png)

- Avaliar Imóvel
  ![Figura do Mockup - Avaliar Imóvel](/Template/img/mockup-avaliar-imovel.png)

- Pop-up Avaliar Imóvel
  ![Figura do Mockup - Pop-up Avaliar Imóvel](/Template/img/mockup-popup-avaliar-imovel.png)

- Minhas Avaliações
  ![Figura do Mockup - Minhas Avaliações](/Template/img/mockup-minhas-avaliacoes.png)

- Meus Imóveis
  ![Figura do Mockup - Meus Imóveis](/Template/img/mockup-meus-imoveis.png)

- Imóveis que já morei
  ![Figura do Mockup - Imóveis que já morei](/Template/img/mockup-imoveis-que-ja-morei.png)

### Estrutura do Projeto

O projeto foi dividido em dois módulos principais:

1. **Módulo AAR\_Services (Service)**:
   - Responsável pela lógica de backend, incluindo a arquitetura do banco de dados, os relacionamentos e as ações CRUD.

   - **Criamos o diagrama ER**:
     ![Diagrama ER](../Parte%201/img/ER/ER01.png)

   **Tabelas Criadas**:

   - **Tabela Immobile**: Contém os dados dos imóveis cadastrados, como CEP, endereço, cidade, proprietário, entre outros.
     ![Diagrama ER](../Parte%201/img/Tabelas/ER_Immobile.png)

   - **Tabela Rating**: Armazena as avaliações dos imóveis, incluindo informações como tempo de locação, recomendações e observações dos usuários.
     ![Diagrama ER](../Parte%201/img/Tabelas/ER_Rating.png)
  
   - **Tabela TypeExperience**: Armazena os tipos de experiência relacionados aos imóveis. Possui registros como **Excelente, Bom, Neutro, Ruim, Péssimo**.
     ![Tabela TypeExperience](../Parte%201/img/Tabelas/ER_TypeExperience.png)

   - **Tabela TypeImmobile**: Armazena os tipos de imóvel disponíveis (ex.: Casa, Apartamento, Loja). Possui registros como **Casa, Apartamento, Loja**.
     ![Tabela TypeImmobile](../Parte%201/img/Tabelas/ER_TypeImmobile.png)

   - **Tabela UserxImmobile**: Relaciona usuários aos imóveis, indicando propriedades e ocupação. São tabelas auxiliares que armazenam os tipos de experiência, tipos de imóvel, e a relação entre usuários e imóveis.
     ![Tabela UserxImmobile](../Parte%201/img/Tabelas/ER_UserxImmobile.png)

   - **Tabela User**: Utiliza a entidade padrão do sistema OutSystems para armazenar informações dos usuários, como data de criação e última alteração.
     ![Tabela User](../Parte%201/img/Tabelas/ER_User.png)

2. **Módulo AAR\_Services**:
   - Responsável pelo front-end e pelas telas da aplicação.

   - O módulo **AAR\_Services** foi adicionado como dependência, mas somente como leitura, para garantir a segurança e centralizar toda a lógica de servidor.

   - No módulo web/reactive, podemos observar as abas completas, incluindo **Triggers, Interface, Logic, e Data**.  

     ![Estrutura do Módulo AAR_WEB](../Parte%201/img/Modulos/estrutura-aar-services.png)

### Configuração dos Módulos

1. **Módulo AAR\_Services**:

   - Contém todas as ações CRUD e a lógica de backend. O módulo foi configurado para ser **público**, permitindo que outros módulos acessem suas funcionalidades.

   - A arquitetura de entidades foi projetada para ser clara e garantir a integridade dos dados. O diagrama de entidade (ER) criado para facilitar a visualização é mostrado abaixo:

     ![Diagrama ER](../Parte%201/img/ER/ER01.png)

2. **Módulo AAR\_WEB**:

   - Concentra todas as telas e componentes de interface. Utiliza a base de dados do módulo **AAR\_Services** somente em modo de leitura, para garantir a segurança e a centralização da lógica.

   - Estruturas como **MainFlow** e layouts de tela foram organizados para facilitar o desenvolvimento posterior. Verifique a estrutura do módulo AAR\_WEB abaixo:

     ![Estrutura do Módulo AAR_WEB](../Parte%201/img/Modulos/estrutura-aar-web.png)

### Conclusão

Essa primeira etapa do projeto incluiu a configuração inicial dos módulos e a criação das entidades do banco de dados, além da definição da interface do usuário. Utilizamos uma abordagem modular que facilita a manutenção e a segurança dos dados, separando a lógica de servidor do front-end.

Na próxima etapa, vamos nos concentrar em finalizar a estruturação das telas no módulo **AAR\_WEB**, garantindo que todas as funcionalidades estejam alinhadas ao objetivo do projeto.
