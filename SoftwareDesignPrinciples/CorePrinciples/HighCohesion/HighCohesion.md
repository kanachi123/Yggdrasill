# High Cohesion

```
Если пишешь модуль,его методы должны относится к одной цели,то есть они
должны быть сильно связаны по цели и релевантности
```  


## *Представим такую ситуацию*

Ты пишешь модуль про рендер численных значении функции и нужно сделать так чтобы было чисто

```cpp

// low cohesion

class renderGraphics{
    std::unique_ptr<WindowRenderer> window;
    std::unique_ptr<Audio> audio;

    public:
    renderGraphics(const WindowRenderer& window)
    {
        
    };

    void clearWindow();
    void drawWindow();
    void displayWindow();
    void startSample();
    void stopSample();

}

```

```
здесь слабая связность потому что в класе рендера есть аудио а оно не связано по цели
лучше отделять на два класса это еще и соответствует SoC
```
```cpp

// high cohesion

class renderGraphics{
    std::unique_ptr<WindowRenderer> window;
    

    public:
    renderGraphics(const WindowRenderer& window)
    {
        
    };

    void clearWindow();
    void drawWindow();
    void displayWindow();

}

class Audio{
    std::unique_ptr<Audio> audio;
    public:
    Audio(const Audio& audio);
    void startSample();
    void stopSample();
}

```

```
здесь уже все сильно связано по цели и каждый из них соответсвтует своей цели
пропадает coupling
```