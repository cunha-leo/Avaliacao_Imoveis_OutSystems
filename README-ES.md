# App Evaluación de Propiedades en OutSystems

Aplicación en OutSystems Reactive para Evaluación de Propiedades

## Índice

- [1ª Parte - Título de la Parte 1](#documentación-de-la-1ª-parte)
- [2ª Parte - Título de la Parte 2](#documentación-de-la-2ª-parte)
- [3ª Parte - Título de la Parte 3](#documentación-de-la-3ª-parte)
- [4ª Parte - Título de la Parte 4](#documentación-de-la-4ª-parte)
- [5ª Parte - Título de la Parte 5](#documentación-de-la-5ª-parte)

## Readme in English - EN

If you are an English reader, visit the link below:

- [Click here documentation](/README-EN.md)

## Readme en Portugués - PT

Si você é um leitor em português, clique no link abaixo:

- [Clique aquí](/README.md)

-----------------------------------

## Documentación de la 1ª Parte

- Entendiendo el proyecto a través de la plantilla
- Creando el proyecto en dos módulos: Web y Services
- Entendiendo la separación de responsabilidades
- Creando la arquitectura de la base de datos

### Mockups y Plantilla de las Pantallas

Antes de comenzar la implementación, se inició con el entendimiento de los mockups de las pantallas utilizando **Drawio** y se destacó la importancia de contar con una plantilla visual y los beneficios que esto aporta.

Esta planificación visual ayudó a garantizar que todos los elementos quedaran claramente definidos antes de la implementación, aportando claridad a la aplicabilidad.

Las pantallas incluyen:

- Pantalla de Login  
  ![Figura del Mockup - Pantalla de Login](./Template/img/mockup-tela-login.png)
- Dashboard  
  ![Figura del Mockup - Dashboard](./Template/img/mockup-dashboard.png)
- Registro de Propiedad  
  ![Figura del Mockup - Registro de Propiedad](./Template/img/mockup-cadastro-imovel.png)
- Evaluar Propiedad  
  ![Figura del Mockup - Evaluar Propiedad](./Template/img/mockup-avaliar-imovel.png)
- Pop-up para Evaluar Propiedad  
  ![Figura del Mockup - Pop-up para Evaluar Propiedad](./Template/img/mockup-popup-avaliar-imovel.png)
- Mis Evaluaciones  
  ![Figura del Mockup - Mis Evaluaciones](./Template/img/mockup-minhas-avaliacoes.png)
- Mis Propiedades  
  ![Figura del Mockup - Mis Propiedades](./Template/img/mockup-meus-imoveis.png)
- Propiedades en las que ya viví  
  ![Figura del Mockup - Propiedades en las que ya viví](./Template/img/mockup-imoveis-que-ja-morei.png)

### Estructura del Proyecto

1. **Módulo AAR_Services (Service)**:
   - Responsable de la lógica de backend, incluyendo la arquitectura de la base de datos, las relaciones y las acciones CRUD.
   - El módulo está configurado para ser **público**, permitiendo que otros módulos accedan a sus funcionalidades de solo lectura.
   - La arquitectura de las entidades fue diseñada para ser clara y garantizar la integridad de los datos.  
     El diagrama de entidad (ER) fue creado para facilitar la visualización y a continuación se muestra una vista previa de cada tabla:
     ![Diagrama ER](./Assets/Parte%201/img/Data/ER/ER01.png)
   - **Creamos el diagrama ER**:  
     ![Diagrama ER](./Assets/Parte%201/img/Data/ER/ER01.png)
   - **Tablas creadas**:
     - **Tabla Immobile**: Contiene los datos de las propiedades registradas, como CEP, dirección, ciudad, propietario, entre otros.  
       ![Diagrama ER](./Assets/Parte%201/img/Data/Table/ER_Immobile.png)
     - **Tabla Rating**: Almacena las evaluaciones de las propiedades, incluyendo información como tiempo de alquiler, recomendaciones y observaciones de los usuarios.  
       ![Diagrama ER](./Assets/Parte%201/img/Data/Table/ER_Rating.png)
     - **Tabla TypeExperience**: Almacena los tipos de experiencia relacionados con las propiedades. Posee registros como **Excelente, Bueno, Neutral, Malo, Pésimo**.  
       ![Tabla TypeExperience](./Assets/Parte%201/img/Data/Table/ER_TypeExperience.png)
     - **Tabla TypeImmobile**: Almacena los tipos de propiedad disponibles (ej.: Casa, Apartamento, Local). Posee registros como **Casa, Apartamento, Local**.  
       ![Tabla TypeImmobile](./Assets/Parte%201/img/Data/Table/ER_TypeImmobile.png)
     - **Tabla UserxImmobile**: Relaciona a los usuarios con las propiedades, indicando la propiedad y la ocupación.  
       Es una tabla auxiliar que almacena los tipos de experiencia, los tipos de propiedad y la relación entre usuarios y propiedades.  
       ![Tabla UserxImmobile](./Assets/Parte%201/img/Data/Table/ER_UserxImmobile.png)
     - **Tabla User**: Utiliza la entidad predeterminada del sistema OutSystems para almacenar la información de los usuarios, como la fecha de creación y la última modificación.  
       ![Tabla User](./Assets/Parte%201/img/Data/Table/ER_User.png)
2. **Módulo AAR_WEB**:
   - Responsable del front-end y de las pantallas de la aplicación.
   - Se ha añadido como dependencia al **AAR_WEB**, con acceso de solo lectura, para garantizar la seguridad y centralizar toda la lógica de servidor en el módulo **AAR_Services**.
   - En el módulo web/reactive se pueden observar todas las pestañas, incluyendo **Triggers, Interface, Logic y Data**.  
     ![Estructura del Módulo AAR_WEB](./Assets/Parte%201/img/Model/estrutura-aar-web.png)

### Conclusión

Esta primera etapa del proyecto incluyó la configuración inicial de los módulos y la creación de las entidades de la base de datos, además de la definición de la interfaz de usuario.  
Utilizamos un enfoque modular que facilita el mantenimiento y la seguridad de los datos, separando la lógica del servidor del front-end.

En la siguiente etapa, nos centraremos en finalizar la estructuración de las pantallas en el módulo **AAR_WEB**, asegurándonos de que todas las funcionalidades estén alineadas con el objetivo del proyecto.

-----------------------------------

## Documentación de la 2ª Parte

- Creación de la Pantalla de Login y de Registro de Propiedades, y sus lógicas

### Pantalla de Login

- Aquí podemos observar, en el lado derecho, que por defecto la pantalla de Login de OutSystems viene con:  
  ![Pantalla de Login](./Assets/Parte%202/img/Tela%20Login/Login01.png)

#### 4 Variables Locales

- **Username**: Se utiliza en el Input **E-mail**  
  ![Var Username](./Assets/Parte%202/img/Tela%20Login/Var_Username.png)
- **Password**: Se utiliza en el Input **Contraseña**  
  ![Var Password](./Assets/Parte%202/img/Tela%20Login/Var_Password.png)
- **IsExecuting**: Se utiliza para indicar la ejecución de alguna acción en la ClientAction **OnInitialize**  
  ![Var IsExecuting](./Assets/Parte%202/img/Tela%20Login/Var_IsExecuting.png)
- **Remember**: Se utiliza en el Input de Checkbox **Recuérdame**  
  ![Var Remember](./Assets/Parte%202/img/Tela%20Login/Var_Remember.png)

#### 3 Acciones del Cliente

- **ForgotPassword**: Para recuperar la contraseña  
  ![ForgotPassword](./Assets/Parte%202/img/Tela%20Login/Client/ForgotPassword.png)
- **Login**: Utilizada en el botón **Entrar**  
  ![Login](./Assets/Parte%202/img/Tela%20Login/Client/Login.png)
  - La lógica del Login asigna la variable local **IsExecuting** a True tras hacer clic:  
    ![IsExecuting](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-IsExecuting.png)
  - A continuación, se llama a la ServerAction **DoLogin**:
    - Recibe las variables locales: Username, Password, Remember.
    - Persiste los datos y verifica que se hayan guardado en la base de datos.
    - Llama a la ServerAction predeterminada de Login de OutSystems (dentro de User).  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin01.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin02.png)  
      ![Do Login](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)
  - Después, se elimina un mensaje de retroalimentación tras iniciar sesión.
  - Finalmente, se redirige al usuario a la pantalla principal:  
    ![Redirect](./Assets/Parte%202/img/Tela%20Login/Client/Logic-Login-Server_DoLogin03.png)
- **OnInitialize**:
  - Se utiliza para ejecutar acciones una vez que la pantalla se ha cargado  
    - Tal como se muestra en la imagen siguiente:  
      ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize01.png)
  - Se utiliza para asignar la variable local "IsExecuting" para implementar la acción  
    - En este caso, el valor predeterminado es False, es decir, al iniciar la pantalla, no se ejecuta ninguna acción.  
      ![OnInitialize](./Assets/Parte%202/img/Tela%20Login/Client/OnInitialize.png)

-----------------------------------

### Cambiando las acciones de Autenticación al camino correcto

- Esto se debe a que la lógica de servidor debe residir en el módulo **ARR_Service**:
  - Simplemente corta la acción desde **ARR_WEB** y pégala en **AAR_Service**, en la pestaña **Logic**, y publica.  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin.png)
  - Debe hacerse pública antes de publicar, para que otros módulos puedan acceder a ella.  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin01.png)
  - Luego, ajusta las dependencias (busca el módulo, haz clic, agrégalo y haz “Apply”).  
    Al aplicar, los errores desaparecerán:  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Login/Server/ServerAction_DoLogin02.png)

