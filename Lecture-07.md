---
theme: ./slidev-theme-penguin-rtl
colorSchema: light
class: text-center
transition: slide-right
title: "المحاضرة 7: الصفوف"
mdc: true
author: Dr. Ossama Nasser
exportFilename: 7- الصفوف
layout: cover
hideInToc: true
---
# المحاضرة 7
## الصفوف
### د. أسامه ناصر
2025-2026

---

```yaml
hideInToc: true
```
# الفهرس
<toc />

---

# مفاهيم عامة
- ما هي مواصفات السيارة؟
	- اللون، الحجم، عدد المقاعد
	- سعة المحرك، استطاعته ونوعه (بنزين، ديزل، كهرباء) أو سيارة هجينة
	- الشركة المصنعة، الموديل وعام التصنيع
	- نوع القيادة: خلفي، أمامي أو دفع رباعي
	- نظام الفرملة
	- مواصفات الرفاهية (مكيف، مقاعد تحتوي تدليك وتدفئة)
	- ... الخ
- كما تمتلك السيارة مجموعة من الوظائف:
	- الوظيفة الأساسية النقل
	- وظائف أخرى:
		- عند الضغط على الفرامل تتوقف السيارة
		- عند الضغط على دواسة الوقود ومع وضع السيارة في وضع القيادة تتحرك السيارة للأمام
---

```yaml
hideInToc: true
```
# مفاهيم عامة
- مجموعة المواصفات (الخصائص) والمهام معًا تشكل السيارة
- البرمجة الغرضية التوجه هي مفهوم برمجي يعمل على إسقاط مفاهيم من الواقع على المفاهيم البرمجية
- من الناحية التقنية تشابه الصفوف السجلات
- تمتلك بالإضافة للحقول مهام ومحددات وصول
- بواني وهوادم
---

# الصفوف
- الصفوف هي البنية الأساسية في البرمجة الغرضية التوجه
- في لغة ++C يتم تعريف الصف بالشكل التالي:
<div grid="~ cols-2 gap-2">
<div>

```cpp
class student{
private:
	long id;
	string firstName;
	string lastName;
	float points;
	int marks[62];
public:
	void changeMarks(int i,int v);
};
```
</div>
<div>

```cpp
struct student{
	long id;
	string firstName;
	string lastName;
	float points;
	int marks[62];
};
```
</div>
</div>

- نلاحظ الاختلاف بين تعريف السجل وتعريف الغرض (قمنا بإضافة حقل يحتوي علامات الطالب في كل المواد في الكلية)
---


```yaml
hideInToc: true
```
# الصفوف
<div grid="~ cols-2 gap-4">
<div>

```cpp{|1|2|3-7|8|9|10|}
class student{
private:
	long id;
	string firstName;
	string lastName;
	float points;
	int marks[62];
public:
	void changeMarks(int i,int v);
};
```
</div>
<div>

- تم تعرف الصف student متضمنًا الحقول التالية:
	- id الرقم الجامعي للطالب
	- firstName الاسم
	- lastName الكنية
	- points معدل الشهادة الثانوية
	- marks مصفوفة تحوي علامات الطالب خلال مسيرته الدراسية
- والتابع التالي:
	- changeMarks لتغير علامة طالب ضمن مادة
</div>
</div>
---

```yaml
hideInToc: true
```
# الصفوف
- طيب يا دكتور، ليش عم نعمل هيك؟
- ألا يمكن أن نغير القيمة مباشرة ضمن السجل ؟
	- نعم يمكننا لكن بكثير من الأحيان توجد قيود على القيم التي يتم التعديل عليها
	- مثلًا التحقق من صحة العلامة (بين 0 و100) التأكد من صحة رقم المادة (بين 0 و61)
	- هذا لا يمكن تنفيذه في السجل ولكن يمكن تنفيذه في الغرض
---

```yaml
hideInToc: true
```
# الصفوف
<div grid="~ cols-2 gap-4">
<div>

