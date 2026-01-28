### ✅ إيه هو الـ Class في C++؟

الـ `class` هو **قالب أو نموذج** (زي التصميم) بتستخدمه علشان تمثل كائن معين  
(Object) بيجمع بين:

- **بيانات (Variables)**
- **وظايف (Functions)**

الخاصة بالكائن ده.

---

### ✅ طب والغرض منه إيه؟

الغرض الأساسي من استخدام الـ `class` هو:

> تنظيم الكود ولمّ كل حاجة تخص كائن معين في مكان واحد.

---

## 📌 مثال 1: Class بسيط باستخدام Arrays و Setters

```cpp
#include <iostream>
#include <cstring>  // لاستخدام strcpy
using namespace std;

class Car {
private:
    // المتغيرات (البيانات)
    char name[15];       // اسم السيارة
    char color[10];      // لون السيارة
    int maxspeed;        // السرعة القصوى
    int model;           // سنة الموديل

public:
    // دالة لتحديد اسم السيارة
    void setName(char n[]) {
        strcpy(name, n);
    }

    // دالة لتحديد لون السيارة
    void setColor(char c[]) {
        strcpy(color, c);
    }

    // دالة لتحديد السرعة القصوى
    void setMaxSpeed(int speed) {
        maxspeed = speed;
    }

    // دالة لتحديد سنة الموديل
    void setModel(int year) {
        model = year;
    }

    // دالة لطباعة بيانات السيارة
    void print() {
        cout << "\n--- Car Information ---\n";
        cout << "Name: " << name << endl;
        cout << "Color: " << color << endl;
        cout << "Maximum Speed: " << maxspeed << " km/h" << endl;
        cout << "Model Year: " << model << endl;
    }
};

int main() {
    Car myCar;
    char name[15], color[10];
    int speed, model;

    // إدخال البيانات
    cout << "Enter car name: ";
    cin >> name;

    cout << "Enter color: ";
    cin >> color;

    cout << "Enter maximum speed: ";
    cin >> speed;

    cout << "Enter model year: ";
    cin >> model;

    // إرسال البيانات للأوبجكت
    myCar.setName(name);
    myCar.setColor(color);
    myCar.setMaxSpeed(speed);
    myCar.setModel(model);

    // طباعة البيانات
    myCar.print();

    return 0;
}
```

---

## 📌 مثال 2: Class باستخدام string (أنضف وأسهل)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Football {
private:
    string team_name, coach;
    int team_member;

public:
    void setNameCoach(string t, string c) {
        team_name = t;
        coach = c;
    }

    void setNum(int n) {
        team_member = n;
    }

    void print() {
        cout << "\n--- Team Info ---\n";
        cout << "Members: " << team_member << '\n';
        cout << "Team Name: " << team_name << '\n';
        cout << "Coach: " << coach << '\n';
    }
};

void Fulla() {
    Football m;
    int team_member;
    string team_name, coach;

    cin >> team_member >> team_name >> coach;

    m.setNum(team_member);
    m.setNameCoach(team_name, coach);
    m.print();
}

signed main() {
    long long t = 1;
    // cin >> t;
    while (t--) {
        Fulla();
    }
}
```

---

### 🧠 ملحوظات سريعة:

- الـ `private`:
  - مينفعش يتشاف أو يتغير من برّه الكلاس.
- الـ `public`:
  - هو اللي بنتعامل معاه من خلال الـ object.
- بنستخدم الـ **functions** علشان نتحكم في البيانات (Encapsulation).

---

⭐ كده ده **جاهز MD – بلوك واحد – يتحط مباشرة في GitHub**  
لو حابب أدمج ده مع **Constructor / Destructor** في README واحد مرتب قولّي وأنا أظبطه 🔥
