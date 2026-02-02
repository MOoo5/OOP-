### ✅ 0️⃣ Pointer (المؤشر)

🔹 **الشرح:**

الـ **Pointer** هو متغير بيخزن **عنوان متغير تاني في الذاكرة**.

يعني بدل ما نخزن القيمة نفسها، بنخزن **مكانها في الرام**.

أي تغيير يحصل عن طريق البوينتر ينعكس على المتغير الأصلي والعكس صحيح.

📌 لإسناد قيمة للبوينتر لازم نستخدم `*`.

---

🔸 **مثال بسيط:**

```cpp
int x = 10;
int *p = &x;   // p بيشاور على x

cout << *p;    // يطبع 10 (قيمة x)
```

---

🔹 **استخدام Pointer مع الكلاسات:**

```cpp
#include <iostream>
#include <string>
using namespace std;

class Car {
public:
    string brand;
};

int main() {
    Car car;
    car.brand = "BMW";

    Car* ptr = &car;          // بوينتر بيشاور على كائن car
    (*ptr).brand = "Audi";   // فك الإشارة باستخدام *
    
    cout << (*ptr).brand;    // Audi
}
```

📌 ملحوظة:  
نقدر نستخدم كمان:
```cpp
ptr->brand = "Audi";
```

وده أسهل وأنضف.

---

## ✳️ New / Delete — [OOP] #07

---

🔹 **الشرح:**

- `new` → بتخصص مساحة في الذاكرة (Heap).
- `delete` → بتحرر المساحة دي من الذاكرة.

أي حاجة تتحجز بـ `new` **لازم** تتحذف بـ `delete`  
وإلا يحصل **Memory Leak** ❌.

---

🔸 **مثال عملي (new + delete + constructor + destructor):**

```cpp
#include <iostream>
#include <string>
using namespace std;

class Car {
private:
    string* brand;

public:
    // Constructor
    Car(string b) {
        brand = new string();   // حجز مساحة في الـ heap
        *brand = b;             // تخزين القيمة
        cout << "Constructor: Car created with brand = " << *brand << endl;
    }

    // Destructor
    ~Car() {
        delete brand;           // تحرير الذاكرة
        cout << "Destructor: Car destroyed and memory freed" << endl;
    }

    void show() {
        cout << "Car brand: " << *brand << endl;
    }
};

int main() {
    Car myCar("Kia");
    myCar.show();

    return 0;
}
`
