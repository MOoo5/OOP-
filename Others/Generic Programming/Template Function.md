# Templates في C++ (القوالب)

Templates هي ميزة تسمح بكتابة كود عام (generic code) يشتغل مع أنواع بيانات مختلفة بدون تكرار الكود.

### المثال الأول: Template بسيط (function template)



```cpp
#include <iostream>
using namespace std;

// template function واحدة لأي نوع
template <class T>
T sum(T x, T y) {
    return x + y;
}

int main() {
    int a = 5, b = 3;
    cout << "مجموع عددين صحيحين = " << sum(a, b) << endl;       // 8

    double c = 4.5, d = 2.7;
    cout << "مجموع عددين عشريين = " << sum(c, d) << endl;     // 7.2

    return 0;
}
```
الشرح:

`template <class T>` → تعني "استخدم أي نوع، وسميه T مؤقتًا"
الـ compiler بيعمل نسخة من الدالة `sum` لكل نوع بنستخدمه (int, double, float, string... إلخ)
نفس الدالة بتشتغل مع أي نوع يدعم عملية `+`

## المثال الثاني: Template بمعاملين مختلفين (two different types)
```cpp
#include <iostream>
using namespace std;

// template بمعاملين من أنواع مختلفة ممكنة
template <class T1, class T2>
T1 sum(T1 x, T2 y) {
    return x + y;   // النتيجة هتكون من نوع T1
}

int main() {
    int a = 10;
    double b = 3.14;

    cout << sum(a, b) << endl;      // 13.14   (نوع الرجوع int → بيقرب لأسفل)

    // لو عايز النتيجة double، ممكن تغير الترتيب أو تستخدم auto
    cout << sum(b, a) << endl;      // 13.14   (نوع الرجوع double)

    return 0;
}

```
ملاحظات مهمة:

نوع الرجوع (return type) هنا هو `T1`→ يعني النوع الأول في الدالة
لو النوعين مختلفين، الـ compiler بيحاول يعمل promotion (ترقية) تلقائي، لكن ممكن يحصل truncation (قطع) لو رجعنا نوع أصغر

ممكن نريح دماغنا ونستمع `auto`
```cpp
template <class T1, class T2>
auto sum(T1 x, T2 y) {
    return x + y;   // auto بيحدد النوع تلقائيًا
}
```


