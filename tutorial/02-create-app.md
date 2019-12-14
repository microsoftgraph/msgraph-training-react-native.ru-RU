<!-- markdownlint-disable MD002 MD041 -->

Для начала создайте новый реагирующий собственный проект.

1. Откройте интерфейс командной строки (CLI) в каталоге, в котором нужно создать проект. Выполните следующую команду, чтобы запустить средство [реагирующих и CLI](https://github.com/facebook/react-native) , и создайте новый реагирующий собственный проект.

    ```Shell
    npx react-native init GraphTutorial
    ```

1. **Необязательно:** Убедитесь, что ваша среда разработки настроена правильно, выполнив проект. В интерфейсе командной строки смените каталог на только что созданный каталог **графтуториал** и выполните одну из следующих команд.

    - Для iOS:`npx react-native run-ios`
    - Для Android: запуск экземпляра эмулятора Android и запуск`npx react-native run-android`

## <a name="install-dependencies"></a>Установка зависимостей

Перед перемещением установите некоторые дополнительные зависимости, которые будут использоваться позже.

- [реагирует на навигацию](https://reactnavigation.org) , чтобы обрабатывать навигацию между представлениями в приложении.
- [реагирующий](https://github.com/kmagiera/react-native-gesture-handler) на себя — обработчик жестов и [реагирующий на себя переанимация](https://github.com/kmagiera/react-native-reanimated), необходимый для реакции на навигацию.
- [реагирующие](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) на себя элементы и [значки с реагирует на векторные изображения](https://github.com/oblador/react-native-vector-icons) , чтобы предоставить значки пользовательскому интерфейсу.
- [реагирующий на себя — приложение — проверка](https://github.com/FormidableLabs/react-native-app-auth) подлинности для обработки проверки подлинности и управления маркерами.
- [время](https://momentjs.com) для обработки синтаксического анализа и сравнения даты и времени.
- [Microsoft — Graph — клиент](https://github.com/microsoftgraph/msgraph-sdk-javascript) для совершения звонков в Microsoft Graph.

1. Откройте подсистему CLI в корневом каталоге вашего собственного проекта.
1. Выполните следующую команду.

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.5.2 react-native-reanimated@1.4.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>Связывание и Настройка зависимостей для iOS

> [!NOTE]
> Если вы не нацелены на iOS, вы можете пропустить этот раздел.

1. Откройте подсистему CLI в каталоге **графтуториал/iOS** .
1. Выполните следующую команду.

    ```Shell
    pod install
    ```

1. Откройте файл **графтуториал/iOS/графтуториал/info. plist** в текстовом редакторе. Добавьте следующий код непосредственно перед последней `</dict>` строкой в файле.

    ```xml
    <key>UIAppFonts</key>
    <array>
      <string>AntDesign.ttf</string>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>Feather.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>FontAwesome5_Brands.ttf</string>
      <string>FontAwesome5_Regular.ttf</string>
      <string>FontAwesome5_Solid.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>Zocial.ttf</string>
    </array>
    ```

1. Откройте файл **графтуториал/iOS/графтуториал/аппделегате. h** в текстовом редакторе. Замените его содержимое приведенным ниже.

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a>Настройка зависимостей для Android

> [!NOTE]
> Если вы не нацелены на Android, вы можете пропустить этот раздел.

1. Откройте файл **графтуториал/Android/App/Build. gradle** в редакторе.
1. Нахождение `defaultConfig` записи и добавление следующего свойства в `defaultConfig`файл.

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    Эта `defaultConfig` запись должна выглядеть примерно так, как показано ниже.

    ```Gradle
    defaultConfig {
        applicationId "com.graphtutorial"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode 1
        versionName "1.0"
        manifestPlaceholders = [
            appAuthRedirectScheme: 'graphtutorial'
        ]
    }
    ```

1. Добавьте указанную ниже строку в конец файла.

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. Сохраните файл.

## <a name="design-the-app"></a>Проектирование приложения

Приложение будет использовать [входной ящик для навигации](https://reactnavigation.org/docs/drawer-based-navigation.html) по разным представлениям. На этом этапе вы создадите базовые представления, используемые приложением, и реализуйте входной ящик навигации.

### <a name="create-views"></a>Создание представлений

В этом разделе вы создадите представления для приложения, чтобы обеспечить поддержку [процесса проверки подлинности](https://reactnavigation.org/docs/auth-flow.html).

1. Создайте новый каталог в каталоге **графтуториал** с именем **views**.
1. Создайте новый файл в каталоге **графтуториал/views** с именем **хомескрин. js**. Добавьте указанный ниже код в файл.

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class HomeScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Welcome',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator animating={this.state.userLoading} size='large' />
            {this.state.userLoading ? null: <Text>Hello {this.state.userName}!</Text>}
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. Создайте новый файл в каталоге **графтуториал/views** с именем **календарскрин. js**. Добавьте указанный ниже код в файл.

    ```JSX
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      // Temporary placeholder view
      render() {
        return (
          <View style={styles.container}>
            <Text>Calendar</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. Создайте новый файл в каталоге **графтуториал/views** с именем **сигнинскрин. js**. Добавьте указанный ниже код в файл.

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      Button,
      StyleSheet,
      View,
    } from 'react-native';

    export default class SignInScreen extends React.Component {
      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        // TEMPORARY
        this.props.navigation.navigate('App');
      };

      render() {
        return (
          <View style={styles.container}>
            <Button title="Sign In" onPress={this._signInAsync}/>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. Создайте новый файл в каталоге **графтуториал/views** с именем **ауслоадингскрин. js**. Добавьте указанный ниже код в файл.

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      ActivityIndicator,
      AsyncStorage,
      Text,
      StyleSheet,
      View,
    } from 'react-native';

    export default class AuthLoadingScreen extends React.Component {

      componentDidMount() {
        this._bootstrapAsync();
      }

      // Fetch the token from storage then navigate to our appropriate place
      // NOTE: Production apps should protect user tokens in secure storage.
      _bootstrapAsync = async () => {
        const userToken = await AsyncStorage.getItem('userToken');

        // This will switch to the App screen or Auth screen and this loading
        // screen will be unmounted and thrown away.
        this.props.navigation.navigate(userToken ? 'App' : 'Auth');
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator size='large' />
            <Text style={styles.statusText}>Logging in...</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      },
      statusText: {
        marginTop: 10
      }
    });
    ```

### <a name="create-a-navigation-drawer"></a>Создание ящика навигации

В этом разделе вы создадите меню для приложения и обновите приложение, чтобы использовать навигацию для перемещения между экранами.

1. Создайте новый каталог в каталоге **графтуториал** с именем **Menus**.
1. Создайте новый файл в каталоге **графтуториал/Menus** с именем **дравермену. js**. Добавьте указанный ниже код в файл.

    ```JSX
    import React from 'react';
    import {
      Image,
      SafeAreaView,
      ScrollView,
      StyleSheet,
      Text,
      View
    } from 'react-native';
    import { DrawerItems } from 'react-navigation';

    export default class DrawerMenuContent extends React.Component {

      state = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      // Check if user tapped on the Sign Out button and
      // sign the user out
      _onItemPressed = async (route) => {
        if (route.route.routeName !== 'Sign Out') {
          this.props.onItemPress(route);
          return;
        }

        // Sign out
        // TEMPORARY
        this.props.navigation.navigate('Auth');
      }

      render() {
        return (
          <ScrollView>
            <SafeAreaView style={styles.container}
              forceInset={{ top: 'always', horizontal: 'never' }}>
              <View style={styles.profileView}>
                <Image source={this.state.userPhoto}
                  resizeMode='contain'
                  style={styles.profilePhoto} />
                <Text style={styles.profileUserName}>{this.state.userName}</Text>
                <Text style={styles.profileEmail}>{this.state.userEmail}</Text>
              </View>
              <DrawerItems {...this.props}
                onItemPress={this._onItemPressed}/>
            </SafeAreaView>
          </ScrollView>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      profileView: {
        alignItems: 'center',
        padding: 10
      },
      profilePhoto: {
        width: 80,
        height: 80,
        borderRadius: 40
      },
      profileUserName: {
        fontWeight: '700'
      },
      profileEmail: {
        fontWeight: '200',
        fontSize: 10
      }
    });
    ```

1. Создайте новый каталог в каталоге **графтуториал** с именем **Images**.
1. Добавьте в этот каталог изображение профиля по умолчанию с именем **но-профиле-пик. png** . Вы можете использовать любое изображение, которое вам нравится, или использовать [его из этого примера](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demos/01-create-app/GraphTutorial/images/no-profile-pic.png).

1. Откройте файл **графтуториал/App. js** и замените все содержимое приведенным ниже фрагментом.

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import {
      createSwitchNavigator,
      createStackNavigator,
      createDrawerNavigator,
      createAppContainer } from "react-navigation";

    import AuthLoadingScreen from './views/AuthLoadingScreen';
    import SignInScreen from './views/SignInScreen';
    import HomeScreen from './views/HomeScreen';
    import CalendarScreen from './views/CalendarScreen';
    import DrawerMenuContent from './menus/DrawerMenu';

    const headerOptions = {
      defaultNavigationOptions: {
        headerStyle: {
          backgroundColor: '#276b80'
        },
        headerTintColor: 'white'
      }
    };

    const AuthStack = createStackNavigator(
      {
        SignIn: SignInScreen
      },
      headerOptions
    );

    const AppDrawer = createDrawerNavigator(
      {
        Home: createStackNavigator({ Home: HomeScreen }, headerOptions),
        Calendar: createStackNavigator({ Calendar: CalendarScreen }, headerOptions),
        'Sign Out': 'SignOut'
      },
      {
        hideStatusBar: false,
        contentComponent: DrawerMenuContent
      }
    );

    export default createAppContainer(createSwitchNavigator(
      {
        AuthLoading: AuthLoadingScreen,
        App: AppDrawer,
        Auth: AuthStack
      },
      {
        initialRouteName: 'AuthLoading'
      }
    ));
    ```

1. Сохраните все изменения.

1. Перезагрузите приложение в симуляторе.

Меню приложения должно работать для перехода между двумя фрагментами и изменения при касании кнопок **входа** **и выхода.**

![Снимки экрана приложения на Android](./images/android-app-screens.png)

![Снимки экрана приложения на iOS](./images/ios-app-screens.png)

> [!NOTE]
> При запуске приложения, посвященного асинхронному хранилищу или Компонентвиллупдате, могут возникать предупреждения. В рамках данного руководства вы можете отклонить эти предупреждения.
