<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="66681-101">В этом руководстве рассказывается, как создать собственное приложение, которое использует API Microsoft Graph для получения сведений о календаре для пользователя.</span><span class="sxs-lookup"><span data-stu-id="66681-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="66681-102">Если вы предпочитаете просто скачать заполненный учебник, вы можете скачать или клонировать [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-react-native).</span><span class="sxs-lookup"><span data-stu-id="66681-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66681-103">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="66681-103">Prerequisites</span></span>

<span data-ttu-id="66681-104">Прежде чем приступить к работе с этим руководством, на вашем компьютере для разработки должны быть установлены следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="66681-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="66681-105">По крайней мере один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="66681-105">At least one of the following:</span></span>
  - <span data-ttu-id="66681-106">[Пакет средств разработки](https://jdk.java.net) для [Android Studio](https://developer.android.com/studio/) **и** Java (требуется для запуска примера на Android)</span><span class="sxs-lookup"><span data-stu-id="66681-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="66681-107">[Xcode](https://developer.apple.com/xcode/) (требуется для запуска примера на iOS)</span><span class="sxs-lookup"><span data-stu-id="66681-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="66681-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="66681-108">Node.js</span></span>](https://nodejs.org)

> [!NOTE]
> <span data-ttu-id="66681-109">Это руководство было написано с помощью функции "реагируя встроенная система CLI", которая имеет определенные предварительные требования в зависимости от операционной системы и целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="66681-109">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="66681-110">Инструкции по настройке компьютера для разработки приведены в разделе [реагирующий основной приступый к началу работы](https://facebook.github.io/react-native/docs/getting-started) .</span><span class="sxs-lookup"><span data-stu-id="66681-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="66681-111">Версии, используемые для этого руководства, перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="66681-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="66681-112">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="66681-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="66681-113">Android Studio версии 3.4.2 с 1.8.0 JRE и пакетом SDK для Android 9,0</span><span class="sxs-lookup"><span data-stu-id="66681-113">Android Studio version 3.4.2 with the 1.8.0 JRE and the Android 9.0 SDK</span></span>
> - <span data-ttu-id="66681-114">Пакет SDK для Java версии 12.0.2</span><span class="sxs-lookup"><span data-stu-id="66681-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="66681-115">Xcode версии 10,3</span><span class="sxs-lookup"><span data-stu-id="66681-115">Xcode version 10.3</span></span>
> - <span data-ttu-id="66681-116">Node. js версии 10.16.0</span><span class="sxs-lookup"><span data-stu-id="66681-116">Node.js version 10.16.0</span></span>

## <a name="feedback"></a><span data-ttu-id="66681-117">Отзывы</span><span class="sxs-lookup"><span data-stu-id="66681-117">Feedback</span></span>

<span data-ttu-id="66681-118">Сообщите о нем в [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-react-native).</span><span class="sxs-lookup"><span data-stu-id="66681-118">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
