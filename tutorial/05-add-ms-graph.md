<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9da46-101">В этом упражнении вы добавите Microsoft Graph в приложение.</span><span class="sxs-lookup"><span data-stu-id="9da46-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="9da46-102">Для этого приложения вы будете использовать [клиентскую библиотеку JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) , чтобы совершать вызовы в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="9da46-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="9da46-103">Получение событий календаря из Outlook</span><span class="sxs-lookup"><span data-stu-id="9da46-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="9da46-104">В этом разделе `GraphManager` описывается расширение класса для добавления функции для получения событий пользователя текущей недели и обновления `CalendarScreen` для использования этих новых функций.</span><span class="sxs-lookup"><span data-stu-id="9da46-104">In this section you will extend the `GraphManager` class to add a function to get the user's events for the current week and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="9da46-105">Откройте файл **графтуториал/Graph/графманажер. Целевой** файл и добавьте указанный ниже метод в `GraphManager` класс.</span><span class="sxs-lookup"><span data-stu-id="9da46-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetCalendarViewSnippet":::

    > [!NOTE]
    > <span data-ttu-id="9da46-106">Рассмотрите, какие действия `getCalendarView` выполняет код.</span><span class="sxs-lookup"><span data-stu-id="9da46-106">Consider what the code in `getCalendarView` is doing.</span></span>
    >
    > - <span data-ttu-id="9da46-107">URL-адрес, который будет вызываться — это `/v1.0/me/calendarView` .</span><span class="sxs-lookup"><span data-stu-id="9da46-107">The URL that will be called is `/v1.0/me/calendarView`.</span></span>
    > - <span data-ttu-id="9da46-108">`header`Функция добавляет `Prefer: outlook.timezone` заголовок в запрос, что приводит к тому, что время в отклике будет в предпочтительном часовом поясе пользователя.</span><span class="sxs-lookup"><span data-stu-id="9da46-108">The `header` function adds the `Prefer: outlook.timezone` header to the request, causing the times in the response to be in the user's preferred time zone.</span></span>
    > - <span data-ttu-id="9da46-109">`query`Функция добавляет `startDateTime` `endDateTime` Параметры и определяет окно представления календаря.</span><span class="sxs-lookup"><span data-stu-id="9da46-109">The `query` function adds the `startDateTime` and `endDateTime` parameters, defining the window of time for the calendar view.</span></span>
    > - <span data-ttu-id="9da46-110">`select`Функция ограничит поля, возвращаемые для каждого события, только теми, которые приложение будет использовать в действительности.</span><span class="sxs-lookup"><span data-stu-id="9da46-110">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="9da46-111">`orderby`Функция сортирует результаты по времени начала.</span><span class="sxs-lookup"><span data-stu-id="9da46-111">The `orderby` function sorts the results by the start time.</span></span>
    > - <span data-ttu-id="9da46-112">`top`Функция ограничит результаты первыми событиями 50.</span><span class="sxs-lookup"><span data-stu-id="9da46-112">The `top` function limits the results to the first 50 events.</span></span>

1. <span data-ttu-id="9da46-113">Откройте **графтуториал/views/календарскрин. Целевой** элемент и замените все его содержимое приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="9da46-113">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      Platform,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import moment from 'moment-timezone';
    import { findOneIana } from 'windows-iana';

    import { UserContext } from '../UserContext';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const CalendarState = React.createContext<CalendarScreenState>({
      loadingEvents: true,
      events: []
    });

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: MicrosoftGraph.Event[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator
                color={Platform.OS === 'android' ? '#276b80' : undefined}
                animating={calendarState.loadingEvents}
                size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {
      static contextType = UserContext;

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const tz = this.context.userTimeZone || 'UTC';
          // Convert user's Windows time zone ("Pacific Standard Time")
          // to IANA format ("America/Los_Angeles")
          // Moment.js needs IANA format
          const ianaTimeZone = findOneIana(tz);

          // Get midnight on the start of the current week in the user's
          // time zone, but in UTC. For example, for PST, the time value
          // would be 07:00:00Z
          const startOfWeek = moment
            .tz(ianaTimeZone!.valueOf())
            .startOf('week')
            .utc();

          const endOfWeek = moment(startOfWeek)
            .add(7, 'day');

          const events = await GraphManager.getCalendarView(
            startOfWeek.format(),
            endOfWeek.format(),
            tz);

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
            <Stack.Navigator>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  headerShown: false
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

<span data-ttu-id="9da46-114">Теперь вы можете запустить приложение, войти и нажать в меню элемент Навигация по **календарю** .</span><span class="sxs-lookup"><span data-stu-id="9da46-114">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="9da46-115">В приложении должен появиться дамп JSON событий.</span><span class="sxs-lookup"><span data-stu-id="9da46-115">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="9da46-116">Отображение результатов</span><span class="sxs-lookup"><span data-stu-id="9da46-116">Display the results</span></span>

<span data-ttu-id="9da46-117">Теперь вы можете заменить дамп JSON на какой-то способ отобразить результаты в удобном для пользователя виде.</span><span class="sxs-lookup"><span data-stu-id="9da46-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="9da46-118">В этом разделе мы покажем, как добавить элемент в `FlatList` экран календаря для отображения событий.</span><span class="sxs-lookup"><span data-stu-id="9da46-118">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="9da46-119">Добавьте приведенный ниже **above** метод над `CalendarScreen` объявлением класса.</span><span class="sxs-lookup"><span data-stu-id="9da46-119">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="9da46-120">Замените `ScrollView` в `CalendarComponent` методе приведенный ниже метод.</span><span class="sxs-lookup"><span data-stu-id="9da46-120">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

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

1. <span data-ttu-id="9da46-121">Запустите приложение, войдите в систему и нажмите элемент навигации по **календарю** .</span><span class="sxs-lookup"><span data-stu-id="9da46-121">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="9da46-122">Вы должны увидеть список событий.</span><span class="sxs-lookup"><span data-stu-id="9da46-122">You should see the list of events.</span></span>

    ![Снимок экрана с таблицей событий](./images/calendar-list.png)
