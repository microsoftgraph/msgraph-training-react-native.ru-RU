<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы добавите Microsoft Graph в приложение. Для этого приложения вы будете использовать [клиентскую библиотеку JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) , чтобы совершать вызовы в Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Получение событий календаря из Outlook

В этом разделе описывается расширение `GraphManager` класса для добавления функции, позволяющей получить события и обновление `CalendarScreen` , чтобы использовать эти новые функции.

1. Откройте файл **графтуториал/Graph/графманажер. Целевой** файл и добавьте указанный `GraphManager` ниже метод в класс.

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetEventsSnippet":::

    > [!NOTE]
    > Рассмотрите, какие действия `getEvents` выполняет код.
    >
    > - URL-адрес, который будет вызываться — это `/v1.0/me/events`.
    > - `select` Функция ограничит поля, возвращаемые для каждого события, только теми, которые приложение будет использовать в действительности.
    > - `orderby` Функция сортирует результаты по дате и времени создания, начиная с самого последнего элемента.

1. Откройте **графтуториал/views/календарскрин. Целевой** элемент и замените все его содержимое приведенным ниже кодом.

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const initialState: CalendarScreenState = { loadingEvents: true, events: []};
    const CalendarState = React.createContext(initialState);

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: any[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator animating={calendarState.loadingEvents} size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const events = await GraphManager.getEvents();

          this.setState({
            loadingEvents: false,
            events: events.value
          });
        } catch(error) {
          Alert.alert(
            'Error getting events',
            JSON.stringify(error),
            [
              {
                text: 'OK'
              }
            ],
            { cancelable: false }
          );
        }
      }

      render() {
        return (
          <CalendarState.Provider value={this.state}>
            <Stack.Navigator screenOptions={ headerOptions }>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  title: 'Calendar',
                  headerLeft: () => <DrawerToggle/>
                }} />
            </Stack.Navigator>
          </CalendarState.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      loading: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
      },
      eventItem: {
        padding: 10
      },
      eventSubject: {
        fontWeight: '700',
        fontSize: 18
      },
      eventOrganizer: {
        fontWeight: '200'
      },
      eventDuration: {
        fontWeight: '200'
      }
    });
    ```

Теперь вы можете запустить приложение, войти и нажать в меню элемент Навигация по **календарю** . В приложении должен появиться дамп JSON событий.

## <a name="display-the-results"></a>Отображение результатов

Теперь вы можете заменить дамп JSON на какой-то способ отобразить результаты в удобном для пользователя виде. В этом разделе мы покажем, как `FlatList` добавить элемент в экран календаря для отображения событий.

1. Откройте файл **графтуториал/Graph/screens/календарскрин. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.

    ```typescript
    import moment from 'moment';
    ```

1. Добавьте приведенный ниже **above** метод над `CalendarScreen` объявлением класса.

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. Замените `ScrollView` в `CalendarComponent` методе приведенный ниже метод.

    ```typescript
    <FlatList data={calendarState.events}
      renderItem={({item}) =>
        <View style={styles.eventItem}>
          <Text style={styles.eventSubject}>{item.subject}</Text>
          <Text style={styles.eventOrganizer}>{item.organizer.emailAddress.name}</Text>
          <Text style={styles.eventDuration}>
            {convertDateTime(item.start.dateTime)} - {convertDateTime(item.end.dateTime)}
          </Text>
        </View>
      } />
    ```

1. Запустите приложение, войдите в систему и нажмите элемент навигации по **календарю** . Вы должны увидеть список событий.

    ![Снимок экрана с таблицей событий](./images/calendar-list.png)