```cpp{|1|2|3|}
void student::changeMark(int i,int v){
if(i>=0 && i<62 && v >= 0 && v <=100)
marks[i]=v;
}
```
</div>
<div>

- <v-click at="1">هنا نحدد أن التابع changeMarks يتبع للصف student, أي أننا نفهم أن كل ما يلي `::student` تابع للصف student</v-click>
- <v-click at="2">نتفخص الوسائط</v-click>
- <v-click at="3">في حال كانت قيم الوسطاء سليمة، نغير العلامة</v-click>
- <v-click at="4">لقد ذكرنا سابقًا أن التابع يعتبر مجال رؤية معزول، أي أنه لا يرى المجال الذي استدعاه، نستثني من هذه القاعدة أن يكون التابع عضو ضمن صف، يصبح في هذه الحالة مجال رؤية التابع يحتوي حقول الصف الذي هو عضو فيه, هذا ما يمكننا من استخدام المتحول `marks` من الصف ضمن التابع `changeMarks`</v-click>
- <v-click at="5">يمكننا كتابة كود التابع ضمن تعريفه في الصف مباشرةً، إلا أن الطريقة المعتمدة هي  كتابته خارج الصف</v-click>
</div>
</div>

---

# محددات الوصول
- تشجع البرمجة الغرضية التوجه على مبدأ التغليف وإخفاء التفاصيل
- بمعنى آخر لا يهمنا كيف يتم يعمل الغرض على تخزين معلومات الطالب، المهم أننا نحصل على المعلومات التي نريدها وقت مانريدها بالشكل الصحيح
- المحدد private يعني أن التوابع والحقول الموجودة هنا خاصة، لا أحد قادر على الوصول إليها سوى التوابع ضمن الصف نفسه والأصدقاء (لاحقًا)
- المحدد public يعني أن كل الكرة الأرضية تمتلك القدرة على الوصول لهذه التوابع والحقول
---

## البناء والهدم
- هنالك مفاهيم محددة يجب الاطلاع عليها مثل البناء والهدم والفرق بين الصف والغرض
- يمكننا النظر إلى الصف على أنه البنية التي تحتوي الحقول والتوابع structure
- الغرض هو الصف عندما يتم بناؤه، أي البنية والقيم structure + value
- عملية البناء تعنى بإنشاء الغرض وإسناد قيم أولية initial values للحقول الموجودة فيه
- الهدم هي مجموعة العمليات التي يتم تنفيذها عند الانتهاء من الغرض وحذفه من الذاكرة
---

## البناء
- الباني هو تابع خاص ضمن الصف يمتلك نفس اسم الصف
- في لغة ++C لدينا 3 أنواع من البواني:
	- الباني الافتراضي (الذي لا يحتاج وسطاء)
	- الباني ذو الوسطاء
	- الباني الناسخ
---

```yaml
hideInToc: true
```
## البناء
- الباني الافتراضي
<div grid="~ cols-2 gap-1">
<div>

```cpp{|5|8|9|10|}
class student{
...
public:
	...
	student();
	
};
student::student(){
id=0;firstName="";lastName="";points=0;
for(int i=0;i<62;i++) marks[i]=0;
}
```
</div>
<div>

- <v-click at="1">تعريف الباني</v-click>
- <v-click at="2">تعريف كود الباني</v-click>
- <v-click at="3">إعطاء قيم ابتدائية للمتحولات</v-click>
- <v-click at="4">تهيئة مصفوفة العلامات</v-click>
</div>
</div>
---

```yaml
hideInToc: true
```
## البناء
- الباني الافتراضي
	- استدعاء الباني
<div grid="~ cols-2 gap-4">
<div>

```cpp{|1|2|}
student x();
student y;
```
</div>
<div>

