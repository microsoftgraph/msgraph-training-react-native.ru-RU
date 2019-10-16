<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="02488-101">Для начала создайте новый реагирующий собственный проект.</span><span class="sxs-lookup"><span data-stu-id="02488-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="02488-102">Откройте интерфейс командной строки (CLI) в каталоге, в котором нужно создать проект.</span><span class="sxs-lookup"><span data-stu-id="02488-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="02488-103">Выполните приведенную ниже команду, чтобы установить средство " [реагирующие и CLI](https://github.com/facebook/react-native) ", а затем создайте новый реагирующий собственный проект.</span><span class="sxs-lookup"><span data-stu-id="02488-103">Run the following command to install the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npm install -g react-native-cli
    react-native init GraphTutorial
    ```

1. <span data-ttu-id="02488-104">**Необязательно:** Убедитесь, что ваша среда разработки настроена правильно, выполнив проект.</span><span class="sxs-lookup"><span data-stu-id="02488-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="02488-105">В интерфейсе командной строки смените каталог на только что созданный каталог **графтуториал** и выполните одну из следующих команд.</span><span class="sxs-lookup"><span data-stu-id="02488-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="02488-106">Для iOS:`react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="02488-106">For iOS: `react-native run-ios`</span></span>
    - <span data-ttu-id="02488-107">Для Android: запуск экземпляра эмулятора Android и запуск`react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="02488-107">For Android: Launch an Android emulator instance and run `react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="02488-108">Установка зависимостей</span><span class="sxs-lookup"><span data-stu-id="02488-108">Install dependencies</span></span>