-----------------------------------

## Pantalla de Registro de Propiedades

### Módulo ARR_WEB

- Ejemplo de pantalla:  
  ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela.png)
- Desde la pestaña **Data**, arrastra al **MainFlow**:
  - Se crean ambas pantallas:  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela01.png)
  - **Immobiles**: Pantalla de Listado  
    ![Server Action DoLogin](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela02.png)
  - **ImmobileDetail**: Pantalla de Registro
    - Elimina el IF predeterminado (que muestra "Cadastrar" o "Editar") y reemplázalo por una Expression:
      - Si ImmobileId es nulo, muestra "Cadastrar"; de lo contrario, "Editar" concatenado con "Propiedad":

        ```javascript
        If(ImmobileId = NullIdentifier(), "Cadastrar", "Editar") + " Propiedad"
        ```

    - Elimina el Form dentro de Column1 para que se expanda:  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela03.png)  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela04.png)
    - Arrastra el componente **Adaptive/Columns2** dentro del Form, dividiendo las columnas:  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela05.png)
    - El diseño ajustado queda así:  
      ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela06.png)
    - Se reemplaza el checkbox por un radioGroup para mejorar la visualización:
      - Configura el Label como None (sin vinculación) y ajusta la posición de los botones.  
        ![CI_Criando Tela](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/CI_Criando%20Tela07.png)
    - Verifica la ClientAction **SaveDetail** para asegurar que los datos se están persistiendo correctamente:  
      ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail.png)
      - Nota: Aún no se está realizando la persistencia de los datos.  
        ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail01.png)
      - Vista visual de la pantalla:  
        ![CI_SaveDetail](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Client/SaveDetail02.png)

