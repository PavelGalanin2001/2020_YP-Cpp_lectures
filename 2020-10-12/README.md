```cpp
#include <iostream>
using namespace std;

class X
{
protected:
    int a;
public:
    X()
    {
        cout << "X";
        a = 10;
    }
};

class Y
{
protected:
    int b;
public:
    Y()
    {
        cout << "Y";
        b = 20;
    }
};

class Z: public X, public Y
{
public:
    Z()
    {
        cout << "Z"; 
    }
    int make_ab()
    {
        return a * b;
    }
};

int main()
{
    Z i;
    cout << i.make_ab();
    return 0;
}
```

Console:

```
XYZ200
```

Вывод происходит, так как происходит множественное наследование и содержит конструкторы по умолчанию.

<div style="page-break-after: always;"></div>

# Виртуальные базовые класса

В С++ ключевое слово `virtual` используется для объявления виртуальный функций, которые переопределяются производных класса. Также ключевое слово `virtual` позволяет определить виртуальные базовые класса.

Пример:

```cpp
#include <iostream>
using namespace std;

class Base
{
public:
    int i;
};

//class d1: public Base
class d1: virtual public Base
{
public:
    int j;
};

//class d2: public Base
class d2: virtual public Base
{
public:
    int k;
};

class d3: public d1, public d2 //d3 наследует d1 и d2
//получается, что в d3 содержится две копии класса Base, поэтому вопрос
{
public:
    int m;
};

int main()
{
    d3 d;
    //d.i = 10;
    d.d2::i = 10;//
    d.j = 20;
    d.k = 30;
    d.m = 40;
    //cout << d.i; // Возникает неопределеность какое и использовать
    // для решения проблемы используем оператор области видимости
    cout << d.d2::i;
    cout << d.j << d.k;
    cout << d.m;
    return 0;
}
```

Console:

```
10203040
```

Возникает неопределеность какое `i` использовать. Для решения проблемы используем оператор области видимости. Чтобы избежать ситуации, когда мы не хотим, чтобы в классе `d3` содержалось две копии `Base` мы будем применять механизм виртуального базового класса.

Когда два или более классов пораждаются от одного общего базового класса можно предотвратить включение нескольких копий базового класса в объект потом.
