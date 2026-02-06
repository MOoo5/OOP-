## أولاً: Operator Overloading يعني إيه؟

يعني إنك تقدر **تغيّر معنى** الرموز اللي بنستخدمها كل يوم  
(`+`  `-`  `*`  `/`  `>>`  `<<`  `cin`  `cout` ... إلخ)  
لما تشتغل مع **كائنات** من الكلاس اللي أنت عملته.

بدل ما تستخدم دوال عادية زي:  
`obj.add(other)` أو `obj.printData()`  

تقدر تخلي الكود يبقى أجمل وأقرب للغة الطبيعية، مثلاً:  
`obj1 + obj2`  
`cout << obj`  
`cin >> obj`

### الثلاثة اللي شرحنهم المرادي 

| الرمز     | الاسم الرسمي              | الغرض الشائع                              | عدد الباراميترات جوا الكلاس؟ |
|-----------|----------------------------|--------------------------------------------|---------------------------------|
| `>>`      | Input / Extraction         | قراءة بيانات **من المستخدم** (cin)       | 2 (عادةً)                       |
| `<<`      | Output / Insertion         | طباعة بيانات **للمستخدم** (cout)         | 2 (عادةً)                       |
| `int()`   | Conversion to int          | تحويل الكائن إلى عدد صحيح (type cast)    | 0 (دالة بدون باراميتر)        |

### ملاحظات سريعة:

- `>>` و `<<` غالبًا بيتم تعريفهم كـ **friend functions** (مش member functions) عشان يقدروا يتعاملوا مع `cin` و `cout` من اليسار.
- `operator int()` (أو أي نوع تاني) بيتم تعريفه كـ **member function** بدون باراميترات، وبيُستخدم للتحويل التلقائي (implicit conversion).

مثال بسيط للتلاتة دول:

```cpp
friend istream& operator>>(istream& in, MyClass& obj);     // >> 
friend ostream& operator<<(ostream& out, const MyClass& obj);  // <<
operator int() const;                                      // int()
```









```cpp
#include <iostream>
using namespace std;

class Distance {
private:
    int feet;    // ≥ 0
    int inches;  // 0–11

public:
    Distance() : feet(0), inches(0) {}
    Distance(int f, int i) : feet(f), inches(i) {}

    // تحميل >>  (cin >> d)
    friend istream& operator>>(istream& in, Distance& d) {
        cout << "عدد الأقدام: ";
        in >> d.feet;

        cout << "عدد البوصات (0-11): ";
        in >> d.inches;

        // تحسين بسيط: لو البوصات زادت عن 11
        if (d.inches >= 12) {
            d.feet += d.inches / 12;
            d.inches %= 12;
        }

        return in;
    }

    // تحميل <<  (cout << d)
    friend ostream& operator<<(ostream& out, const Distance& d) {
        out << d.feet << " قدم و " << d.inches << " بوصة";
        return out;
    }
};

int main() {
    Distance d1(5, 9);
    Distance d2;

    cout << "ادخل مسافة جديدة:\n";
    cin >> d2;

    cout << "\nالنتيجة:\n";
    cout << "d1 = " << d1 << endl;
    cout << "d2 = " << d2 << endl;

    return 0;
}
```