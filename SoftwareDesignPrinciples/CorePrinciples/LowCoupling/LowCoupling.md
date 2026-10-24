# LowCoupling 

**Coupling** это связанность компонентов между собой в системе

**Coupling бывает разных видов**
 
 Data,Stamp,Control,External,Common,Content,Temporal,Sequential,Communicational,Functional,Interaction,Component

## **Для начала определение каждого из них потом подробное обяснение**  

Data - это такая связанность при котором два компонента дают только необходимые простые данные(именно простые,то что нужно не больше),чаще всего это low coupling  

Stamp - это такая связанность при котором мы передаем компоненту целую структуру или обьект,хотя нам нужно лишь часть этого компонента  

Control - это такая связанность при котором один компонент дает другому компоненту данные для изменения ее состояния(например дескрипторы,хендлеры,конечные автоматы,перечисления,цепи Маркова)  

External - это такая зависимость при котором компонент зависит от внешнего компонента/элемента изменение которого будет влияет на работу этого компонента(CMakeLists,API,handler files,JSON,http(GET,POST,PUT...))  

Common - это такая связанность при котором несколько компонентов обращаются к данным,которые общие для всех компонентов(Static,global,например при Race condition(Threads with Data Sharing without mutex etc...),json...)  

Content - это такая связанность при котором отдельные компоненты напрямую вмешиваются в внутренности другого компонента(реализации...например нарушение инкапусляции другого компонента вход за защищенные или закрытые области видимости другого объекта без гетеров,ссылок,и указателей итд)  

Temporal - это такая связанность при котором компоненты и их итоговый результат связанны временнем и последовательностью взаимодействия этих компонент между собой(асинхронное программирование,DI,Pipline/Chain of Responsibility,State Machine...)  

Sequentional - это такая связанность при котором результат или состояние компонента связано с результатом прошлого компонента  

Communicational - это такая связанность при котором два или более компонента работают с с одними и теми же данными(но они не всегда глобальны...)  

Functional - это такая связанность при котором несколько компонентов связаны реализацией(функционально изменение реализации одного влияет на другой компонент,функциональное программирование,связанность методов в классах,вложенные методы)  

Interaction - это такая связанность при котором видна степень зависимости между компонентам,которая возникает из-за того,как они взаимодействуют  

Component - это такая связанность при котором видна степень зависимости одного компонента от другого компонента/ов  


![just in time learning](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNnVqOWZhcHdxeDdhOGF4YTkxM3I4bjZxaWo0bzdjbDVobWp3anA2bSZlcD12MV9naWZzX3NlYXJjaCZjdD1n/BX3SQrafxKRielHmM4/giphy.gif)  

## Data coupling

**Она является одной из самых слабых связанностьей,
потому что,мы непосредственно передаем модулю или компоненту нужные данные в прямом виде либо используя интерфейс без зависимости от внутренней релаизации** 

*например f(g(x)) -> return g(x)*

то есть внутренней реализацией они не связаны  

```
то есть нет жесткой связанности через реализацию или через передачу целого компонента как в других связанностях
```  
## Stamp coupling

**здесь передача может быть непрямой и мы входим в внутренную структуру мы берем целую структуру обьект итд и передеаем полностью чтобы взять одну вещь**

-передай гаечный ключ
-а как через data coupling или stamp coupling?
-через Stamp
-вот рюкзак в ней чемодан с гаечным ключем
-тогда data
-вот ключ возьми

```cpp

#include <renderig.hpp>

// mini shit programm,but kiss 

Window window;//global -> Common coupling

class Point{
    int x,y;
    int_32 color;

    public:
    Point()= default;
    //geters,seters
    }

Pair<double,double> move(const &Point point){

    return {++(point.first),++(point.second)}  
}

int main(){

    
    unique_ptr<point> Point;

    while(window.open()){//control coupling

        auto [x,y] = move(Point);//stamp coupling

        //data coupling and stamp coupling
        draw(&window,&x,&y,&shape);
    }
}

```

## Control coupling 

**Есть ситуации когда нужно передать флаг решающий состояние например ивенты или дескрипторы,но через структуры и перечисления удобнее ну либо классы**

```cpp



typedef enum {CREATE,READ,UPDATE,DELETE} CRUD;
class Descriptor{
    CRUD flag;
    public:
    Descriptor()=default;
    CRUD getFlag()const{
        return flag;
    }
    void setFlag(CRUD flag){
        this->flag = flag;
    }
};

class Handler{

    std::unique_ptr<Descriptor> des;
    public:

    Handler(const Descritor& des):des(std::make_unique<Descriptor>(des)){};

    //implemetation CRUD
    //...
    
    void Choice(){
        switch(des->getFlag()){
            case CREATE: Create();break;
            case READ: Read();break;
            case UPDATE: Update();break;
            case DELETE: Delete();break;
            default:break;
        }

    } 

}

```


## External coupling 

```cpp

// simpleFramework.hpp

#pragma once
#include <SimpleFramework.h>

System::System{
        //another metods etc implemetations
}

///-----------///

//in main

#include <Simpleframework.hpp>
#include <nlohmann/json.hpp>

using json = nlohmann::json;

class systemStrategy : public System{ //external coupling
    public:
    void strategy();
}

int main(){
    //...
}
```  

## Common coupling 

//shit code,but a good example...

```cpp

uint8_t r;
uint8_t g;
uint8_t b;
Color::Color buffer[];
static int poopCount = 0;


void update_rgb(const Event& event){

    r = event->getNewR();
    g = event->getNewG();
    b = event->getNewB();
}

class Renderer{
    
    public:
    Renderer(const Window& wind){
        wind->setDisplay(buffer);
        poopCount++;//common coupling

    };
};

class Window{
    
    public:
        Window(){
            poopCount++;
        };

        void update(const Event& event){
            int i = 0;
            for(const auto& it : event){
                update_rgb(event);//common coupling
                buffer[i++] = Color::Pixel(r,g,b);//common coupling
            }
        }
}



```