<span data-ttu-id="02488-109">Перед перемещением установите некоторые дополнительные зависимости, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="02488-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="02488-110">[реагирует на навигацию](https://reactnavigation.org) , чтобы обрабатывать навигацию между представлениями в приложении.</span><span class="sxs-lookup"><span data-stu-id="02488-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="02488-111">[реагирующий](https://github.com/kmagiera/react-native-gesture-handler) на себя — обработчик жестов и [реагирующий на себя переанимация](https://github.com/kmagiera/react-native-reanimated), необходимый для реакции на навигацию.</span><span class="sxs-lookup"><span data-stu-id="02488-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler) and [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), required by react-navigation.</span></span>
- <span data-ttu-id="02488-112">[реагирующие](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) на себя элементы и [значки с реагирует на векторные изображения](https://github.com/oblador/react-native-vector-icons) , чтобы предоставить значки пользовательскому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="02488-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="02488-113">[реагирующий на себя — приложение — проверка](https://github.com/FormidableLabs/react-native-app-auth) подлинности для обработки проверки подлинности и управления маркерами.</span><span class="sxs-lookup"><span data-stu-id="02488-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="02488-114">[время](https://momentjs.com) для обработки синтаксического анализа и сравнения даты и времени.</span><span class="sxs-lookup"><span data-stu-id="02488-114">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="02488-115">[Microsoft — Graph — клиент](https://github.com/microsoftgraph/msgraph-sdk-javascript) для совершения звонков в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="02488-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="02488-116">Откройте подсистему CLI в корневом каталоге вашего собственного проекта.</span><span class="sxs-lookup"><span data-stu-id="02488-116">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="02488-117">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="02488-117">Run the following command.</span></span>

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.3.0 react-native-reanimated@1.1.0
    npm install react-native-elements@1.1.0 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@1.7.0
    react-native link react-native-vector-icons
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="02488-118">Связывание и Настройка зависимостей для iOS</span><span class="sxs-lookup"><span data-stu-id="02488-118">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="02488-119">Если вы не нацелены на iOS, вы можете пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="02488-119">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="02488-120">Откройте подсистему CLI в каталоге **графтуториал/iOS** .</span><span class="sxs-lookup"><span data-stu-id="02488-120">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="02488-121">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="02488-121">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="02488-122">Откройте файл **графтуториал/iOS/графтуториал/аппделегате. h** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="02488-122">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="02488-123">Замените его содержимое приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="02488-123">Replace its contents with the following.</span></span>

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="02488-124">Настройка зависимостей для Android</span><span class="sxs-lookup"><span data-stu-id="02488-124">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="02488-125">Если вы не нацелены на Android, вы можете пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="02488-125">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="02488-126">Откройте файл **графтуториал/Android/App/Build. gradle** в редакторе.</span><span class="sxs-lookup"><span data-stu-id="02488-126">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="02488-127">Нахождение `defaultConfig` записи и добавление следующего свойства в `defaultConfig`файл.</span><span class="sxs-lookup"><span data-stu-id="02488-127">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

1. <span data-ttu-id="02488-128">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="02488-128">Save the file.</span></span> <span data-ttu-id="02488-129">Эта `defaultConfig` запись должна выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="02488-129">The `defaultConfig` entry should look similar to the following.</span></span>

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

## <a name="design-the-app"></a><span data-ttu-id="02488-130">Проектирование приложения</span><span class="sxs-lookup"><span data-stu-id="02488-130">Design the app</span></span>

<span data-ttu-id="02488-131">Приложение будет использовать [входной ящик для навигации](https://reactnavigation.org/docs/drawer-based-navigation.html) по разным представлениям.</span><span class="sxs-lookup"><span data-stu-id="02488-131">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="02488-132">На этом этапе вы создадите базовые представления, используемые приложением, и реализуйте входной ящик навигации.</span><span class="sxs-lookup"><span data-stu-id="02488-132">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="02488-133">Создание представлений</span><span class="sxs-lookup"><span data-stu-id="02488-133">Create views</span></span>

<span data-ttu-id="02488-134">В этом разделе вы создадите представления для приложения, чтобы обеспечить поддержку [процесса проверки подлинности](https://reactnavigation.org/docs/auth-flow.html).</span><span class="sxs-lookup"><span data-stu-id="02488-134">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow.html).</span></span>

1. <span data-ttu-id="02488-135">Создайте новый каталог в каталоге **графтуториал** с именем **views**.</span><span class="sxs-lookup"><span data-stu-id="02488-135">Create a new directory in the **GraphTutorial** directory named **views**.</span></span>
1. <span data-ttu-id="02488-136">Создайте новый файл в каталоге **графтуториал/views** с именем **хомескрин. js**.</span><span class="sxs-lookup"><span data-stu-id="02488-136">Create a new file in the **GraphTutorial/views** directory named **HomeScreen.js**.</span></span> <span data-ttu-id="02488-137">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="02488-137">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02488-138">Создайте новый файл в каталоге **графтуториал/views** с именем **календарскрин. js**.</span><span class="sxs-lookup"><span data-stu-id="02488-138">Create a new file in the **GraphTutorial/views** directory named **CalendarScreen.js**.</span></span> <span data-ttu-id="02488-139">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="02488-139">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02488-140">Создайте новый файл в каталоге **графтуториал/views** с именем **сигнинскрин. js**.</span><span class="sxs-lookup"><span data-stu-id="02488-140">Create a new file in the **GraphTutorial/views** directory named **SignInScreen.js**.</span></span> <span data-ttu-id="02488-141">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="02488-141">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02488-142">Создайте новый файл в каталоге **графтуториал/views** с именем **ауслоадингскрин. js**.</span><span class="sxs-lookup"><span data-stu-id="02488-142">Create a new file in the **GraphTutorial/views** directory named **AuthLoadingScreen.js**.</span></span> <span data-ttu-id="02488-143">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="02488-143">Add the following code to the file.</span></span>

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

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="02488-144">Создание ящика навигации</span><span class="sxs-lookup"><span data-stu-id="02488-144">Create a navigation drawer</span></span>

<span data-ttu-id="02488-145">В этом разделе вы создадите меню для приложения и обновите приложение, чтобы использовать навигацию для перемещения между экранами.</span><span class="sxs-lookup"><span data-stu-id="02488-145">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="02488-146">Создайте новый каталог в каталоге **графтуториал** с именем **Menus**.</span><span class="sxs-lookup"><span data-stu-id="02488-146">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="02488-147">Создайте новый файл в каталоге **графтуториал/Menus** с именем **дравермену. js**.</span><span class="sxs-lookup"><span data-stu-id="02488-147">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.js**.</span></span> <span data-ttu-id="02488-148">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="02488-148">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02488-149">Откройте файл **графтуториал/App. js** и замените все содержимое приведенным ниже фрагментом.</span><span class="sxs-lookup"><span data-stu-id="02488-149">Open the **GraphTutorial/App.js** file and replace the entire contents with the following.</span></span>

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

1. Save all of your changes.

1. Reload the application in your emulator.

The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.

![Screenshots of the application on Android](./images/android-app-screens.png)

![Screenshots of the application on iOS](./images/ios-app-screens.png)

> [!NOTE]
> You may receive warnings when running the app about Async Storage or componentWillUpdate. For the purposes of this tutorial, you can dismiss those warnings.