- <v-click at="1">يتم استدعاء باني الغرض من خلال وضع قوسين بعد المتحول وفي حال عدم تمرير عدم أي وسيط نستخدم الباني الافتراضي</v-click>
- <v-click at="2">هنا نلاحظ أننا لم نضع أي قوس بعد اسم المتحول المعبر عن الغرض، هذه الطريقة في الكتابة تستدعي الباني الافتراضي</v-click>
</div>
</div>
---

```yaml
hideInToc: true
```
## البناء
- الباني ذو الوسطاء
	- يتم تمرير وسطاء في هذا الباني
<div grid="~ cols-2 gap-4">
<div>

```cpp
class student{
...
public:
	...
	student(long, string,string,points);
};
```
</div>
<div>

```cpp
student::student(long id,string fisrtName,string lastname,float ponits){
	id=id;
	firstName=firstName;
	lastName=lastName;
	points=points;
	for(int i=0;i<62;i++) marks[i]=0;
}
```
</div>
</div>
---

```yaml
hideInToc: true
```
## البناء
- الباني ذو الوسطاء
	- يتم تمرير وسطاء في هذا الباني
<div grid="~ cols-2 gap-4">
<div>
```cpp
student::student(long id,string fisrtName,string lastname,float ponits){
	id=id;
	firstName=firstName;
	lastName=lastName;
	points=points;
	for(int i=0;i<62;i++) marks[i]=0;
}
```
</div>
<div>

- السؤال المهم: هل التعبير `id=id` صحيح
	- قواعديًا نعم، منطقيًا لا
	- لنتذكر الملاحظة أن مجال رؤية التابع العضو في صف يتضمن التابع والصف الذي هو عضو فيه
	- في حالتنا هذه لدينا متحولين باسم id الأول وسيط للتابع والثاني حقل ضمن الصف
	- أيهما أقرب للتابع ؟ الوسيط أم حقل؟ الوسيط طبعًا
	- لذلك يعمل المترجم على اعتبار id تشير إلى الوسيط وليس للحقل
	- ما الحل؟
		- لدينا حلان، الأول إعادة تسمية الوسيط والثاني استخدام المؤشر `this`
</div>
</div>
---

```yaml
hideInToc: true
```
## البناء
- الباني ذو الوسطاء
	- يتم تمرير وسطاء في هذا الباني
<div grid="~ cols-2 gap-4">
<div>
```cpp{|2|2|2,8|2,9|6|}
student::student(long id,string fisrtName,string lastname,float ponits){
	this->id=id;
	this->firstName=firstName;
	this->lastName=lastName;
	this->points=points;
	for(int i=0;i<62;i++) marks[i]=0;
}
student x(1,"a","b",232);
student y(2,"za","vb",432);
```
</div>
<div>

- <v-click at="1">this هو مؤشر خاص ضمن لغة ++c يشير الغرض الذي استدعى هذا التابع</v-click>
- <v-click at="2">نلاحظ أننا استخدمنا المؤشر this لاستدعاء الحقل بمعنى آخر ميزنا بين id التي هي حقل وid التي هي وسيط</v-click>
- <v-click at="3">في هذا الاستدعاء قام الغرض x باستدعاء الباني ذو الوسطاء، وعليه فإن قيمة this ضمن هذا الباني تشير إلى الغرض x أي أن `this=&x`</v-click>
- <v-click at="4">في هذا الاستدعاء قام الغرض y باستدعاء الباني ذو الوسطاء، وعليه فإن قيمة this ضمن هذا الباني تشير إلى الغرض x أي أن `this=&y`</v-click>
- <v-click at="5">لعدم تعريف المتحول marks ضمن التابع لسنا ملزمين باستخدام المؤشر this</v-click>
</div>
</div>
---

```yaml
hideInToc: true
```
## البناء
- الباني الناسخ
	- نستخدم هذا الباني لنسخ القيم من غرض لآخر
<div grid="~ cols-2 gap-4">
<div>

```cpp
class student{
...
public:
	...
	student(student&);
};
```
</div>
<div>