### Módulo: ARR_Services

#### Pantalla Registrar Propiedad y Editar Propiedad

- Para persistir los datos en la pantalla "Registrar Propiedad":
  - Crea una carpeta con el nombre de la Tabla correspondiente.
  - Aquí crearás la acción que persistirá los datos.

- **Server Action: Immobile_CreateOrUpdate**  
  ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate.png)
  - La acción espera:
    - **Parámetro de Entrada**: Immobile  
      (Se pretende persistir la Tabla Immobile utilizando este parámetro).
    - **Parámetro de Salida**: Output  
      - Se crea una Structure para el Output:  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate01.png)
      - Configura los atributos:
        - Success (valor por defecto: false)  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate03.png)
        - Message  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate04.png)
        - AccessKey  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate05.png)
        - Id (Long Integer)  
          ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate06.png)
      - Una vez creada la Structure, configura el Parámetro de Salida:  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate07.png)
  - Crea el flujo de la ServerAction:  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate08.png)
  - **Validación Inicial:**  
    - Verifica si el usuario es igual a NullIdentifier():  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate09.png)
  - Si **Immobile.Id** es nulo (registro nuevo):
    - Si es verdadero: Ejecuta **CreateImmobile**
    - Si es falso: Ejecuta **UpdateImmobile**  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate10.png)
    - En el caso de un registro nuevo, antes de persistir, rellena los campos **CreatedBy** y **CreatedAt**:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate11.png)
    - En el Source, elimina el objeto Immobile y agrega los campos de forma individual:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate12.png)
    - > ⚠️ **ATENCIÓN:** Asegúrate de utilizar los valores del parámetro de entrada para cada campo, excepto para **CreatedBy** (usa GetUserId()) y **CreatedAt** (usa CurrDateTime()).  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate13.png)  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate14.png)  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate15.png)
    - Los campos **CreatedBy** y **CreatedAt** son los únicos que no se toman del parámetro de entrada:
      - **CreatedBy:** se asigna con la función GetUserId()
      - **CreatedAt:** se asigna con la función CurrDateTime()  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate16.png)
    - Observación:
      - En **UpdateImmobile**: Se asigna directamente el parámetro de entrada.  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate19.png)
      - En **CreateImmobile**: Se asignan los campos individualmente, configurando CreatedBy con GetUserId().  
        ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.png)
  - Asigna los parámetros de salida:
    - **1º:** Crea un Assign para CreateImmobile en el que Output.Id recibe el ID generado por CreateImmobile.  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate20.1.png)
    - **2º:** Crea un Assign para UpdateImmobile en el que Output.Id recibe el ID del registro actualizado.  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate22.png)  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate23.png)
