# App Property Evaluation in OutSystems

OutSystems Reactive application for Property Evaluations

## Table of Contents

- [Part 1 - Part 1 Title](#documentation-of-part-1)
- [Part 2 - Part 2 Title](#documentation-of-part-2)
- [Part 3 - Part 3 Title](#documentation-of-part-3)
- [Part 4 - Part 4 Title](#documentation-of-part-4)
- [Part 5 - Part 5 Title](#documentation-of-part-5)

## Readme en Portugués - PT

Si você é um leitor em português, clique no link abaixo:

- [Clique aquí](/README.md)

## Readme in Spanish - ES

If you are a Spanish reader, click the link below:

- [Click here](/README-ES.md)

-----------------------------------

## Documentation of Part 1

- Understanding the project through the template
- Creating the project in two modules: Web and Services
- Understanding the separation of responsibilities
- Creating the database architecture

### Mockups and Screen Template

Before starting the implementation, we began by understanding the screen mockups using **Drawio** and emphasizing the importance of having a visual template along with its benefits.

This visual planning helped ensure that all elements were clearly defined before implementation, providing clarity for the application’s use.

The screens include:

- Login Screen  
  ![Login Screen Mockup](./Template/img/mockup-tela-login.png)
- Dashboard  
  ![Dashboard Mockup](./Template/img/mockup-dashboard.png)
- Property Registration  
  ![Property Registration Mockup](./Template/img/mockup-cadastro-imovel.png)
- Evaluate Property  
  ![Evaluate Property Mockup](./Template/img/mockup-avaliar-imovel.png)
- Evaluate Property Pop-up  
  ![Evaluate Property Pop-up Mockup](./Template/img/mockup-popup-avaliar-imovel.png)
- My Evaluations  
  ![My Evaluations Mockup](./Template/img/mockup-minhas-avaliacoes.png)
- My Properties  
  ![My Properties Mockup](./Template/img/mockup-meus-imoveis.png)
- Properties I’ve Lived In  
  ![Properties I’ve Lived In Mockup](./Template/img/mockup-imoveis-que-ja-morei.png)

### Project Structure

1. **AAR_Services Module (Service)**:
   - Responsible for the backend logic, including the database architecture, relationships, and CRUD actions.
   - The module is configured to be **public**, allowing other modules to access its read-only functionalities.
   - The entity architecture was designed to be clear and to ensure data integrity.  
     The entity (ER) diagram was created to facilitate visualization; below is a preview of each table:
     ![ER Diagram](./Assets/Parte%201/img/Data/ER/ER01.png)
   - **We created the ER diagram**:  
     ![ER Diagram](./Assets/Parte%201/img/Data/ER/ER01.png)
   - **Tables Created**:
     - **Immobile Table**: Contains data for registered properties, such as ZIP code, address, city, owner, among others.  
       ![Immobile Table Diagram](./Assets/Parte%201/img/Data/Table/ER_Immobile.png)
     - **Rating Table**: Stores property evaluations, including information such as rental duration, recommendations, and user observations.  
       ![Rating Table Diagram](./Assets/Parte%201/img/Data/Table/ER_Rating.png)
     - **TypeExperience Table**: Stores types of experience related to properties. It includes records such as **Excellent, Good, Neutral, Bad, Terrible**.  
       ![TypeExperience Table](./Assets/Parte%201/img/Data/Table/ER_TypeExperience.png)
     - **TypeImmobile Table**: Stores the available property types (e.g., House, Apartment, Store). It includes records such as **House, Apartment, Store**.  
       ![TypeImmobile Table](./Assets/Parte%201/img/Data/Table/ER_TypeImmobile.png)
     - **UserxImmobile Table**: Relates users to properties, indicating ownership and occupancy.  
       This auxiliary table stores the experience types, property types, and the relationship between users and properties.  
       ![UserxImmobile Table](./Assets/Parte%201/img/Data/Table/ER_UserxImmobile.png)
     - **User Table**: Uses OutSystems’ default entity to store user information, such as creation date and last modification date.  
       ![User Table](./Assets/Parte%201/img/Data/Table/ER_User.png)
2. **AAR_WEB Module**:
   - Responsible for the front-end and the screens of the application.
   - It is added as a dependency to **AAR_WEB** with read-only access, ensuring security and centralizing all server-side logic in the **AAR_Services** module.
   - In the web/reactive module, you can see all the tabs, including **Triggers, Interface, Logic, and Data**.  
     ![AAR_WEB Module Structure](./Assets/Parte%201/img/Model/estrutura-aar-web.png)

### Conclusion

This first stage of the project included the initial configuration of the modules and the creation of the database entities, as well as the definition of the user interface.  
We used a modular approach that facilitates maintenance and data security by separating server logic from the front-end.

In the next stage, we will focus on finalizing the screen layouts in the **AAR_WEB** module, ensuring that all functionalities are aligned with the project’s objectives.

-----------------------------------

## Documentation of Part 2

- Creation of the Login Screen and Property Registration Screen, and their logic

### Login Screen

- On the right side, you can see that by default the OutSystems Login screen comes with:  
  ![Login Screen](./Assets/Parte%202/img/Tela%20Login/Login01.png)

#### 4 Local Variables

- **Username**: Used in the **E-mail** input  
  ![Var Username](./Assets/Parte%202/img/Tela%20Login/Var_Username.png)
- **Password**: Used in the **Password** input  
  ![Var Password](./Assets/Parte%202/img/Tela%20Login/Var_Password.png)
- **IsExecuting**: Used to indicate execution in the ClientAction **OnInitialize**  
  ![Var IsExecuting](./Assets/Parte%202/img/Tela%20Login/Var_IsExecuting.png)
- **Remember**: Used in the **Remember me** checkbox input  
  ![Var Remember](./Assets/Parte%202/img/Tela%20Login/Var_Remember.png)

#### 3 Client Actions

- **ForgotPassword**: For password recovery  
  ![ForgotPassword](./Assets/Parte%202/img/Tela%20Login/Client/ForgotPassword.png)
- **Login**: Triggered by the **Enter** button  
  ![Login](./Assets/Parte%202/img/Tela%20Login/Client/Login.png)
  - The Login logic sets the local variable **IsExecuting** to True after the button is clicked:  
    ![IsExecuting](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-IsExecuting.png)
  - Then, it calls the ServerAction **DoLogin**:
    - Receives the local variables: Username, Password, Remember.
    - Persists the data and verifies that they were saved in the database.
    - Calls the default OutSystems Login ServerAction (within User).  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin01.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin02.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)
  - Afterwards, it removes a feedback message after login.
  - Finally, it redirects the user to the main screen:  
    ![Redirect](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)
- **OnInitialize**:
  - Used to execute actions after the screen has loaded (as shown in the image below):  
    ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize01.png)
  - It uses the local variable "IsExecuting" to implement the action, with the default being False (i.e., no action is executed on screen load).  
    ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize.png)

-----------------------------------

### Changing the Authentication Actions to the Correct Path

- This is because the server logic must reside in the **ARR_Service** module:
  - Simply cut the action from **ARR_WEB** and paste it into **AAR_Service** under the **Logic** tab, then publish.  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin.png)
  - Make the action public before publishing so that other modules can access it.  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin01.png)
  - Then, adjust the dependencies (find the module, click it, add it, and click “Apply”).  
    The errors will disappear:  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin02.png)

