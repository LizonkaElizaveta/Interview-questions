**1. ЧЕМ STUB ОТЛИЧАЕТСЯ ОТ MOCK?**

Ответ: Разница в том, что стаб ничего не проверяет, а лишь имитирует заданное состояние. А мок – это объект, у которого есть ожидания. Например, что данный метод класса должен быть вызван определенное число раз. Иными словами, ваш тест никогда не сломается из-за «стаба», а вот из-за мока может.

**2. ЧТО ТАКОЕ UNIT TESTING?**

Ответ: Модульное тестирование - процесс проверки на корректность функционирования отдельных частей исходного кода программы путем запуска тестов в искусственной среде.

**3. ЧТО ТАКОЕ ФИКСТУРЫ?**

Ответ: Фикстуры - состояние среды тестирования, которое требуется для успешного выполнения тестового метода.

**4. КАКИЕ ЕСТЬ АННОТАЦИИ ФИКСТУР?**

Ответ: 

* @BeforeClass - запускается только один раз при запуске теста;
* @Before - запускается перед каждым тестовым методом"
* @After - запускается после каждого метода;
* @AfterClass - запускается после того, как отработали все методы.

**5. ДЛЯ ЧЕГО НУЖНА АННОТАЦИЯ @IGNORE?**

Ответ: Аннотация @Ignore заставляет инфраструктуру тестирования проигнорировать данный тестовый метод. Аннотация предусматривает наличия комментария о причине игнорирования теста, полезного при следующем обращении к нему.

**6. ЧТО ТАКОЕ ИНТЕГРАЦИОННЫЕ ТЕСТЫ?**

Ответ: Интеграционные тесты - тесты, проверяющие работоспособность двух или более модулей системы, но в совокупности.