- >❗ **EXCEPCIÓN:**  
  - Agrega una excepción al flujo seleccionando "Todas las Exceptions".
  - En un Assign, configura:
    - Output.Success = False
    - Output.Message = AllExceptions.ExceptionMessage  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate25.png)
  - En AllExceptions, la excepción aborta el flujo (Abort Transcription = Yes).  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate26.png)

### Módulo: ARR_WEB

- Elimina los elementos que no se van a utilizar:
  - Por ejemplo, elimina el Aggregate **GetUsers**:  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate27.png)  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate28.png)
- Crea el flujo de la **Client Action: SaveDetail**:
  - Primero valida si el formulario es inválido (False):  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate29.png)
  - Si el formulario es válido, llama a la ServerAction Immobile_CreateOrUpdate (pasándole el parámetro Immobile):  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate30.png)  
    ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate31.png)
  - Usa un IF para verificar si la persistencia fue exitosa:
    - Si no lo fue, muestra un mensaje de ERROR (Output.Message):  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate32.png)
    - Si fue exitosa, muestra un mensaje de ÉXITO y redirige a la pantalla de listado de **Immobiles**:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate35.png)
    - Finaliza con un REDIRECT:  
      ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate36.png)
- Verifica en pantalla que los datos se estén persistiendo (observa que el CEP aún es ficticio; se utilizará una API para el CEP):  
  ![ServerAction  Immobile_CreateOrUpdate](./Assets/Parte%202/img/Tela%20Cadastro%20de%20Imoveis/Server/Immobile_CreateOrUpdate37.png)

### PRÓXIMA ETAPA

- ✨ **IMPLEMENTANDO EL CEP**:
  - 🛠️ Crea una acción **OnChange** para el campo **CEP**.
  - ✏️ Al modificar el campo **CEP**, se ejecutará un evento OnChange que llamará a un servicio; si el CEP existe, completará automáticamente la dirección, el barrio y la ciudad.

-----------------------------------

## Documentación de la 3ª Parte

- Creación de Pantallas y lógica de Login y Registro de Propiedades:
  - Ajustes en los textos (labels)
  - Uso de un componente de la Forge (API)
  - Aseguramiento de la aplicación mediante AccessKey
  - Eventos OnChange
  - Evento OnScroolingEnd
  - Generación aleatoria de AccessKey
  - Uso de Widget List en lugar de TableList
  - Relaciones (Join) entre tablas
  - Pantalla Mis Propiedades
  - Pantalla Evaluar Propiedades

## Inicio

## Generando AccessKey aleatorio

- Hasta el momento, para la edición o acciones mostradas en la URL se expone el ID, lo que genera vulnerabilidad.
- Como medida de seguridad, se utilizará el AccessKey, que enmascara este ID.  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey.png)

### Access Key en ARR_SERVICES

- En el módulo Services, la ServerAction (**Immobile_CreateOrUpdate**) posee en su Output los parámetros (*Success, Message, AccessKey, Id*).
- Sin embargo, el flujo de (**CreateImmobile**) aún no recibe el **AccessKey** porque no se ha asignado en la tabla.  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey01.png)

#### Creando el Access Key

- 1º Crea un atributo en la tabla Immobile, en la pestaña **Data**:
  - Este atributo debe ser de tipo **Text** (ya que recibirá una HASH).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey02.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey03.png)
- 2º Una vez creado el atributo, regresa al flujo de la ServerAction (**Immobile_CreateOrUpdate**) en la rama **CreateImmobile**; allí, el atributo AccessKey estará disponible.
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey04.png)
- 3º Utiliza una función del sistema para configurar el AccessKey:
  - En las dependencias, añade la ServerAction (**GenerateGuid**).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey05.png)
- 4º Regresa al flujo de la ServerAction (**Immobile_CreateOrUpdate**) y asigna el valor generado por GenerateGuid al atributo AccessKey del Immobile.  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey06.png)
  - Así, cada vez que se cree un nuevo registro, se generará un AccessKey.
- 5º Publica y luego ve al módulo ARR_WEB.

### Access Key en ARR_WEB

- Una vez finalizada la parte de **ARR_SERVICES**, en ARR_WEB actualiza las dependencias (Refresh all → Apply → Publicar).  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey07.png)
- 1º La pantalla **ImmobileDetail** espera un parámetro de entrada (**Immobile Identifier**); cámbialo por **AccessKey**:
  - DataType: **Text** (porque ahora se espera una hash).
  - No es necesario que sea obligatorio.
  - También deberás modificar el GET y la lista para reflejar este cambio.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey08.png)
- 2º Modifica el **GetImmobileBy**:
  - Al hacer clic, notarás un error por comparar un Identificador con tipos de datos diferentes, ya que se cambió el parámetro de Id a AccessKey. Ajusta el filtro para comparar **Immobile.AccessKey** con el parámetro **AccessKey**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey10.png)
