### 1. ⛳ تعريف سريع:

---

- **Destructor** = دالة بتشتغل **لما الأوبجكت يخلص عمره**  
  (يعني يخرج من المكان اللي اتعرّف فيه).
- شكلها:
  ```cpp
  ~اسم_الكلاس()
  ```

---

### 2. 📌 خصائص مهمة:

- مالوش باراميتر (مش بياخد أي مدخلات).
- مالوش return (حتى مش `void`).
- الكلاس بيكون فيه **Destructor واحد بس**.
- مينفعش نعمل أكتر من Destructor (مفيش Overload).

---

### 3. ⏱️ إمتى بيشتغل؟

- لما الأوبجكت يخرج من **نهاية الـ scope**.
- أو لما تعمل `delete` لو الأوبجكت معمول بـ `new`.
- لو عرّفت أوبجكت جوه أي function أو constructor  
  **أول ما السكوب يخلص** الـ Destructor بيتنادى تلقائي.

---

### 4. 🎯 بيعمل إيه؟

- بينضف الموارد اللي كان الأوبجكت مستخدمها، زي:
  - حذف الميموري (`delete`)
  - قفل ملفات
  - طباعة رسالة أو تنفيذ أي شغل قبل ما الأوبجكت "يموت"

---

### 5. 💡 ترتيب التدمير:

- الكائنات بتتدمر **عكس ترتيب إنشائها**.

> آخر واحد اتعمل → أول واحد يتدمر

---

### ✨ مثال عملي كامل:

```cpp
#include <bits/stdc++.h>
using namespace std;

class Football {
private:
    string team_name, coach;
    int team_member;

public:
    // ✨ Constructor
    Football(int members, string t_name, string c_name) {
        team_member = members;
        team_name = t_name;
        coach = c_name;
        cout << "Constructor called for team: " << team_name << '\n';
    }

    // ✨ Destructor
    ~Football() {
        cout << "Destructor called for team: " << team_name << '\n';
    }

    void print() {
        cout << "\n--- Team Info ---\n";
        cout << "Members: " << team_member << '\n';
        cout << "Team Name: " << team_name << '\n';
        cout << "Coach: " << coach << '\n';
    }
};

void Fulla() {
    int team_member;
    string team_name, coach;

    cin >> team_member >> team_name >> coach;

    // هنا الكائن بيتعمل داخل الـ scope
    Football m(team_member, team_name, coach);
    m.print();

    // عند نهاية Fulla()
    // الكائن m هيتدمر تلقائيًا ويتنادى الـ Destructor
}

int main() {
    int t = 1;
    // cin >> t;
    while (t--) {
        Fulla();
    }
}
```

---

### 🧠 مثال توضيحي بسيط:

```cpp
{
    Football f(11, "Madrid", "Zidane");
}
// ← هنا Destructor يشتغل بعد القوس ده مباشرة
```
