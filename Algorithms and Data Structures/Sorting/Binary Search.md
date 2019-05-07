# Бинарный поиск

Бинарный поиск - это алгоритм для поиска в элементах. Бинарный поиск работает только в том случае, если список отсортирован.

``` java
int binarySearch(int search, int mass[], int len) {
        int low, high, middle;
        low = 0;
        high = len - 1;
        while (low <= high) {
            middle = (low + high) / 2;
            if (search < mass[middle]) {
                high = middle - 1;
            } else if(search > mass[middle]){
                low = middle + 1;
            }
            else return middle;
        }
        return -1;
    }
```

* Бинарный поиск работает намного быстрее простого.
* Время выполнения О(log n), а с увеличением размера списка, в котором ищется значение, оно становится намного быстрее.

![](https://old.yotx.ru/graph.ashx?clr0=ff0000&exp0=log%28x%3B3%29&mix=0&max=100&asx=on&u=mm&nx=x&aiy=on&asy=on&ny=y&iw=600&ih=400&ict=png&aa=on)

* Бинарный поиск работает ТОЛЬКО в отсортированном списке.