-----------------------------------

## Property Registration Screen

### Module ARR_WEB

- Example screen:  
  ![Example Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela.png)
- From the **Data** tab, drag it to the **MainFlow**:
  - Both screens are created:  
    ![Example Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela01.png)
  - **Immobiles**: List screen  
    ![List Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela02.png)
  - **ImmobileDetail**: Detail (registration) screen
    - Remove the default IF (which shows "Cadastrar" or "Editar") and replace it with an Expression:
      - If ImmobileId is null, display "Cadastrar"; otherwise, display "Editar" concatenated with " Property":

        ```javascript
        If(ImmobileId = NullIdentifier(), "Cadastrar", "Editar") + " Property"
        ```

    - Remove the Form from within Column1 so that it expands:  
      ![Detail Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela03.png)  
      ![Detail Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela04.png)
    - Drag the **Adaptive/Columns2** component into the Form to divide the columns:  
      ![Detail Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela05.png)
    - The adjusted layout appears as follows:  
      ![Detail Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela06.png)
    - Replace the checkbox with a radioGroup for improved visual appearance:
      - Set the Label to None (i.e., no binding) and adjust the button positions.  
        ![Detail Screen](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela07.png)
    - Check the ClientAction **SaveDetail** to verify that data is being persisted correctly:  
      ![SaveDetail Action](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail.png)
      - Note: Data persistence is not active yet.  
        ![SaveDetail Action](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail01.png)
      - Visual view of the screen:  
        ![SaveDetail Action](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail02.png)

### Module: ARR_Services

#### Register and Edit Property Screen

- To persist data on the "Register Property" screen:
  - Create a folder named after the corresponding Table.
  - Here you will create the action that persists the data.

