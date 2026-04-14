---
theme: ./slidev-theme-penguin-rtl
colorSchema: light
class: text-center
transition: slide-right
title: "المحاضرة 4: السجلات"
mdc: true
author: Dr. Ossama Nasser
exportFilename: 4- السجلات
layout: cover
hideInToc: true
---
# المحاضرة 4
## السجلات
### د. أسامه ناصر
2025-2026

---

```yaml
hideInToc: true
```
# الفهرس
<toc />

---

# ماهي السجلات
- السجلات هي نمط بيانات معقد يعتمد على تعريف مجموعة من الحقول ضمن نفس المتحول
<div grid="~ cols-2 gap-4">
<div>

```cpp{|1|2,5|3-4|5|}
struct Complex
{
double x;
double y;
};
```
</div>
<div>

- <v-click at="1">نستخدم الكلمة المفتاحية `struct` لنعلم المترجم أننا نريد أن ننشئ سجلًا خاصًا بنا يليها اسم النمط (في حالتنا هذه Complex)</v-click>
- <v-click at="2">يبدأ تعريف محتوى السجل (حقوله) بالرمز `{` وينتهي بالرمز`}`</v-click>
- <v-click at="3">نعرف حقلان هما x (الجزء الحقيقي)و y(الجزء العقدي)</v-click>
- <v-click at="4">يتم انهاء التعريف بالرمز `;`</v-click>
</div>
</div>

- <v-click at="5">نلاحظ أننا قمنا بجمع قيمتين ضمن قيمة واحدة، بمعنى آخر غلفنا قيمتين هما x وy باسم هو Complex</v-click>

---

```yaml
hideInToc: true
```

# ماهي السجلات
- تفيدنا السجلات بتجميع المتحولات المرتبطة بنفس الهدف في حزمة واحدة فقط
- لاستخدام السجل نستخدمه كنوع بيانات مثلًا `Complex number`
<div grid="~ cols-2 gap-1">
<div>

- <v-click at="1"> تعريف متحول من نوع Complex</v-click>
- <v-click at="2">نلاحظ أننا نستخدم الرمز `.` للوصول للحقول ضمن السجل</v-click>
- <v-click at="2">ندخل الحقول كل حقل على حدىً ونطبع الحقول كل حقل على حدىً</v-click>
</div>
<div>

```cpp{|6|7-10|}
struct Complex{
    double x;
    double y;
};
int main(){
   Complex number;
   cin>>number.x>>number.y;
   cout<<number.x<<
   ((number.y>=0)?" + ":" ")
   <<number.y<<"i"<<endl;
   return 0;
}

```
</div>
</div>
---

# تعريف السجلات
- تبين لنا كيفية تعريف سجل
- كيف يمكننا تهيئته بقيم ابتدائية؟
<div grid="~ cols-2 gap-1">
<div>

- <v-click at="1">تعريف المتحول وإسناد قيمتين للحقول xوy</v-click>
- <v-click at="2">تعريف المتحول وإسناد قيمة للحقل x</v-click>
- <v-click at="3">طباعة القيمة `2i+1`</v-click>
- <v-click at="4">طباعة القيمة `0i+1`</v-click>
	- <v-click at="4">يتم المعالجة مثل المصفوفة، الحقول التي لا تسند لها قيم تأخذ القيمة 0</v-click>
</div>
<div>



```cpp{|2|3|4-6|7-9|}
int main(){
Complex number1={1,2};
Complex number2={1};
cout<<number1.x<<
((number1.y>=0)?" + ":" ")
<number1.y<<"i"<<endl;
cout<<number2.x<<
((number2.y>=0)?" + ":" ")
<<number2.y<<"i"<<endl;
}
```

</div>
</div>

---

```yaml
hideInToc: true
```
# تعريف السجلات
- هل يمكننا استخدام سجل ضمن سجل ؟
- نعم، الحقول ضمن السجل هي متحولات
- مثال:
<div grid="~ cols-3 gap-1">
<div>

```cpp
struct Point{
double x;
double y;
};
```
</div>
<div>

```cpp
struct Triangle{
Point a;
Point b;
Point c;
};
//or
struct Triangle{
Point[3] heads;
};
```
</div>
<div>

```cpp
struct Rectangle{
Point a;
Point b;
Point c;
Point d;
};
//or
struct Rectangle{
Point[4] heads;
};
```
</div>
</div>
---

```yaml
hideInToc: true
```
# تعريف السجلات
- هنالك شروط محددة للتعريف الحقول ضمن سجل
<div grid="~ cols-2 gap-4">
<div>

```cpp
struct Complex
{
    double x;
    double y;
    Complex xc;
};
```
- هذا التعريف خاطئ, لا يمكن تعريف السجل ضمن نفسه
</div>
<div>

```cpp
struct Complex
{
    double x;
    double y;
    Complex* xc;
};
```
- هذا التعريف سليم، يمكن تعريف مؤشر على نفس نوع السجل ضمن نفسه
</div>
</div>
---

