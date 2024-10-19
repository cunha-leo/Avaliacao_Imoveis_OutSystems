# Projeto Aplicativo Avaliação de Imóveis

## Índice

- 1ª Parte: Configuração Inicial e Estruturação dos Módulos

## Documentação da 1ª Parte - Projeto Aplicativo Avaliação de Imóveis

### Introdução

O projeto **Aplicativo Avaliação de Imóveis** está sendo desenvolvido como parte do módulo 4 da formação em OutSystems. O foco desta primeira parte foi definir a estrutura do projeto, configurar os módulos principais, e construir a base da aplicação. Esta documentação detalha o progresso até o momento e descreve as escolhas feitas em termos de arquitetura, componentes, e funcionalidades.

### Estrutura do Projeto

O projeto foi dividido em dois módulos principais:

1. **Módulo AAR_Services (Service)**:
   - Responsável pela lógica de backend, incluindo a arquitetura do banco de dados, os relacionamentos e as ações CRUD.
   - Criamos o diagrama ER para facilitar a visualização do banco de dados. [Link para o diagrama ER](https://example.com/diagrama-er)

   **Tabelas Criadas**:

   - **Tabela Immobile**: Contém os dados dos imóveis cadastrados, como CEP, endereço, cidade, proprietário, entre outros.
     [Link para a tabela Immobile](https://example.com/tabela-immobile)

   - **Tabela TypeExperience**: Armazena os tipos de experiência relacionados aos imóveis. Possui registros como **Excelente, Bom, Neutro, Ruim, Péssimo**.
     [Link para a tabela TypeExperience](https://example.com/tabela-typeexperience)

   - **Tabela TypeImmobile**: Armazena os tipos de imóvel disponíveis (ex.: Casa, Apartamento, Loja). Possui registros como **Casa, Apartamento, Loja**.
     [Link para a tabela TypeImmobile](https://example.com/tabela-typeimmobile)

   - **Tabela UserxImmobile**: Relaciona usuários aos imóveis, indicando propriedades e ocupação. São tabelas auxiliares que armazenam os tipos de experiência, tipos de imóvel, e a relação entre usuários e imóveis.
     [Link para a tabela UserxImmobile](https://example.com/tabela-userximmobile)

   - **Tabela User**: Utiliza a entidade padrão do sistema OutSystems para armazenar informações dos usuários, como data de criação e última alteração.
     [Link para a tabela User](https://example.com/tabela-user)

2. **Módulo AAR_WEB**:
   - Responsável pelo front-end e pelas telas da aplicação.
   - O módulo **AAR_Services** foi adicionado como dependência, mas somente como leitura, para garantir a segurança e centralizar toda a lógica de servidor.
   - No módulo web/reactive, podemos observar as abas completas, incluindo **Triggers, Interface, Logic, e Data**. [Link para a estrutura do módulo AAR_WEB](https://example.com/estrutura-aar-web)

### Mockups e Template das Telas

Antes de começar a implementação, criamos um mockup das telas utilizando o **Drawio**. As telas incluem:

- Tela de Login
- Dashboard
- Cadastro de Imóvel
- Avaliar Imóvel
- Pop-up Avaliar Imóvel
- Minhas Avaliações
- Meus Imóveis
- Imóveis que já morei

Esse planejamento visual ajudou a garantir que todos os elementos fossem claramente definidos antes da implementação. As imagens dos mockups estão listadas abaixo para referência:

- **Figura do Mockup - Tela de Login**: [Link para a imagem](https://example.com/mockup-tela-login)
- **Figura do Mockup - Dashboard**: [Link para a imagem](https://example.com/mockup-dashboard)

### Configuração dos Módulos

1. **Módulo AAR_Services**:

   - Contém todas as ações CRUD e a lógica de backend. O módulo foi configurado para ser **público**, permitindo que outros módulos acessem suas funcionalidades.
   - A arquitetura de entidades foi projetada para ser clara e garantir a integridade dos dados. O diagrama de entidade (ER) criado para facilitar a visualização é mostrado na [Figura 2](https://example.com/diagrama-er).

2. **Módulo AAR_WEB**:

   - Concentra todas as telas e componentes de interface. Utiliza a base de dados do módulo **AAR_Services** somente em modo de leitura, para garantir a segurança e a centralização da lógica.
   - Estruturas como **MainFlow** e layouts de tela foram organizados para facilitar o desenvolvimento posterior. Verifique a estrutura do módulo AAR_WEB na [Figura 1](https://example.com/estrutura-aar-web).

### Conclusão

Essa primeira etapa do projeto incluiu a configuração inicial dos módulos e a criação das entidades do banco de dados, além da definição da interface do usuário. Utilizamos uma abordagem modular que facilita a manutenção e a segurança dos dados, separando a lógica de servidor do front-end.

Na próxima etapa, vamos nos concentrar em finalizar a estruturação das telas no módulo **AAR_WEB**, garantindo que todas as funcionalidades estejam alinhadas ao objetivo do projeto.
