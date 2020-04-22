<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f0df3-101">Для начала создайте новый реагирующий собственный проект.</span><span class="sxs-lookup"><span data-stu-id="f0df3-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="f0df3-102">Откройте интерфейс командной строки (CLI) в каталоге, в котором нужно создать проект.</span><span class="sxs-lookup"><span data-stu-id="f0df3-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="f0df3-103">Выполните следующую команду, чтобы запустить средство [реагирующих и CLI](https://github.com/facebook/react-native) , и создайте новый реагирующий собственный проект.</span><span class="sxs-lookup"><span data-stu-id="f0df3-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. <span data-ttu-id="f0df3-104">**Необязательно:** Убедитесь, что ваша среда разработки настроена правильно, выполнив проект.</span><span class="sxs-lookup"><span data-stu-id="f0df3-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="f0df3-105">В интерфейсе командной строки смените каталог на только что созданный каталог **графтуториал** и выполните одну из следующих команд.</span><span class="sxs-lookup"><span data-stu-id="f0df3-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="f0df3-106">Для iOS:`npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="f0df3-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="f0df3-107">Для Android: запуск экземпляра эмулятора Android и запуск`npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="f0df3-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="f0df3-108">Установка зависимостей</span><span class="sxs-lookup"><span data-stu-id="f0df3-108">Install dependencies</span></span>

