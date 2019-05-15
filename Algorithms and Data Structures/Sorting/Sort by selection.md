# Сортировка выбором

Сортировка выбором представляет собой механизм сортировки, который начинается с поиска наименьшего элемента в массиве и размешение его первым.
Затем находится второй наименьший элемент и размещается вторым, и так до тех пор пока весь массив не отсортируется.

``` java
 public static void selectionSort(int mass[]) {
        for (int i = 0; i < mass.length; i++) {
            int min = mass[i];
            int min_index = i;
            for (int j = i + 1; j < mass.length; j++) {
                if (mass[j] < min) {
                    min = mass[j];
                    min_index = j;
                }
            }
            if (i != min_index) {
                int tmp = mass[i];
                mass[i] = mass[min_index];
                mass[min_index] = tmp;
            }
        }
    }
```

* Время выполнения О(n^2).

![](https://hsto.org/getpro/habr/post_images/195/e1f/6a1/195e1f6a1379554ca9025338301a78ed.png)