- **Server Action: Immobile_CreateOrUpdate**  
  ![Server Action: Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate.png)
  - The action expects:
    - **Input Parameter**: Immobile  
      (This parameter is used to persist data to the Immobile Table.)
    - **Output Parameter**: Output  
      - Create a Structure for the Output:  
        ![Output Structure](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate01.png)
      - Configure the attributes:
        - Success (default value: false)  
          ![Success Attribute](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate03.png)
        - Message  
          ![Message Attribute](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate04.png)
        - AccessKey  
          ![AccessKey Attribute](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate05.png)
        - Id (Long Integer)  
          ![Id Attribute](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate06.png)
      - Once the Structure is created, set up the Output Parameter:  
        ![Output Parameter](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate07.png)
  - Create the flow for the ServerAction:  
    ![ServerAction Flow](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate08.png)
  - **Initial Validation:**  
    - Check if the user is equal to NullIdentifier():  
      ![Initial Validation](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate09.png)
  - If **Immobile.Id** is null (new record):
    - If true: Execute **CreateImmobile**
    - If false: Execute **UpdateImmobile**  
      ![Create or Update Decision](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate10.png)
    - In the case of a new record, fill in the **CreatedBy** and **CreatedAt** fields before persisting:  
      ![Fill CreatedBy/CreatedAt](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate11.png)
    - In the Source, remove the Immobile and add the fields individually:  
      ![Configure Fields Individually](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate12.png)
    - > ⚠️ **NOTE:** Ensure that you use the values from the input parameter for each field, except for **CreatedBy** (use GetUserId()) and **CreatedAt** (use CurrDateTime()).  
      ![Field Assignment](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate13.png)  
      ![Field Assignment](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate14.png)  
      ![Field Assignment](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate15.png)
    - The **CreatedBy** and **CreatedAt** fields are the only ones that do not take their values from the input parameter:
      - **CreatedBy:** assign using the GetUserId() function
      - **CreatedAt:** assign using the CurrDateTime() function  
        ![Assign CreatedBy/CreatedAt](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate16.png)
    - Note:
      - In **UpdateImmobile**: Directly assign the input parameter.  
        ![Update Assignment](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate19.png)
      - In **CreateImmobile**: Assign the fields individually, styling the CreatedBy with GetUserId().  
        ![Create Assignment](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.png)
  - Assign the output parameters:
    - **1st:** Create an Assign for CreateImmobile where Output.Id receives the ID from CreateImmobile.  
      ![Assign Create ID](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.1.png)
    - **2nd:** Create an Assign for UpdateImmobile where Output.Id receives the ID from the updated record.  
      ![Assign Update ID](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate22.png)  
      ![Assign Update ID](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate23.png)
- >❗ **EXCEPTION:**  
  - Add an exception to the flow by selecting "All Exceptions".
  - In an Assign, set:
    - Output.Success = False
    - Output.Message = AllExceptions.ExceptionMessage  
      ![Exception Assign](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate25.png)
  - In AllExceptions, the exception aborts the flow (Abort Transcription = Yes).  
    ![Abort Exception](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate26.png)

### Module: ARR_WEB

- Remove elements that will not be used:
  - For example, delete the Aggregate **GetUsers**:  
    ![Delete GetUsers](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate27.png)  
    ![Delete GetUsers](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate28.png)
- Create the flow for the **Client Action: SaveDetail**:
  - First, validate if the form is invalid (False):  
    ![Validate Form](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate29.png)
  - If the form is valid, call the ServerAction Immobile_CreateOrUpdate (passing the Immobile parameter):  
    ![Call ServerAction](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate30.png)  
    ![Call ServerAction](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate31.png)
  - Use an IF to check if the persistence was successful:
    - If not, display an ERROR message (Output.Message):  
      ![Error Message](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate32.png)
    - If successful, display a SUCCESS message and redirect to the **Immobiles** list screen:  
      ![Success Message](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate35.png)
    - End with a REDIRECT:  
      ![Redirect](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate36.png)
- Verify on-screen that the data is being persisted (note: the ZIP code is still fictitious; an API will be used for the ZIP code):  
  ![Persist Data](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate37.png)

### NEXT STEP

- ✨ **IMPLEMENTING THE ZIP CODE (CEP)**:
  - 🛠️ Create an **OnChange** action for the **CEP** field.
  - ✏️ When the **CEP** field is modified, an OnChange event will trigger a service; if the CEP exists, it will automatically fill in the address, neighborhood, and city.

-----------------------------------

## Documentation of Part 3

- Creating Screens and the Login and Property Registration logic:
  - Adjustments in labels
  - Using a Forge component (API)
  - Securing the application with AccessKey
  - OnChange events
  - OnScroolingEnd event
  - Generating a random AccessKey
  - Using a Widget List instead of TableList
  - Joins between tables
  - My Properties screen
  - Evaluate Properties screen

## Start

## Generating a Random AccessKey