```cpp
student::student(student& c){
	id=c.id;
	firstName=c.firstName;
	lastName=c.lastName;
	points=c.points;
	for(int i=0;i<62;i++) marks[i]=c.marks[i];
}
```
</div>
</div>

- نقوم بنسخ القيم
- مررنا الوسيط c بالمرجع لتجنب استنساخ الغرض في الذاكرة
---

## الهادم
- يتسخدم الهادم لتنظيم بعض العمليات أثناء حذف الغرض من الذاكرة
- يسمح لنا ذلك بإغلاق الملفات وحذف المؤشرات والمصفوفات الديناميكية من الذاكرة في المراحل الأخيرة من عمر الغرض في الذاكرة

```cpp
class student{
...
public:
	...
	~student();
};
```

- لا يمتلك الهادم أي وسيط، وله نفس اسم الصف يسبقه الرمز ~
- إذا لم يتم تعريف أي هادم يتم إضافة هادم فارغ
- إذا لم يتم تعريف أي باني يتم إضافة باني فارغ بدون وسطاء

---

```yaml
hideInToc: true
```
## البناء والهدم
- ترتيب الاستدعاء عند تعريف الغرض محليًا
	- يتم استدعاء الباني دومًا بصفة أول تابع في الصف
	- يستدعى الهادم من قبل المترجم في آخر سطر من مجال الرؤية الذي تم تعريف الغريض فيه
	- إذا لم يتم إنهاء البرنامج بشكل سليم لن يستدعى الهادم
- ترتيب الاستدعاء للأغراض العامة Global
	- يتم بناء الأغراض اتعرف بصفة متحولات متحولات عامة Global قبل استدعاء أي تابع في البرنامج
	- يتم استدعاء الهادم في نهاية تنفيذ البرنامج إذ تمت بشكل سليم
	- إذا لم يتم إنهاء البرنامج بشكل سليم لن يستدعى الهادم
- ترتيب الاستدعاء للاغراض الساكنة static
	- يتم استدعاء الباني لمرة واحدة فقط عند الوصول لسطر تعريف المتحول الساكن للمرة الأولى
	- يتم استدعاء الهادم في نهاية تنفيذ البرنامج إذ تمت بشكل سليم
	- إذا لم يتم إنهاء البرنامج بشكل سليم لن يستدعى الهادم
---

```yaml
hideInToc: true
```
## البناء والهدم
- لدينا الكود التالي:
<div grid="~ cols-3 gap-1">
<div>
```cpp
class student{
  private:
   long id;
   string firstName;
   string lastName;
   float points;
   int marks[62];
  public:
   student();
   student(long,string,
   string,float);
   ~student();};
```
</div>
<div>
```cpp
student::student(){}
student::student(long id,string firstName,
string lastName,float points){
this->id=id;
this->firstName=firstName;
this->lastName=lastName;

```
</div>
<div>
```cpp
this->points=points;
cout<<"Building student with Id: "
<<id<<endl;
}
student::~student(){
cout<<"Destroying student with Id: "<<id<<endl;}
```
</div>
</div>
---

```yaml
hideInToc: true
```
## البناء والهدم
والاستدعاء التالي:
```cpp
student gl(10,"first","First",22);

int main(){
cout<<"main starts"<<endl;
  student mn(11,"second","Second",33);
  cout<<"the loop starts"<<endl;
  for (int i=0;i<5;i++)
    student mm(12+i,"third","Thrid",44);
cout<<"the loop ends"<<endl;   
cout<<"main ending"<<endl;
return 0;
}
```
---

```
Building student with Id: 10
main starts
Building student with Id: 11
the loop starts
Building student with Id: 12
Destroying student with Id: 12
Building student with Id: 13
Destroying student with Id: 13
Building student with Id: 14
Destroying student with Id: 14
Building student with Id: 15
Destroying student with Id: 15
Building student with Id: 16
Destroying student with Id: 16
the loop ends
main ending
Destroying student with Id: 11
Destroying student with Id: 10
```
---