<span data-ttu-id="f0df3-109">Перед перемещением установите некоторые дополнительные зависимости, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="f0df3-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="f0df3-110">[реагирует на навигацию](https://reactnavigation.org) , чтобы обрабатывать навигацию между представлениями в приложении.</span><span class="sxs-lookup"><span data-stu-id="f0df3-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="f0df3-111">[реагирующий на жест — обработчик](https://github.com/kmagiera/react-native-gesture-handler), реагирующий на жесты, [реагирующий на машинный код — контекст](https://github.com/th3rdwave/react-native-safe-area-context), реагирующий на экран, реагирующий на [экран](https://github.com/kmagiera/react-native-screens), [реагирующий на себя переанимация](https://github.com/kmagiera/react-native-reanimated)и [представление с маскированием](https://github.com/react-native-community/react-native-masked-view) , которое необходимо для навигации.</span><span class="sxs-lookup"><span data-stu-id="f0df3-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler), [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context), [react-native-screens](https://github.com/kmagiera/react-native-screens), [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), and [masked-view](https://github.com/react-native-community/react-native-masked-view) required by react-navigation.</span></span>
- <span data-ttu-id="f0df3-112">[реагирующие](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) на себя элементы и [значки с реагирует на векторные изображения](https://github.com/oblador/react-native-vector-icons) , чтобы предоставить значки пользовательскому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="f0df3-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="f0df3-113">[реагирующий на себя — приложение — проверка](https://github.com/FormidableLabs/react-native-app-auth) подлинности для обработки проверки подлинности и управления маркерами.</span><span class="sxs-lookup"><span data-stu-id="f0df3-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="f0df3-114">[асинхронное хранилище](https://github.com/react-native-community/react-native-async-storage) для хранения маркеров.</span><span class="sxs-lookup"><span data-stu-id="f0df3-114">[async-storage](https://github.com/react-native-community/react-native-async-storage) to provide storage for tokens.</span></span>
- <span data-ttu-id="f0df3-115">[время](https://momentjs.com) для обработки синтаксического анализа и сравнения даты и времени.</span><span class="sxs-lookup"><span data-stu-id="f0df3-115">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="f0df3-116">[Microsoft — Graph — клиент](https://github.com/microsoftgraph/msgraph-sdk-javascript) для совершения звонков в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="f0df3-116">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="f0df3-117">Откройте подсистему CLI в корневом каталоге вашего собственного проекта.</span><span class="sxs-lookup"><span data-stu-id="f0df3-117">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="f0df3-118">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f0df3-118">Run the following command.</span></span>

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="f0df3-119">Связывание и Настройка зависимостей для iOS</span><span class="sxs-lookup"><span data-stu-id="f0df3-119">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="f0df3-120">Если вы не нацелены на iOS, вы можете пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="f0df3-120">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="f0df3-121">Откройте подсистему CLI в каталоге **графтуториал/iOS** .</span><span class="sxs-lookup"><span data-stu-id="f0df3-121">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="f0df3-122">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f0df3-122">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="f0df3-123">Откройте файл **графтуториал/iOS/графтуториал/info. plist** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="f0df3-123">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="f0df3-124">Добавьте следующий код непосредственно перед последней `</dict>` строкой в файле.</span><span class="sxs-lookup"><span data-stu-id="f0df3-124">Add the following just before the last `</dict>` line in the file.</span></span>

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

1. <span data-ttu-id="f0df3-125">Откройте файл **графтуториал/iOS/графтуториал/аппделегате. h** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="f0df3-125">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="f0df3-126">Замените его содержимое приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="f0df3-126">Replace its contents with the following.</span></span>

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="f0df3-127">Настройка зависимостей для Android</span><span class="sxs-lookup"><span data-stu-id="f0df3-127">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="f0df3-128">Если вы не нацелены на Android, вы можете пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="f0df3-128">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="f0df3-129">Откройте файл **графтуториал/Android/App/Build. gradle** в редакторе.</span><span class="sxs-lookup"><span data-stu-id="f0df3-129">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="f0df3-130">Нахождение `defaultConfig` записи и добавление следующего свойства в `defaultConfig`файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-130">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="f0df3-131">Эта `defaultConfig` запись должна выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f0df3-131">The `defaultConfig` entry should look similar to the following.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. <span data-ttu-id="f0df3-132">Добавьте указанную ниже строку в конец файла.</span><span class="sxs-lookup"><span data-stu-id="f0df3-132">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="f0df3-133">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-133">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="f0df3-134">Проектирование приложения</span><span class="sxs-lookup"><span data-stu-id="f0df3-134">Design the app</span></span>

<span data-ttu-id="f0df3-135">Приложение будет использовать [входной ящик для навигации](https://reactnavigation.org/docs/drawer-based-navigation.html) по разным представлениям.</span><span class="sxs-lookup"><span data-stu-id="f0df3-135">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="f0df3-136">На этом этапе вы создадите базовые представления, используемые приложением, и реализуйте входной ящик навигации.</span><span class="sxs-lookup"><span data-stu-id="f0df3-136">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="f0df3-137">Создание представлений</span><span class="sxs-lookup"><span data-stu-id="f0df3-137">Create views</span></span>

<span data-ttu-id="f0df3-138">В этом разделе вы создадите представления для приложения, чтобы обеспечить поддержку [процесса проверки подлинности](https://reactnavigation.org/docs/auth-flow).</span><span class="sxs-lookup"><span data-stu-id="f0df3-138">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow).</span></span>

1. <span data-ttu-id="f0df3-139">Откройте **графтуториал/index. js** и добавьте следующий элемент в начало файла перед всеми другими `import` операторами.</span><span class="sxs-lookup"><span data-stu-id="f0df3-139">Open **GraphTutorial/index.js** and add the following to the top of the file, before any other `import` statements.</span></span>

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. <span data-ttu-id="f0df3-140">Создание нового каталога в каталоге **графтуториал** с именем **screens**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-140">Create a new directory in the **GraphTutorial** directory named **screens**.</span></span>
1. <span data-ttu-id="f0df3-141">Создайте новый файл в каталоге **графтуториал/screens** с именем **хомескрин. Целевой**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-141">Create a new file in the **GraphTutorial/screens** directory named **HomeScreen.tsx**.</span></span> <span data-ttu-id="f0df3-142">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-142">Add the following code to the file.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();
    const UserState = React.createContext({userLoading: true, userName: ''});

    type HomeScreenState = {
      userLoading: boolean;
      userName: string;
    }

    const HomeComponent = () => {
      const userState = React.useContext(UserState);

      return (
        <View style={styles.container}>
          <ActivityIndicator animating={userState.userLoading} size='large' />
          {userState.userLoading ? null: <Text>Hello {userState.userName}!</Text>}
        </View>
      );
    }

    export default class HomeScreen extends React.Component {

      state: HomeScreenState = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <UserState.Provider value={this.state}>
              <Stack.Navigator screenOptions={headerOptions}>
                <Stack.Screen name='Home'
                  component={HomeComponent}
                  options={{
                    title: 'Welcome',
                    headerLeft: () => <DrawerToggle/>
                  }} />
              </Stack.Navigator>
          </UserState.Provider>
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

1. <span data-ttu-id="f0df3-143">Создайте новый файл в каталоге **графтуториал/screens** с именем **календарскрин. Целевой**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-143">Create a new file in the **GraphTutorial/screens** directory named **CalendarScreen.tsx**.</span></span> <span data-ttu-id="f0df3-144">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-144">Add the following code to the file.</span></span>

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();

    // Temporary placeholder view
    const CalendarComponent = () => (
      <View style={styles.container}>
        <Text>Calendar</Text>
      </View>
    );

    export default class CalendarScreen extends React.Component {

      render() {
        return (
          <Stack.Navigator screenOptions={ headerOptions }>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                title: 'Calendar',
                headerLeft: () => <DrawerToggle/>
              }} />
          </Stack.Navigator>
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

1. <span data-ttu-id="f0df3-145">Создайте новый файл в каталоге **графтуториал/screens** с именем **сигнинскрин. Целевой**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-145">Create a new file in the **GraphTutorial/screens** directory named **SignInScreen.tsx**.</span></span> <span data-ttu-id="f0df3-146">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-146">Add the following code to the file.</span></span>

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { NavigationContext } from '@react-navigation/native';

    export default class SignInScreen extends React.Component {
      static contextType = NavigationContext;

      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        const navigation = this.context;

        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [ { name: 'Main' } ]
        });
      };

      render() {
        const navigation = this.context;
        navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });

        return (
          <View style={styles.container}>
            <Button title='Sign In' onPress={this._signInAsync}/>
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

1. <span data-ttu-id="f0df3-147">Создайте новый файл в каталоге **графтуториал/screens** с именем **ауслоадингскрин. Целевой**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-147">Create a new file in the **GraphTutorial/screens** directory named **AuthLoadingScreen.tsx**.</span></span> <span data-ttu-id="f0df3-148">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-148">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="f0df3-149">Создание ящика навигации</span><span class="sxs-lookup"><span data-stu-id="f0df3-149">Create a navigation drawer</span></span>

<span data-ttu-id="f0df3-150">В этом разделе вы создадите меню для приложения и обновите приложение, чтобы использовать навигацию для перемещения между экранами.</span><span class="sxs-lookup"><span data-stu-id="f0df3-150">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="f0df3-151">Создайте новый каталог в каталоге **графтуториал** с именем **Menus**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-151">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="f0df3-152">Создайте новый файл в каталоге **графтуториал/Menus** с именем **хеадеркомпонентс. Целевой**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-152">Create a new file in the **GraphTutorial/menus** directory named **HeaderComponents.tsx**.</span></span> <span data-ttu-id="f0df3-153">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-153">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. <span data-ttu-id="f0df3-154">Создайте новый файл в каталоге **графтуториал/Menus** с именем **дравермену. Целевой**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-154">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.tsx**.</span></span> <span data-ttu-id="f0df3-155">Добавьте указанный ниже код в файл.</span><span class="sxs-lookup"><span data-stu-id="f0df3-155">Add the following code to the file.</span></span>

    ```typescript
    import React, { FC } from 'react';
    import {
      Alert,
      Image,
      StyleSheet,
      Text,
      View,
      ImageSourcePropType
    } from 'react-native';
    import {
      createDrawerNavigator,
      DrawerContentScrollView,
      DrawerItem,
      DrawerItemList,
      DrawerContentComponentProps
    } from '@react-navigation/drawer';
    import { NavigationContext } from '@react-navigation/native';

    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuState = {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
    }

    const CustomDrawerContent: FC<CustomDrawerContentProps> = props => (
      <DrawerContentScrollView {...props}>
          <View style={styles.profileView}>
            <Image source={props.userPhoto}
              resizeMode='contain'
              style={styles.profilePhoto} />
            <Text style={styles.profileUserName}>{props.userName}</Text>
            <Text style={styles.profileEmail}>{props.userEmail}</Text>
          </View>
          <DrawerItemList {...props} />
          <DrawerItem label='Sign Out' onPress={props.signOut}/>
      </DrawerContentScrollView>
    );

    export default class DrawerMenuContent extends React.Component {
      static contextType = NavigationContext;

      state: DrawerMenuState = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        const navigation = this.context;
        // Sign out
        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [{ name: 'SignIn' }]
        });
      }

      render() {
        const navigation = this.context;
        navigation.setOptions({
          headerShown: false,
        });

        return (
          <Drawer.Navigator
            drawerType='front'
            drawerContent={props => (
              <CustomDrawerContent {...props}
                userName={this.state.userName}
                userEmail={this.state.userEmail}
                userPhoto={this.state.userPhoto}
                signOut={this._signOut} />
            )}>
            <Drawer.Screen name='Home'
              component={HomeScreen}
              options={{drawerLabel: 'Home'}} />
            <Drawer.Screen name='Calendar'
              component={CalendarScreen}
              options={{drawerLabel: 'Calendar'}} />
          </Drawer.Navigator>
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

1. <span data-ttu-id="f0df3-156">Создайте новый каталог в каталоге **графтуториал** с именем **Images**.</span><span class="sxs-lookup"><span data-stu-id="f0df3-156">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="f0df3-157">Добавьте в этот каталог изображение профиля по умолчанию с именем **но-профиле-пик. png** .</span><span class="sxs-lookup"><span data-stu-id="f0df3-157">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="f0df3-158">Вы можете использовать любое изображение, которое вам нравится, или использовать [его из этого примера](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span><span class="sxs-lookup"><span data-stu-id="f0df3-158">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="f0df3-159">Откройте файл **графтуториал/App. Целевой сервера** и замените все содержимое приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="f0df3-159">Open the **GraphTutorial/App.tsx** file and replace the entire contents with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. <span data-ttu-id="f0df3-160">Сохраните все изменения.</span><span class="sxs-lookup"><span data-stu-id="f0df3-160">Save all of your changes.</span></span>

1. <span data-ttu-id="f0df3-161">Перезагрузите приложение в симуляторе.</span><span class="sxs-lookup"><span data-stu-id="f0df3-161">Reload the application in your emulator.</span></span>

<span data-ttu-id="f0df3-162">Меню приложения должно работать для перехода между двумя фрагментами и изменения при касании кнопок **входа** **и выхода.**</span><span class="sxs-lookup"><span data-stu-id="f0df3-162">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Снимки экрана приложения на Android](./images/android-app-screens.png)

![Снимки экрана приложения на iOS](./images/ios-app-screens.png)
