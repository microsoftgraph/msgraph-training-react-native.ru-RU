<!-- markdownlint-disable MD002 MD041 -->

Для начала создайте новый реагирующий собственный проект.

1. Откройте интерфейс командной строки (CLI) в каталоге, в котором нужно создать проект. Выполните следующую команду, чтобы запустить средство [реагирующих и CLI](https://github.com/facebook/react-native) , и создайте новый реагирующий собственный проект.

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **Необязательно:** Убедитесь, что ваша среда разработки настроена правильно, выполнив проект. В интерфейсе командной строки смените каталог на только что созданный каталог **графтуториал** и выполните одну из следующих команд.

    - Для iOS: `npx react-native run-ios`
    - Для Android: запуск экземпляра эмулятора Android и запуск `npx react-native run-android`

## <a name="install-dependencies"></a>Установка зависимостей

Перед перемещением установите некоторые дополнительные зависимости, которые будут использоваться позже.

- [реагирует на навигацию](https://reactnavigation.org) , чтобы обрабатывать навигацию между представлениями в приложении.
- [реагирующий на жест — обработчик](https://github.com/kmagiera/react-native-gesture-handler), реагирующий на жесты, [реагирующий на машинный код — контекст](https://github.com/th3rdwave/react-native-safe-area-context), реагирующий на экран, реагирующий на [экран](https://github.com/kmagiera/react-native-screens), [реагирующий на себя переанимация](https://github.com/kmagiera/react-native-reanimated)и [представление с маскированием](https://github.com/react-native-community/react-native-masked-view) , которое необходимо для навигации.
- [реагирующие](https://reactnativeelements.com/docs/) на себя элементы и [значки с реагирует на векторные изображения](https://github.com/oblador/react-native-vector-icons) , чтобы предоставить значки пользовательскому интерфейсу.
- [реагирующий на себя — приложение — проверка](https://github.com/FormidableLabs/react-native-app-auth) подлинности для обработки проверки подлинности и управления маркерами.
- [асинхронное хранилище](https://react-native-async-storage.github.io/async-storage/docs/install) для хранения маркеров.
- [DateTimePicker](https://github.com/react-native-datetimepicker/datetimepicker) для добавления в пользовательский интерфейс выбора даты и времени.
- [время](https://momentjs.com) для обработки синтаксического анализа и сравнения даты и времени.
- [Windows — IANA](https://github.com/rubenillodo/windows-iana) для перевода часовых поясов Windows в формат IANA.
- [Microsoft — Graph — клиент](https://github.com/microsoftgraph/msgraph-sdk-javascript) для совершения звонков в Microsoft Graph.

1. Откройте подсистему CLI в корневом каталоге вашего собственного проекта.
1. Выполните следующую команду.

    ```Shell
    npm install @react-navigation/native@5.8.8 @react-navigation/drawer@5.11.1 @react-navigation/stack@5.12.5
    npm install @react-native-community/masked-view@0.1.10 react-native-safe-area-context@3.1.8 windows-iana
    npm install react-native-reanimated@1.13.1 react-native-screens@2.14.0 @react-native-async-storage/async-storage@1.13.2
    npm install react-native-elements@2.3.2 react-native-vector-icons@7.1.0 react-native-gesture-handler@1.8.0
    npm install react-native-app-auth@6.0.1 moment@2.29.1 moment-timezone @microsoft/microsoft-graph-client@2.1.1
    npm install @react-native-community/datetimepicker@3.0.4
    npm install @microsoft/microsoft-graph-types --save-dev
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
1. Нахождение `defaultConfig` записи и добавление следующего свойства в файл `defaultConfig` .

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

1. Откройте **графтуториал/index.js** и добавьте следующий элемент в начало файла перед всеми остальными `import` операторами.

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. Создайте новый файл в каталоге **графтуториал** с именем **аусконтекст. целевого сервера** и добавьте следующий код.

    :::code language="typescript" source="../demo/GraphTutorial/AuthContext.tsx" id="AuthContextSnippet":::

1. Создайте новый файл в каталоге **графтуториал** с именем **UserContext. целевого сервера** и добавьте следующий код.

    :::code language="typescript" source="../demo/GraphTutorial/UserContext.tsx" id="UserContextSnippet":::

1. Создание нового каталога в каталоге **графтуториал** с именем **screens**.
1. Создайте новый файл в каталоге **графтуториал/screens** с именем **хомескрин. Целевой**. Добавьте указанный ниже код в файл.

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="HomeScreenSnippet":::

1. Создайте новый файл в каталоге **графтуториал/screens** с именем **календарскрин. Целевой**. Добавьте указанный ниже код в файл.

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

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
          <Stack.Navigator>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                headerShown: false
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
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';

    type SignInProps = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default class SignInScreen extends React.Component<SignInProps> {
      static contextType = AuthContext;

      _signInAsync = async () => {
        await this.context.signIn();
      };

      componentDidMount() {
        this.props.navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });
      }

      render() {
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
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';
    import { UserContext } from '../UserContext';
    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuProps = {
      navigation: StackNavigationProp<ParamListBase>;
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

    export default class DrawerMenuContent extends React.Component<DrawerMenuProps> {
      static contextType = AuthContext;

      state = {
        // TEMPORARY
        userLoading: true,
        userFirstName: 'Adele',
        userFullName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userTimeZone: 'UTC',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        this.context.signOut();
      }

      async componentDidMount() {
        this.props.navigation.setOptions({
          headerShown: false,
        });
      }

      render() {
        const userLoaded = !this.state.userLoading;

        return (
          <UserContext.Provider value={this.state}>
            <Drawer.Navigator
              drawerType='front'
              screenOptions={{
                headerStyle: {
                  backgroundColor: '#276b80'
                },
                headerTintColor: 'white'
              }}
              drawerContent={props => (
                <CustomDrawerContent {...props}
                  userName={this.state.userFullName}
                  userEmail={this.state.userEmail}
                  userPhoto={this.state.userPhoto}
                  signOut={this._signOut} />
              )}>
              <Drawer.Screen name='Home'
                component={HomeScreen}
                options={{drawerLabel: 'Home', headerTitle: 'Welcome'}} />
              { userLoaded &&
                <Drawer.Screen name='Calendar'
                  component={CalendarScreen}
                  options={{drawerLabel: 'Calendar'}} />
              }
            </Drawer.Navigator>
          </UserContext.Provider>
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
1. Добавьте в этот каталог изображение профиля по умолчанию с именем **no-profile-pic.png** . Вы можете использовать любое изображение, которое вам нравится, или использовать [его из этого примера](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).

1. Откройте файл **графтуториал/App. Целевой сервера** и замените все содержимое приведенным ниже.

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import * as React from 'react';
    import { NavigationContainer, ParamListBase } from '@react-navigation/native';
    import { createStackNavigator, StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from './AuthContext';
    import SignInScreen from './screens/SignInScreen';
    import DrawerMenuContent from './menus/DrawerMenu'
    import AuthLoadingScreen from './screens/AuthLoadingScreen';

    const Stack = createStackNavigator();

    type Props = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default function App({ navigation }: Props) {
      const [state, dispatch] = React.useReducer(
        (prevState: any, action: any) => {
          switch (action.type) {
            case 'RESTORE_TOKEN':
              return {
                ...prevState,
                userToken: action.token,
                isLoading: false
              };
            case 'SIGN_IN':
              return {
                ...prevState,
                isSignOut: false,
                userToken: action.token
              }
            case 'SIGN_OUT':
              return {
                ...prevState,
                isSignOut: true,
                userToken: null
              }
          }
        },
        {
          isLoading: true,
          isSignOut: false,
          userToken: null
        }
      );

      React.useEffect(() => {
        const bootstrapAsync = async () => {
          let userToken = null;
          // TEMPORARY
          dispatch({ type: 'RESTORE_TOKEN', token: userToken });
        };

        bootstrapAsync();
      }, []);

      const authContext = React.useMemo(
        () => ({
          signIn: async () => {
            dispatch({ type: 'SIGN_IN', token: 'placeholder-token' });
          },
          signOut: async () => {
            dispatch({ type: 'SIGN_OUT' });
          }
        }),
        []
      );

      return (
        <AuthContext.Provider value={authContext}>
          <NavigationContainer>
            <Stack.Navigator>
              {state.isLoading ? (
                <Stack.Screen name="Loading" component={AuthLoadingScreen} />
              ) : state.userToken == null ? (
                <Stack.Screen name="SignIn" component={SignInScreen} />
              ) : (
                <Stack.Screen name="Main" component={DrawerMenuContent} />
              )}
            </Stack.Navigator>
          </NavigationContainer>
        </AuthContext.Provider>
      );
    }
    ```

1. Сохраните все изменения.

1. Перезагрузите приложение в симуляторе.

Меню приложения должно работать для перехода между двумя фрагментами и изменения при касании кнопок **входа** **и выхода.**

![Снимки экрана приложения на Android](./images/android-app-screens.png)

![Снимки экрана приложения на iOS](./images/ios-app-screens.png)