# Getters  & Setters
- كيف يمكن لنا أن نقرأ قيم الحقول بعد البناء في الغرض إذا كانت هذه الحقول private
- الحل بكل بساطة باستخدام توابع تعرف باسم getters
	- مجموعة من التوابع تعطي القيم الخاصة بالحقول الموجودة ضمن الصف
	- سمية بهذا الاسم لأنها عادةً تبدأ بالكلمة get
```cpp
class student{
...
public:
	...
	long getId(){return id;}
	string getFirstName(){return firstName;}
	string getLastName(){return lastName;}
	float getPoints(){return points;}
};
```
---

```yaml
hideInToc: true
```
# Getters  & Setters
- كيف يمكن لنا أن نعدل قيم الحقول بعد البناء في الغرض إذا كانت هذه الحقول private
- الحل بكل بساطة باستخدام توابع تعرف باسم setters
	- مجموعة من التوابع تعطي القيم الخاصة بالحقول الموجودة ضمن الصف
	- سمية بهذا الاسم لأنها عادةً تبدأ بالكلمة get
```cpp
class student{
...
public:
	...
	long setId(long v){id=v;}
	string setFirstName(string firstName){student::firstName=firstName;}
	string setLastName(string firstName){ this->lastName=lastName;}
	float setPoints(float x){ points=x;}
	};
```
---

# فوائد الصفوف
- تبسيط البرمجة
	- من خلال دمج المنطق (التوابع) مع البيانات (الحقول) ضمن كتلة واحدة تصبح عملية البرمجة أسهل وأكثر وضوحًا
- الوجهات
	- لا نقصد هنا الواجهات البرمجية
	- نقصد الواجهات البرمجية Programming Interface
	- ماذا يعني هذا؟ لا يهم كيف يعمل الغرض في الداخل، المهم أننا نحصل على النتيجة المطلوبة
- إعادة استخدام البرمجيات Software Resuse
	- إمكانية إعادة استخدام الكود المكتوب من خلال:
		- التركيب Composition: استخدام غرض ضمن غرض
		- الوراثة Inheritance: صف جديد يرث صف قديم
---

# مجال الرؤية في الصف
- أي تابع أو عنصر ضمن الصف قادر على رؤية محتويات الصف كاملًا
- أي تابع ضمن الصف قادر على رؤية العناصر (المتحولات\الحقول، التوابع) ضمن هذا الصف
	- في حال وجد ضمن التابع متحول يحمل نفس اسم متحول\حقل ضمن الصف فوفقًا لقواعد مجال الرؤية (الأقرب أولًا) سيرى التابع المتحول الخاص به وليس حقل الصف
	- لحل هذه المشكلة نستخدم إما المتحول `this` أو `ClassName::VariableName`
- للوصول لعناصر الصف نتعامل معه بالشكل التالي:
```cpp
	Class1 c;
	Class1 *c1=new Class1()
	c.function1();
	c1->function1();
	(*c1).function1();
```

---

# فصل الكود عن الواجهة
- مالذي نعنيه عندما نقوم بكتابة الكود
```cpp
#include<iostream>
```

- أي أننا نلجأ لقراءة الملف `iostream.h` لمعرفة محتوياته
- هذا الملف يسمى بالملف الرئسي ويحتوي فقط التعاريف دون أي منطق برمجي
- المنطق البرمجي يكون موجود ضمن ملف `cpp` مرافق له بنفس الاسم `iostream.cpp`
- مالغرض من هذه العملية؟
	- عندما ترغب بتوزيع الكود الذي تعبت وأنت تكتبه، كي تتجنب سرقته والتلاعب به تلجأ لتحويله إلى ملفات تنفيذية (صيغة dll)
	- تقوم بإرسال الملفات الرئسية `headers` مع الملفات التنفيذية `dll` إلى من يريد استخدامه وبالتالي تتضمن ألّا يتم التلاعب بالكود الخاص بك
--- 

