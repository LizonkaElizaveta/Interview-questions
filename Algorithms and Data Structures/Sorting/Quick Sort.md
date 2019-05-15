# Быстрая сортировка

Алгоритм быстрой сортировки является одним из самых быстрых алгоритмов сортировки. Суть алгоритма заключается в следующем : берется некоторый элемент массива(желательно средний эелемент); элементы, которые находятся слева и больше по значению чем первоначальный, меняются местами с элементами, которые находятся справа и меньше первоначального. Аналогичная операция выполняется для наборов данных слева и справа от начального. И так далее по рекурсии.

``` java
public static void quickSort(int[] array, int low, int high) {
    if (array.length == 0) {
         return;
    }
    if (low >= high) {
        return;
    }
    int middle = (low + high) / 2;
    int oppora = array[middle];

    int i = low, j = high;
    while (i <= j) {
        while (array[i] < oppora) {
            i++;
        }

        while (array[j] > oppora) {
            j--;
        }

        if (i <= j) {
            int temp = array[i];
            array[i] = array[j];
            array[j] = temp;
            i++;
            j--;
        }
    }
    if (low < j) {
        quickSort(array, low, j);
    }
    if (high > i) {
        quickSort(array, i, high);
    }
}
```

* Среднее время выполнения быстрой сортировки составляет O(n*log n)
* В худшем случае быстрая сортировка работает за время O(n^2)
![](https://hsto.org/getpro/habr/post_images/195/e1f/6a1/195e1f6a1379554ca9025338301a78ed.png)