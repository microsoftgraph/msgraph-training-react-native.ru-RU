<!-- markdownlint-disable MD002 MD041 -->

Для начала создайте новый реагирующий собственный проект.

1. Откройте интерфейс командной строки (CLI) в каталоге, в котором нужно создать проект. Выполните следующую команду, чтобы запустить средство [реагирующих и CLI](https://github.com/facebook/react-native) , и создайте новый реагирующий собственный проект.

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **Необязательно:** Убедитесь, что ваша среда разработки настроена правильно, выполнив проект. В интерфейсе командной строки смените каталог на только что созданный каталог **графтуториал** и выполните одну из следующих команд.

    - Для iOS:`npx react-native run-ios`
    - Для Android: запуск экземпляра эмулятора Android и запуск`npx react-native run-android`

## <a name="install-dependencies"></a>Установка зависимостей

Перед перемещением установите некоторые дополнительные зависимости, которые будут использоваться позже.

- [реагирует на навигацию](https://reactnavigation.org) , чтобы обрабатывать навигацию между представлениями в приложении.
- [реагирующий на жест — обработчик](https://github.com/kmagiera/react-native-gesture-handler), реагирующий на жесты, [реагирующий на машинный код — контекст](https://github.com/th3rdwave/react-native-safe-area-context), реагирующий на экран, реагирующий на [экран](https://github.com/kmagiera/react-native-screens), [реагирующий на себя переанимация](https://github.com/kmagiera/react-native-reanimated)и [представление с маскированием](https://github.com/react-native-community/react-native-masked-view) , которое необходимо для навигации.
- [реагирующие](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) на себя элементы и [значки с реагирует на векторные изображения](https://github.com/oblador/react-native-vector-icons) , чтобы предоставить значки пользовательскому интерфейсу.
- [реагирующий на себя — приложение — проверка](https://github.com/FormidableLabs/react-native-app-auth) подлинности для обработки проверки подлинности и управления маркерами.
- [асинхронное хранилище](https://github.com/react-native-community/react-native-async-storage) для хранения маркеров.
- [время](https://momentjs.com) для обработки синтаксического анализа и сравнения даты и времени.
- [Microsoft — Graph — клиент](https://github.com/microsoftgraph/msgraph-sdk-javascript) для совершения звонков в Microsoft Graph.

1. Откройте подсистему CLI в корневом каталоге вашего собственного проекта.
1. Выполните следующую команду.

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
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

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

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

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. Добавьте указанную ниже строку в конец файла.

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. Сохраните файл.

## <a name="design-the-app"></a>Проектирование приложения

Приложение будет использовать [входной ящик для навигации](https://reactnavigation.org/docs/drawer-based-navigation.html) по разным представлениям. На этом этапе вы создадите базовые представления, используемые приложением, и реализуйте входной ящик навигации.

### <a name="create-views"></a>Создание представлений

В этом разделе вы создадите представления для приложения, чтобы обеспечить поддержку [процесса проверки подлинности](https://reactnavigation.org/docs/auth-flow).

1. Откройте **графтуториал/index. js** и добавьте следующий элемент в начало файла перед всеми другими `import` операторами.

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. Создание нового каталога в каталоге **графтуториал** с именем **screens**.
1. Создайте новый файл в каталоге **графтуториал/screens** с именем **хомескрин. Целевой**. Добавьте указанный ниже код в файл.

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

1. Создайте новый файл в каталоге **графтуториал/screens** с именем **календарскрин. Целевой**. Добавьте указанный ниже код в файл.

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

1. Создайте новый файл в каталоге **графтуториал/screens** с именем **сигнинскрин. Целевой**. Добавьте указанный ниже код в файл.

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

1. Создайте новый файл в каталоге **графтуториал/screens** с именем **ауслоадингскрин. Целевой**. Добавьте указанный ниже код в файл.

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a>Создание ящика навигации

В этом разделе вы создадите меню для приложения и обновите приложение, чтобы использовать навигацию для перемещения между экранами.

1. Создайте новый каталог в каталоге **графтуториал** с именем **Menus**.
1. Создайте новый файл в каталоге **графтуториал/Menus** с именем **хеадеркомпонентс. Целевой**. Добавьте указанный ниже код в файл.

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. Создайте новый файл в каталоге **графтуториал/Menus** с именем **дравермену. Целевой**. Добавьте указанный ниже код в файл.

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

1. Создайте новый каталог в каталоге **графтуториал** с именем **Images**.
1. Добавьте в этот каталог изображение профиля по умолчанию с именем **но-профиле-пик. png** . Вы можете использовать любое изображение, которое вам нравится, или использовать [его из этого примера](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).

1. Откройте файл **графтуториал/App. Целевой сервера** и замените все содержимое приведенным ниже.

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. Сохраните все изменения.

1. Перезагрузите приложение в симуляторе.

Меню приложения должно работать для перехода между двумя фрагментами и изменения при касании кнопок **входа** **и выхода.**

![Снимки экрана приложения на Android](./images/android-app-screens.png)

![Снимки экрана приложения на iOS](./images/ios-app-screens.png)