```yaml
hideInToc: true
```
# فصل الكود عن الواجهة
## لنقم بتجهيز العملية هذه لكودنا الخاص بالصف student
محتويات الملف `student.h`
<div grid="~ cols-2 gap-1">
<div>

```cpp
#ifndef STUDENT_H
#define STUDENT_H
#include<string>
using namespace std;
class student{
  private:
    long id;
    string firstName;
    string lastName;
    float points;
    int marks[62];
```
</div>
<div>

```cpp
  public:
    student();
    student(student&);
    student(long,string,
    string,float);
    ~student();
    void changeMark(int,int);
    long getId();
    string getFirstName();
    string getLastName();   
```
</div>

</div>
--- 

```yaml
hideInToc: true
```
# فصل الكود عن الواجهة
## لنقم بتجهيز العملية هذه لكودنا الخاص بالصف student
محتويات الملف `student.h`


```cpp
float getPoint();
    int getMark(int);
    void setId(long);
    void setFirstName(string);
    void setLastName(string);
    void setPoints(float);
};
#endif
```
---

```yaml
hideInToc: true
```
# فصل الكود عن الواجهة
## لنقم بتجهيز العملية هذه لكودنا الخاص بالصف student
محتويات الملف `student.h`
<div grid="~ cols-2 gap-1">
<div>

```cpp{|1,2|11|}
#ifndef STUDENT_H
#define STUDENT_H
#include<string>
using namespace std;
class student{
  private:
  ....
  public:
  ...
  }
  #endif
```
  </div>
  <div>
  
  - <v-click at="1">السطر الأول والثاني بدء عملية تعريف الملف الرئسي</v-click>
  - <v-click at="2">السطر الأخير إنهاء عملية التعريف</v-click>
  </div>
  </div>
---

```yaml
hideInToc: true
```
# فصل الكود عن الواجهة
## لنقم بتجهيز العملية هذه لكودنا الخاص بالصف student
محتويات الملف `student.cpp`
```cpp
#include "student.h"

using namespace std;
student::student(){
  points=0;
  id=0;
  firstName="";
  lastName="";
  for(int i=0;i<62;i++)
    marks[i]=0;
}
...
```
---

```yaml
hideInToc: true
```
# فصل الكود عن الواجهة
- استخدام ضمن الـ main
<div grid="~ cols-2 gap-1">
<div>


```cpp
#include<iostream>
#include<string>
#include "student.h"
using namespace std;
int main(){
student c;long id;
string firstName,lastName;
float points;
cin>>id>>firstName
>>lastName>>points;
c.setId(id);
c.setFirstName(firstName);
c.setLastName(lastName);
c.setPoints(points);
}
```
</div>
<div>

- نلاحظ الفرق بين عمليتي الـ include للملفات التي جاءت مع ++C (مثل iostream وstring) بأنها ضمن `<>`
- أما ملفنا الخاص فهو ضمن `""`
</div>
</div>
---

# مشكلة المرجع
- من المشاكل التي يمكن أن نعاني منها أن نعيد قيمة من أحد عناصر التابع الخاصة private بالمرجع
```cpp
class student{
  private:
  ...
  public 
  ...
  long& getId();
  ...
  };
```

- نلاحظ تعديل التابع `getId` ليعيد القيمة بالمرجع
---

```yaml
hideInToc: true
```
# مشكلة المرجع
- من المشاكل التي يمكن أن نعاني منها أن نعيد قيمة من أحد عناصر التابع الخاصة private بالمرجع

```cpp
student c;
...
long& x=c.getId();
x=10;
cout<<c.getId();
```

- تكون قيمة الخرج 10 مما يعني أن التعديل على القيمة المعادة بالمرجع أثر على القيمة المخزنة ضمن الغرض دون المرور بالتابع `setId` ضاربين بعرض الحائط قواعد محددات الوصول
---

```yaml
hideInToc: true
```
# مشكلة المرجع
- في هذه الحالة لا يجب استخدام الإعادة بالمرجع
<img src="./media/7/zat.jpg">