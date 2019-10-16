<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f7d51-101">В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7d51-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="f7d51-102">Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f7d51-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="f7d51-103">Для этого в приложение будет интегрирована библиотека [реагирующих на приложения](https://github.com/FormidableLabs/react-native-app-auth) .</span><span class="sxs-lookup"><span data-stu-id="f7d51-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="f7d51-104">Создайте новый каталог в каталоге **графтуториал** с именем **AUTH**.</span><span class="sxs-lookup"><span data-stu-id="f7d51-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="f7d51-105">Создайте новый файл в каталоге **графтуториал/auth** с именем **AuthConfig. js**.</span><span class="sxs-lookup"><span data-stu-id="f7d51-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.js**.</span></span> <span data-ttu-id="f7d51-106">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f7d51-106">Add the following code to the file.</span></span>

    ```js
    export const AuthConfig = {
      appId = 'YOUR_APP_ID_HERE',
      appScopes = [
        'openid',
        'offline_access',
        'profile',
        'User.Read',
        'Calendars.Read'
      ]
    };
    ```

    <span data-ttu-id="f7d51-107">Замените `YOUR_APP_ID_HERE` идентификатором приложения, указанным в регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="f7d51-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7d51-108">Если вы используете систему управления версиями, например Git, то теперь мы бы не могли исключить файл **AuthConfig. js** из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="f7d51-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="f7d51-109">Реализация входа</span><span class="sxs-lookup"><span data-stu-id="f7d51-109">Implement sign-in</span></span>

<span data-ttu-id="f7d51-110">В этом разделе вы создадите вспомогательный класс проверки подлинности и обновите приложение, чтобы войти в систему и выйти из нее.</span><span class="sxs-lookup"><span data-stu-id="f7d51-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="f7d51-111">Создайте новый файл в каталоге **графтуториал/auth** с именем **аусманажер. js**.</span><span class="sxs-lookup"><span data-stu-id="f7d51-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.js**.</span></span> <span data-ttu-id="f7d51-112">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f7d51-112">Add the following code to the file.</span></span>

    ```js
    import { AuthConfig } from './AuthConfig';
    import { AsyncStorage } from 'react-native';
    import { authorize, refresh } from 'react-native-app-auth';
    import moment from 'moment';

    const config = {
      clientId: AuthConfig.appId,
      redirectUrl: Platform.OS === 'ios' ? 'urn:ietf:wg:oauth:2.0:oob' : 'graph-tutorial://react-native-auth',
      scopes: AuthConfig.appScopes,
      additionalParameters: { prompt: 'select_account' },
      serviceConfiguration: {
        authorizationEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/authorize',
        tokenEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/token',
      }
    };

    export class AuthManager {

      static signInAsync = async () => {
        const result = await authorize(config);

        // Store the access token, refresh token, and expiration time in storage
        await AsyncStorage.setItem('userToken', result.accessToken);
        await AsyncStorage.setItem('refreshToken', result.refreshToken);
        await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);
      }

      static signOutAsync = async () => {
        // Clear storage
        await AsyncStorage.removeItem('userToken');
        await AsyncStorage.removeItem('refreshToken');
        await AsyncStorage.removeItem('expireTime');
      }

      static getAccessTokenAsync = async() => {
        const expireTime = await AsyncStorage.getItem('expireTime');

        if (expireTime !== null) {
          // Get expiration time - 5 minutes
          // If it's <= 5 minutes before expiration, then refresh
          const expire = moment(expireTime).subtract(5, 'minutes');
          const now = moment();

          if (now.isSameOrAfter(expire)) {
            // Expired, refresh
            const refreshToken = await AsyncStorage.getItem('refreshToken');

            const result = await refresh(config, {refreshToken: refreshToken});

            // Store the new access token, refresh token, and expiration time in storage
            await AsyncStorage.setItem('userToken', result.accessToken);
            await AsyncStorage.setItem('refreshToken', result.refreshToken);
            await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);

            return result.accessToken;
          }

          // Not expired, just return saved access token
          const accessToken = await AsyncStorage.getItem('userToken');
          return accessToken;
        }

        return null;
      }
    }
    ```

