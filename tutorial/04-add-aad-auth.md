<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD. Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph. Для этого в приложение будет интегрирована библиотека [реагирующих на приложения](https://github.com/FormidableLabs/react-native-app-auth) .

1. Создайте новый каталог в каталоге **графтуториал** с именем **AUTH**.
1. Создайте новый файл в каталоге **графтуториал/auth** с именем **AuthConfig. js**. Добавьте указанный ниже код в файл.

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

    Замените `YOUR_APP_ID_HERE` идентификатором приложения, указанным в регистрации приложения.

> [!IMPORTANT]
> Если вы используете систему управления версиями, например Git, то теперь мы бы не могли исключить файл **AuthConfig. js** из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.

## <a name="implement-sign-in"></a>Реализация входа

В этом разделе вы создадите вспомогательный класс проверки подлинности и обновите приложение, чтобы войти в систему и выйти из нее.

1. Создайте новый файл в каталоге **графтуториал/auth** с именем **аусманажер. js**. Добавьте указанный ниже код в файл.

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

1. Откройте файл **графтуториал/views/сигнинскрин. js** и добавьте приведенный `import` ниже оператор в начало файла.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Замените существующий `_signInAsync` метод на приведенный ниже.

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

1. Добавьте приведенный ниже метод в класс `HomeScreen`.

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

1. Откройте файл **графтуториал/Menus/дравермену. js** и добавьте приведенный `import` ниже оператор в начало файла.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. В `_onItemPressed` `// TEMPORARY` строке замените строку на приведенную ниже строку.

    ```js
    await AuthManager.signOutAsync();
    ```

1. Сохраните изменения и перезагрузите приложение в симуляторе.

Если вы входите в приложение, на экране **приветствия** должен отобразиться маркер доступа.

## <a name="get-user-details"></a>Получение сведений о пользователе

В этом разделе описывается создание настраиваемого поставщика проверки подлинности для клиентской библиотеки Graph, создание вспомогательного класса для хранения всех вызовов Microsoft Graph и обновление классов `HomeScreen` и `DrawerMenuContent` использование этого нового класса для получения пользователя, вошедшего в систему.

1. Создайте новый каталог в каталоге **графтуториал** с именем **Graph**.
1. Создайте новый файл в каталоге **графтуториал/Graph** с именем **графауспровидер. js**. Добавьте указанный ниже код в файл.

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

1. Создайте новый файл в каталоге **графтуториал/Graph** с именем **графманажер. js**. Добавьте указанный ниже код в файл.

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

1. Откройте файл **графтуториал/views/хомескрин. js** и добавьте приведенный `import` ниже оператор в начало файла.

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Замените `componentDidMount` метод на приведенный ниже.

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

1. Откройте файл **графтуториал/views/дравермену. js** и добавьте приведенный `import` ниже оператор в начало файла.

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Добавьте указанный `DrawerMenuContent` ниже `componentDidMount` метод в класс.

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

Если вы сохраните изменения и перезагрузили приложение сейчас, после того как вы обновите пользовательский интерфейс, отобразите отображаемое имя и адрес электронной почты пользователя.