- 3º En el filtro del **GetImmobileBy**, establece el MaxRecord en 1 (ya que se espera una búsqueda única).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey11.png)
- 4º En la lista de propiedades, cambia el parámetro de entrada a **AccessKey**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey12.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey13.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/AccessKey/AccessKey14.png)

-----------------------------------

## Utilizando el componente de la Forge (API) CEP

- ✨ **IMPLEMENTANDO EL CEP**:
  - 🛠️ Crea una acción **OnChange** para el campo **CEP**.
  - ✏️ Al modificar el campo **CEP**, se ejecutará un evento OnChange que llamará a un servicio; si el CEP existe, completará automáticamente la dirección, el barrio y la ciudad, y de lo contrario, mostrará un mensaje de error.

### Descargando el Componente en la Forge (ViaCEP)

- Descarga el componente ViaCEP - Endereços:
  - En la pestaña **Forge**, busca **ViaCEP** y, una vez encontrado, instálalo en el Studio.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP.png)

### Aplicando en ARR_WEB

- 1º Este componente es una aplicación separada (ViaCEP); por lo tanto, debes referenciarlo en tu proyecto de la misma forma que se hace con ARR_Service.
  - Haz clic en el enchufe (plug) y agrégalo a tu proyecto.
  - Posee una ServerAction (**CEP**) que recibe un parámetro (CEP) y devuelve un Output con los datos de dirección (a través de una Structure con campos como CEP, Logradouro, Complemento, Barrio, Localidad, Uf, Ibge, …, Erro).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP01.png)
  - Una vez aplicado, lo verás en la pestaña **Logic**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP02.png)
- 2º En la pantalla, en el Input **CEP**, crea una acción OnChange que, al modificarse el campo, active una trigger que llame al servicio CEP.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP03.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP04.png)
- 3º Aplicando la lógica:
  - Agrega un IF: si la longitud del CEP es mayor a 7 (es decir, 8 caracteres o más):

    ```js
    Length(GetImmobileByAccessKey.List.Current.Immobile.CEP) > 7
    ```

  - Si es falso, finaliza; si es verdadero, llama a la API ViaCEP para obtener la información del CEP.
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP05.png)
  - Arrastra la ServerAction **Via_CEP : CEP** desde la pestaña Logic, configura los parámetros y conéctala a la condición.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP06.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP07.png)
  - Configura los Inputs para que reciban automáticamente los valores del Output del servicio CEP:
    - 1º Verifica si el servicio CEP devolvió la información.
    - 2º Si CEP.Output.Erro es True, finaliza.
    - 3º En caso contrario, utiliza un Assign para completar los campos de dirección con los datos del Output del servicio CEP.  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP09.png)  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP10.png)  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP11.png)  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP12.png)
    - 4º Crea un Assign adicional para limpiar los campos en caso de que, al modificar el CEP, el servicio no encuentre información (CEP.Output.Erro sea True).  
      ![Tela de Login](./Assets/Parte%203/img/Tela%20Editar%20Imovel/API%20ViaCEP/ViaCEP13.png)
    - ⚠️ **NOTA:** Con el evento OnChange puedes buscar y manipular cualquier información basándote en el valor ingresado.

-----------------------------------

## Mis Propiedades

- Pantalla de Listado de Propiedades:
  - Inicialmente, reutiliza esta pantalla para crear el listado de propiedades.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis01.png)
- Realiza los ajustes iniciales para acercarla al diseño del template:
  - 1º Cambia el nombre de la página.
  - 2º Elimina el enlace "Casa" (ya que se usará en la edición de la dirección).
  - 3º Ajusta la posición de las columnas.
  - 4º Renombra el botón a **Cadastrar Propiedad**.
  - 5º Agrega el enlace de edición en la columna **Dirección**.
  - 6º Agrega una columna de **Acción** con el ícono de **Eliminar**.
  - 7º Agrega la columna de **Registro**.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis02.png)
- Configura las **Expressions** para que muestren los valores correctos en cada columna:
  - 1º **Evaluaciones**: Muestra la suma de las evaluaciones para la propiedad.
    - Para ello, ajusta el Aggregate (GetImoveis) para realizar el join con la tabla de evaluaciones y agrupar la información:
      - Crea un join:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis03.png)
      - Configura el join como **With or Without** para obtener registros con o sin evaluación.
      - Utiliza **Group by** y **Count** para agrupar y contar:
        - Group by (por ejemplo: CEP, Id, Calle, Número, CreatedAt, Tipo de Propiedad, AccessKey)  
          ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis06.png)
        - Count: Cantidad de registros agrupados  
          ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis05.png)
      - El Aggregate mostrará únicamente los campos agrupados:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis08.png)
      - Elimina la reordenación de las columnas:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis09.png)
      - Actualiza las Expressions para que utilicen los nuevos valores del Aggregate:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis10.png)
      - Resultado final:  
        ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis11.png)
  - 2º Ajusta la formateación del campo **Creado en** usando la función DateFormate():  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis12.png)
  - 3º Ajusta la acción del **Search** para que busque tanto por CEP como por Dirección:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/TelaMeusImoveis13.png)
