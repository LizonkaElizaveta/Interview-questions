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

![](https://hsto.org/getpro/habr/post_images/195/e1f/6a1/195e1f6a1379554ca9025338301a78ed.png)

* Бинарный поиск работает ТОЛЬКО в отсортированном списке.