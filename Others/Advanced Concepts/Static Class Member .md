## 🔹 أولًا: Static Data Member

### ✅ يعني إيه؟

هو متغير بيتخزن **لكل الكائنات مع بعض**، مش لكل object لوحده.

يعني كل النسخ من الكلاس تشترك في نفس المتغير.

---

### ✅ مثال:

```cpp
#include <iostream>
using namespace std;

class Car {
public:
    static int count; // static member

    Car() {
        count++; // كل مرة كائن بيتعمل، نزود العداد
    }
};

int Car::count = 0; // لازم تعريف خارجي

int main() {
    Car c1;
    Car c2;
    Car c3;

    cout << "Total Cars: " << Car::count << endl;
}

//او كداا
#include <iostream>
using namespace std;

class Car {
public:
    static int count;

    Car() {
        count++; 
        // بنطبع هنا جوه الكونسـتراكتور
        cout << "A new car was created! Total cars now: " << count << endl;
    }
};

int Car::count = 0;

int main() {
    Car c1; // هنا هيطبع: Total cars now: 1
    Car c2; // هنا هيطبع: Total cars now: 2
    Car c3; // هنا هيطبع: Total cars now: 3

    cout << "\nFinal count in main: " << Car::count << endl;
}

```

### 🧾 النتيجة:

```

Total Cars: 3

A new car was created! Total cars now: 1 
A new car was created! Total cars now: 2
A new car was created! Total cars now: 3
Final count in main: 3

```

---

## 🔹 ثانيًا: Static Member Function

### ✅ يعني إيه؟

هي دالة **ثابتة** بتشتغل من غير ما تحتاج تعمل object من الكلاس.

✅ تقدر تستدعيها كده:

```cpp
ClassName::functionName();

```

---

### ✅ مثال:

```cpp
#include <iostream>
using namespace std;

class Math {
public:
    static int square(int x) {
        return x * x;
    }
};

int main() {
    cout << Math::square(5) << endl; // 25      لو الفانكشن استاتك بس 
   
    
    Math m;
    m.square();                          //او اقدر استدعيه بالطرييقه العادييه
}

```

---

## 🔐 ملاحظات مهمة:

| الخاصية | Static Variable | Static Function |
| --- | --- | --- |
| مرتبط بالكلاس | ✅ | ✅ |
| لازم object | ❌ | ❌ |
| تستخدم `this` | ❌ | ❌ |
| تشوف static فقط | عادي | تشوف static بس |

---

## ✅ مثال يجمع الاتنين:

```cpp
#include <iostream>
using namespace std;

class Account {
private:
    static int count;

public:
    Account() {
        count++;
    }

    static void showCount() {
        cout << "Total accounts: " << count << endl;
    }
};

int Account::count = 0;

int main() {
    Account a1, a2;
    Account::showCount(); // نقدر نستدعيها بدون كائن
}

```