1. <span data-ttu-id="f7d51-113">Откройте файл **графтуториал/views/сигнинскрин. js** и добавьте приведенный `import` ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="f7d51-113">Open the **GraphTutorial/views/SignInScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f7d51-114">Замените существующий `_signInAsync` метод на приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="f7d51-114">Replace the existing `_signInAsync` method with the following.</span></span>

    ```js
    _signInAsync = async () => {
      try {
        await AuthManager.signInAsync();
        this.props.navigation.navigate('App');
      } catch (error) {
        alert(error);
      }
    };

1. Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f7d51-115">Добавьте приведенный ниже метод в класс `HomeScreen`.</span><span class="sxs-lookup"><span data-stu-id="f7d51-115">Add the following method to the `HomeScreen` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        const accessToken = await AuthManager.getAccessTokenAsync();

        // TEMPORARY
        this.setState({userName: accessToken, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="f7d51-116">Откройте файл **графтуториал/Menus/дравермену. js** и добавьте приведенный `import` ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="f7d51-116">Open the **GraphTutorial/menus/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f7d51-117">В `_onItemPressed` `// TEMPORARY` строке замените строку на приведенную ниже строку.</span><span class="sxs-lookup"><span data-stu-id="f7d51-117">In `_onItemPressed`, replace the `// TEMPORARY` line with the following.</span></span>

    ```js
    await AuthManager.signOutAsync();
    ```

1. <span data-ttu-id="f7d51-118">Сохраните изменения и перезагрузите приложение в симуляторе.</span><span class="sxs-lookup"><span data-stu-id="f7d51-118">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="f7d51-119">Если вы входите в приложение, на экране **приветствия** должен отобразиться маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="f7d51-119">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="f7d51-120">Получение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="f7d51-120">Get user details</span></span>

<span data-ttu-id="f7d51-121">В этом разделе описывается создание настраиваемого поставщика проверки подлинности для клиентской библиотеки Graph, создание вспомогательного класса для хранения всех вызовов Microsoft Graph и обновление классов `HomeScreen` и `DrawerMenuContent` использование этого нового класса для получения пользователя, вошедшего в систему.</span><span class="sxs-lookup"><span data-stu-id="f7d51-121">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="f7d51-122">Создайте новый каталог в каталоге **графтуториал** с именем **Graph**.</span><span class="sxs-lookup"><span data-stu-id="f7d51-122">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="f7d51-123">Создайте новый файл в каталоге **графтуториал/Graph** с именем **графауспровидер. js**.</span><span class="sxs-lookup"><span data-stu-id="f7d51-123">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.js**.</span></span> <span data-ttu-id="f7d51-124">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f7d51-124">Add the following code to the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';

    // Used by Graph client to get access tokens
    // See https://github.com/microsoftgraph/msgraph-sdk-javascript/blob/dev/docs/CustomAuthenticationProvider.md
    export class GraphAuthProvider {
      getAccessToken = async() => {
        return await AuthManager.getAccessTokenAsync();
      }
    }
    ```

1. <span data-ttu-id="f7d51-125">Создайте новый файл в каталоге **графтуториал/Graph** с именем **графманажер. js**.</span><span class="sxs-lookup"><span data-stu-id="f7d51-125">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.js**.</span></span> <span data-ttu-id="f7d51-126">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f7d51-126">Add the following code to the file.</span></span>

    ```js
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
        return graphClient.api('/me').get();
      }
    }
    ```

1. <span data-ttu-id="f7d51-127">Откройте файл **графтуториал/views/хомескрин. js** и добавьте приведенный `import` ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="f7d51-127">Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="f7d51-128">Замените `componentDidMount` метод на приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="f7d51-128">Replace the `componentDidMount` method with the following.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();
        // Set the user name to the user's given name
        this.setState({userName: user.givenName, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="f7d51-129">Откройте файл **графтуториал/views/дравермену. js** и добавьте приведенный `import` ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="f7d51-129">Open the **GraphTutorial/views/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="f7d51-130">Добавьте указанный `DrawerMenuContent` ниже `componentDidMount` метод в класс.</span><span class="sxs-lookup"><span data-stu-id="f7d51-130">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();

        // Update UI with display name and email
        this.setState({
          userName: user.displayName,
          // Work/School accounts have email address in mail attribute
          // Personal accounts have it in userPrincipalName
          userEmail: user.mail !== null ? user.mail : user.userPrincipalName,
        });
      } catch(error) {
        alert(error);
      }
    }
    ```

<span data-ttu-id="f7d51-131">Если вы сохраните изменения и перезагрузили приложение сейчас, после того как вы обновите пользовательский интерфейс, отобразите отображаемое имя и адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="f7d51-131">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
