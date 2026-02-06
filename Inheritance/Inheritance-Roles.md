# Constructors في الوراثة (Inheritance) في C++  
ترتيب الاستدعاء والفرق بين الطريقتين

## القاعدة الأساسية (المهمة جدًا)

عند إنشاء كائن من الكلاس المشتق (ابن):  
→ يتم استدعاء constructor الكلاس الأم **قبل** constructor الابن دائمًا

## الطريقة الأولى: بدون استدعاء صريح لـ constructor الأم

```cpp
#include <iostream>
using namespace std;

class Mother {
public:
    Mother() {
        cout << "Mother: default (empty) constructor\n";
    }
    
    Mother(int x) {
        cout << "Mother: parameterized constructor = " << x << endl;
    }
};

class Daughter : public Mother {
public:
    // بدون : Mother(....)
    Daughter(int val) {
        cout << "Daughter: parameterized constructor = " << val << endl;
    }
};

int main() {
    Daughter obj(777);
    return 0;
}
```


```cpp
Mother: default (empty) constructor
Daughter: parameterized constructor = 777
```
ملاحظة مهمة جدًا:

الـ compiler تلقائيًا ينادي الـ default constructor (الفاضي) للأم
لو `الأم` ما عندهاش default constructor (يعني بس parameterized constructors موجودة)
→ خطأ ترجمة (compilation error)

## لطريقة الثانية: استدعاء صريح باستخدام member initializer list 
```cpp
#include <iostream>
using namespace std;

class Mother {
public:
    Mother() {
        cout << "Mother: default (empty) constructor\n";
    }
    
    Mother(int x) {
        cout << "Mother: parameterized constructor = " << x << endl;
    }
};

class Daughter : public Mother {
public:
    // ← هنا الفرق المهم
    Daughter(int val) : Mother(val)
    {
        cout << "Daughter: parameterized constructor = " << val << endl;
    }
};

int main() {
    Daughter obj(777);
    return 0;
}
```

```cpp
Mother: parameterized constructor = 777
Daughter: parameterized constructor = 777
```


## خلاصة في جملة واحدة (افتكرها دايمًا)
لو ما كتبتش : Mother(....) في constructor الابن، الـ compiler هينادي الـ default constructor (الفاضي) للأم تلقائيًا.

لو مفيش default constructor في الأم → خطأ
عشان تتجنب المشكلة وتتحكم في القيم → استخدم دائمًا : Mother(القيمة المناسبة)

ده الفرق الأساسي والشائع في الوراثة لما في constructors بباراميترات.


# Multiple Inheritance في C++  
(الوراثة المتعددة)

### تعريف بسيط جدًا

الوراثة المتعددة (Multiple Inheritance) تعني:  
**كلاس واحد يرث من أكثر من كلاس أساسي (base class) في نفس الوقت.**

### مثال بسيط جدًا لتوضيح المفهوم

```cpp
#include <iostream>
using namespace std;

// الكلاس الأول (أحد الآباء)
class Engine {
public:
    void start() {
        cout << "Engine started\n";
    }
};

// الكلاس الثاني (أب آخر)
class Wheels {
public:
    void roll() {
        cout << "Wheels rolling\n";
    }
};

// الكلاس المشتق → يرث من Engine و Wheels معًا
class Car : public Engine, public Wheels {
public:
    void drive() {
        start();          // موروث من Engine
        roll();           // موروث من Wheels
        cout << "Car is driving!\n";
    }
};

int main() {
    Car myCar;
    myCar.drive();
    return 0;
}
```
```cpp

Engine started
Wheels rolling
Car is driving!

```

# Multiple Inheritance في C++  
(الوراثة المتعددة)

### في المثال ده:

- `Car` مشتق من **أكثر من كلاس واحد**  
  → ده اسمه **Multiple Inheritance**

- `Car` هو:  
  **derived class** أو **subclass** أو **child class**

- `Engine` و `Wheels` هما:  
  **base classes** أو **superclasses** أو **parent classes** (أكثر من واحد)

### ملخص بسيط جدًا

| النوع                  | الوصف                                      | عدد الكلاسات الأساسية |
|------------------------|--------------------------------------------|--------------------------|
| Single Inheritance     | وراثة من كلاس واحد فقط                     | 1                        |
| Multiple Inheritance   | وراثة من أكثر من كلاس في نفس الوقت        | أكثر من 1               |
--- 

### ملاحظات سريعة مهمة

- **Multiple Inheritance** مسموح في C++  
  (عكس Java مثلاً اللي بتمنعه تمامًا)

- ممكن يسبب مشاكل زي **Diamond Problem**  
  (مشكلة الماس) لو ما استخدمتش `virtual inheritance`

- الأكثر شيوعًا وأمانًا في التصميم الحديث:  
  **Single Inheritance + Composition**  
  أو استخدام **Interfaces** (كلاسات مجردة abstract classes)  
  بدل الاعتماد الكبير على الوراثة المتعددة

### خلاصة في سطر واحد:

**Multiple Inheritance** = كلاس واحد يورث مباشرة من أكثر من كلاس أساسي في وقت واحد  
→ ميزة قوية في C++، لكن استخدمها بحذر عشان تتجنب التعقيد والأخطاء.