- Creando la Acción **DELETE**:
  - 1º Crea una ClientAction (en el módulo ARR_WEB) inicialmente vacía.
  - 2º En el módulo ARR_Server, crea la ServerAction para eliminar el registro:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete01.png)
  - 3º En la pestaña **Data**, arrastra la acción de Delete de la tabla Immobile a la ServerAction, añadiendo el parámetro ID para el CRUD de Delete.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete02.png)
  - 4º Configura el Output del CRUD (la salida del Delete).  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete03.png)
  - 5º Crea el flujo de excepción (AllExceptions):
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Server/Immobile_Delete05.png)
  - 6º Regresa al módulo ARR_WEB y configura el flujo que llama a la ServerAction y muestra los mensajes de éxito o error:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete01.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete02.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete03.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Meus%20Imoveis/Client/Immobile_Delete04.png)

## Pantalla de Evaluación

- **1º** Organiza la Pantalla de Evaluación utilizando un componente **List** (Main Content > List > Container > Content\CardsSectioned).  
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel01.png)
- **2º** Crea un Aggregate específico para esta pantalla:
  - Relaciona la tabla **Immobile** con **UserXImmobile** (para obtener las propiedades en las que el usuario ya vivió).
  - Relaciona **Immobile** con **TypeImmobile** (utilizando join Only With).
  - Relaciona **Immobile** con **Rating** (utilizando join With or Without).
  - Agrupa la información y cuenta las evaluaciones:
    - Group by: Immobile.Id, Immobile.Street, Immobile.Street_Number, TypeImmobile.Label, Immobile.AccessKey  
    - Count: Rating.Id  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel03.png)
- **3º** Añade el Aggregate al Source:
  ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel04.png)
  - Actualiza las Expressions y estiliza el Container:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel05.png)
  - Crea un Group By en **TypeImmobile.Id** para mostrar un ícono acorde al tipo de propiedad:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel06.png)
  - Crea un IF para mostrar el ícono en función del **TypeImmobile**:  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel07.png)
- **4º** Implementa el scroll infinito para que, al desplazar la pantalla, se carguen más registros:
  - Configura el evento **On Scroll Ending** del componente List para que invoque una ClientAction (por ejemplo, "New Infinite Scroll Client Action").  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel08.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel09.png)
  - La ClientAction "ScrollEnding" utiliza una variable local **MaxRecords** que define la cantidad de registros a mostrar inicialmente.  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel10.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel11.png)  
    ![Tela de Login](./Assets/Parte%203/img/Tela%20Avaliações/Avaliar_Imovel12.png)

-----------------------------------

## Documentación de la 4ª Parte

### Modal de Evaluación, Pantalla Mis Evaluaciones, Propiedades en las que ya viví y Ajustes Generales

- Ajustes en el menú
- Modal de evaluación
- Persistencia de datos
- Pantalla Mis Evaluaciones
- Pantalla Propiedades en las que ya viví
- Ajustes generales

#### Creando el Modal de Evaluación

- Visualización del modal:  
  ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao01.png)
- **1º** En el módulo ARR_SERVICES, crea la ServerAction **Rating_CreateOrUpdate**:
  - Flujo:
    - Si es un registro nuevo, utiliza el CRUD "CreatingRating" y asigna mediante un Assign:
      - Output.Succes = True  
      - Output.Message = "Evaluación creada con éxito"  
      - Output.Id = CreateRating.Id
    - Si no es un registro nuevo, utiliza el CRUD "UpdateRating" y asigna:
      - Output.Succes = True  
      - Output.Message = "Evaluación actualizada con éxito"  
      - Output.Id = Rating.Id
    - Ambos flujos finalizan con éxito.
    - En caso de excepción, utiliza AllExceptions para asignar:
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
- **2º** En el módulo ARR_WEB, crea el Modal (Pop-up) de Evaluación:
  - Agrega un componente para el pop-up y define una variable local **ShowPopupRating** (Boolean, por defecto False).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao10.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao11.png)
  - Asigna esta variable al pop-up.
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao12.png)
  - Crea una ClientAction (por ejemplo, **ShowPopupRating**) que invierta el valor de la variable (para abrir/cerrar el pop-up).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao13.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao14.png)
  - Crea una variable local para almacenar la tabla **Rating** que se utilizará en el formulario del pop-up.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao15.png)
  - Ajusta la estructura del pop-up (título, subtítulo y campos del formulario) según el mockup.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao16.png)