```yaml
hideInToc: true
```
# تعريف السجلات
- كل ما يلي صحيح
```cpp
Complex a;
Complex array[10];
Complex ptr=&a;
Complex ptrN=new Complex;
Complex &ref=a;
Complex ptrArray=new Complex[10];
```
---

# السجلات والتوابع
- تعامل السجلات مع التوابع مثل أي نوع من أنواع البيانات

<div grid="~ cols-2 gap-1">
<div>

```cpp
void print(Complex number){
cout<<number.x<<
((number.y>=0)?" + ":" ")
<<number.y<<"i"<<endl;
}

Complex create(){
Complex c={0};
return c;
}
```
</div>
<div>

```cpp
void enter(Complex& number){
cin>>number.x
   >>number.y;
}
void enter(Complex* number){
cin>>number->x
>>number->y;
}
```
</div>
</div>
---

# السجلات والمؤشرات
- يمكننا تعريف مؤشر على سجل `Complex * ptr` لكن سيحدث لدينا اختلاف في كيفية الوصول إلى حقول السجل
- يمكننا الوصول إلى حقول سجل باستخدام المؤشرات بطريقتين:
	- السهم - >
		- `ptr->x`
	- معامل *
		- <div dir="ltr">`(*ptr).x`</div>
		- العملية `.` لها أولوية أعلى من `*` وبالتالي `ptr.x*` تنفذ أولًا `.` أي الحصول على محتوى الحقل x ثم تنفيذ عملية الـ derefrencing
--- 

# التحميل الزائد للعمليات
- نحن نعلم أن Complex هو عدد عقدي يمكن تنفيذ العمليات الرياضية عليه، وبناءً على ذلك يفترض أن تعطي العملية التالية نتيجة:
```cpp
int main(){
Complex c1={1,2};
Complex c2={3,4};
cout<<c1+c2;
}
```

- إلا أن المترجم يعطي أخطاءً لما؟
- بكل بساطة، نحن من عرف العدد العقدي وليس المترجم وبالتالي هو لا يعرف كيف سينفذ عملية الجمع عليه وبناءً على ذلك سيرمي خطأ أثناء الترجمة
- كما نلاحظ أن العملية `>>` غير معرفة بالنسبة للعدد العقدي لنفس السبب مما يتسبب بخطأ ترجمة
--- 

```yaml
hideInToc: true
```
# التحميل الزائد للعمليات
- أن نوضح لـ ++C كيفية تنفيذ هذه العمليات على السجلات
- الشكل الأول:
```cpp
struct Complex
{
    double x;
    double y;
};
Complex& operator+(Complex& n1,Complex n2){
n1.x+=n2.x;
n1.y+=n2.y;
return n1;
}
ostream& operator<<(ostream& cout,Complex & n){
cout<< n.x<<((n.y>=0)?" + ":"" )<< n.y<<"i";
return cout;
}
```
---

```yaml
hideInToc: true
```
# التحميل الزائد للعمليات
- أن نوضح لـ ++C كيفية تنفيذ هذه العمليات على السجلات
- الشكل الثاني:
```cpp
struct Complex
{
    double x;
    double y;
Complex& operator+(Complex n2){
this->x+=n2.x;
this->y+=n2.y;
return *this // will talk about this later
}
};
ostream& operator<<(ostream& cout,Complex & n){
cout<< n.x<<((n.y>=0)?" + ":"" )<< n.y<<"i";
return cout;
}
```
---

```yaml
hideInToc: true
```
# التحميل الزائد للعمليات
- أن نوضح لـ ++C كيفية تنفيذ هذه العمليات على السجلات
- الشكل الثالث:
```cpp
struct Complex
{
    double x;
    double y;
friend ostream& operator<<(ostream& cout,Complex & n){
cout<< n.x<<((n.y>=0)?" + ":"" )<< n.y<<"i";
return cout;
}
//we will talk about friends later (if you have any)
};
Complex& operator+(Complex& n1,Complex n2){
n1.x+=n2.x;
n1.y+=n2.y;
return n1;
}
```
---

```yaml
hideInToc: true
```
# التحميل الزائد للعمليات
- أن نوضح لـ ++C كيفية تنفيذ هذه العمليات على السجلات
- الشكل الرابع:
```cpp
struct Complex
{
    double x;
    double y;
friend ostream& operator<<(ostream& cout,Complex & n){
cout<< n.x<<((n.y>=0)?" + ":"" )<< n.y<<"i";
return cout;
}
//we will talk about friends later (if you have any)
Complex& operator+(Complex n2){
this->x+=n2.x;
this->y+=n2.y;
return *this // will talk about this later
}};
```
---

# التحميل الزائد للعمليات
- عليكم الآن تحقيق الطرح والقسمة والضرب
<img src="./media/4/sukuna.png" class="w-180"> 