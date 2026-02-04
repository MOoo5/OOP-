# **Array of object and Pointers to Objects**

# مقدمة مهمة جدًا قبل أي حاجة

## اسم الـ Array لوحده = Pointer على أول عنصر

لو عندك:

```cpp
int arr[5] = {1,2,3,4,5};

```

فـ:

```cpp
arr

```

ده **بيشاور على أول عنصر في المصفوفة**

يعني بالظبط كده:

```cpp
&arr[0]

```

---

## ❗ نقطة خطيرة (اسم الـ array ثابت)

اسم الـ array هو **Pointer ثابت (const pointer)**:

```cpp
arr++;// ❌ غلط
arr = x;// ❌ غلط

```

لكن ينفع:

```cpp
arr[i];// ✅
*(arr + i);// ✅

```

يعني:

- العنوان نفسه ثابت
- القيم اللي جواه عادي تتغير

---

## 🧭 أطبع كل عناصر الـ Array باستخدام Pointer إزاي؟

### ✅ الطريقة الأولى (Pointer مساعد):

```cpp
int arr[5] = {1,2,3,4,5};

int* p = arr;

for (int i =0; i <5; i++) {
    cout << *(p + i) <<" ";
}

```

🔹 الخرج:

```
1 2 3 4 5

```

---

### ✅ الطريقة التانية (تحريك الـ Pointer نفسه):

```cpp
int arr[5] = {1,2,3,4,5};

int* p = arr;

for (int i =0; i <5; i++) {
    cout << *p <<" ";
    p++;
}

```

⚠️ مهم:

- اللي اتحرك هو `p`
- إنما `arr` نفسه **ما بيتحركش**

---

### 🧪 إثبات إن `arr` Pointer:

```cpp
cout << arr << endl;
cout << &arr[0] << endl;

```

الاتنين نفس العنوان ✔️

---

## 🧠 خلاصة المقدمة:

| حاجة | معناها |
| --- | --- |
| `arr` | Pointer لأول عنصر |
| `arr` ثابت | ما ينفعش يتحرك |
| `arr[i]` | = `*(arr + i)` |
| نلف على array | نستخدم pointer مساعد |

---

# 1️⃣ Array of Objects

يعني **مصفوفة عادية من كائنات**

كلها بتتحجز **مرة واحدة في الـ Stack**

### ✅ مثال:

```cpp
#include<iostream>
using namespace std;

class Car {
public:
    string brand;
int speed;

void display() {
        cout << brand <<" - " << speed << endl;
    }
};

int main() {
    Car cars[2];// Array of objects (Stack)

    cars[0].brand ="BMW";
    cars[0].speed =200;

    cars[1].brand ="Mercedes";
    cars[1].speed =180;

    cars[0].display();
    cars[1].display();
}

```

### ✅ النتيجة:

```
BMW -200
Mercedes -180

```

📌 الوصول:

```cpp
cars[i].x

```

---

# 2️⃣ Pointer to Object

يعني عندك **Pointer بيشاور على Object واحد**

### ✅ مثال:

```cpp
#include <iostream>
using namespace std;

class Car {
public:
    string brand;
    int speed;

    void display() {
        cout << brand << " - " << speed << endl;
    }
};

int main() {
    // Array of objects (Stack)
    Car cars[3];

    cars[0].brand = "Toyota";
    cars[0].speed = 160;

    cars[1].brand = "BMW";
    cars[1].speed = 220;

    cars[2].brand = "Kia";
    cars[2].speed = 150;

    // Pointer بيشاور على أول عنصر في الأراي
    Car* ptr = cars;   // = &cars[0]

    // نلف على الأراي باستخدام الـ pointer
    for (int i = 0; i < 3; i++) {
        ptr->display(); // نفس (*ptr).display()
        ptr++;          // نروح على العنصر اللي بعده
    }
}

```

### ✅ النتيجة:

```
Toyota -160

```

📌 الوصول:

```cpp
ptr->x

```

---

# 3️⃣ Array of Pointers to Objects

يعني:

- Array في الـ Stack
- جواه **Pointers**
- كل Pointer بيشاور على Object في الـ Heap

### ✅ مثال:

```cpp
#include<iostream>
using namespace std;

class Car {
public:
    string brand;
int speed;

void display() {
        cout << brand <<" - " << speed << endl;
    }
};

int main() {
    Car* cars[2];// Array of pointers (Stack)

    cars[0] =newCar();// Object في Heap
    cars[1] =newCar();

    cars[0]->brand ="Audi";
    cars[0]->speed =210;

    cars[1]->brand ="Kia";
    cars[1]->speed =150;

    cars[0]->display();
    cars[1]->display();

// Cleanup
delete cars[0];
delete cars[1];
}

```

### ✅ النتيجة:

```
Audi -210
Kia -150

```

📌 الوصول:

```cpp
cars[i]->x

```

⚠️ لازم `delete` عشان تمنع Memory Leak

---

## 🧠 الخلاصة النهائية (الدماغ ترتاح 😌):

| النوع | مكان التخزين | الوصول | ملاحظات |
| --- | --- | --- | --- |
| Array of Objects | Stack | `cars[i].x` | سريع وبسيط |
| Pointer to Object | Stack + Pointer | `ptr->x` | Object واحد |
| Array of Pointers | Stack + Heap | `cars[i]->x` | مرن بس محتاج `new/delete` |
| اسم Array | Pointer ثابت | — | بيشاور على أول عنصر |