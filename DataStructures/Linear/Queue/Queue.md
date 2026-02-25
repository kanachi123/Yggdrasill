# ***Queue***

## **Очередь - это структура данных,которая работает по FIFO(first in,first out)** обратное LIFO
###### FIFO ,а не FIFA(первым забил гол,первым забил болт)
## так работают кассы или например: расстрелы при сталине:первым пришел,первым ушел

### ~~чтобы не навязались геи с их можем повторить,напомню давно вермахт и ссср развалились~~

### простой пример принтер,ты кидаешь файл первым и он распечатывается первым

### очереди бывают одностороними и двусторонними

### то есть в первом случае добавляем с одной стороны удаляем с другой

![list](https://kroki.io/mermaid/svg/eNpLy8kvT85ILCpR8AniUgCC4tKk9KLEggyFwNLU0lSwEAhkpCamaGh4AElNTbhgqmG0kmtOam5qXolSLELUCKuoMTbRksTMHA2NECAJNTY1L4WLC2ahgq6uHdASCGUEoYzBFEgfWJlLaiHInRoaSlCWkqYmWAVIP1iFax5MBZQFUwEyAwAbh0In)

### в двухстороннем с обоих сторон можно добавлять и удалять
![list](https://kroki.io/mermaid/svg/eNpLy8kvT85ILCpR8AniUgCC4tKk9KLEggwFl9TC0lSwEAikFeXnlWhouIEoTU24cKphtJJrTmpual6JUixC1AirqDE20aLUxCINjSAgCTU2NS-FiwtupYKurh3QFghlBKGMwRRII1idY0qKG8R1SjCmkqYmWA3YCLCioNTc_LJUmDokHqZSoCFBYEcpQVkwJXAbIdqhihAcZHUA3KFdsQ==)


```cpp

namespace my_td
{
    template<typename T>
    struct node{
        struct node<T> *next = nullptr;
        T value;
    };

    template<typename T>
    class FIFO{
        node<T> *front = nullptr;
        node<T> *back = nullptr;
    public:
        FIFO() : front(nullptr), back(nullptr) {}

        ~FIFO() {
            while (!is_empty()) {
                node<T>* tmp = dequeue();
                delete tmp;
            }
        }
        T* peek() const {
            return front ? &(front->value):   nullptr;
        }
        
        node<T> *dequeue(void){
            if(!front)
                return nullptr;
            node<T>* tmp = front;
            front = front->next;
            tmp->next = nullptr;
            return tmp;
            //удаляем с начала
        }
        void enqueue(const T &item){
            node<T>* tmp = new node<T>;
            tmp->value = item;
            tmp->next = nullptr;

            if(!back){
                front = back = tmp;
            }else{
                back->next = tmp;
                back = p;
            }
        }

    };

}
```
