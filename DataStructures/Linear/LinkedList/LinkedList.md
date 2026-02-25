# ***LinkedList***

## Связанный список - это структура данных которая является динамичной.
### Она состоит из узлов(Nodes) которые хранят в себе значения(data/value)
### и ссылки(связи смотреть на одномерные простые графы,но это потом когда будем разбирать графы,а пока просто указатели на следующий или предыдущий нод/узел)

### порядок элементов связного списка может не совпадать с порядком расположения элементов данных в памяти компьютера,
### **а порядок обхода списка всегда явно задаётся его внутренними связями**

![list](https://kroki.io/mermaid/svg/eNptj08LgkAQxe9-ikEJCvSg3hQ6eegQBl2jw9SuObTsijv2jz58u1p0cS4z8HtveO_SY9fCdh-Am8UCKtmQJn0BbYS0cCduQSAjoBag5YOhM6RZ9qNhI1FAkqyhTg9h5WVvqJ0oPI64TieYzcJsgvkszCc4KLVchn6Fq1XwC7nrmIxGBZafyodtTA8nyS4W3MgOqOiFXjIazgqtdb3GStCQUkXU-Ikt9-YqiyhN8--d3ElwW2Tdo_x7XY-4zmKXyX8ogw8UJltR)

```python

class Node:
    def __init__(self, data):
        self.data = data  # Данные
        self.next = None  # Ссылка на следующий узел

```

### Двусвязный список (Doubly Linked List)

### Узел хранит ссылки на следующий и предыдущий узлы.

### Можно проходить список в обе стороны.
### Пример:
   
   ![list](https://kroki.io/mermaid/svg/eNptjzFrwzAQhXf_iodDIAF7sL05pVOGDMGBrqXDtZLjo0Iy1iV2S398JeHSJbfcwffe8d51onHA-SVDmO0WR92zZXuFdUp7zCwDFAmBrILVi2B0bEVPyXDSpPBUls_oqtf8GHU_6IIqf0u8q1ZaP6T1SpuHtEGCN2N2uzyufL9PJPsLexmFnSUDL18mhu7dhHctIR7u7G9k-JuiJBk-DHkf-qVq6NmYdtPHKbxM7lO3m6pq1rucWcnQ1uNy-PeGOkVXFyFY_HDIfgE78FyP)

### Циклический список (Circular Linked List)

### Последний узел ссылается на первый, образуя круг.

### Может быть односвязным или двусвязным.

![list](https://kroki.io/mermaid/svg/eNptj7EOgjAQhnee4iJhgwHYMHFicDCYuBqH0xa42LSEnoLGh7ctGhdvuuT7_8t33YhDD7tDBG6SBGrZkibdgTZCWpiIexDICKgFaDkzDIY0yzEUthIFZNkGmvy4qn3sBY0LrU4BN_kCi7-wWGD5F5YB-vtR9HXbD0xGowLLD-UdWzPCWbKzgTvZGyp6oo-EwkWhte6d8Am0pFQVt35Sy6O5yirO8_KzZxMJ7qtimNe_rtNPmyJ1Kv7COnoDCzRYsQ==)

```python

# Создание узлов
node1 = Node("A")
node2 = Node("B")
node3 = Node("C")

# Связываем узлы
node1.next = node2
node2.next = node3

# Обход списка и печать данных
current = node1
while current:
    print(current.data)
    current = current.next

```

## кстати по сути jnz,jmp,while итд можно описать как цикличный связанный список

### **по сути стек,очереди,деревья итд можно описать через связанные списки**


//это есть и в старой репозитории мне лень имплементировать заного вот через метапрограммирование...через шаблоны
```cpp

#include <iostream>
using namespace std;
template<typename T>
struct ListNode
{
    T val;
    ListNode* next;
    ListNode(T _val) : val(_val), next(nullptr) {}
};

template<typename T>
struct List
{
    ListNode<T>* firstNode;
    ListNode<T>* lastNode;
    
    List() : firstNode(nullptr), lastNode(nullptr) {}
    ~List() {
        ListNode<T>* p = firstNode;
        while (p) {
            ListNode<T>* tmp = p;
            p = p->next;
            delete tmp;
       }
    }

    bool isEmpty()
    {
        return firstNode == nullptr;
    }

    void push_back(T _val)
    {
        ListNode<T>* p = new ListNode<T>(_val);
        
        if (isEmpty()) 
        {
            firstNode = p;
            lastNode = p;
        } 
        else 
        {
            lastNode->next = p;
            lastNode = p;
        }
    }
    
    inline ListNode<T>* getFirstNode(){
        return firstNode;
    }
    
    
    inline ListNode<T>* getLastNode(){
        return lastNode;
    }

    void print() 
    {
        if (isEmpty()) 
        {
            return;
        }
        
        ListNode<T>* p = firstNode;
        std::cout << p->val;
        p = p->next;

        while (p != nullptr) 
        {
            std::cout << "->" << p->val;
            p = p->next;
        }
        
        std::cout << std::endl;
    }
};

int main() 
{
    List<int> l1,l2,l3;
    size_t m;
    
    cout<<"list size"<<endl;
    cin>>m;
    
    for (size_t i = 0; i < m; i++)
    {
        l1.push_back(rand()%9);
        l2.push_back(rand()%9);
    }
    {
    
    	ListNode<int>* p1=l1.getFirstNode();
    	ListNode<int>* p2=l2.getFirstNode();
    	
    	int curr = 0;
    	for(size_t i = 0;i<m;i++)
    	{
    		int tmp = 	p1->val+p2->val+curr;
    		if(tmp/10==0){
    		    l3.push_back(tmp);
    		    curr = 0;
    		    
    		}
    		else
    		{
    		    l3.push_back(tmp%10);
    		    curr++;
    		}
    		p1=p1->next;
    		p2=p2->next;
        
    	}
    }
    
    l1.print();
    l2.print();
    l3.print();

    return 0;
}

```
