# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="76801-101">Выполнение завершенного проекта</span><span class="sxs-lookup"><span data-stu-id="76801-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76801-102">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="76801-102">Prerequisites</span></span>

<span data-ttu-id="76801-103">Чтобы запустить завершенный проект в этой папке, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="76801-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="76801-104">По крайней мере один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="76801-104">At least one of the following:</span></span>
  - <span data-ttu-id="76801-105">[Пакет средств разработки](https://jdk.java.net) для [Android Studio](https://developer.android.com/studio/) **и** Java (требуется для запуска примера на Android)</span><span class="sxs-lookup"><span data-stu-id="76801-105">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="76801-106">[Xcode](https://developer.apple.com/xcode/) (требуется для запуска примера на iOS)</span><span class="sxs-lookup"><span data-stu-id="76801-106">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="76801-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="76801-107">Node.js</span></span>](https://nodejs.org)
- <span data-ttu-id="76801-108">Личная учетная запись Майкрософт с почтовым ящиком на Outlook.com или рабочей или учебной учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="76801-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

> <span data-ttu-id="76801-109">**Примечание:** Это руководство было написано с помощью функции "реагируя встроенная система CLI", которая имеет определенные предварительные требования в зависимости от операционной системы и целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="76801-109">**Note:** This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="76801-110">Инструкции по настройке компьютера для разработки приведены в разделе [реагирующий основной приступый к началу работы](https://facebook.github.io/react-native/docs/getting-started) .</span><span class="sxs-lookup"><span data-stu-id="76801-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="76801-111">Версии, используемые для этого руководства, перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="76801-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="76801-112">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="76801-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="76801-113">Android Studio версии 3.6.2 с пакетом SDK для Android 9,0</span><span class="sxs-lookup"><span data-stu-id="76801-113">Android Studio version 3.6.2 with the Android 9.0 SDK</span></span>
> - <span data-ttu-id="76801-114">Пакет SDK для Java версии 12.0.2</span><span class="sxs-lookup"><span data-stu-id="76801-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="76801-115">Xcode версии 11,4</span><span class="sxs-lookup"><span data-stu-id="76801-115">Xcode version 11.4</span></span>
> - <span data-ttu-id="76801-116">Node. js версии 12.16.2</span><span class="sxs-lookup"><span data-stu-id="76801-116">Node.js version 12.16.2</span></span>

<span data-ttu-id="76801-117">Если у вас нет учетной записи Майкрософт, у вас есть несколько вариантов для получения бесплатной учетной записи:</span><span class="sxs-lookup"><span data-stu-id="76801-117">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="76801-118">Вы можете [зарегистрироваться для создания новой личной учетной записи Майкрософт](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="76801-118">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="76801-119">Вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.</span><span class="sxs-lookup"><span data-stu-id="76801-119">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="76801-120">Регистрация приложения в центре администрирования Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76801-120">Register an application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="76801-121">Откройте браузер и перейдите в [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) и войдите с помощью **личной учетной записи** (т.е. учетной записи Майкрософт) или **рабочей или учебной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="76801-121">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="76801-122">Выберите **Azure Active Directory** на панели навигации слева, затем выберите **Регистрация приложений** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="76801-122">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="76801-123">Снимок экрана с регистрациями приложений</span><span class="sxs-lookup"><span data-stu-id="76801-123">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="76801-124">Выберите **Новая регистрация**.</span><span class="sxs-lookup"><span data-stu-id="76801-124">Select **New registration**.</span></span> <span data-ttu-id="76801-125">На странице**Зарегистрировать приложение** задайте необходимые значения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="76801-125">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="76801-126">Введите **имя** `React Native Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="76801-126">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="76801-127">Введите **поддерживаемые типы учетных записей** для **учетных записей в любом каталоге организаций и личных учетных записей Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="76801-127">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="76801-128">В разделе **URI перенаправления**измените раскрывающийся список на **общедоступный клиент (мобильный & Настольный)** и `graph-tutorial://react-native-auth`задайте значение.</span><span class="sxs-lookup"><span data-stu-id="76801-128">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth`.</span></span>

    ![Снимок страницы "регистрация приложения"](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="76801-130">Выберите **регистр**.</span><span class="sxs-lookup"><span data-stu-id="76801-130">Select **Register**.</span></span> <span data-ttu-id="76801-131">На странице " **реагирующий собственный график** " СКОПИРУЙТЕ значение **идентификатора Application (Client)** и сохраните его, он понадобится на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="76801-131">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом приложения для новой регистрации приложения](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="76801-133">В разделе **Управление**выберите **Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="76801-133">Under **Manage**, select **Authentication**.</span></span> <span data-ttu-id="76801-134">На странице **Перенаправление URI** добавьте еще один URI перенаправления типа **Public client (Mobile & Desktop)** с URI `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="76801-134">On the **Redirect URIs** page, add another redirect URI of type **Public client (mobile & desktop)**, with the URI `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="76801-135">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="76801-135">Select **Save**.</span></span>

    ![Снимок экрана со страницей URI перенаправления](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a><span data-ttu-id="76801-137">Настройка примера</span><span class="sxs-lookup"><span data-stu-id="76801-137">Configure the sample</span></span>

1. <span data-ttu-id="76801-138">Переименуйте файл **графтуториал/auth/AuthConfig. TS. example** в **AuthConfig. TS**.</span><span class="sxs-lookup"><span data-stu-id="76801-138">Rename the **GraphTutorial/auth/AuthConfig.ts.example** file to **AuthConfig.ts**.</span></span>
1. <span data-ttu-id="76801-139">Измените файл **AuthConfig. TS** и внесите следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="76801-139">Edit the **AuthConfig.ts** file and make the following changes.</span></span>
    1. <span data-ttu-id="76801-140">Замените `YOUR_APP_ID_HERE` **идентификатором приложения** , полученным на портале регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="76801-140">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

1. <span data-ttu-id="76801-141">В интерфейсе командной строки (CLI) перейдите в каталог **графтуториал** и выполните следующую команду, чтобы установить требования.</span><span class="sxs-lookup"><span data-stu-id="76801-141">In your command-line interface (CLI), navigate to the **GraphTutorial** directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

1. <span data-ttu-id="76801-142">В интерфейсе командной строки (CLI) перейдите в каталог **графтуториал/iOS** и выполните следующую команду для установки требований.</span><span class="sxs-lookup"><span data-stu-id="76801-142">In your command-line interface (CLI), navigate to the **GraphTutorial/ios** directory and run the following command to install requirements.</span></span>

    ```Shell
    pod install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="76801-143">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="76801-143">Run the sample</span></span>

### <a name="run-on-ios-simulator"></a><span data-ttu-id="76801-144">Запуск в имитаторе iOS</span><span class="sxs-lookup"><span data-stu-id="76801-144">Run on iOS Simulator</span></span>

<span data-ttu-id="76801-145">Выполните следующую команду в командной панели CLI, чтобы запустить приложение в симуляторе iOS.</span><span class="sxs-lookup"><span data-stu-id="76801-145">Run the following command in your CLI to start the application in an iOS Simulator.</span></span>

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a><span data-ttu-id="76801-146">Запуск на эмуляторе Android</span><span class="sxs-lookup"><span data-stu-id="76801-146">Run on Android emulator</span></span>

<span data-ttu-id="76801-147">Запустите экземпляр эмулятора Android и Android и выполните следующую команду в командной панели управления, чтобы запустить приложение в эмуляторе Android.</span><span class="sxs-lookup"><span data-stu-id="76801-147">Launch and Android emulator instance and run the following command in your CLI to start the application in an Android emulator.</span></span>

```Shell
react-native run-android
```
