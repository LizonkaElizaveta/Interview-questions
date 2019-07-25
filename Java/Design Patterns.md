Паттерн проектирования — это часто встречающееся решение определённой проблемы при проектировании архитектуры программ.

Три основные группы паттернов:

* Порождающие паттерны беспокоятся о гибком создании объектов без внесения в программу лишних зависимостей;
* Структурные паттерны показывают различные способы построения связей между объектами;
* Поведенческие паттерны заботятся об эффективной коммуникации между объектами.

# Порождающие паттерны

## 1. Паттерн Одиночка

Одиночка — это порождающий паттерн проектирования, который гарантирует, что у класса есть только один экземпляр, и предоставляет к нему глобальную точку доступа.

Все реализации одиночки сводятся к тому, чтобы скрыть конструктор по умолчанию и создать публичный статический метод, который и будет контролировать жизненный цикл объекта-одиночки.

![](https://refactoring.guru/images/patterns/diagrams/singleton/structure-ru.png)

``` java
public class Singleton {
  private static Singleton instance;
  private Singleton () {}

  public static synchronized Singleton getInstance() {
    if (instance == null) {
      instance = new Singleton();
    }
    return instance;
  }
}
```

## 2. Паттерн Строитель

Строитель — это порождающий паттерн проектирования, который позволяет создавать сложные объекты пошагово. Строитель даёт возможность использовать один и тот же код строительства для получения разных представлений объектов.

Паттерн Строитель предлагает вынести конструирование объекта за пределы его собственного класса, поручив это дело отдельным объектам, называемым строителями.

``` java
public class Good{
   public final int a;
   public final int b;
   public final int c;
   public final int d;
   public final int e;
   public final int f;
//Реализация Builder через статический внутренний класс
public static class Builder{
//Обязательные параметры
    public int a;
    public int b;
//Необязательные параметры со значениями по умолчанию
public int c = 0;
public int d = 0;
public int e = 0;
public int f = 0;
//Конструктор с обязательными параметрами
public Builder(int a, int b){
this.a=a;
this.b=b;
}
//Методы с возвращающим типом Builder для необязательного параметра с, d, e, f,
  public Builder c (int val) {
            c = val;
            return this;
        }
  public Builder d (int val) {
            d = val;
            return this;
        }
  public Builder e (int val) {
            e = val;
            return this;
        }
  public Builder f (int val) {
            f = val;
            return this;
        }
//Метод с возвращающим типом Good для генерации объекта
public Good buidl() {
            return new Good (this); }
private Good(Builder builder) {
        a = builder.a;
        b = builder.b;
        c = builder.c;
        d = builder.d;
        e = builder.e;
        f = builder.f;     }
```

## 3. Паттерн Фабричный метод

Используется, когда у нас есть суперкласс с несколькими подклассами и на основе ввода, нам нужно вернуть один из подкласса. Класс не знает какого типа объект он должен создать. Объекты создаются в зависимости от входящих данных.

``` java
class Factory {
    public OS getCurrentOS(String inputos) {
        OS os = null;
        if (inputos.equals("windows")) {
            os = new windowsOS();
        } else if (inputos.equals("linux")) {
            os = new linuxOS();
        } else if (inputos.equals("mac")) {
            os = new macOS();
        }
        return os;
    }
}
interface OS {
    void getOS();
}
class windowsOS implements OS {
    public void getOS () {
        System.out.println("применить для виндовс");
    }
}
class linuxOS implements OS {
    public void getOS () {
        System.out.println("применить для линукс");
    }
}
class macOS implements OS {
    public void getOS () {
        System.out.println("применить для мак");
    }
}

public class FactoryTest {//тест
    public static void main(String[] args){
        String win = "linux";
        Factory factory = new Factory();
        OS os = factory.getCurrentOS(win);
        os.getOS();
    }
}
```

## Паттерн Абстрактная фабрика

Позволяет выбрать конкретную реализацию фабрики из семейства возможных фабрик. Создает семейство связанных объектов. Легко расширять.

``` java
interface Lada {
    long getLadaPrice();
}
interface Ferrari {
    long getFerrariPrice();
}
interface Porshe {
    long getPorshePrice();
}
interface InteAbsFactory {
    Lada getLada();
    Ferrari getFerrari();
    Porshe getPorshe();
}
class UaLadaImpl implements Lada {// первая
    public long getLadaPrice() {
        return 1000;
    }
}
class UaFerrariImpl implements Ferrari {
    public long getFerrariPrice() {
        return 3000;
    }
}
class UaPorsheImpl implements Porshe {
    public long getPorshePrice() {
        return 2000;
    }
}
class UaCarPriceAbsFactory implements InteAbsFactory {
    public Lada getLada() {
        return new UaLadaImpl();
    }
    public Ferrari getFerrari() {
        return new UaFerrariImpl();
    }
    public Porshe getPorshe() {
        return new UaPorsheImpl();
    }
}// первая
class RuLadaImpl implements Lada {// вторая
    public long getLadaPrice() {
        return 10000;
    }
}
class RuFerrariImpl implements Ferrari {
    public long getFerrariPrice() {
        return 30000;
    }
}
class RuPorsheImpl implements Porshe {
    public long getPorshePrice() {
        return 20000;
    }
}
class RuCarPriceAbsFactory implements InteAbsFactory {
    public Lada getLada() {
        return new RuLadaImpl();
    }
    public Ferrari getFerrari() {
        return new RuFerrariImpl();
    }
    public Porshe getPorshe() {
        return new RuPorsheImpl();
    }
}// вторая

public class AbstractFactoryTest {//тест
    public static void main(String[] args) {
        String country = "UA";
        InteAbsFactory ifactory = null;
        if(country.equals("UA")) {
            ifactory = new UaCarPriceAbsFactory();
        } else if(country.equals("RU")) {
            ifactory = new RuCarPriceAbsFactory();
        }

        Lada lada = ifactory.getLada();
        System.out.println(lada.getLadaPrice());
    }
}

```

# Структурные паттерны

## 1. Адаптер

Адаптер — это структурный паттерн проектирования, который позволяет объектам с несовместимыми интерфейсами работать вместе.

``` java
class PBank {
    private int balance;
    public PBank() { balance = 100; }
    public void getBalance() {
        System.out.println("PBank balance = " + balance);
    }
}
class ABank {
    private int balance;
    public ABank() { balance = 200; }
    public void getBalance() {
        System.out.println("ABank balance = " + balance);
    }
}
class PBankAdapter extends PBank {
    private ABank abank;
    public PBankAdapter(ABank abank) {
        this.abank = abank;
    }
    public void getBalance() {
        abank.getBalance();
    }
}

public class Main {//тест
    public static void main(String[] args) {
        PBank pbank = new PBank();
        pbank.getBalance();
        PBankAdapter abank = new PBankAdapter(new ABank());
        abank.getBalance();
    }
}
```

## 2. Паттерн Компоновщик

Компоновщик — это структурный паттерн проектирования, который позволяет сгруппировать множество объектов в древовидную структуру, а затем работать с ней так, как будто это единичный объект.

``` java
import java.util.ArrayList;
import java.util.List;
interface Car {
    void draw(String color);
}
class SportCar implements Car {
    public void draw(String color) {
        System.out.println("SportCar color: " + color);
    }
}
class UnknownCar implements Car {
    public void draw(String color) {
        System.out.println("UnknownCar color: " + color);
    }
}
class Drawing implements Car {
    private List<Car> cars = new ArrayList<Car>();
    public void draw(String color) {
        for(Car car : cars) {
            car.draw(color);
        }
    }
    public void add(Car s){
        this.cars.add(s);
    }
    public void clear(){
		System.out.println();
        this.cars.clear();
    }
}

public class CompositeTest {//тест
    public static void main(String[] args) {
        Car sportCar = new SportCar();
        Car unknownCar = new UnknownCar();
        Drawing drawing = new Drawing();
        drawing.add(sportCar);
        drawing.add(unknownCar);
        drawing.draw("green");
        drawing.clear();
        drawing.add(sportCar);
        drawing.add(unknownCar);
        drawing.draw("white");
    }
}
```

# Поведенческие паттерны

## 1. Паттерн Наблюдатель

Наблюдатель — это поведенческий паттерн проектирования, который создаёт механизм подписки, позволяющий одним объектам следить и реагировать на события, происходящие в других объектах.

``` java
import java.util.ArrayList;
import java.util.List;
interface Observer {
    void event(List<String> strings);
}
class University {
    private List<Observer> observers = new ArrayList<Observer>();
    private List<String> students = new ArrayList<String>();
    public void addStudent(String name) {
        students.add(name);
        notifyObservers();
    }
    public void removeStudent(String name) {
        students.remove(name);
        notifyObservers();
    }
    public void addObserver(Observer observer){
        observers.add(observer);
    }
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }
    public void notifyObservers(){
        for (Observer observer : observers) {
            observer.event(students);
        }
    }
}
class Director implements Observer {
    public void event(List<String> strings) {
        System.out.println("The list of students has changed: " + strings);
    }
}

public class ObserverTest {//тест
    public static void main(String[] args) {
        University university = new University();
        Director director = new Director();
        university.addStudent("Vaska");
        university.addObserver(director);
        university.addStudent("Anna");
        university.removeStudent("Vaska");
    }
}
```

## 2. Шаблонный метод

Паттерн Шаблонный метод предлагает разбить алгоритм на последовательность шагов, описать эти шаги в отдельных методах и вызывать их в одном шаблонном методе друг за другом.

``` java
abstract class Car {
    abstract void startEngine();
    abstract void stopEngine();

    public final void start(){
        startEngine();
        stopEngine();
    }
}
class OneCar extends Car {
    public void startEngine() {
        System.out.println("Start engine.");
    }
    public void stopEngine() {
        System.out.println("Stop engine.");
    }
}
class TwoCar extends Car {
    public void startEngine() {
        System.out.println("Start engine.");
    }
    public void stopEngine() {
        System.out.println("Stop engine.");
    }
}

public class TemplateTest {//тест
    public static void main(String[] args) {
        Car car1 = new OneCar();
        car1.start();
        System.out.println();
        Car car2 = new TwoCar();
        car2.start();
    }
}
```

