# Polymorphism في C++  
(التعددية الشكلية / التعدد الأشكال)

### إيه هو Polymorphism بالظبط؟

**Polymorphism** يعني:  
نفس اسم الدالة → لكنها تتصرف بطريقة مختلفة حسب نوع الكائن الحقيقي اللي بنناديها عليه.

في C++، النوع الأشهر والأهم هو **Runtime Polymorphism**  
(التعددية الشكلية وقت التشغيل)، وده اللي بنحققه باستخدام:

- `virtual` functions في الكلاس الأب
- Pointers أو References من نوع الكلاس `الأب` تشير إلى كائنات من كلاسات مشتقة
- Pointers أو References  بتتعرف لازم من كلاس `الاب`

### ليه بنستخدم Polymorphism؟

1. نكتب كود **عام ومرن** يتعامل مع أنواع مختلفة بنفس الطريقة  
   (بدون if-else كتير عشان نفرق بين المستطيل والمثلث والدائرة... إلخ)

2. نعمل تصميم **قابل للتوسع**  
   لو بعدين عايز تضيف شكل جديد (مثل مربع أو خماسي)، الكود القديم ما يتغيرش

3. نستخدم pointer/reference للكلاس الأب → ونخليه يشير لأي ابن  
   ولما ننادي الدالة → يتنفذ النسخة الخاصة بالابن (مش الأب)

### مثال كلاسيكي بسيط (الأشهر في الكتب والمحاضرات)

```cpp
#include <iostream>
using namespace std;

// الكلاس الأساسي (Base Class)
class CPolygon {
protected:
    int width, height;

public:
    void set_values(int a, int b) {
        width = a;
        height = b;
    }

    // الدالة الافتراضية (virtual) – شرط أساسي للـ Polymorphism
    virtual int area() {          // بنكتبها عشان لما اجي استدعي بالبونيتر فانكشن موجوده عند الابن ومش موجوده عن الاب ميدينيش ايرور
        return 0;                // قيمة افتراضية (يمكن تجاوزها)
    }
};

// كلاس مشتق 1: مستطيل
class CRectangle : public CPolygon {
public:
    int area() override {           // override → تجاوز الدالة
        return (width * height);
    }
};

// كلاس مشتق 2: مثلث
class CTriangle : public CPolygon {
public:
    int area() override {           // override → تجاوز الدالة
        return (width * height / 2);
    }
};

int main() {
    CRectangle rect;
    CTriangle  tri;

    // Pointers من نوع الكلاس الأب (هنا يبدأ الـ Polymorphism)
    CPolygon *p1 = &rect;   // يشير إلى مستطيل
    CPolygon *p2 = &tri;    // يشير إلى مثلث

    p1->set_values(10, 5);
    p2->set_values(10, 5);

    // نفس الدالة area() → لكن سلوك مختلف
    cout << "مساحة المستطيل: " << p1->area() << endl;   // 50
    cout << "مساحة المثلث : " << p2->area() << endl;    // 25

    return 0;
}
```

```cpp
مساحة المستطيل: 50
مساحة المثلث : 25
```
شرح النقاط المهمة خطوة بخطوة

## Pointers to Base Class
`CPolygon *p1 = &rect;`
`CPolygon *p2 = &tri;`
→ الـ pointer من نوع الكلاس الأب (`CPolygon*`) لكنه يشير إلى كائن من كلاس مشتق (ابن)

Polymorphism الحقيقي (Runtime Polymorphism)
لما ننادي `p1->area()` → يتم تنفيذ `CRectangle::area()`
لما ننادي `p2->area()` → يتم تنفيذ `CTriangle::area()`
→ نفس الاسم `area()` لكنه يتصرف بشكل مختلف حسب النوع الحقيقي للكائن `(late binding)`

الشرط الأساسي لتحقيق Polymorphism
الدالة في الكلاس الأب لازم تكون `virtualvirtual int area() { ... }`
في الكلاسات المشتقة → يُفضل استخدام `override` (اختياري لكن مفيد جدًا للأمان)

بدون `virtual`
لو شلت كلمة `virtual` من `area()` في `CPolygon`
→ هيتنفذ `CPolygon::area()` دائمًا `(static binding)`
→ مش هيحصل تعدد أشكال (Polymorphism مش هيشتغل)


## ملخص سريع جدًا

| العنصر                    | دوره في Polymorphism |
|---------------------------|----------------------|
| Pointer/Reference to Base | يشير إلى أي كائن مشتق |
| virtual function          | يسمح بـ Late Binding (يختار الدالة وقت التشغيل) |
| override في الابن         | يوضح أن الدالة بتتجاوز دالة الأب |
| بدون virtual              | Early Binding (يتم الربط وقت الترجمة) |