- Ajustes adicionales:
  - 1º Cambia el input de checkbox de las recomendaciones por un **Radio group** (opciones Sí o No).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao17.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao18.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao19.png)
  - 2º Cambia el campo "Observación" por un **textArea** y configura el Label como "None".
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao20.png)
  - 3º Configura el título y la descripción del pop-up para que sean dinámicos, utilizando variables locales (por ejemplo, "TypeImmobile" e "ImmobileAddress") que se asignan en la acción **ShowPopupRating**.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao21.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao22.png)
  - 4º Captura el ID de la evaluación al hacer clic, utilizando la variable local Rating.  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao24.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao25.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao23.png)
  - 5º Para persistir los datos del pop-up, crea la ClientAction **SaveOnClick** que:
    - Llama a la ServerAction **Rating_CreateOrUpdate**.
    - Utiliza un IF para verificar si el Output indica éxito o error y muestra el mensaje correspondiente.
    - En caso de éxito, limpia las variables locales (título, descripción, ID) y cierra el pop-up (asignando ShowPopupRating = False).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao26.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao27.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao28.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao29.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao30.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao31.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao32.png)
  - 6º En la ServerAction **Rating_CreateOrUpdate** (módulo Services), configura los campos **CreatedAt** (usando CurrDateTime()) y **CreatedBy** (usando GetUserId()).  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao33.png)
    - Luego, actualiza las dependencias en el módulo Web para reflejar el cambio.  
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao34.png)
  - 7º Crea la pantalla "MyRating" para que, después de confirmar el pop-up, se liste la evaluación del usuario:
    - Extrae de la pestaña **Data** la tabla Immobile (la cual ya tiene las relaciones entre Immobile, TypeImmobile y User).
    - Crea un Join con la tabla **Rating** para traer las evaluaciones.
      - Utiliza join **Only With** para traer únicamente los registros que tengan evaluación.
      - Agrega un filtro para que el usuario logueado vea solo sus evaluaciones:

        ```js
        Rating.CreatedBy = GetUserId()
        ```

    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao35.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao36.png)  
    ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao37.png)
    - Organiza la tabla para que incluya las columnas: Dirección, CEP, Evaluaciones, Recomendaciones y fecha (usa funciones como DateTimeToDate para formatear).  
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao38.png)
    - Crea un campo "Search" para buscar evaluaciones por calle o CEP:
      - Crea un Input Search con un placeholder descriptivo.
      - Define una variable local "SearchRating" de tipo Texto para capturar lo ingresado.  
        ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao42.png)
      - Configura la acción OnChange (por ejemplo, "SearchOnChange") para actualizar la lista solo si la longitud del texto es >= 3 o igual a 0:

        ```js
        Length(SearchRatings) >= 3 or Length(SearchRatings) = 0
        ```

      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao40.png)  
      ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao41.png)
      - En el Aggregate, crea un filtro que utilice LIKE en los campos de calle y CEP.  
        ![Parte 4](./Assets/Parte%204/img/ModalAvaliacao-TelaAvaliarImovel/ModalAvaliacao39.png)

-----------------------------------

## Documentación de la 5ª Parte

- **En esta Parte:**
  - Ajustes en el menú
  - Evento de edición (en la pantalla Mis Evaluaciones)
  - Pantalla del Dashboard
  - Cómo consumir datos para gráficos desde el módulo Services
  - Cómo manipular los datos de los gráficos
  - Adición de un atributo en el Aggregate
  - Uso de Switch
  - Pantalla de Propiedades en las que ya viví
  - Ajustes generales

### Ajustando el Menú

- Configura el menú con nombres uniformes para facilitar la navegación.  
  ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao43.png)

-----------------------------------

### Creando la Pantalla del Dashboard

- El Dashboard mostrará gráficos con métricas importantes.
- 1º En el módulo Services, en la pestaña "Logic", crea una carpeta para las acciones de servidor específicas del Dashboard.  
  ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao44.png)
- 2º Crea una ServerAction para cada gráfico.  
  ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao45.png)
  - Estas acciones deben ser públicas para poder ser consumidas en el módulo Web.  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao46.png)
