## **Массив - это стуктура данных которая является упорядоченным набором однотипных элементов/данных,которые хранятся в памяти непрерывно один за другим**

### **доступ к этим элементам осуществляется быстро по индексу который обычно начинается с 0,либо через имя самого массива,который является указателем на начало области массива суммируя по шагу к нужной(асемблер или си подобные языки)**


### **Массивы бывают нескольких видов:**
    1. _одномерные_ 
    2. _двумерные(матрицы)NxN не перепутать с NxM_ 
    3. _многомерные_ 



```cpp
int main(){
    
    constexpr size_t size = 0b11111110011;//число 2033 чтобы понтоватся что можно писать не как эти нубы а можешь через двоичку
    int array[size]{0};

    std::cout<<array[0]<<"="<<*array<<std::endl;//можно как через имя потому что указатель так и через []
    
    void* ptr = array;
    int step = 4;
    //ptr = ptr + step <=> array[4] равносильно потому что имя массива и есть указатель на область памяти

    constexpr size_t rows = 0xFFA65;//16ричное
    constexpr sizt_t cols = 0234342;//8ричное 
    int array[rows][cols]{0};

    //например

    //array[i][j] <=> *(array + j + i * cols) <=> array[i * cols + j]
    //...
    //array[i][j][k]...[n-1] <=> array[i1×(d2×d3×⋯×dn)+i2×(d3×⋯×dn)+...+in-1]

}
```

Массив как пространство $R^n$

a[i][j][k] это пространство размерности $$R^3$$  

Каждый элемент многомерного массива можно рассматривать как элемент некоторого многомерного пространства, где его координаты соответствуют индексам массива.

##**массивы бывают по размеру статичными и динамичными**

```cpp


    constexpr size_t size = 0;
    
    std::vector<int> array;//нефиксировно т.е. динамично
    std::array<int,size> a;//фиксировано т.е. статично

    for(int i = 0;;i++)
        array.resize(i);
    
    delete[] array;
    delete[] a;


    return BULLSHIT;


```


##экскурс немного по разным штукамв разных языках программирования

```cpp
int arr[5] = {1, 2, 3, 4, 5};  // Массив инициализируется значениями
int arr[5] = {1, 2};  // Только первые два элемента будут инициализированы, остальные будут равны 0
std::vector<int> vec = {1, 2, 3, 4, 5};
std::vector<int> vec(size, value);  // Все элементы вектора будут равны value

```

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {5, 2, 9, 1, 5, 6};
    
    std::sort(vec.begin(), vec.end());  // Сортируем элементы вектора

    for (int num : vec) {
        std::cout << num << " ";
    }

    return 0;
}
```


```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    auto it = std::find(vec.begin(), vec.end(), 3);  // Ищем элемент в векторе

    if (it != vec.end()) {
        std::cout << "Found 3 at position " << std::distance(vec.begin(), it) << std::endl;
    } else {
        std::cout << "3 not found" << std::endl;
    }

    return 0;
}
```


#немного python если забудете можн использовать как бы мини шпаргалка

```python

import array

# Создание массива
my_array = array.array('i', [1, 2, 3, 4, 5])  # 'i' означает целые числа (int)

# Доступ к элементам
print(my_array[0])  # 1
print(my_array[-1])  # 5

# Добавление элемента
my_array.append(6)
print(my_array)  # array('i', [1, 2, 3, 4, 5, 6])

# Удаление элемента
my_array.remove(4)
print(my_array)  # array('i', [1, 2, 3, 5, 6])

# Изменение элемента
my_array[2] = 10
print(my_array)  # array('i', [1, 2, 10, 5, 6])

arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
sum_arr = arr1 + arr2  # Сложение массивов
print(sum_arr)  # [5 7 9]

arr = np.array([[1, 2], [3, 4]])
print(arr.shape)  # (2, 2) - размерность массива
print(arr[0, 1])  # 2 - доступ к элементам двумерного массива

```