- Up to now, for editing or actions shown in the URL, the ID is exposed, which creates a vulnerability.
- As a security measure, we will use the AccessKey, which masks this ID.  
  ![AccessKey Example](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey.png)

### Access Key in ARR_SERVICES

- In the Services module, the ServerAction (**Immobile_CreateOrUpdate**) outputs the parameters (*Success, Message, AccessKey, Id*).
- However, the (**CreateImmobile**) flow does not yet receive the **AccessKey** because it has not been assigned to the table.  
  ![AccessKey Example](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey01.png)

#### Creating the Access Key

- 1º Create an attribute in the Immobile table on the **Data** tab:
  - This attribute should be of type **Text** (since it will receive a HASH).  
    ![Create Attribute](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey02.png)  
    ![Create Attribute](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey03.png)
- 2º Once the attribute is created, return to the flow of the ServerAction (**Immobile_CreateOrUpdate**) in the **CreateImmobile** branch; the AccessKey attribute will now be available.
  ![AccessKey Available](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey04.png)
- 3º Use a system function to generate the AccessKey:
  - In the dependencies, add the ServerAction (**GenerateGuid**).  
    ![GenerateGuid](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey05.png)
- 4º Return to the flow of the ServerAction (**Immobile_CreateOrUpdate**) and assign the value generated by GenerateGuid to the Immobile’s AccessKey attribute.  
  ![Assign AccessKey](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey06.png)
  - Thus, every time a new record is created, an AccessKey will be generated.
- 5º Publish, then go to ARR_WEB.

### Access Key in ARR_WEB

- Once the **ARR_SERVICES** part is complete, update the dependencies in ARR_WEB (Refresh all → Apply → Publish).  
  ![Update Dependencies](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey07.png)
- 1º The **ImmobileDetail** screen expects an input parameter (**Immobile Identifier**); change it to **AccessKey**:
  - DataType: **Text** (since a hash is expected).
  - It does not need to be mandatory.
  - You will also need to modify the GET and the list to reflect this change.  
    ![Change Parameter](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey08.png)
- 2º Modify the **GetImmobileBy**:
  - When you click it, you will see an error comparing an Identifier with different data types, because the parameter changed from Id to AccessKey. Adjust the filter to compare **Immobile.AccessKey** with the **AccessKey** parameter.  
    ![Adjust Filter](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey10.png)
- 3º In the filter of **GetImmobileBy**, set the MaxRecord to 1 (since a unique search is expected).  
    ![Set MaxRecord](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey11.png)
- 4º In the properties list, change the input parameter to **AccessKey**.  
    ![Change List Parameter](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey12.png)  
    ![Change List Parameter](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey13.png)  
    ![Change List Parameter](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey14.png)

-----------------------------------

## Using the Forge Component (API) for CEP

- ✨ **IMPLEMENTING CEP**:
  - 🛠️ Create an **OnChange** action for the **CEP** field.
  - ✏️ When the **CEP** field is modified, an OnChange event will trigger a service; if the CEP exists, it will automatically fill in the address, neighborhood, and city, otherwise, it will display an error message.

### Downloading the Component from the Forge (ViaCEP)

- Download the ViaCEP - Endereços component:
  - In the **Forge** tab, search for **ViaCEP** and, once found, install it in the Studio.  
    ![ViaCEP Component](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP.png)

### Applying in ARR_WEB

- 1º This component is a separate application (ViaCEP); therefore, you must reference it in your project just as you do with ARR_Service.
  - Click on the plug and add it to your project.
  - It has a ServerAction (**CEP**) that takes a parameter (CEP) and returns an Output with address data (via a Structure with fields such as CEP, Logradouro, Complemento, Bairro, Localidade, Uf, Ibge, …, Erro).  
    ![ViaCEP Output](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP01.png)
  - Once applied, it will appear in the **Logic** tab.  
    ![ViaCEP in Logic](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP02.png)
- 2º In the screen, in the **CEP** input, create an OnChange action that, when the field is modified, triggers a process to call the CEP service.  
    ![CEP OnChange](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP03.png)  
    ![CEP OnChange](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP04.png)
