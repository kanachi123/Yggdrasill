# ***Binary Tree***

### **В прошлый раз мы говорили про графы, дерево это частный случай дерева.**
**Бинарное дерево первое по легкости, начнем**


### **Бинарное дерево - это древовидная структура данных,в которой каждая нода имеет не более двух потомков,которые называются левыми и правыми потомками**

![tree](https://i.gifer.com/Bes9.gif)

бинарное дерево курильщика

         Бог
        /   \
    овцы     козлы

бинарное дерево далбоеба

         далбоеб
        /      \ 
     черное     белое

Ян Лукасевич:
-что мне делать я вообще 1/2
бинаршик:
-молчи,либо уходи изучать другие деревья


бинарное дерево политолога
```
              - - - -  бог - - - - - 
           /                          \
    радикально левые           радикально правые- - - - - - - - - 
         /    \                          /                        \          
    сталин     социал демократы     правый либертанианец          гитлер(плохой чиновник)
    /     \                          /      \  
расcтрелять можем повторить      светов       левый либертанианец          /      \
                                                                  вилкой глаз    вж  
                                                                  /        \   
                                       среди вас одноглазых не вижу в тюрьме вилок нет
                                             /        \
     как хочешь мне без разницы куда себе засунешь    спроси у своих друзей,они на опыте
```

бинарное дерево центриста

-мне один биг тейсти,без маянеза,внутри смеш бургер,но добавь листки лазаньи,а на верхушке вишню с молотком

короче система из конечных автоматов ,но ладно это не по теме особо сейчас просто база по дереву(создаешь какое интерактивное кино где у тебя дерево решении короче,или ты хацкер который связал все через maltego и осинтит данные чтобы взломать пентагон)
```
начало
 ├─ пойти налево
 │   ├─ встретил NPC
 │   └─ нашел предмет
 └─ пойти направо
     ├─ ловушка
     └─ выход
```
Так устроены многие интерактивные истории:

Detroit: Become Human

Until Dawn

Там буквально рисуют огромные деревья решений

как автомат будет
```
состояние 0
 ├─ действие A → состояние 1
 │   ├─ действие C → состояние 3
 │   └─ действие D → состояние 4
 └─ действие B → состояние 2
```
 или осинт дерево связей людей или связей данных человека 
```
 человек
 ├─ email
 │   ├─ сайт
 │   └─ аккаунт
 └─ телефон
     └─ соцсеть
```
,но главное у бинарного дерева в узле два потомка

1) нет потомков
   A

2) один потомок(лист мы эту структуру данных уже разбирали)
   A
  /
 B

3) два потомка
   A
  / \
 B   C


## ***теперь нормальное определение бинарного дерева через теорию множеств***

бинарное дерево - это пара множества вершин и множества ориентированных ребер,такая что выполняются условия:T(V,E)
1. есть корень(рут),у которого нет родителя
    $\exists r \in V$  
2. у каждой вершины не более одного родителя
    $\forall v \in V \ {r} \exists! u \in V : (u,v) \in E$
    #### **для любой вершины кроме рута принадлежащей к множеству всех вершин данного дерева существует одна единственная вершина принадлежащая множеству всех вершин данного множества такая что пара этих вершин принадлежит множеству оринтерованных ребер данного множества ребер** *это если читать буквально по кванторам*
3. у любого из вершин не может быть больше двух потомков(по языку теории множеств,мощность любого выборочного подмножества,не больше двух)
    $|{u \in V | (v,u) \in E}| \leq 2$    

впринце я могу писать более академично,педантно,так еще и граматически правильно с пунктуацией и без мата,чтобы не думали что за сапожник,но я дедпул:  
![նստել եմ ծառի տակ,նկարում եմ նապաստակ](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExZnE2c2E1MzFybGh1Mmp0d2V3emhocWpsbDZ0ZG1hdmxjd2k3Yml0biZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/SmgdGLAzMPOUw/giphy.gif)  
##### *նստել եմ binary ծառի տակ,նկարում եմ նապաստակ*

