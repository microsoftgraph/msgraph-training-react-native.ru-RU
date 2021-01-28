<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e49c8-101">В этом упражнении вы создадим новое приложение Azure AD с помощью Центра администрирования Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e49c8-101">In this exercise you will create a new Azure AD native application using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="e49c8-102">Откройте браузер и перейдите в [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) и войдите с помощью **личной учетной записи** (т.е. учетной записи Майкрософт) или **рабочей или учебной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="e49c8-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="e49c8-103">Выберите **Azure Active Directory** на панели навигации слева, затем выберите **Регистрация приложений** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="e49c8-103">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="e49c8-104">Снимок экрана с регистрацией приложений</span><span class="sxs-lookup"><span data-stu-id="e49c8-104">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="e49c8-105">Выберите **Новая регистрация**.</span><span class="sxs-lookup"><span data-stu-id="e49c8-105">Select **New registration**.</span></span> <span data-ttu-id="e49c8-106">На странице **Зарегистрировать приложение** задайте необходимые значения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e49c8-106">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="e49c8-107">Введите **имя** `React Native Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="e49c8-107">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="e49c8-108">Введите **поддерживаемые типы учетных записей** для **учетных записей в любом каталоге организаций и личных учетных записей Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e49c8-108">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="e49c8-109">В **URI** перенаправления измените выпадаю на общедоступный клиент **(мобильный**& настольном компьютере) и установите значение `graph-tutorial://react-native-auth/` .</span><span class="sxs-lookup"><span data-stu-id="e49c8-109">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth/`.</span></span>

    ![Снимок экрана: страница "Регистрация приложения"](./images/aad-register-an-app.png)

1. <span data-ttu-id="e49c8-111">Нажмите **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="e49c8-111">Select **Register**.</span></span> <span data-ttu-id="e49c8-112">На странице **учебника React Native Graph** скопируйте значение ИД приложения **(клиента)** и сохраните его, оно потребуется вам на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="e49c8-112">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Снимок экрана: ИД нового приложения для регистрации](./images/aad-application-id.png)