- 3º Applying the logic:
  - Add an IF: if the length of the CEP is greater than 7 (i.e., 8 characters or more):

    ```js
    Length(GetImmobileByAccessKey.List.Current.Immobile.CEP) > 7
    ```

  - If false, exit; if true, call the ViaCEP API to retrieve the CEP information.
    ![CEP Call](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP05.png)
  - Drag the **Via_CEP : CEP** ServerAction from the Logic tab, configure its parameters, and connect it to the IF condition.  
    ![Call ViaCEP](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP06.png)  
    ![Call ViaCEP](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP07.png)
  - Configure the input fields to automatically receive the values from the CEP service’s Output:
    - 1º Check if the CEP service returned data.
    - 2º If CEP.Output.Erro is True, exit.
    - 3º Otherwise, use an Assign to fill in the address fields with the data from CEP.Output.  
      ![Assign CEP Data](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)  
      ![Assign CEP Data](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP10.png)  
      ![Assign CEP Data](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP11.png)  
      ![Assign CEP Data](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP12.png)
    - 4º Create an additional Assign to clear the fields if, upon changing the CEP, the service returns an error (i.e., CEP.Output.Erro is True).  
      ![Clear CEP Data](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP13.png)
    - ⚠️ **NOTE:** The OnChange event allows you to fetch and manipulate any information based on the value entered.

-----------------------------------

## My Properties

- Property Listing Screen:
  - Initially, reuse this screen to create the properties listing.  
    ![Properties List Screen](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis01.png)
- Make the initial adjustments to match the template design:
  - 1º Change the name of the page.
  - 2º Remove the "Casa" link (as it will be used in the address editing).
  - 3º Adjust the position of the columns.
  - 4º Rename the button to **Cadastrar Property**.
  - 5º Add the edit link in the **Address** column.
  - 6º Add an **Action** column with the **Delete** icon.
  - 7º Add the **Registration** column.  
    ![Properties List Screen](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis02.png)
- Configure the **Expressions** so that they display the correct values in each column:
  - 1º **Evaluations**: Displays the sum of evaluations for the property.
    - To do this, adjust the Aggregate (GetImoveis) to perform a join with the evaluations table and group the information:
      - Create a join:  
        ![Join for Evaluations](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis03.png)
      - Configure the join as **With or Without** to retrieve records with or without evaluations.
      - Use **Group by** and **Count** to group and count:
        - Group by (e.g., ZIP, Id, Street, Number, CreatedAt, Property Type, AccessKey)  
          ![Group By](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis06.png)
        - Count: the number of grouped records  
          ![Count](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis05.png)
      - The Aggregate will then display only the grouped fields:  
        ![Grouped Data](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis08.png)
      - Remove any reordering of columns:  
        ![Remove Reordering](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis09.png)
      - Update the Expressions to use the new values from the Aggregate:  
        ![Update Expressions](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis10.png)
      - Final result:  
        ![Final Properties List](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis11.png)
  - 2º Adjust the formatting of the **Created on** field using the DateFormate() function:  
    ![Date Formatting](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis12.png)
  - 3º Adjust the **Search** action to search by both ZIP and Address:  
    ![Search Action](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis13.png)
- Creating the **DELETE** Action:
  - 1º Create an initially empty ClientAction in the ARR_WEB module.
  - 2º In the ARR_Server module, create the ServerAction for deletion:  
    ![Delete Action](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete01.png)
  - 3º In the **Data** tab, drag the Delete action from the Immobile table to the ServerAction, adding the ID parameter for the Delete CRUD.  
    ![Drag Delete Action](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete02.png)
  - 4º Configure the CRUD Output (the deletion output).  
    ![CRUD Output](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete03.png)
  - 5º Create the exception flow (AllExceptions):  
    ![Exception Flow](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete05.png)
  - 6º Return to the ARR_WEB module and set up the flow that calls the ServerAction and displays success or error messages:  
    ![Client Delete Flow](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete01.png)  
    ![Client Delete Flow](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete02.png)  
    ![Client Delete Flow](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete03.png)  
    ![Client Delete Flow](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete04.png)

## Evaluation Screen

- **1º** Organize the Evaluation Screen using a **List** component (Main Content > List > Container > Content\CardsSectioned).  
  ![Evaluation Screen](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel01.png)
- **2º** Create a specific Aggregate for this screen:
  - Relate the **Immobile** table with **UserXImmobile** (to obtain the properties where the user has lived).
  - Relate **Immobile** with **TypeImmobile** (using an Only With join).
  - Relate **Immobile** with **Rating** (using a With or Without join).
  - Group the information and count the evaluations:
    - Group by: Immobile.Id, Immobile.Street, Immobile.Street_Number, TypeImmobile.Label, Immobile.AccessKey  
    - Count: Rating.Id  
    ![Evaluation Aggregate](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel03.png)
- **3º** Add the Aggregate to the Source:
  ![Evaluation Source](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel04.png)
  - Update the Expressions and style the Container:  
    ![Styled Container](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel05.png)
  - Create a Group By on **TypeImmobile.Id** to display an icon corresponding to the property type:  
    ![Group By Icon](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel06.png)
  - Create an IF to display the icon based on **TypeImmobile**:  
    ![Conditional Icon](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel07.png)
