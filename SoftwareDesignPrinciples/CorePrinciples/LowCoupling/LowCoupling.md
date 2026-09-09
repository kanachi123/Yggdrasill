# LowCoupling 

**Coupling** это связанность компонентов между собой в системе

**Coupling бывает разных видов**
 
 Data,Stamp,Control,External,Common,Content,Temporal,Sequential


## представим такую систему car,engine,wheels 


```cpp

class car{
    std::unique_ptr<Engine> engine;
    std::unique_ptr<Wheels> wheels;
    public:
    car(){};
}


```  




