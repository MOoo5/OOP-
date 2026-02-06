# الوراثة (Inheritance) في C++

## مفهوم الوراثة باختصار
الوراثة هي آلية تسمح لكلاس جديد (**Derived Class / Sub Class / Child Class**)  
أن يرث الخصائص والسلوكيات (المتغيرات والدوال) من كلاس موجود مسبقًا (**Base Class / Super Class / Parent Class**).

### المصطلحات الشائعة (بالإنجليزي والعربي)

| المصطلح بالإنجليزي     | المصطلح بالعربي          | الاسم الشائع الآخر       |
|---------------------------|----------------------------|----------------------------|
| Base Class                | الكلاس الأساسي            | Super Class, Parent Class  |
| Derived Class             | الكلاس المشتق             | Sub Class, Child Class     |
| Inheritance               | الوراثة                    | —                          |
| Reusability               | إعادة الاستخدام           | —                          |

## مستويات الوصول (Access Specifiers) وتأثيرها في الوراثة

| نوع العضو (Member) | يمكن الوصول إليه داخل...                  | يمكن الوصول إليه في الكلاس المشتق؟ | يمكن الوصول إليه من خارج الكلاس؟ |
|---------------------|---------------------------------------------|---------------------------------------|-------------------------------------|
| `private`           | نفس الكلاس فقط                              | **لا**                                | **لا**                              |
| `protected`         | نفس الكلاس + الكلاسات المشتقة             | **نعم**                               | **لا**                              |
| `public`            | في أي مكان (داخل وخارج الكلاس)            | **نعم**                               | **نعم**                             |

### ملخص سريع للوصول في الوراثة

- `private` → خاص جدًا → **لا يُرث** (لا يمكن للكلاس المشتق الوصول إليه مباشرة)
- `protected` → وسط → **يُرث** ويمكن للكلاس المشتق استخدامه، لكن لا يُرى من برا
- `public` → عام → **يُرث** ويبقى عام في الكلاس المشتق (في الوراثة العامة public inheritance)

## أنواع الوراثة في C++ (من حيث طريقة الوراثة)

| نوع الوراثة          | الكتابة                              | تأثير على الأعضاء public في Base |
|-----------------------|---------------------------------------|-------------------------------------|
| Public Inheritance    | `class Derived : public Base`         | تبقى public                        |
| Protected Inheritance | `class Derived : protected Base`      | تتحول إلى protected               |
| Private Inheritance   | `class Derived : private Base`        | تتحول إلى private                 |

(الأكثر شيوعًا بكتير هو **public inheritance**)

# مثال على الوراثة (Inheritance) في C++


```cpp
#include <iostream>
#include <vector>
using namespace std;

// الكلاس الأساسي (Base Class)
class CPolygon {
protected:
    int width, height;

public:
    void set_values(int a, int b) {
        width  = a;
        height = b;
    }
};

// الكلاس المشتق (Derived Class) - وراثة عامة (public inheritance)
class CRectangle : public CPolygon {
public:
    int area() {
        return (width * height);
    }
};

// مثال إضافي: مثلث (اختياري لتوضيح الفكرة)
class CTriangle : public CPolygon {
public:
    int area() {
        return (width * height / 2);
    }
};

int main() {
    CRectangle rect;
    CTriangle  tri;

    // نستخدم دالة موروثة من CPolygon
    rect.set_values(10, 5);
    tri.set_values(10, 5);

    // نستخدم الدوال الخاصة بكل كلاس مشتق
    cout << "مساحة المستطيل = " << rect.area() << endl;
    cout << "مساحة المثلث  = " << tri.area()  << endl;

    return 0;
}

```
# الوراثة الخاصة (Private Inheritance) في C++



```cpp
#include <iostream>
using namespace std;

class A {
private:
    int i;          // private → لا يُرث أبدًا بشكل مباشر

protected:
    int j;          // protected → يُرث، لكن يتغير حسب نوع الوراثة

public:
    int k;          // public → يتغير حسب نوع الوراثة
};

class B : private A {   // ← هنا الوراثة الخاصة (private inheritance)
    int x;              // عضو خاص بـ B

public:
    int y;

    // يمكن الوصول إلى j داخل B لأنه protected في A
    int get_j() {
        return j;
    }

    // لو حاولت نعمل دالة ترجع k → هتشتغل برضو
    int get_k() {
        return k;
    }
};

int main() {
    B OP;

    OP.y = 9;           // ✓ OK → y عضو public في B

    // OP.k = 7;        // ✗ خطأ – لا يمكن الوصول إلى k من خارج B
                        // لأن public members في A أصبحت private في B

    // OP.j             // ✗ خطأ – j أصبح private في B (حتى لو كان protected في A)

    cout << OP.y << endl;           // ✓ 9
    // cout << OP.k;                // ✗ compilation error
    // cout << OP.get_j();          // ✓ يشتغل (لأن get_j داخل B)

    return 0;
}
```

# الوراثة الخاصة (Private Inheritance) في C++ – تلخيص نهائي وواضح

- الكود **داخل الكلاس B** يترجم بدون مشاكل  
  (لأن B يقدر يوصل للأعضاء الموروثة من A: `j` و `k`)

- لكن في `main()`:

  - `OP.k = 7;`  
    → **خطأ ترجمة**  
    `'int A::k' is inaccessible`  
    أو  
    `cannot access public member declared in class 'A'`

  - `OP.y = 9;`  
    → **تمام وصحيح**  
    (لأن `y` عضو معرّف داخل B نفسه، مش موروث)
    ---
    
# القاعدة الأساسية في Private Inheritance (وراثة خاصة) في C++

### القاعدة الأساسية والمهمة جدًا:

كل الأعضاء (members) اللي بتتورث من الكلاس الأب `A`  
→ **بتتحول إلى private** بالنسبة للكلاس المشتق `B`

### يعني إيه بالتفصيل:

| نوع العضو في الكلاس الأب (A) | يصبح إيه في الكلاس المشتق (B) بعد private inheritance | يقدر يوصل له مين من برا B؟ | يقدر يوصل له داخل B؟          |
|-------------------------------|-----------------------------------------------------------|-------------------------------|---------------------------------|
| private                       | ما بيتورثش خالص                                          | لا أحد                        | لا                              |
| protected                     | private                                                   | لا                            | نعم (داخل B فقط)               |
| public                        | private                                                   | لا                            | نعم (داخل B فقط)               |

### باختصار شديد (الجملة اللي تلخص كل حاجة):

**في الـ private inheritance كل حاجة بتيجي من الكلاس الأب بتبقى private بالنسبة للكلاس المشتق.**

- حتى الأعضاء اللي كانت `public` في `A` → **بتتحول لـ private** في `B`
- يعني: **محدش بره `B`** يقدر يستخدم أي حاجة موروثة من `A` مباشرة
- لكن **جوا `B` نفسه** → تقدر تستخدمها عادي جدًا (في الدوال والمتغيرات الداخلية)

