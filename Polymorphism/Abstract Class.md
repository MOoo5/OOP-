# Abstract Class في C++  
(الكلاس المجرد / Abstract Class)


```cpp
#include <iostream>
using namespace std;

// Abstract Class (كلاس مجرد)
class CPolygon {
protected:
    int width, height;

public:
    void set_values(int a, int b) {
        width = a;
        height = b;
    }

    // Pure Virtual Function → ده اللي بيخلي الكلاس abstract
    virtual int area(void) = 0;   // = 0 معناها "مش لازم تتنفذ هنا، لازم الابن ينفذها"
};

int main() {
    // CPolygon poly;         // خطأ ترجمة! مش مسموح إنشاء كائن من abstract class
    // CPolygon poly2;        // خطأ: cannot instantiate abstract class

    CPolygon *ppoly1;         // صحيح تمامًا! pointer لـ abstract class مسموح
    // ppoly1 = new CPolygon(); // خطأ لو حاولت new

    // مثال صحيح: pointer لكلاس مجرد يشير إلى كائن من كلاس مشتق
    // (لازم نعمل كلاس مشتق ينفذ area() أولاً)

    return 0;
}
```
شرح Abstract Class خطوة بخطوة
1. إيه هو Abstract Class؟

كلاس مجرد (abstract) هو كلاس مش بيسمح بإنشاء كائنات (objects) منه مباشرة
هدفه: يكون قالب أساسي للكلاسات المشتقة (الأبناء)
يحتوي على واحدة أو أكثر من الدوال الـ pure virtual
(دالة virtual بدون تنفيذ = 0 في النهاية)

```cpp
virtual int area(void) = 0;
```
`virtual` → عشان تدعم polymorphism
`= 0` → pure virtual → معناها:
"الدالة دي لازم تتنفذ في الكلاسات المشتقة، أنا مش هنفذها هنا"
لما يكون فيه دالة pure virtual واحدة على الأقل → الكلاس يبقى abstract

---
## 3. القاعدة المهمة جدًا (Abstract Class)

| الحاجة                     | مسموح؟ | السبب |
|----------------------------|--------|-------|
| إنشاء كائن عادي            | لا     | `CPolygon poly;` → خطأ ترجمة: cannot instantiate abstract class |
| إنشاء pointer للكلاس المجرد | نعم    | `CPolygon *p;` → تمام، عشان الـ pointer مش بيحتاج تنفيذ الدوال |
| `new` للكلاس المجرد        | لا     | `new CPolygon();` → خطأ ترجمة |
| استخدامه في polymorphism   | نعم    | `CPolygon *p = new CRectangle();` → ده صحيح وهو الاستخدام الشائع |

---

## 4. ليه بنستخدم Abstract Class؟

- نضمن إن كل الكلاسات المشتقة تنفذ دوال معينة (زي `area()`)
- نعمل Interface أو قالب مشترك بدون تنفيذ كامل
- نستخدم Polymorphism بأمان (Pointer للأب يشير لأي ابن)
- نمنع إنشاء كائنات غير مكتملة (لأن الكلاس المجرد مش كامل)

---

## 5. ملخص بسيط جدًا

- **Abstract Class** = كلاس فيه `pure virtual function` واحدة على الأقل (`= 0`)
- مش ممكن نعمل منه Object (كائن عادي)
- ممكن نعمل Pointer أو Reference له
- الاستخدام الشائع:  
  `pointer` للـ Abstract Class يشير إلى كائن من كلاس مشتق حقيقي
