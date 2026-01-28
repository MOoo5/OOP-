### ✅ إيه هو الـ `struct`؟

الـ `struct` يعني **تركيبة** أو **هيكل**.

بنستخدمه لما نحب نجمع كذا متغير (بيانات) تحت اسم واحد، علشان نمثل **كائن أو شيء واحد**.

---

## ✅ مثال بسيط:

```cpp
struct Car {
    string brand;
    int speed;
};
```

ده معناه إنك عملت **موديل عربية** فيه:
- `brand` → اسم العربية  
- `speed` → سرعتها  

---

## ✅ طرق تعيين القيم للـ struct

### 🔹 الطريقة الأولى (العادية):

```cpp
Car myCar;
myCar.brand = "BMW";
myCar.speed = 200;

// للطباعة
cout << myCar.speed;
```

---

### 🔹 الطريقة التانية (Initialization List):

```cpp
Car myCar = {"BMW", 200};

// للطباعة
cout << myCar.speed;
```

📌 **ملحوظة مهمة**  
لازم ترتب القيم **بنفس ترتيب المتغيرات** داخل الـ struct.

---

## 🧠 مثال كامل بالطريقة العادية:

```cpp
#include <iostream>
using namespace std;

struct Car {
    string brand;
    int speed;
};

int main() {
    Car myCar;
    myCar.brand = "BMW";
    myCar.speed = 200;

    cout << "Brand: " << myCar.brand << endl;
    cout << "Speed: " << myCar.speed << endl;
}
```

---

## 🧠 مثال كامل باستخدام الأقواس:

```cpp
#include <iostream>
using namespace std;

struct Car {
    string brand;
    int speed;
};

int main() {
    Car myCar = {"BMW", 200};

    cout << "Brand: " << myCar.brand << endl;
    cout << "Speed: " << myCar.speed << endl;
}
```

---

## 📌 struct داخل function

يعني نقدر نستخدم الـ `struct` جوه
