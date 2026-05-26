# **QuadTree**

```

QuadTree - это дерево похожее на KD-tree,но в котором у каждого внутреннего узла ровно четыре потомка

```
```
Алгоритм деления (построение квадтри)Базовый узел (Root): Пространство с яблоком целиком помещается в один квадрат.Проверка на однородность: Если квадрат заполнен изображением яблока неравномерно, он делится на 4 равные части: северо-западную (NW), северо-восточную (NE), юго-западную (SW) и юго-восточную (SE).Рекурсия: Каждая из 4 частей проверяется заново. Процесс деления идет до тех пор, пока каждый узел не станет полностью однородным (содержит только цвет яблока или только цвет фона) либо пока не будет достигнут заданный предел.Результат: Яблоко разбивается на сетку из блоков разного размера: более мелкие пиксели окружают контур и детали яблока, а крупные блоки описывают плоские фоновые участки.
```

*это как если у тебя большой шоколад ты делишь ее по ровну для чтереех друзей,но так что они все хотят,чтобы каждый их кусок делилось снова по три части чтобы они дали своим четырем друзьям*
![chocolate](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExb2R3eGY3ODVxNDdrNGFlYTQyM3dxd2o1b2lhb2l0Y2ZoMWx4czF3eiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/l2JhrQPo0u1fZG0O4/giphy.gif)

## **Чанки,LOD,два ствола**

**Разработчики используют квадродерево ландшафта:Корень: Вся карта игры — это один гигантский квадрат.Первое деление: Карта делится на 4 больших квадранта. В трех из них игрока нет (они далеко) — компьютер оставляет их как есть, прорисовывая одной размытой текстурой.Рекурсия: Тот квадрант, где находится ваш самолет, делится еще на 4 квадрата.Глубокая рекурсия: Квадрат прямо под самолетом делится на 4 части, те еще на 4, и так далее, пока под вами не окажутся крошечные квадраты.Итог: Горы вдали выглядят как огромные простые кубы, а трава под ногами разбита на миллионы мелких квадратиков. И все это — одно живое рекурсивное дерево.**

![](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExNHczaDFlcnVmdmV6NXU4ZWw0ZmF6d3U5cG02YWt2ODQyMnNsczl6aSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/B1fLJQIb4G4P6/giphy.gif)

## чанки подгрузка в майнкрафт и колизии в 2д играх

Как Minecraft делит мир на «Чанки» (Стриминг мира)Вы наверняка замечали, что мир в Minecraft бесконечен, но когда вы бежите вперед, он подгружается ровными квадратными блоками. Это и есть работа квадродерева.Как это устроено: Весь мир игры — это один бесконечный квадрат.Логика деления: Игра берет этот квадрат и делит его на 4 огромные части. Вы находитесь в одной из них. Игра берет эту четверть и снова делит на 4 части. И так по цепочке до тех пор, пока мир не разобьется на финальные квадраты 16х16 блоков — чанки (chunks).Зачем это нужно: Компьютер держит в памяти и детально обрабатывает (рост травы, движение зомби) только те мелкие квадраты, которые находятся вокруг вас. Квадраты, которые от вас далеко, квадродерево «схлопывает» обратно в один большой неактивный кусок, чтобы ваш ПК не сгорел от перегрузки.


![](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExb2tsNG02NWs0NjNoeDY5MWlsaWpmdmY0cG9uNWRzbXR0OGRjdnRnZiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/2CNIgAtDDaShxvix7E/giphy.gif)

Vampire Survivors (или любая «выживалка» против толпы монстров)В Vampire Survivors на вас одновременно бегут 5 000 зомби, летучих мышей и скелетов. При этом ваш персонаж постоянно стреляет во все стороны магией.Проблема: Как игре понять, какая молния в какого конкретно зомби попала, если их на экране тысячи?Решение через квадродерево: Экран мгновенно делится на 4 больших квадранта (Верхний-Левый, Верхний-Правый, Нижний-Левый, Нижний-Правый).Если вы запустили огненный шар строго вправо, игра смотрит на квадродерево и сразу выкидывает из расчетов левую половину экрана. Там монстров проверять вообще не нужно.Правую половину экрана игра рекурсивно делит на 4 части, потом еще на 4, пока не найдет тот самый маленький квадратик пространства, где физически столкнулись ваш огненный шар и текстура монстра.Благодаря этому игра легко просчитывает тысячи попаданий в секунду даже на слабом смартфоне.

например rougelike игры
![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*5T_f5FYGh14bJSrs7N3ULQ.gif)

