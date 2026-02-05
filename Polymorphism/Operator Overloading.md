## ✅ يعني إيه Operator Overloading؟

يعني إنك **تعيد تعريف العمليات (زي + - * ==)** علشان تشتغل على **الكائنات (Objects)** اللي إنت عاملها في كلاس، مش بس الأرقام.

---

## ✅ ليه نستخدمها؟

علشان بدل ما تعمل دوال غريبة، تقدر تكتب كود طبيعي زي:

```cpp

c3 = c1 - c2;

```

وكأنك بتتعامل مع أرقام، بس دول كائنات من نوع `triangle`.

---

## ✅ شكل دالة الـ Overload:

جوا الكلاس بنكتب دالة بالشكل ده:

```cpp
<نوع_الراجع> operator<الرمز>(<كائن تاني>)

                                                       triangle operator-(triangle c2)
```

---

## ✅ المثال بتاعك بالشرح:

### 🔸 الكلاس:

```cpp
class triangle {
private:
    float width, height;

```

ده كلاس اسمه `triangle` فيه عرض وارتفاع.

---

### 🔸 Constructor:

```cpp
triangle(float a = 0, float b = 0)

```

علشان تقدر تنشئ كائن من غير ما تبعت له أرقام، أو تبعت له عرض وارتفاع.

---

### 🔸 الدوال:

```cpp
void getdata()      // تاخد قيم من المستخدم
void showdata()     // تطبع القيم

```

---

### 🔸 وده المهم: Operator Overload لـ

```cpp

triangle operator-(triangle c2) {
    triangle c3;
    c3.width = width - c2.width;
    c3.height = height - c2.height;
    return c3;
}

```

📌 الدالة دي معناها:

> "لما تعمل c1 - c2، هاتلي مثلث جديد c3 ناتج طرح عرض وارتفاع c2 من c1."
> 

---

## ✅ وفي `main()`:

```cpp

triangle c1, c2(3.5, 1.5), c3;

c1.getdata();          // تاخد قيم من المستخدم
c3 = c1 - c2;          // هنا استخدمنا operator overloading
c3.showdata();         // نطبع النتيجة

```

---

## 🔚 ملخص سريع:

| الحاجة | معناها |
| --- | --- |
| `operator-` | بتخلي `-` تشتغل على كائنات `triangle` |
| `c3 = c1 - c2` | معناها استدعاء `c1.operator-(c2)` |
| بنرجّع `triangle` | عشان نخزّن الناتج في `c3` |

الكود كامل#

```cpp
using namespace std;

class triangle
{
private:
    float width, height;

public:
    triangle(float a = 0, float b = 0)
    {
        width = a;
        height = b;
    }

    void getdata()
    {
        cout << "Enter width \n";
        cin >> width;
        cout << "Enter height \n";
        cin >> height;
    }

    void showdata()
    {
        cout << "width and height = (" << width << "," << height << ")" << endl;
    }

    triangle operator-(triangle c2)
    {
        triangle c3;
        c3.width = width - c2.width;
        c3.height = height - c2.height;
        return c3;
    }
};

int main()
{
    triangle c1, c2(3.5, 1.5), c3;
    c1.getdata();
    c3 = c1 - c2; // c1.operator-(c2)
    c3.showdata();
}
```