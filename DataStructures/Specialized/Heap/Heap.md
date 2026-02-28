# ***Heap*** 

## ***Куча - это специализированная структура данных,она описывается как дерево,которое имеет свойства кучи: B узел является потомком узла A(то есть A есть parent B или наоборот B является child of A) при том что f(A) $\ge$ f(B),где k(X) - ключ узла.***

### ***грубо говоря сортируется по максимуму,что больше оно и станет родителем узлов по меньше***
### **короче root это max/min от множества max(value),где value максимально возможное значение нашего множества**
![heap](https://kroki.io/mermaid/svg/eNrjSi9KLMhQCHHhUgACRw0NMwNNTTDbSUPDBMZ21tAwhbFdNDQMYWxXDQ0jGNsNqh5ikIKurp2CExLbGWIomO2CxHaFWABmu3EBAN2hF2M=)

#### ***heap является максимально эффективной реализацией абстрактного типа данных***

#### ***удобно когда работаешьс макисмумами и минимумами в каком множестве значении***

#### ***над кучами можно проводить операции удаления максимума и минимума,поиска максимумов и минимумов, уменьшение/увеличение значения ключ,добавление ключа либо слияния кучей для создания новой кучи как объединение двух сортированнах множеств***

### **heap бывает двух видов**
1. *Max-heap*
2. *Min-heap*

## Min-heap
      2
     / \
    5   8
   / \
  10 12
## Max-heap
      10
     / \
    7   8
   / \
  0   1

#### **обычно хип имплементируют через массивы,хотя кому не лень могут написать свой STL с кучей,я не стану,ибо есть алгоритмический подход,у меня нет столько времени,у нас еще другие папки кроме структур данных**
#### **ps: для heap не использовать adjacencyMatrix позже в асимптотическом анализе расскажу` Big(O)**

### *коротко про алгоритм*
###### **родитель имеет два ребенка один правы другой левый,**
###### ****у зайца два яйца одно левое,другое правое,оба висят на сантиметр ниже ****

##  **Если элемент находится в позиции i, то:**
### *Родитель → (i - 1) // 2*
#### *Правый ребёнок → 2\*i + 2*

```python 
#готовая библиотека
import heapq

heap = []
heapq.heappush(heap, 10)
heapq.heappush(heap, 3)
heapq.heappush(heap, 7)

print(heap)  # [3, 10, 7]
```



```cpp


namespace my_hp{
#include <iostream>
#include <vector>
#include <type_traits>
#include <stdexcept>

    template<typename T>
    class heap{

        std::vector<T> hp;
        void sift_up(size_t index) {
        while (index > 0) {
            size_t parent = (index - 1) / 2;//parent id
            if (hp[index] < hp[parent]) { 
                std::swap(hp[index], hp[parent]);/* меняем родителя и ребенка местами, если родитель больше по значению */
                index = parent;
            } else {
                break;
            }
            /* сортируем так,пока все не будут в своих местах,это будет вызиватся каждый раз,когда пушим новое значение,а чтение уже ваша проблема */
        }
    }

    public:
        heap() = default;
        heap(const T& value){
            push_heap(value);
        }
        void push_heap(const T& value) {
            static_assert(std::is_arithmetic<T>::value, 
                      "T must be a numeric type");
            hp.push_back(value);
            sift_up(hp.size() - 1);
        }
        void pop_heap() {
            if (hp.empty()) return;
            hp.pop_back();/* для этого нужно написать еще sift_down,но мне лень вы как то сами */
        }

        const std::vector<T>& get_heap() const { return hp; }
        T get_value(const size_t& i)const{
            if (i >= hp.size()) throw std::out_of_range("Index out of heap");
            return hp[i];
        } 
    }

    };
}
```


#### **это не по массивам,я просто увлекся**
