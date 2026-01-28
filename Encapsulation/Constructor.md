# 🛠️ يعني إيه Constructor؟

**Constructor** يعني "البنّاء"، وده اسم على مسمّى...

هو **دالة خاصة جوا الكلاس بتشتغل لوحدها أول ما تعمل object**، وبتستخدم علشان:

> "تجهّز الكائن (object) وتحط فيه القيم الأولية".

---

## ✅ شكله عامل إزاي؟

```cpp
class Car {
public:
    Car() {
        cout << "Constructor اشتغل\n";
    }
};
```

وبعدين:

```cpp
int main() {
    Car myCar;  // أول ما تكتب السطر ده، Constructor بيتنفذ تلقائي
}
```

---

## 🎯 الغرض من Constructor:

- تهيئة المتغيرات بتاعة الكائن (object) أول ما يتعمل.
- توفير كود بدل ما تكتب `set` لكل حاجة.
- أحيانًا يكون فيه أكتر من نوع منه حسب اللي عايزه.

---

## 🔥 أنواع الـ Constructors:

| النوع | الشرح | مثال |
| --- | --- | --- |
| ✅ **Default Constructor** | من غير أي باراميتر | `Car() {}` |
| ✅ **Parameterized Constructor** | بياخد قيم وانت بتنشئ الـ object | `Car(string name, int speed)` |
| ✅ **Copy Constructor** | بياخد object تاني وينسخه | `Car(const Car &other)` |

---

## 📌 1. Default Constructor:

```cpp
class Car {
public:
    Car() {
        cout << "أنا Default Constructor!\n";
    }
};
```

---

## 📌 2. Parameterized Constructor:

```cpp
class Car {
private:
    string name;
    int speed;

public:
    Car(string n, int s) {
        name = n;
        speed = s;
    }

    void print() {
        cout << name << " - " << speed << " km/h\n";
    }
};
```

```cpp
int main() {
    Car c1("Toyota", 180);
    c1.print();
}
```

---

## 📌 3. Copy Constructor:

```cpp
#include <iostream>
using namespace std;

class Car {
private:
    string name;

public:
    // Constructor
    Car(string n) {
        name = n;
    }

    // Copy constructor
    Car(const Car &c) {
        name = c.name;
    }

    void print() {
        cout << "Name: " << name << '\n';
    }
};

int main() {
    Car car1("Toyota");
    Car car2(car1);    // Car car2 = car1;

    cout << "Car 1: ";
    car1.print();

    cout << "Car 2 (copy of Car 1): ";
    car2.print();

    return 0;
}
```

---

## 💡 ملاحظات مهمة:

- اسم الـ Constructor هو **نفس اسم الكلاس بالظبط**.
- **مفيهوش return type** (ولا حتى `void`).
- ممكن يكون عندك **أكتر من Constructor** (Overloading).

---

## ✨ مثال عملي كامل:

```cpp
#include <bits/stdc++.h>
using namespace std;

class Football {
private:
    string team_name, coach;
    int team_member;

public:
    // ✨ Constructor بياخد البيانات كلها
    Football(int members, string t_name, string c_name) {
        team_member = members;
        team_name = t_name;
        coach = c_name;
    }

    void print() {
        cout << "\n--- Team Info ---\n";
        cout << "Members: " << team_member << '\n';
        cout << "Team Name: " << team_name << '\n';
        cout << "Coach: " << coach << '\n';
    }
};

void Fulla() {
    int team_member;
    string team_name, coach;

    cin >> team_member >> team_name >> coach;

    // ✨ استخدمنا الـ constructor هنا
    Football m(team_member, team_name, coach);
    m.print();
}

signed main() {
    ll t = 1;
    //cin >> t;
    while (t--) {
        Fulla();
    }
}
```