## ***Имплементация***

```cpp

namespace bTree{

template<typename T>
class BinaryTree{
    class Node{
        public:
        T value;
        std::unique_ptr<Node> left;//RAII
        std::unique_ptr<Node> right;
        Node(const T& val) : value(val), left(nullptr), right(nullptr) {}
    };
    std::unique_ptr<Node>root;
    void insertHelper(std::unique_ptr<Node>& node, const T& value);
    Node* searchHelper(Node* node, const T& value) const;
    void removeHelper(std::unique_ptr<Node>& node, const T& value);
    public:
        BinaryTree() : root(nullptr) {}//можно и constructor() = delete;
        BinaryTree(const T& val) : root(std::make_unique<Node>(val)) {}

        BinaryTree(const T& rootVal,const T& leftVal): BinaryTree(rootVal)
        {
            root->left = std::make_unique<Node>(leftVal);
        }
        BinaryTree(const T& rootVal,const T& leftVal,const T& rightVal) : BinaryTree(rootVal, leftVal)
        {
            root->right = std::make_unique<Node>(rightVal);
        }
        Node* getRoot() const { return root.get(); }
        void inorder() const;
        void inorder(Node* node) const;
        bool empty() const {
            return root == nullptr;
        }
        void insert(const T& value);
        Node* search(const T& value) const;
        void remove(const T& value);

};
template<typename T>
void BinaryTree<T>::insertHelper(std::unique_ptr<Node>& node, const T& value)
{
    if (!node)
    {
        node = std::make_unique<Node>(value);
        return;
    }

    if (value < node->value)
        insertHelper(node->left, value);
    else
        insertHelper(node->right, value);
}
template<typename T>
void BinaryTree<T>::insert(const T& value){
    insertHelper(root,value);
}
template<typename T>
Node* BinaryTree<T>::search(const T& value)const{
    return  searchHelper(root.get(),value);
}
template<typename T>
Node* BinaryTree<T>::searchHelper(Node* node,const T& value)const{
    if(!node)//если рут пустой нечего не делаем
        return nullptr;
    else if(value == node->value) //сравниваем ноду с значением если есть совпадение даем указатель на ноду
        return node;
    else if(value < node->value)
        return searchHelper(node->left.get(),value);//левый потомок меньше по значениею родителя
    else{
        return searchHelper(node->right.get(),value);
    }
}

template<typename T>
void BinaryTree<T>::inorderHelper()const{
    if(!node)
        return;
    inorderHelper(node->left.get());
    inorderHelper(node->right.get());
}

template<typename T>
void BinaryTree<T>::inorder()const{
    
    inorderHelper(root.get());
}

template<typename T>
void BinaryTree<T>::removeHelper(std::unique_ptr<Node>& node, const T& value){
    if (!node)
        return;

    if (value < node->value)
    {
        removeHelper(node->left, value);
    }
    else if (value > node->value)
    {
        removeHelper(node->right, value);
    }
    else
    {
        if (!node->left && !node->right)//если нет указателя вообще просто сброс ноды
        {
            node.reset();
            /* 
            эквивалентно{
                            delete node.get();node = nullptr;RAII короче
                        }
             */
        }
        else if (!node->left)//если нет указателя на левую ноду правую ноду переносим на главную(переносим целую ветку из нод под нее)
        {
            node = std::move(node->right);
        }
        else if (!node->right)
        {
            node = std::move(node->left);//переносим значение,мув семантика
        }
        else
        {
            Node* min = node->right.get();

            while (min->left)
                min = min->left.get();

            node->value = min->value;

            removeHelper(node->right, min->value);
        }

    }
}

template<typename T>
void BinaryTree<T>::remove(const T& value){
    
    inorderHelper(root,value);
}
}


```