- 3º Creando la ServerAction para Rating (Evaluaciones):
  - I - Arrastra un Aggregate y añade la tabla **Rating**.
  - II - Crea un join (Only With) con la tabla **TypeExperience**.
    - Realiza un Count en Rating.ID y agrupa por TypeExperience.Label.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao47.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao48.png)
  - 4º Transfiere estos datos a una estructura compatible con gráficos, utilizando **DataPoint**.
    - Añade 2 parámetros de salida:
      - Output: la estructura con mensaje y éxito.
      - Un parámetro de salida del tipo List of DataPoint.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao50.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao51.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao52.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao53.png)
  - 5º Estructura el flujo de la ServerAction (Rating):
    - I - Crea el Aggregate con los joins y configura los parámetros de salida.
    - II - Usa la acción ListAppendAll para trasladar los datos del Aggregate al DataPoint.
    - III - Con un Assign, establece:
      - Output.Success = True  
      - Output.Message = "Datos recolectados con éxito"
    - IV - Configura el flujo de excepción (AllExceptions):
      - Output.Success = False  
      - Output.Message = AllExceptions.ExceptionMessage  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao54.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao55.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao56.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao57.png)
- 4º Creando la ServerAction para ImmobileRegister:
  - De forma similar a la acción anterior, crea una ServerAction para obtener la cantidad de registros de Immobile por fecha de creación.
  - I - Añade los parámetros de entrada, Output y Source.
  - II - En el flujo:
    - Arrastra la tabla **Immobile**.
    - Realiza un Count en Immobile.Id y agrupa por Immobile.CreatedAt.
    - Usa ListAppendAll para llenar los DataPoints (Value = Count, Label = CreatedAt).
    - Con un Assign, establece:
      - Output.Success = True  
      - Output.Message = "Datos recolectados con éxito"
    - Configura el flujo de excepción de forma similar.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao58.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao59.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao60.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao61.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao62.png)
- 5º En el módulo Web, actualiza las dependencias y crea los gráficos:
  - Crea una pantalla llamada **Dashboard**.
  - Añade un título y un subtítulo.
  - En el Widget Tree, crea un Card con un layout de 3 columnas:
    - En la Columna 1, añade un componente **PieChart**.
    - En la Columna 2, añade un componente **LineChart**.
  - En la pestaña Interface > Elements, crea “Fetch Data from Other Source” para los gráficos:
    - Haz clic derecho sobre la pantalla Dashboard y selecciona "Fetch Data from Other Source".
    - En el flujo, arrastra las ServerActions para RatingGraph y ImmobileRegisterGraph.
    - Con un Assign, configura:
      - Para RatingGraph: DataPointList = RatingGraph.DataPoint
      - Para ImmobileRegisterGraph: DataPointList = ImmobileRegister.DataPoint
    - Configura los Outputs de cada Fetch como List of DataPoint.
    - En los componentes de gráfico, define la propiedad DataPointList utilizando los Outputs:
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

### Creando la Pantalla "Propiedades en las que ya viví"

- En esta pantalla, el objetivo es utilizar un atributo calculado en el Aggregate.
  - Configura el Dashboard como pantalla principal.
  - Crea una Screen llamada **ImmobileLived**.
  - En el Aggregate de esta Screen:
    - Añade la tabla **Immobile** y realiza un Join con la tabla **UserXImmobile**.
    - Muestra los campos: Propiedad, CEP, Dirección + Número.
    - Añade un Switch para indicar si ya viviste en la propiedad.
      - Para ello, crea un nuevo atributo (New Attribute) en el Aggregate con la fórmula:

        ```js
        CreatedAt <> NullDate()
        ```

  - Vincula este atributo al componente Switch.
- En el módulo Services, crea la lógica para el Switch:
  - Crea 3 ServerActions:
    - **UserXimmobile_CreateOrUpdate**: para crear o actualizar el registro.
    - **UserxImmobile_Delete**: para eliminar el registro.
    - **StatusChange**: para determinar, en función del estado (Switch), si se debe crear o eliminar el registro.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao84.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao85.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao87.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao86.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao88.png)
- En el módulo Web, actualiza las dependencias y configura el Switch:
  - En el componente Switch, asigna la variable local para recibir el valor del atributo (por ejemplo, `GetImmobiles.List.Current.Check`).
  - Configura el evento OnChange para llamar a la ClientAction (por ejemplo, "SwitchOnChange") que a su vez invoca la ServerAction **StatusChange** con los parámetros necesarios.  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao97.png)
  - En la ClientAction "SwitchOnChange", procesa el retorno:
    - Si Output.Success es True, muestra un mensaje de éxito.
    - Si no, muestra un mensaje de error.  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao98.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao99.png)  
      ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao100.png)
- Finalmente, crea un Input Search para la tabla:
  - Crea una variable local "SearchImmobile" de tipo Texto.
  - En el Aggregate, limita el Max.Record a 10 y crea un filtro para buscar por CEP y Dirección.  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao101.png)  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao102.png)  
    ![Parte 5](./Assets/Parte%205/img/ModalAvaliacao103.png)
