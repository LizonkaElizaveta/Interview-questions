**1. ЧТО ТАКОЕ СЕРИАЛИЗАЦИЯ?**

Ответ: Сериализация это процесс сохранения состояния объекта в последовательность байт; десериализация это процесс восстановления объекта, из этих байт. Java Serialization API предоставляет стандартный механизм для создания сериализуемых объектов.

**2. КАК ИСКЛЮЧИТЬ ПОЛЯ ИЗ СЕРИАЛИЗАЦИИ?**Ч

Ответ: Для того, чтобы исключить поля из сериализуемого потока, необходимо пометить поле модификатором transient.

**3. ЧТО ЗНАЧИТ TRANSIENT?**

Ответ: Свойство класса, помечанные модификатором transient, не сериализуется. Обычно в таких полях хранится промежуточное состояние объекта, которое, к примеру, проще вычислить, чем сериализовать, а затем десериализовать. Другой пример такого поля -ссылка на экземпляр объекта, который не требует сериализации или не м.б. сериализован.

**4. КАК ИЗМЕНИТЬ СТАНДАРТНОЕ ПОВЕДЕНИЕ СЕРИАЛИЗАЦИИ/ДЕСЕРИАЛИЗАЦИИ?**

Ответ: В большинстве случаев мы не определяем поведение вручную,  а полагаемся на стандартную реализацию, и очень не удобно постоянно переопределять какие-то методы сериализации + постоянно следить за добавлением новых полей, добавлять их в методы. Специально для этих целей есть Externalizable.

Чтобы изменить стандартное поведение сериализации нужно переопределить и поместить в свои файлы классов 2 метода:

![](https://2.bp.blogspot.com/-hiuLy14Et2s/VzVfqXtpOgI/AAAAAAAAAp0/upsRxpWdcSQ68QfVKgXO_rZem8RV2BcTACLcB/s1600/q004_p01.jpg)

Оба метода объявлены как private, это гарантирует, что методы не будут переопределены или перезагружены. Виртуальная машина при вызове соответствующего метода автоматически проверяет, не были ли они объявлены в классе объекта. Виртуальная машина в любой момент может вызвать private методы вашего класса, но другие объекты этого сделать не смогут. Т.об. обеспечивается целостность класса и нормальная работа протокола сериализации.

**5. ВЫ СОЗДАЛИ КЛАСС, ЧЕЙ СУПЕРКЛАСС СЕРИАЛИЗУЕМЫЙ, НО ПРИ ЭТОМ ВЫ НЕ ХОТИТЕ, ЧТОБЫ ВАШ КЛАСС БЫЛ СЕРИАЛИЗУЕМЫМ, КАК ОСТАНОВИТЬ СЕРИАЛИЗАЦИЮ?**

Ответ: Вы не можете "разреализовать" интерфейс, поэтому если супер класс реализует Serializable, то и созданный вами новый класс также будет реализовывать его. Чтобы остановить автоматическую сериализацию, вы можете применить private методы для создания исключительной ситуации NotSerializableException.

![](https://4.bp.blogspot.com/-d2m04NwlIXw/VzVgATJBoII/AAAAAAAAAp4/VRv-fj4pAl0ZXs9MmnaSSMQvxpLtu7BCACLcB/s1600/q005_p01.jpg)

Любая попытка записать или прочитать этот объект приведет к возникновению исключительной ситуации. Запомните, если методы объявлены как private, никто не сможет модифицировать ваш код, изменяя код класса. Java не позволяет переопределять такие методы.

**6. КАК СОЗДАТЬ СОБСТВЕННЫЙ ПРОТОКОЛ СЕРИАЛИЗАЦИИ?**

Ответ: Вместо реализации  интерфейса Serializable, вы можете реализовать интерфейс Externalizable, который содержит 2 метода:

![](https://2.bp.blogspot.com/-hiuLy14Et2s/VzVfqXtpOgI/AAAAAAAAAp0/upsRxpWdcSQ68QfVKgXO_rZem8RV2BcTACLcB/s1600/q004_p01.jpg)

Для создания собственного протокола нужно просто переопределить эти 2 метода. Хотя это и наиболее сожный способ, при этом он наиболее контролируемый.

**7. КАКАЯ РОЛЬ ПОЛЯ SERIALVERSIONUID В СЕРИАЛИЗАЦИИ?**

Ответ: Поле private static final long serialVersionUID содержит  уникальный идентификатор версии сериализованного класса. Оно вычисляется по содержимому класса - полям, их порядку добавления, методам, их порядку объявления. Соответственно, при любом изменении в классе это поле поменяет свое значение. Это поле записывается в поток при сериализации класса. Кстати, это единственный случай, когда static-поле сериализуется.

**8. В ЧЕМ ПРОБЛЕМА СЕРИАЛИЗАЦИИ SINGLETON-ОВ?**

Ответ: Проблема в том, что после сериализации мы получим другой объект. Т.об. сериализация дает возможность создать Singleton-ы еще раз, что не совсем нужно. Конечно можно запретить сериализацию Singleton-ов, но это, фактически, уход от проблемы.

Решение заклчается в следующем. В классе определяется метод со следующей сигнатурой: 

![](https://2.bp.blogspot.com/-6PjojebOvSA/VzVgcjY18pI/AAAAAAAAAqE/CQGNk_unbwY141IJRtHR3mialELDpOGxwCLcB/s1600/q008_p01.jpg)

Модификатор доступа можно сделать как private, protected, default. Назначение этого метода - возвращать замещающий объект вместо объекта, на котором он вызван.