**Шутеры на гигантских картах (PUBG / Warzone) — Слышимость звуковКогда на огромной карте играют 100 человек, сервер должен постоянно решать: кто из игроков слышит этот конкретный выстрел?Перебирать всех 100 игроков и считать расстояние до каждого — долго.Сервер делит карту на 4 части. Выстрел произошел в верхнем правом квадрате? Игроки из остальных трех квадратов сразу отсекаются — звук до них точно не долетит.Верхний правый квадрат делится дальше, пока сервер не найдет мелкие квадраты с игроками, которые сидят в соседних домах от стрелка. Им звук отправляется в первую очередь.**
![](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExeHdjMWxsZGhrdnZocWg1OXZka25vMnBsYjR4d25sMGNxZDgwYzdpMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/30n5IcdZkkuvLfYmR0/giphy.gif)

**Культовая стратегия Spore — Космический масштабПомните этап «Космос» в Spore, где вы можете отдалить камеру от одной планеты до масштаба целой галактики с миллионами звезд? Это классический Quadtree в 3D (октодерево, но принцип тот же).Когда вы смотрите на галактику, она разбита на 4 больших сектора. Каждый сектор — это просто одна светящаяся точка (туманность).Вы приближаете камеру к одному сектору — игра делает split() (деление на 4), и туманность распадается на 4 группы звездных систем.Приближаете еще ближе — конкретная группа делится, и перед вами появляются физические планеты. Игра загружает данные только по мере углубления в рекурсию.**


## quad_tree

```cpp

namespace quad{



class QuadTree{
        class Node{
            std::unique_ptr<Node> northWest;
            std::unique_ptr<Node> northEast;
            std::unique_ptr<Node> southWest;
            std::unique_ptr<Node> southEast;
            //можно обобщать через 

            /*
                template<size_t N>
                std::array<std::unique_ptr<Node>, N> children;
                enum Quadrant {
                    NW,
                    NE,
                    SW,
                    SE
                };
                
                Node<T, 2>  binary
                Node<T, 4>  quad
                Node<T, 8>  oct 
            */
            /* но это квадтри по этому не к месту,мы же обсуждаем частный случай,иначе пришлось бы удалить папку по octTree */

            std::vector<std::any> objects;//хранение любых типов в одном векоре

            /*
                как доставать...
                auto& value = std::any_cast<MyClass&>(objects[i]); 
                
                */
            public:
            Node():northWest(nullptr),northEast(nullptr),southWest(nullptr),southEast(nullptr) {}
            Node()    
        }


}

}


```


## quad_tree_colision


мини программа колизии на SFML

