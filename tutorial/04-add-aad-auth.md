<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD. Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph. Для этого в приложение будет интегрирована библиотека [реагирующих на приложения](https://github.com/FormidableLabs/react-native-app-auth) .

1. Создайте новый каталог в каталоге **графтуториал** с именем **AUTH**.
1. Создайте новый файл в каталоге **графтуториал/auth** с именем **AuthConfig. TS**. Добавьте указанный ниже код в файл.

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    Замените `YOUR_APP_ID_HERE` идентификатором приложения, указанным в регистрации приложения.

> [!IMPORTANT]
> Если вы используете систему управления версиями (например, Git), то теперь будет полезно исключить файл **AuthConfig. TS** из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.

## <a name="implement-sign-in"></a>Реализация входа

В этом разделе вы создадите вспомогательный класс проверки подлинности и обновите приложение, чтобы войти в систему и выйти из нее.

1. Создайте новый файл в каталоге **графтуториал/auth** с именем **аусманажер. TS**. Добавьте указанный ниже код в файл.

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. Откройте **графтуториал/App. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. Замените существующее `authContext` объявление следующим.

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. Откройте файл **графтуториал/Menus/дравермену. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Добавьте следующий код в `componentDidMount` функцию.

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

1. Сохраните изменения и перезагрузите приложение в симуляторе.

Если вы входите в приложение, на экране **приветствия** должен отобразиться маркер доступа.

## <a name="get-user-details"></a>Получение сведений о пользователе

В этом разделе описывается создание настраиваемого поставщика проверки подлинности для клиентской библиотеки Graph, создание вспомогательного класса для хранения всех вызовов Microsoft Graph и обновление `DrawerMenuContent` класса для использования этого нового класса для получения пользователя, вошедшего в систему.

1. Создайте новый каталог в каталоге **графтуториал** с именем **Graph**.
1. Создайте новый файл в каталоге **графтуториал/Graph** с именем **графауспровидер. TS**. Добавьте указанный ниже код в файл.

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. Создайте новый файл в каталоге **графтуториал/Graph** с именем **графманажер. TS**. Добавьте указанный ниже код в файл.

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

1. Откройте файл **графтуториал/views/дравермену. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Замените `componentDidMount` метод на приведенный ниже.

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

Если вы сохраните изменения и перезагрузили приложение сейчас, после того как вы обновите пользовательский интерфейс, отобразите отображаемое имя и адрес электронной почты пользователя.
