<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="31d45-101">В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31d45-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="31d45-102">Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="31d45-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="31d45-103">Для этого в приложение будет интегрирована библиотека [реагирующих на приложения](https://github.com/FormidableLabs/react-native-app-auth) .</span><span class="sxs-lookup"><span data-stu-id="31d45-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="31d45-104">Создайте новый каталог в каталоге **графтуториал** с именем **AUTH**.</span><span class="sxs-lookup"><span data-stu-id="31d45-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="31d45-105">Создайте новый файл в каталоге **графтуториал/auth** с именем **AuthConfig. TS**.</span><span class="sxs-lookup"><span data-stu-id="31d45-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.ts**.</span></span> <span data-ttu-id="31d45-106">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="31d45-106">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    <span data-ttu-id="31d45-107">Замените `YOUR_APP_ID_HERE` идентификатором приложения, указанным в регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="31d45-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31d45-108">Если вы используете систему управления версиями (например, Git), то теперь будет полезно исключить файл **AuthConfig. TS** из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="31d45-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="31d45-109">Реализация входа</span><span class="sxs-lookup"><span data-stu-id="31d45-109">Implement sign-in</span></span>

<span data-ttu-id="31d45-110">В этом разделе вы создадите вспомогательный класс проверки подлинности и обновите приложение, чтобы войти в систему и выйти из нее.</span><span class="sxs-lookup"><span data-stu-id="31d45-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="31d45-111">Создайте новый файл в каталоге **графтуториал/auth** с именем **аусманажер. TS**.</span><span class="sxs-lookup"><span data-stu-id="31d45-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.ts**.</span></span> <span data-ttu-id="31d45-112">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="31d45-112">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. <span data-ttu-id="31d45-113">Откройте **графтуториал/App. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="31d45-113">Open the **GraphTutorial/App.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. <span data-ttu-id="31d45-114">Замените существующее `authContext` объявление следующим.</span><span class="sxs-lookup"><span data-stu-id="31d45-114">Replace the existing `authContext` declaration with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. <span data-ttu-id="31d45-115">Откройте файл **графтуториал/Menus/дравермену. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="31d45-115">Open the **GraphTutorial/menus/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="31d45-116">Добавьте следующий код в `componentDidMount` функцию.</span><span class="sxs-lookup"><span data-stu-id="31d45-116">Add the following code to the `componentDidMount` function.</span></span>

    ```typescript
    try {
      const accessToken = await AuthManager.getAccessTokenAsync();

      // TEMPORARY
      this.setState({userFirstName: accessToken, userLoading: false});
    } catch (error) {
      Alert.alert(
        'Error getting token',
        JSON.stringify(error),
        [
          {
            text: 'OK'
          }
        ],
        { cancelable: false }
      );
    }
    ```

1. <span data-ttu-id="31d45-117">Сохраните изменения и перезагрузите приложение в симуляторе.</span><span class="sxs-lookup"><span data-stu-id="31d45-117">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="31d45-118">Если вы входите в приложение, на экране **приветствия** должен отобразиться маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="31d45-118">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="31d45-119">Получение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="31d45-119">Get user details</span></span>

<span data-ttu-id="31d45-120">В этом разделе описывается создание настраиваемого поставщика проверки подлинности для клиентской библиотеки Graph, создание вспомогательного класса для хранения всех вызовов Microsoft Graph и обновление `DrawerMenuContent` класса для использования этого нового класса для получения пользователя, вошедшего в систему.</span><span class="sxs-lookup"><span data-stu-id="31d45-120">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `DrawerMenuContent` class to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="31d45-121">Создайте новый каталог в каталоге **графтуториал** с именем **Graph**.</span><span class="sxs-lookup"><span data-stu-id="31d45-121">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="31d45-122">Создайте новый файл в каталоге **графтуториал/Graph** с именем **графауспровидер. TS**.</span><span class="sxs-lookup"><span data-stu-id="31d45-122">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.ts**.</span></span> <span data-ttu-id="31d45-123">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="31d45-123">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. <span data-ttu-id="31d45-124">Создайте новый файл в каталоге **графтуториал/Graph** с именем **графманажер. TS**.</span><span class="sxs-lookup"><span data-stu-id="31d45-124">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.ts**.</span></span> <span data-ttu-id="31d45-125">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="31d45-125">Add the following code to the file.</span></span>

    ```typescript
    import { Client } from '@microsoft/microsoft-graph-client';
    import { GraphAuthProvider } from './GraphAuthProvider';

    // Set the authProvider to an instance
    // of GraphAuthProvider
    const clientOptions = {
      authProvider: new GraphAuthProvider()
    };

    // Initialize the client
    const graphClient = Client.initWithMiddleware(clientOptions);

    export class GraphManager {
      static getUserAsync = async() => {
        // GET /me
        return await graphClient
          .api('/me')
          .select('displayName,givenName,mail,mailboxSettings,userPrincipalName')
          .get();
      }
    }
    ```

1. <span data-ttu-id="31d45-126">Откройте файл **графтуториал/views/дравермену. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="31d45-126">Open the **GraphTutorial/views/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="31d45-127">Замените `componentDidMount` метод на приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="31d45-127">Replace the `componentDidMount` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

<span data-ttu-id="31d45-128">Если вы сохраните изменения и перезагрузили приложение сейчас, после того как вы обновите пользовательский интерфейс, отобразите отображаемое имя и адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="31d45-128">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