- **4º** Implement infinite scrolling so that as the user scrolls, more records are loaded:
  - Configure the **On Scroll Ending** event of the List component to trigger a ClientAction (e.g., "New Infinite Scroll Client Action").  
    ![Infinite Scroll](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel08.png)  
    ![Infinite Scroll](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel09.png)
  - The "ScrollEnding" ClientAction uses a local variable **MaxRecords** to define how many records are initially displayed.  
    ![MaxRecords Setup](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel10.png)  
    ![MaxRecords Setup](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel11.png)  
    ![MaxRecords Setup](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel12.png)

-----------------------------------

## Documentation of Part 4

### Evaluation Modal, My Evaluations Screen, Properties I’ve Lived In, and General Adjustments

- Menu adjustments
- Evaluation modal
- Data persistence
- My Evaluations screen
- Properties I’ve Lived In screen
- General adjustments

#### Creating the Evaluation Modal

- Modal display example:  
  ![Evaluation Modal](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao01.png)
- **1º** In the ARR_SERVICES module, create the ServerAction **Rating_CreateOrUpdate**:
  - Flow:
    - If it is a new record, use the "CreatingRating" CRUD and assign via an Assign:
      - Output.Succes = True  
      - Output.Message = "Evaluation created successfully"  
      - Output.Id = CreateRating.Id
    - If it is not a new record, use the "UpdateRating" CRUD and assign:
      - Output.Succes = True  
      - Output.Message = "Evaluation updated successfully"  
      - Output.Id = Rating.Id
    - Both flows end successfully.
    - In case of an exception, use AllExceptions to assign:
      - Output.Succes = False  
      - Output.Message = AllExceptions.ExceptionMessage  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao02.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao03.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao04.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao05.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao06.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao07.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao08.png)  
    ![Rating CreateOrUpdate Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/Server/ModalAvaliacao09.png)
- **2º** In the ARR_WEB module, create the Evaluation Modal (Pop-up):
  - Add a component for the modal and define a local variable **ShowPopupRating** (Boolean, default False).  
    ![ShowPopupRating Variable](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao10.png)  
    ![ShowPopupRating Variable](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao11.png)
  - Bind this variable to the modal.
    ![Bind Variable to Modal](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao12.png)
  - Create a ClientAction (e.g., **ShowPopupRating**) that toggles the variable (to open/close the modal).  
    ![Toggle Modal Action](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao13.png)  
    ![Toggle Modal Action](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao14.png)
  - Create a local variable to store the **Rating** table data that will be used in the modal’s form.  
    ![Local Rating Variable](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao15.png)
  - Adjust the modal structure (title, subtitle, form fields) according to the mockup.  
    ![Modal Structure](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao16.png)
- Additional adjustments:
  - 1º Replace the checkbox input for recommendations with a **Radio group** (options: Yes or No).  
    ![Radio Group for Recommendations](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao17.png)  
    ![Radio Group for Recommendations](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao18.png)  
    ![Radio Group for Recommendations](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao19.png)
  - 2º Replace the "Observation" field with a **textArea** and set its Label to "None".  
    ![TextArea for Observation](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao20.png)
  - 3º Configure the modal title and description to be dynamic by using local variables (e.g., "TypeImmobile" and "ImmobileAddress") that are set in the **ShowPopupRating** action.  
    ![Dynamic Title and Description](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao21.png)  
    ![Dynamic Title and Description](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao22.png)
  - 4º Capture the evaluation ID when clicking, using the local Rating variable.  
    ![Capture Evaluation ID](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao24.png)  
    ![Capture Evaluation ID](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao25.png)  
    ![Capture Evaluation ID](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao23.png)
  - 5º To persist the modal data, create the ClientAction **SaveOnClick** that:
    - Calls the ServerAction **Rating_CreateOrUpdate**.
    - Uses an IF to check if the Output indicates success or error and displays the corresponding message.
    - If successful, clears the local variables (title, description, ID) and closes the modal (by setting ShowPopupRating = False).  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao26.png)  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao27.png)  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao28.png)  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao29.png)  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao30.png)  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao31.png)  
    ![SaveOnClick Flow](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao32.png)
  - 6º In the ServerAction **Rating_CreateOrUpdate** (in the Services module), configure the **CreatedAt** field (using CurrDateTime()) and the **CreatedBy** field (using GetUserId()).  
    ![Configure CreatedAt/CreatedBy](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao33.png)
    - Then update the dependencies in the Web module so the changes are reflected.  
      ![Update Dependencies](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao34.png)
  - 7º Create the "MyRating" screen so that, after confirming the modal, the user’s evaluations are listed:
    - From the **Data** tab, bring in the Immobile table (which already has relationships between Immobile, TypeImmobile, and User).
    - Create a join with the **Rating** table to fetch the evaluations.
      - Use an Only With join to fetch only the records that have evaluations.
      - Add a filter so that the logged-in user sees only their evaluations:

        ```js
        Rating.CreatedBy = GetUserId()
        ```

    ![MyRating Screen](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao35.png)  
    ![MyRating Screen](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao36.png)  
    ![MyRating Screen](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao37.png)
    - Organize the table to include the columns: Address, ZIP, Evaluations, Recommendations, and Date (use functions like DateTimeToDate for formatting).  
      ![MyRating Table](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao38.png)
    - Create a "Search" field to search evaluations by street or ZIP:
      - Add an Input Search with an appropriate placeholder.
      - Define a local variable "SearchRating" (Text) to capture the input.  
        ![Search Field](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao42.png)
      - Configure the OnChange action (e.g., "SearchOnChange") to update the table only if the input length is >= 3 or equals 0:

        ```js
        Length(SearchRatings) >= 3 or Length(SearchRatings) = 0
        ```

      ![Search OnChange](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao40.png)  
      ![Search OnChange](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao41.png)
      - In the Aggregate, create a filter using LIKE on the street and ZIP fields.  
        ![Aggregate Filter](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao39.png)

