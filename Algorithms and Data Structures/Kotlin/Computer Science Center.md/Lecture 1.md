# Лекция 1. Основы Kotlin.

## val/var

```kotlin
fun main(args: Array<String>) {
    require(args.size > 0)
    val firstName:String = args[0]
    var lastName = args[args.lastIndex]
    lastName = "Not Akhin"
    println("Hello, $firstName $lastName)
}
```
- обратная аннотация, тип следует после двоеточия;
- функция через fun;
- requere - говорит, что у этой фунции есть какой-то precondition, если условие не выполнятеся выбрасывается IllegalArgumentException;
- val - неизменяемая переменная(в Java как final);
- var - изменяемая переменная;
- имеется вывод типов, поэтому присваивание типу необязательно;
- $ используется вместо + в строках;

## Nullability

```kotlin
fun getFirstName(names:Arrays<String>): String? {
    if (args.size > 0) return args[0]
    else return null
}

// fun getFirstName(names:Arrays<String>): String? {
//    return if (args.size > 0) args[0]
//           else null
//}

fun getLastName(names:Arrays<String>): String? {
    if (args.size > 1) return args[args.lastIndex]
    else return null
}
```
- String? - это return String либо null;
- если написать String? =, то можно выбросить return из кода;
- если функция ничего не возращает -  пишем unit;

```kotlin
fun main(args: Array<String>) {
    val firstName = getFirstName(args) ?: "John"
    var lastName = getLastName(args) ?: "Doe"
    println("Hello, $firstName $lastName)
}
```
- ?: - если не null, компилятор возращает значение, иначе то, что стоит справа;

## Smart Casts

```kotlin
fun shorten(name: String?): String {
   if (true == name?.isNotEmpty()) {
       return name!!.get(0) + "."
   } else {
        return ""
    }
}

// fun shorten(name: String?) = 
//   if (true == name?.isNotEmpty()) "${name[0]}."
//   else ""

```
- если тип переменной заканчивается ? - Kotlin не позволяет вызвать метод просто так, предлагает использовать save-call оператор(?.). Это позволяет работать с цепочкой данных
- !! делает из Тип? - Тип
- null не равен true/false;
- благодаря smart casts можно name!!.get(0) написать как name[0];

## When

``` kotlin
fun honorify(sex:Sex, maritalStatus: MaritalStatus) = 
    when(Pair(sex,maritalStatus)) {
        Pair(Sex.Male,MaritalStatus.Married),
         Pair(Sex.Male,MaritalStatus.Unknow) -> "Mr."
         else -> throw IllegalArgumentException 
         ("unknow combination of ($sex, $maritalStatus)")
    }
 
 // import Sex.Male 

 // fun honorify(sex:Sex, maritalStatus: MaritalStatus) = 
 //   when(sex to maritalStatus) {
 //       Male to Married, 
 //        Male to Unknow -> "Mr." 
 //    }



 // import Sex.Male as M

 // fun honorify(sex:Sex, maritalStatus: MaritalStatus) = 
 //   when(sex to maritalStatus) {
 //        M to MM
 //        M to UM -> "Mr."
 //    }

```
- when - это switch в Java, если выполнилось одно условие - остальные не выполняются;
- для создания пары используется to;
- as для создания псевдонима;
- в string interpolation можно написать функцию так:
``` kotlin
println("Hello, ${honorify(sex,maritalStatus)} + ${shorten(firstNmae)} $lastName")
```

## Loops

``` kotlin
fun main(args:Array<String>) {
    for(arg in args) {
        val info = arg.split(" ")
        println(buildGreeting(info))
    }
}

// fun main(args:Array<String>) {
//    for(i in 0..args.lastIndex) {
//        val info = args[i].split(" ")
//        println(buildGreeting(info))
//    }
//}

// fun main(args:Array<String>) {
//    for(i in 0 until args.size) {
//        val info = args[i].split(" ")
//        println(buildGreeting(info))
//    }
//}

// fun main(args:Array<String>) {
//    for(i in args.indices) {
//        val info = args[i].split(" ")
//        println(buildGreeting(info))
//    }
//}


```
- реализации цикла forEach выше;
- для счетчиков используется ..args.lastIndex, until или args.indices, все эти операторы не включают последний элемент;
- while и do-while как в Java;

## Types
- все типы являются объектами;
- примитивные типы при необходимости "боксятся";
- у всего могут быть методы, поля и свойства;
- объекты сравниваются на структурное равенство при помощи ==;

## Equals
``` kotlin
fun main(args: Array<String>) {
    val a: Int? = 127
    val b: Int? = 127
    println(a===b)} // output: true

// fun main(args: Array<String>) {
// val a: Int? = 128
// val b: Int? = 128
// println(a===b) } 
// output: false
```
- ссылочное равенство можно проверить через ===;
- из-за боксинга возможны сюрпризы;

## Numbers
- обычные числа из Java(Byte, Int, Short, Long, Float,Double);
- нет неявного преобразования типов;

## Arrays
``` java
final String[] oops = {"only", "strings", "here"};
final Object[] yeah = oops; // Impossible in Kotlin
yeah[1] = 42;
```
- массивы инвариантны по типу хранимого объекта;

``` kotlin 
val fibs = arrayOf(1,1,2,4,5,6)
val sqrt = Array(7) {i -> i*i}
val fastFibs = intArrayOf(1,2,6,7)
```
- для создания массивов используются builder-ы(arrayOf), для создания более конкретных массивов - intArrayOf;





