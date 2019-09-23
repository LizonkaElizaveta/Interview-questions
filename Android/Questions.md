**1. ЧТО ТАКОЕ APPLICATION?**

Ответ: Application - это базовый класс в приложении Android для поддержания глобального состояния приложения, который содержит все другие компоненты, такие как activities и services. Application или любой подкласс Application, создается перед любым другим классом при создании вашего приложения.

**2. ЧТО ТАКОЕ CONTEXT?**

Ответ: 

* **Context** -  интерфейс, предоставляющий глобальную информацию о среде приложения. Является абстрактным классом, реализация которого происходит с помощью Android-системы. Context позволяет получить доступ к ресурсам приложения и его классам, а также осуществлять вызовы операций на уровне приложения, например запуск Activity, Service, Broadcasting и Receiving intents, и тд.
* **Application Context** - этот контекст связан с жизненным циклом приложения. Application Context можно использовать там, где нужен контекст, жизненный цикл которого отделен от текущего контекста, или когда вы передаете контекст за пределы действия.
* **Activity Context** - этот контект доступен в activity и связан с жизненным циклом activity. Activity Context следует использовать, когда вы передаете контекст в области activity или вам нужен контекст, жизненный цикл которого привязан к текущему.

![](https://i.stack.imgur.com/sUSE6.png)

**3. ЧТО ТАКОЕ ARMV7?**

Ответ: В Andoroid есть 3 архитектуры процессора. ARMv7 является наиболее распространенным, посколько он оптимизирован для потребления батареи. ARM64 является усовершенствованной версией, которая поддерживает  64-битную обработку для более мощных вычислений. ARMx86, наименее используется из этих 3, так как потребляет много батареи, но является самой мощной.

**4. ПОЧЕМУ БАЙТ-КОД НЕ МОЖЕТ БЫТЬ ЗАПУЩЕН В ANDROID?**

Ответ:  Android использует DVM(Dalvek Virtual Machine), а не JVM(Java Virtual Machine). В версия Android 4.4 Kitkat имеется возможность переключится с Dalvik на ART(Android Runtime). В Android 5.0 Dalvik был полностью заменён на ART. В отличие от Dalvik, который использует JIT-компиляцию (во время выполнения приложения), ART компилирует приложение во время его установки. За счет этого планируется повышение скорости работы программ и одновременно увеличение времени работы от батареи. Недостатком является более долгая загрузка устройства.

**5. ЧТО ТАКОЕ BUILDTYPE В GRADLE? И ДЛЯ ЧЕГО ВЫ ЭТО МОЖЕТЕ ИСПОЛЬЗОВАТЬ?**

Ответ: Build types определяют свойства, которые Gradle использует при сборке и упаковке вашего Android-приложения. Build type определяет способ сборки(например, запускается ли ProGuard), какие ресурсы включены в сборку. Gradle может создать варианты сборки для различных комбинаций вашего проекта.

**6. ОБЪЯСНИТЕ ПРОЦЕСС СБОРКИ В ANDROID?**

Ответ: 

1. Первый шаг включает в себя компиляцию папки ресурсов(/res) с помощью инструмента aapt(android asset packaging tool). Создается класс R.java, который содержит константы.
2. Второй шаг заключается в том, что исходный код java компилируется в файлы .class с помощью javac. Затем файлы классов преобразуются в байт-код Dalvik с помощью инструмента "dx", которы вклчен в инструменты sdk. Выходными данными являются classes.dex.
3. Последний шаг включает в себя apkbuilder, который принимает все входные данные и создает apk(ключ упаковки Android).

**7. ЧТО ТАКОЕ АРХИТЕКТУРА ПРИЛОЖЕНИЙ В ANDROID?**

Ответ: Service, Intent, ContentProvider, BroadcastReciever

**8. ЧТО ТАКОЕ ACTIVITY?**

Ответ: Activity - окно пользовательского интерфейса.

**9. ОБЪЯСНИТЕ ЖИЗНЕННЫЙ ЦИКЛ ACTIVITY?**

Ответ: 

* OnCreate() - когда представление создается впервые;
* OnStart() - вызывается, когда activity становится видимой для пользователя. Затем следует onResume (), если activity выходит на передний план, или onStop (), если она становится скрытой;
* OnResume() - вызывается, когда activity начнет взаимодействовать с пользователем. На данный момент ваша активность находится на вершине стека активностей;
* OnPause() - вызывается, когда activity переходит в фоновый режим, но еще не была уничтожена;
* OnStop() - вызывается, когда activity больше не видна пользователю;
* OnDestroy() - вызывается, когда activity завершилась;
* OnRestart() - будет вызываться всякий раз, когда активность возвращается из невидимого состояния.

![](https://i.stack.imgur.com/kUtt7.png)

**10. КАКИЕ РАЗЛИЧИЯ МЕЖДУ ONCREATE() И ONSTART()?**

Ответ: Метод onCreate () вызывается один раз в течение жизненного цикла activity, либо при запуске приложения, либо когда activity было уничтожено и затем воссоздано, например, во время изменения конфигурации. Метод onStart () вызывается всякий раз, когда activity становится видимой для пользователя, обычно после onCreate () или onRestart ().