-----------------------------------

## Documentation of Part 5

- **In this Part:**
  - Menu adjustments
  - Edit event (on the My Evaluations screen)
  - Dashboard screen
  - How to fetch data for charts from the Services module
  - How to manipulate the chart data
  - Adding an attribute in the Aggregate
  - Using Switch
  - Properties I’ve Lived In screen
  - General adjustments

### Adjusting the Menu

- Configure the menu with consistent names to facilitate navigation.  
  ![Menu Adjustment](./Assets/Parte%205/img/ModalAvaliacao43.png)

-----------------------------------

### Creating the Dashboard Screen

- The Dashboard will display charts with important metrics.
- 1º In the Services module, under the "Logic" tab, create a folder for Dashboard-specific server actions.  
  ![Dashboard Folder](./Assets/Parte%205/img/ModalAvaliacao44.png)
- 2º Create a ServerAction for each chart.  
  ![Create Chart Actions](./Assets/Parte%205/img/ModalAvaliacao45.png)
  - These actions must be public so that they can be consumed in the Web module.  
    ![Make Actions Public](./Assets/Parte%205/img/ModalAvaliacao46.png)
- 3º Creating the ServerAction for Rating (Evaluations):
  - I - Drag an Aggregate and add the **Rating** table.
  - II - Create a join (Only With) with the **TypeExperience** table.
    - Perform a Count on Rating.ID and group by TypeExperience.Label.  
      ![Rating Aggregate](./Assets/Parte%205/img/ModalAvaliacao47.png)  
      ![Rating Aggregate](./Assets/Parte%205/img/ModalAvaliacao48.png)
  - 4º Transfer this data to a structure compatible with charts using **DataPoint**.
    - Add 2 output parameters:
      - Output: the structure with a message and success flag.
      - An output parameter of type List of DataPoint.  
      ![DataPoint Setup](./Assets/Parte%205/img/ModalAvaliacao50.png)  
      ![DataPoint Setup](./Assets/Parte%205/img/ModalAvaliacao51.png)  
      ![DataPoint Setup](./Assets/Parte%205/img/ModalAvaliacao52.png)  
      ![DataPoint Setup](./Assets/Parte%205/img/ModalAvaliacao53.png)
  - 5º Structure the flow of the ServerAction (Rating):
    - I - Create the Aggregate with the joins and configure the output parameters.
    - II - Use the ListAppendAll action to transfer the Aggregate data to the DataPoint.
    - III - With an Assign, set:
      - Output.Success = True  
      - Output.Message = "Data collected successfully"
    - IV - Configure the exception flow (AllExceptions):
      - Output.Success = False  
      - Output.Message = AllExceptions.ExceptionMessage  
      ![Rating Flow](./Assets/Parte%205/img/ModalAvaliacao54.png)  
      ![Rating Flow](./Assets/Parte%205/img/ModalAvaliacao55.png)  
      ![Rating Flow](./Assets/Parte%205/img/ModalAvaliacao56.png)  
      ![Rating Flow](./Assets/Parte%205/img/ModalAvaliacao57.png)
