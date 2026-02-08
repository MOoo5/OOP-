
# شرح التعامل مع Exceptions في C++



```cpp
#include <iostream>
using namespace std;

int main() {
    int hour;

    cin.exceptions(cin.failbit); // مش مهم اوي بس يفضل يعني نكتبه 

    try {
        cin >> hour;

        if (hour < 0)
            throw "error";

        cout << "the time is " << hour << ":00\n";
    }
    catch (char* e) {
        cout << "wrong value\n";
    }

    return 0;
}
```

فكرة الكود باختصار

الكود بيعرض مثال على استخدام Exceptions في C++ للتعامل مع:

إدخال غلط من المستخدم

أو قيمة غير منطقية (زي وقت بالسالب)

بدل ما البرنامج يكرش أو يكمل غلط، بنمسك الخطأ ونتعامل معاه بشكل آمن.


```cpp
try {
    cin >> hour;
}
```

بنحط أي كود متوقع يحصل فيه خطأ جوّه `try`.

لو المستخدم كتب حاجة غلط (مثلاً: `abc`)
→ هيحصل Exception.

```cpp
if (hour < 0)
    throw "error";
    ```
    
هنا بنعمل Exception بإيدنا:

لو الساعة بالسالب → ده منطقياً غلط

فبنرمي رسالة خطأ "error".

4. التنفيذ الطبيعي لو مفيش أخطاء
```cpp
cout << "the time is " << hour << ":00\n";
```
5. مسك الـ Exception (catch)
```cpp
catch (char* e) {   // ممكن نكتب كلمه const  عشان نحافظ علي ال علشان نحافظ على الـ const correctness.
    cout << "wrong value\n";
}

```

أي Exception من نوع `char*` هيتلقط هنا

سواء اللي جاية من:

`throw "error"`;

أو من `cin` لو الإدخال غلط.


## خلاصة السريعة

`try`
→ بنحط فيه الكود اللي ممكن يطلع Error

`throw`
→ بنرمي Exception لما نحس إن في مشكلة

`catch`
→ بنمسك الـ Exception ونتعامل معاه

`cin.exceptions(cin.failbit);`
→ بتخلي cin يرمي Exception تلقائيًا لو الإدخال غلط

---

# التعامل مع Exceptions باستخدام Class في C++

## الفكرة العامة

بدل ما نرمي Exception كنص (`throw "error"`)، بنعمل **Class خاص بالـ Exception**  
وده أحسن من ناحية:
- التنظيم
- إضافة معلومات أكتر عن الخطأ
- اتباع الـ Best Practices في C++

---



```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

// كلاس Exception مخصص
class InvalidHourException : public std::exception {
public:
    const char* what() const noexcept override {
        return "Invalid hour value! Hour must be between 0 and 23.";
    }
};

int main() {
    int hour;

    cin.exceptions(cin.failbit);

    try {
        cin >> hour;

        if (hour < 0 || hour > 23)
            throw InvalidHourException();

        cout << "the time is " << hour << ":00\n";
    }
    catch (const InvalidHourException& e) {
        cout << e.what() << endl;
    }
    catch (const std::exception& e) {
        cout << "Input error: " << e.what() << endl;
    }

    return 0;
}
```