[эту написал когда то хз когда вот ссылка](https://github.com/kanachi123/SFML-projects/blob/main/quad_tree_collision)

```cpp

//crpo.h

#pragma once

#include <iostream>
#include <string>
#include <sstream>
#include <cmath>

const double PI = 3.14;

std::ostringstream out;

class Point {
    double _x = 0, _y = 0;
public:
    Point(double x = 0, double y = 0) : _x(x), _y(y) {}

    Point& setX(double x) { _x = x; return *this; }
    double getX() const { return _x; }
    Point& setY(double y) { _y = y; return *this; }
    double getY() const { return _y; }

    Point& operator++() { ++_x; ++_y; return *this; }
    Point operator++(int) { Point temp = *this; _x++; _y++; return temp; }
    Point& operator--() { --_x; --_y; return *this; }
    Point operator--(int) { Point temp = *this; _x--; _y--; return temp; }

    Point operator+(const Point& other) const { return Point(_x + other._x, _y + other._y); }
    Point operator-(const Point& other) const { return Point(_x - other._x, _y - other._y); }
    Point& operator+=(const Point& other) { _x += other._x; _y += other._y; return *this; }
    Point& operator-=(const Point& other) { _x -= other._x; _y -= other._y; return *this; }
    bool operator==(const Point& other) const { return _x == other._x && _y == other._y; }
    bool operator!=(const Point& other) const { return !(*this == other); }
    bool operator>(const Point& other) const { return std::hypot(_x, _y) > std::hypot(other._x, other._y); }
    bool operator<(const Point& other) const { return std::hypot(_x, _y) < std::hypot(other._x, other._y); }
    bool operator>=(const Point& other) const { return *this == other || *this > other; }
    bool operator<=(const Point& other) const { return *this == other || *this < other; }

    friend std::istream& operator>>(std::istream& in, Point& point);
    friend std::ostream& operator<<(std::ostream& os, const Point& point);
};

std::istream& operator>>(std::istream& in, Point& point) {
    in >> point._x >> point._y;
    return in;
}

std::ostream& operator<<(std::ostream& os, const Point& point) {
    os << "(" << point._x << " , " << point._y << ")" << std::endl;
    return os;
}

class circle {
public:
    circle() : pos(new Point()), radius(1) { _count++; }
    circle(double radius) : circle() { std::cout << "circle count updated\ncount = " << get_count() << std::endl << std::endl; this->radius = (radius > 0) ? radius : 1; }
    circle(double x, double y, double radius) : circle(radius) { pos->setX(x).setY(y); }
    circle(const circle& other) : pos(new Point(*(other.pos))), radius(other.radius) { _count++; }
    ~circle() { delete pos; _count--; std::cout << "circle has been deleted" << std::endl; }

    circle& setPos(const Point&);
    Point getPos() const;
    circle& setRadius(double);
    double getRadius() const;
    static int get_count() { return _count; };
    std::string info()const;
    circle& setPoint(const Point& p) { pos->setX(p.getX()).setY(p.getY()); return *this; };
    Point getPoint()const { return *pos; };
    circle& operator =(const circle& other) { if (this != &other) { *pos = *(other.pos); radius = other.radius; } return *this; }
    friend double getArea(const circle& c);
    friend std::istream& operator>>(std::istream& in, circle& c);
    friend std::ostream& operator<<(std::ostream& os, const circle& c);
private:
    Point* pos;
    double radius = 2;
    int static _count;
};

std::istream& operator>>(std::istream& in, circle& c) {
    double x, y;
    in >> x >> y;
    c.setPos(Point(x, y));
    return in;
}
std::ostream& operator<<(std::ostream& os, const circle& c) {
    os << "(" << c.getPos().getX() << " , " << c.getPos().getY() << ")" << std::endl;
    return os;
}

int circle::_count = 0;

circle& circle::setPos(const Point& p) {
    delete pos;
    pos = new Point(p.getX(), p.getY());
    return *this;
}
Point circle::getPos()const { return *pos; }
double circle::getRadius()const { return radius; }
std::string circle::info() const {
    out << "circle info\n\nradius = " << radius << "\nx = " << pos->getX() << "\ny = " << pos->getY() << std::endl << std::endl;
    std::string result = out.str();
    return result;
}
circle& circle::setRadius(double radius) { this->radius = radius; return *this; }
bool isPoint(const Point& point, const circle& pos, double radius) {
    double dx = point.getX() - pos.getPos().getX();
    double dy = point.getY() - pos.getPos().getY();
    return (dx * dx + dy * dy == radius * radius);
}
double getDistance(const circle& c1, const circle& c2) {
    double dx = c2.getPos().getX() - c1.getPos().getX();
    double dy = c2.getPos().getY() - c1.getPos().getY();
    return std::sqrt(dx * dx + dy * dy);
}
int number_of_intersections(const circle& c1, const circle& c2) {
    double d = getDistance(c1, c2);
    double r1 = c1.getRadius();
    double r2 = c2.getRadius();
    if (d > r1 + r2 || d < std::abs(r1 - r2))
        return 0;
    else if (std::abs(d - (r1 + r2)) < 1e-6 || std::abs(d - std::abs(r1 - r2)) < 1e-6)
        return 1;
    else
        return 2;
}
double getLength(const circle& c) { return 2 * PI * c.getRadius(); }
double getArea(const circle& c) { return PI * std::pow(c.radius, 2); }
void setNewX(circle& c, double len) {
    Point p = c.getPos();
    p.setX(p.getX() + len);
    c.setPos(p);
}
void setNewY(circle& c, double len) {
    Point p = c.getPos();
    p.setY(p.getY() + len);
    c.setPos(p);
}
void setNewSize(circle& c, double k) { c.setRadius(k); }

```
```cpp

//main.cpp
#include "crpo.h"
#include <SFML/Graphics.hpp>
#include <cstdlib>
#include <ctime>
#include <iostream>
#include <vector>

using namespace sf;
using namespace std;

const int N = 1000;
const int WINDOWSIZE = 800;

struct particle {
  circle back;
  CircleShape front;
  double mass = 0.001;
  float vx = 0, vy = 0;
};

struct Quadtree {

    float x, y, width, height;
    int capacity;
    vector<particle*> particles;
    bool divided = false;
    Quadtree *nw = nullptr, *ne = nullptr, *sw = nullptr, *se = nullptr;

    Quadtree(float x_, float y_, float w_, float h_, int cap = 4)
        : x(x_), y(y_), width(w_), height(h_), capacity(cap) {}

    ~Quadtree() {
        delete nw; delete ne; delete sw; delete se;
    }

    bool contains(const particle& p) const {
        float px = p.back.getPoint().getX();
        float py = p.back.getPoint().getY();
        return (px >= x && px < x + width && py >= y && py < y + height);
    }

    void subdivide() {
        float hw = width / 2, hh = height / 2;
        nw = new Quadtree(x, y, hw, hh, capacity);
        ne = new Quadtree(x + hw, y, hw, hh, capacity);
        sw = new Quadtree(x, y + hh, hw, hh, capacity);
        se = new Quadtree(x + hw, y + hh, hw, hh, capacity);
        divided = true;
    }

    void insert(particle* p) {
        if (!contains(*p)) return;
        if (particles.size() < capacity) {
            particles.push_back(p);
        } else {
            if (!divided) subdivide();
            nw->insert(p); ne->insert(p); sw->insert(p); se->insert(p);
        }
    }

    void query(float qx, float qy, float qr, vector<particle*>& found) const {
        
        if (qx + qr < x || qx - qr > x + width || qy + qr < y || qy - qr > y + height)
            return;
        for (auto* p : particles) {
            float px = p->back.getPoint().getX();
            float py = p->back.getPoint().getY();
            float dx = px - qx, dy = py - qy;
            if (dx * dx + dy * dy <= qr * qr)
                found.push_back(p);
        }
        if (divided) {
            nw->query(qx, qy, qr, found);
            ne->query(qx, qy, qr, found);
            sw->query(qx, qy, qr, found);
            se->query(qx, qy, qr, found);
        }
    }
};

void updatePosition(vector<particle> &shape, Quadtree& qtree) {
    
    for (int i = 0; i < N; i++) {
        setNewX(shape[i].back, static_cast<double>(shape[i].vx));
        setNewY(shape[i].back, static_cast<double>(shape[i].vy));
    }

    for (int i = 0; i < N; i++) {
        vector<particle*> neighbors;
        float radius = static_cast<float>(shape[i].back.getRadius()) * 2.0f;
        qtree.query(
            shape[i].back.getPoint().getX(),
            shape[i].back.getPoint().getY(),
            radius,
            neighbors
        );
        for (auto* other : neighbors) {
            if (other == &shape[i]) continue;
            if (other < &shape[i]) continue;                       
            if (getDistance(shape[i].back, other->back) < shape[i].back.getRadius() + other->back.getRadius()) {
                
                shape[i].vx *= -1.f;
                shape[i].vy *= -1.f;
                other->vx *= -1.f;
                other->vy *= -1.f;
                
            }
        }
    }
    
    for (int i = 0; i < N; i++) {
        float x = shape[i].back.getPoint().getX();
        float y = shape[i].back.getPoint().getY();
        
        float r = static_cast<float>(shape[i].back.getRadius());
        if (x - r < 0 || x + r > WINDOWSIZE) shape[i].vx *= -1.f;
        if (y - r < 0 || y + r > WINDOWSIZE) shape[i].vy *= -1.f;
    }

    for (int i = 0; i < N; i++) {
        shape[i].front.setPosition(
            static_cast<float>(shape[i].back.getPoint().getX()),
            static_cast<float>(shape[i].back.getPoint().getY()));
    }
}

void initParticle(vector<particle> &shape) {
  srand(static_cast<unsigned int>(time(nullptr)));

  for (int i = 0; i < N; i++) {
    CircleShape tmp;
    circle c(2);
    particle p;
    c.setPoint(Point(rand() % 800, rand() % 800));
    Vector2f position(static_cast<float>(c.getPos().getX()),
                      static_cast<float>(c.getPos().getY()));

    tmp.setFillColor(Color(rand() % 255, rand() % 255, rand() % 255));
    tmp.setOutlineColor(Color(rand() % 255, rand() % 255, rand() % 255));
    tmp.setRadius(static_cast<float>(c.getRadius()));
    tmp.setPosition(position);

    p.back = c;
    p.front = tmp;
    p.mass = static_cast<double>(rand() % 200+1);
    p.vx = static_cast<float>(rand()%50);
    p.vy = static_cast<float>( rand()%50);

    shape.push_back(p);
  }
}

int main() {
    RenderWindow window(VideoMode(WINDOWSIZE, WINDOWSIZE), "project 4");
    vector<particle> shape;

    initParticle(shape);

    while (window.isOpen()) {
        Quadtree qtree(0, 0, WINDOWSIZE, WINDOWSIZE);

        for (int i = 0; i < N; i++) {
            qtree.insert(&shape[i]);
        }

        Event event;
        while (window.pollEvent(event)) {
            if (event.type == Event::Closed) {
                window.close();
            }
        }
        window.clear(Color::White);
        for (int i = 0; i < N; i++) {
            window.draw(shape[i].front);
        }
        updatePosition(shape, qtree);
        window.display();
    }
}
```