- 4º Creating the ServerAction for ImmobileRegister:
  - Similarly, create a ServerAction to obtain the count of Immobile records by creation date.
  - I - Add the input, Output, and Source parameters.
  - II - In the flow:
    - Drag the **Immobile** table.
    - Perform a Count on Immobile.Id and group by Immobile.CreatedAt.
    - Use ListAppendAll to populate the DataPoints (Value = Count, Label = CreatedAt).
    - With an Assign, set:
      - Output.Success = True  
      - Output.Message = "Data collected successfully"
    - Configure the exception flow similarly.  
      ![ImmobileRegister Flow](./Assets/Parte%205/img/ModalAvaliacao58.png)  
      ![ImmobileRegister Flow](./Assets/Parte%205/img/ModalAvaliacao59.png)  
      ![ImmobileRegister Flow](./Assets/Parte%205/img/ModalAvaliacao60.png)  
      ![ImmobileRegister Flow](./Assets/Parte%205/img/ModalAvaliacao61.png)  
      ![ImmobileRegister Flow](./Assets/Parte%205/img/ModalAvaliacao62.png)
- 5º In the Web module, update the dependencies and create the charts:
  - Create a screen named **Dashboard**.
  - Add a title and subtitle.
  - In the Widget Tree, create a Card with a 3-column layout:
    - In Column 1, add a **PieChart** component.
    - In Column 2, add a **LineChart** component.
  - In the Interface > Elements tab, create “Fetch Data from Other Source” actions for the charts:
    - Right-click on the Dashboard screen and select "Fetch Data from Other Source".
    - In the flow, drag the ServerActions for RatingGraph and ImmobileRegisterGraph.
    - With an Assign, set:
      - For RatingGraph: DataPointList = RatingGraph.DataPoint
      - For ImmobileRegisterGraph: DataPointList = ImmobileRegister.DataPoint
    - Configure the outputs of each Fetch as List of DataPoint.
    - In the chart components, set the DataPointList property using the Fetch outputs:
      - PieChart: RatingGraph.DataPointList
      - LineChart: ImmobileRegisterGraph.DataPointList  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao64.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao66.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao67.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao76.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao68.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao69.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao70.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao71.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao72.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao73.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao74.png)  
      ![Dashboard Charts](./Assets/Parte%205/img/ModalAvaliacao75.png)

-----------------------------------

### Creating the "Properties I’ve Lived In" Screen

- In this screen, the goal is to use a calculated attribute in the Aggregate.
  - Set the Dashboard as the main screen.
  - Create a screen named **ImmobileLived**.
  - In the Aggregate for this screen:
    - Add the **Immobile** table and perform a Join with the **UserXImmobile** table.
    - Display the fields: Property, ZIP, Address + Number.
    - Add a Switch to indicate if you have lived in the property.
      - Create a new attribute (New Attribute) in the Aggregate with the formula:

        ```js
        CreatedAt <> NullDate()
        ```

  - Bind this attribute to the Switch component.
- In the Services module, create the logic for the Switch:
  - Create 3 ServerActions:
    - **UserXimmobile_CreateOrUpdate**: to create or update the record.
    - **UserxImmobile_Delete**: to delete the record.
    - **StatusChange**: to determine, based on the Switch status, whether to create or delete the record.  
      ![StatusChange Actions](./Assets/Parte%205/img/ModalAvaliacao84.png)  
      ![StatusChange Actions](./Assets/Parte%205/img/ModalAvaliacao85.png)  
      ![StatusChange Actions](./Assets/Parte%205/img/ModalAvaliacao87.png)  
      ![StatusChange Actions](./Assets/Parte%205/img/ModalAvaliacao86.png)  
      ![StatusChange Actions](./Assets/Parte%205/img/ModalAvaliacao88.png)
- In the Web module, update the dependencies and configure the Switch:
  - In the Switch component, bind the local variable to receive the attribute value (e.g., `GetImmobiles.List.Current.Check`).
  - Configure the OnChange event to call a ClientAction (e.g., "SwitchOnChange") which, in turn, invokes the ServerAction **StatusChange** with the necessary parameters.  
    ![Switch Configuration](./Assets/Parte%205/img/ModalAvaliacao97.png)
  - In the "SwitchOnChange" ClientAction, handle the response:
    - If Output.Success is True, display a success message.
    - Otherwise, display an error message.  
      ![Switch Response](./Assets/Parte%205/img/ModalAvaliacao98.png)  
      ![Switch Response](./Assets/Parte%205/img/ModalAvaliacao99.png)  
      ![Switch Response](./Assets/Parte%205/img/ModalAvaliacao100.png)
- Finally, create an Input Search for the table:
  - Create a local variable "SearchImmobile" of type Text.
  - In the Aggregate, limit Max.Record to 10 and create a filter to search by ZIP and Address.  
    ![Search Filter](./Assets/Parte%205/img/ModalAvaliacao101.png)  
    ![Search Filter](./Assets/Parte%205/img/ModalAvaliacao102.png)  
    ![Search Filter](./Assets/Parte%205/img/ModalAvaliacao103.png)
