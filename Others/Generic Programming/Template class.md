## يه هو Class Template؟

زي function template، لكن بدل ما يكون دالة عامة، بيكون كلاس كامل عام
يعني تقدر تعمل كلاس واحد، والـ compiler يعمل نسخ منه لكل نوع بيانات تستخدمه
مفيد جدًا لما عايز تخزن أو تعالج بيانات من أنواع مختلفة بنفس الطريقة (مثل Stack، Queue، List، Pair... إلخ)


```cpp
#include <iostream>
using namespace std;

// Class Template: كلاس عام يخزن رقمين من نفس النوع
template <class T>          // أو template <typename T>
class number {
private:
    T first;
    T second;

public:
    // Constructor
    number(T a, T b) {
        first = a;
        second = b;
    }

    // دالة max ترجع أكبر الرقمين
    T max() {
        return (first > second) ? first : second;
    }

    // دالة اختيارية للطباعة
    void print() {
        cout << "الرقم الأول: " << first << endl;
        cout << "الرقم الثاني: " << second << endl;
        cout << "الأكبر: " << max() << endl << endl;
    }
};

int main() {
    // استخدام مع أعداد صحيحة
    number<int> ob1(10, 20);
    ob1.print();

    // استخدام مع أعداد عشرية
    number<double> ob2(3.14, 2.718);
    ob2.print();

    // استخدام مع نصوص (لأن string يدعم >)
    number<string> ob3("Ahmed", "Mohamed");
    ob3.print();

    return 0;
}
```

```cpp
الرقم الأول: 10
الرقم الثاني: 20
الأكبر: 20

الرقم الأول: 3.14
الرقم الثاني: 2.718
الأكبر: 3.14

الرقم الأول: Ahmed
الرقم الثاني: Mohamed
الأكبر: Mohamed
```

شرح خطوة بخطوة

template <class T>
→ معناها: "الكلاس ده عام، النوع اللي هيشتغل بيه هيسمى T"
→ الـ compiler بيعمل نسخة من الكلاس لكل نوع بنستخدمه `(int, double, string...)`
داخل الكلاس:
`T first, second;` → المتغيرات من النوع T (نفس النوع للاثنين)
`number(T a, T b)` → الـ constructor بياخد معاملين من نفس النوع T
`T max() `→ ترجع أكبر قيمة، والرجوع نوعه T

في `main()`:
`number<int>` → نسخة من الكلاس للأعداد الصحيحة
`number<double>` → نسخة للأعداد العشرية
`number<string>` → نسخة للنصوص (لأن `string` يدعم مقارنة `>`)


ليه استخدمنا template هنا؟
بدل ما تكتب 3 كلاسات منفصلة:

```cpp
class number_int { int first, second; ... };
class number_double { double first, second; ... };
class number_string { string first, second; ... };
```

# Template Specialization في C++
(تخصص القالب لنوع معين)

### الفكرة الأساسية

لما يكون عندك **class template** عام يشتغل مع أي نوع،  
لكن عايز تعمل **نسخة خاصة** (مخصصة) لنوع معين (مثلاً `char` بس)،  
هنا بتستخدم **template specialization**.

يعني:
- لكل الأنواع العادية → يستخدم النسخة العامة
- لنوع معين (مثل `char`) → يستخدم النسخة الخاصة اللي كتبتها أنت


```cpp
#include <iostream>
using namespace std;

// النسخة العامة (Template الأساسي)
template <class T>
class A_char {
public:
    A_char(T x) {
        cout << x << " is not character" << endl;
    }
};

// التخصص (Specialization) لنوع char فقط
template <>
class A_char<char> {           // ← template <> معناها "تخصص كامل"
public:
    A_char(char x) {
        cout << x << " is a character" << endl;
    }
};

int main() {
    A_char<int> obj1(7);           // يستخدم النسخة العامة
    A_char<double> obj2(5.199);    // يستخدم النسخة العامة
    A_char<char> obj3('A');        // ← يستخدم النسخة الخاصة (specialized)

    return 0;
}
```

```cpp
7 is not character
5.199 is not character
A is a character
```

النسخة العامة
```cpp
template <class T>
class A_char { ... };
```
→ تشتغل مع أي نوع (int, double, float, string, vector... إلخ)


التخصص الكامل
```cpp
template <>                    // ← فارغ هنا لأنه تخصص كامل
class A_char<char> { ... };    // ← محدد النوع char صراحة
```
→ لما النوع يكون `char` بالظبط → الـ compiler يستخدم النسخة دي بدل العامة