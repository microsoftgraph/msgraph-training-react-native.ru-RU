<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="2b0cd-101">В этом разделе мы добавим возможность создания событий в календаре пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-the-new-event-screen"></a><span data-ttu-id="2b0cd-102">Создание экрана создания события</span><span class="sxs-lookup"><span data-stu-id="2b0cd-102">Create the new event screen</span></span>

1. <span data-ttu-id="2b0cd-103">Откройте **./граф/графманажер.ТС** и добавьте в класс следующую функцию `GraphManager` .</span><span class="sxs-lookup"><span data-stu-id="2b0cd-103">Open **./graph/GraphManager.ts** and add the following function to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="CreateEventSnippet":::

    <span data-ttu-id="2b0cd-104">Эта функция использует Graph SDK для создания нового события.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-104">This function uses the Graph SDK to create a new event.</span></span>

1. <span data-ttu-id="2b0cd-105">Создайте новый файл в файле **./СКРИНС** с именем **невевентскрин. целевого сервера** и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-105">Create a new file in the **./screens** named **NewEventScreen.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/NewEventScreen.tsx" id="NewEventScreenSnippet":::

    <span data-ttu-id="2b0cd-106">Определите, что `createEvent` делает функция.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-106">Consider what the `createEvent` function does.</span></span> <span data-ttu-id="2b0cd-107">Он создает `MicrosoftGraph.Event` объект, используя значения из формы, а затем передает этот объект в `GraphManager.createEvent` функцию.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-107">It creates a `MicrosoftGraph.Event` object using the values from the form, then passes that object to the `GraphManager.createEvent` function.</span></span>

1. <span data-ttu-id="2b0cd-108">Откройте **./менус/дравермену.тскс** и добавьте приведенный ниже `import` оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-108">Open **./menus/DrawerMenu.tsx** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import NewEventScreen from '../screens/NewEventScreen';
    ```

1. <span data-ttu-id="2b0cd-109">Добавьте следующий код внутри `<Drawer.Navigator>` элемента непосредственно над `</Drawer.Navigator>` строкой.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-109">Add the following code inside the `<Drawer.Navigator>` element, just above the `</Drawer.Navigator>` line.</span></span>

    ```typescript
    { userLoaded &&
      <Drawer.Screen name='NewEvent'
        component={NewEventScreen}
        options={{drawerLabel: 'New event'}} />
    }
    ```

1. <span data-ttu-id="2b0cd-110">Сохраните изменения и перезапустите или обновите приложение.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-110">Save your changes and restart or refresh the app.</span></span> <span data-ttu-id="2b0cd-111">В меню выберите пункт **создать событие** , чтобы открыть форму создать событие.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-111">Select the **New event** option on the menu to get to the new event form.</span></span>

1. <span data-ttu-id="2b0cd-112">Заполните форму и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="2b0cd-112">Fill in the form and select **Create**.</span></span>

    ![Снимок экрана с формой создания события](images/new-event-form.png)
