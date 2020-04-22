<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1176c-101">В этом упражнении вы добавите Microsoft Graph в приложение.</span><span class="sxs-lookup"><span data-stu-id="1176c-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="1176c-102">Для этого приложения вы будете использовать [клиентскую библиотеку JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) , чтобы совершать вызовы в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1176c-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="1176c-103">Получение событий календаря из Outlook</span><span class="sxs-lookup"><span data-stu-id="1176c-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="1176c-104">В этом разделе описывается расширение `GraphManager` класса для добавления функции, позволяющей получить события и обновление `CalendarScreen` , чтобы использовать эти новые функции.</span><span class="sxs-lookup"><span data-stu-id="1176c-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="1176c-105">Откройте файл **графтуториал/Graph/графманажер. Целевой** файл и добавьте указанный `GraphManager` ниже метод в класс.</span><span class="sxs-lookup"><span data-stu-id="1176c-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetEventsSnippet":::

    > [!NOTE]
    > <span data-ttu-id="1176c-106">Рассмотрите, какие действия `getEvents` выполняет код.</span><span class="sxs-lookup"><span data-stu-id="1176c-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="1176c-107">URL-адрес, который будет вызываться — это `/v1.0/me/events`.</span><span class="sxs-lookup"><span data-stu-id="1176c-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="1176c-108">`select` Функция ограничит поля, возвращаемые для каждого события, только теми, которые приложение будет использовать в действительности.</span><span class="sxs-lookup"><span data-stu-id="1176c-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="1176c-109">`orderby` Функция сортирует результаты по дате и времени создания, начиная с самого последнего элемента.</span><span class="sxs-lookup"><span data-stu-id="1176c-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="1176c-110">Откройте **графтуториал/views/календарскрин. Целевой** элемент и замените все его содержимое приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="1176c-110">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

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

<span data-ttu-id="1176c-111">Теперь вы можете запустить приложение, войти и нажать в меню элемент Навигация по **календарю** .</span><span class="sxs-lookup"><span data-stu-id="1176c-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="1176c-112">В приложении должен появиться дамп JSON событий.</span><span class="sxs-lookup"><span data-stu-id="1176c-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="1176c-113">Отображение результатов</span><span class="sxs-lookup"><span data-stu-id="1176c-113">Display the results</span></span>

<span data-ttu-id="1176c-114">Теперь вы можете заменить дамп JSON на какой-то способ отобразить результаты в удобном для пользователя виде.</span><span class="sxs-lookup"><span data-stu-id="1176c-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="1176c-115">В этом разделе мы покажем, как `FlatList` добавить элемент в экран календаря для отображения событий.</span><span class="sxs-lookup"><span data-stu-id="1176c-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="1176c-116">Откройте файл **графтуториал/Graph/screens/календарскрин. Целевой** файл и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="1176c-116">Open the **GraphTutorial/graph/screens/CalendarScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import moment from 'moment';
    ```

1. <span data-ttu-id="1176c-117">Добавьте приведенный ниже **above** метод над `CalendarScreen` объявлением класса.</span><span class="sxs-lookup"><span data-stu-id="1176c-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="1176c-118">Замените `ScrollView` в `CalendarComponent` методе приведенный ниже метод.</span><span class="sxs-lookup"><span data-stu-id="1176c-118">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

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

1. <span data-ttu-id="1176c-119">Запустите приложение, войдите в систему и нажмите элемент навигации по **календарю** .</span><span class="sxs-lookup"><span data-stu-id="1176c-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="1176c-120">Вы должны увидеть список событий.</span><span class="sxs-lookup"><span data-stu-id="1176c-120">You should see the list of events.</span></span>

    ![Снимок экрана с таблицей событий](./images/calendar-list.png)
