---
theme: ./slidev-theme-penguin-rtl
colorSchema: light
class: text-center
transition: slide-right
title: "المحاضرة 8: الصفوف الجزء الثاني"
mdc: true
author: Dr. Ossama Nasser
exportFilename: 8- الصفوف  الجزء الثاني
layout: cover
hideInToc: true
---
# المحاضرة 8
## الصفوف الجزء الثاني
### د. أسامه ناصر
2025-2026

---

```yaml
hideInToc: true
```
# الفهرس
<toc />

---

```yaml
hideInToc: true
```
# في الحلقة السابقة
- تعرفنا على الصفوف
- كيفية التعامل معها
- توابع الـ Getter وSetter
---

# أثر الكلمة const على الصفوف والأغراض
- عندما نعمل على تعريف صف class جديد نحن نعمل على تعريف نمط بيانات جديد Data Type
- يمكن أن يستخدم هذا النمط مع الكلمة const
```cpp
const class1 c;
```

- قمنا بتعريف غرض من الصف class1 وحددنا أنه ثابت
- في ++C إذا كان الغرض ثابت يجب ألا يكون قابلًا للتعديل لا هو ولا محتوياته
- بمعنى آخر يجب أن نحدد بعض التوابع على أنها const والبعض الآخر عادي
- ؟؟؟
---

```yaml
hideInToc: true
```
# أثر الكلمة const على الصفوف والأغراض
- بفرض لدينا الصف التالي:
```cpp
class Time{
private:
	int hour,minute,second;
public:
	Time(int=0,int=0,int=0);
	void setHour(int);
	void setMinute(int);
	void setSecond(int);
	void setTime(int,int,int);
	int getHour();
	int getMinute();
	int getSecond();
	void printMilitary();
	void printStandard();
};
```
---


```yaml
hideInToc: true
```
# أثر الكلمة const على الصفوف والأغراض
- بفرض لدينا الصف التالي:
```cpp
void Time::Time(int h=0,int m=0,int s=0){setTime(h,m,s);}
void Time::setHour(int h){hour=(h>=0 && h<24)? h:0;}
void Time::setMinute(int m){minute=(m>=0 && m<60)? m:0;}
void Time::setSecond(int s){second=(s>=0 && s<60)? s:0;}
void Time::setTime(int h,int m,int s){
	setHour(h); setMinute(m); setSecond(s);
}
int Time::getHour(){return hour;}
int Time::getMinute(){return Minute;}
int Time::getSecond(){return Second;}
void Time::printMilitary(){cout<<h<<m<<s;}
void printStandard(){cout<<((h>12)?h-12:h)<<":"<<m<<":"<<s<<" "<<((h>=12)?"PM":"AM");}
```
---


```yaml
hideInToc: true
```
# أثر الكلمة const على الصفوف والأغراض
- في حال أردنا أن نعرف الغرض على أنه const يجب أن يسبق تعريف الغرض الكلمة المفتاحية const
```cpp
const bdate(1,1,1991);
```

- في لغة ++C أن يكون الغرض ثابت يعني أن تكون أعضاء الغرض نفسه ثابتة
	- أي بما أن الغرض ثابت فيجب ألا نمتلك القدرة على تعديل محتويات هذا الغرض، لذلك يمكننا وسم بعض التوابع الأعضاء member function ضمن صف ما على أنها توابع ثابتة
	- أي يمكن استدعاء هذه التوابع في حال كان الغرض ثابتًا وأي تابع غير موسوم على أنه ثابت لا يمكن استدعائه
---

```yaml
hideInToc: true
```
# أثر الكلمة const على الصفوف والأغراض
<div grid="~ cols-2 gap-2">
<div>

```cpp{10-13}
class Time{
private:
	int hour,minute,second;
public:
	Time(int=0,int=0,int=0);
	void setHour(int);
	void setMinute(int);
	void setSecond(int);
	void setTime(int,int,int);
	int getHour() const;
	int getMinute() const;
	int getSecond() const;
	void printMilitary() const;
	void printStandard();
};
```
</div>
<div>

-نلاحظ وجود كلمة const في نهاية تعريف التابع، مما يسمح لنا باستدعاء هذا التابع في حال كان الغرض const
</div>
</div>
---

```yaml
hideInToc: true
```
# أثر الكلمة const على الصفوف والأغراض
- لا يؤثر إضافة كلمة const في تعريف التابع على كود التابع
```cpp
int Time::getHour() const{return hour;}
int Time::getMinute() const{return Minute;}
int Time::getSecond() const{return Second;}
void Time::printMilitary() const{cout<<h<<m<<s;}
```
---

```yaml
hideInToc: true
```
# أثر الكلمة const على الصفوف والأغراض
- التأثير في الاستدعاء
- التابع الموسوم بكلمة const يمكن استدعائه في حال كان الغرض ثابت أو متحول
- في حال كان الغرض ثابت const عندها لا يمكن سوى استدعاء التوابع الموسومة بـ const
<div grid="~ cols-2 gap-2">
<div>

```cpp{|1-2|3|4-5|6|7-8|9|}
Time t(10,12,13);
const Time c(10,12,13);
t.setHour(15);
cout<<t.getMinute()<<endl;
t.printMilitary();
t.printStandard();
cout<<c.getMinute()<<endl;
c.printMilitary();
c.printStandard();
```
</div>
<div>

- <v-click at="1">تعريف غرضين الأول متحول عادي variable والثاني ثابت constant</v-click>
- <v-click at="2">استدعاء التابع setHour **الغير** موسوم بالكلمة const على الغرض المتغير variable</v-click>
- <v-click at="3">استدعاء التوابع الموسومة بالكلمة const على الصف المتغير variable </v-click>
- <v-click at="4">استدعاء تابع غير موسوع بالكلمة const</v-click> 
- <v-click at="5">استدعاء توابع موسومة بالكلمة const على غرض const</v-click>
- <v-click at="6">التابع printStandard غير موسوع بالكلمة const وبالتالي لا يمكن استدعائه على غرض ثابت const مما يسبب خطأ في المترجم لعدم قدرتنا على استدعاء تابع غير ثابت على غرض ثابت</v-click>
</div>

</div>
---

# حقل ثابت ضمن الغرض
- مالذي يمكن أن يحدث في حال كان حقل ضمن الغرض من نوع const مالذي سيحدث؟
```cpp
class Increment{
	public:
		Increment(int c=0, int i=1);
		void addIncrement() { count += increment; }
		void print() const {cout << "count = " << count << ", increment = " << increment << endl;}
	private:
		int count;
		const int increment;

}
```

- نحن نعرف أن أي قيمة تسبقها كلمة const تعني أنها قيمة ثابتة
- في هذه الحالة يجب إعطاء هذا الثابت قيمة قبل استخدام الغرض
- يتم تفعيل ذلك في الباني
---

```yaml
hideInToc: true
```

# حقل ثابت ضمن الغرض
- في هذه الحالة يكون تحقيق الباني بالشكل التالي:
```cpp
Increment::Increment(int c=0,int i=1):increment(i){
count=c;
}
```

- المميز هنا ما يوجد بعد بالنقطتين في الباني وقبل أقواس الكود
	`increment(i)`
- هذه تعني أننا نهيء قيمة الحقل increment بالقيمة i التي تم تمريرها في الباني
- بناءً على ذلك يتم تهيئة قيمة الثابت increment عند بناء الغرض، وبالتالي في كل مرة نبني الغرض نعطي قيمة مختلفة لهذا الثابت وتبقى القيمة ثابتة طوال دورة حياة الغرض (لكل غرض على حدىً)
- هذه الطريقة تجبر المترجم على إسناد القيم قبل تنفيذ كود الباني، بمعنى آخر يتم إضافة أسطر إضافية في بداية الباني من قبل المترجم لتنفيذ هذه التعليمات قبل تنفيذ أي كود ضمن الباني مما يضمن اسناد قيم للثوابت
- هذه الطريقة في إسناد القيم قابلة للاستخدام مع أي نوع من الحقول وليس فقط الثوابت، لكنها الطريقة الوحيدة للثوابت
---

```yaml
hideInToc: true
```

# حقل ثابت ضمن الغرض
- في حال كنا نريد إسناد قيم لعدة حقول بالاعتماد على هذه الطريقة
```cpp
Increment::Increment(int c=0,int i=1):increment(i),count(c){}
```
---

# التوابع والصفوف الصديقة
## التابع الصديق
- التابع الصديق هو تابع لا ينتمي للصف ولكن يحق له الوصول للحقول من نوع private (خاص) و protected (محمي)
## الصف الصديق 
- هو صف خارجي كليّا عن الصف الحالي (لا يرتبط بأي علاقة من نوع تراكب composition أي صف داخل صف أو علاقة وراثة)
## ميزات علاقة الصداقة
- العلاقة من طرف واحد، A صديق B لا يعني بالضرورة أن يكون B صديق A
- العلاقة غير متعدية، A صديق B وB صديق C لا يعني بالضرورة أن يكون A صديق C
- الصداقة تمنح ولا تؤخذ أي A صديق B يعني أن B يمنج الصداقة لـ A ولا يمكن لـ A أن يكون صديق B إذا لم تحدد العلاقة ضمن B أولًا
---

```yaml
hideInToc: true
```
# التوابع والصفوف الصديقة
## التابع الصديق
<div grid="~ cols-2 gap-4">
<div>

- يتم تعريف التابع الصديق كقالب ضمن الصف قبل أي كلمة private أو public (لأنت التابع الصديق ليس جزءًا من التابع)
- ينبغي أن يتقبل هذا التابع غرضًا من الصف
- كود التابع الصديق يكون كتلة منفصلة عن الصف
</div>

<div>

```cpp
class Count{
	friend void setX(Count &,int );
public:
	Count(){x=0;}
	void print() const {cout<<x<<endl;}
private:
	int x;
};
void setX(Count& c,int x){
	c.x=x;
}
```
</div>
</div>
---

# التعامل مع المؤشرات
- في حال تعريف الغرض بالاعتماد على المؤشر يجب استخدام الكلمة new التي تستدعي باني الغرض
```cpp
Class1 *x=new Class1();
Class1 *y=new Class1(1,2);
Class1 *z=new Class1(x);
```

- يجب ألا ننسى مقابل كل تعليمة new يجب علينا أن نستدعي تعليمة delete
```cpp
delete x;
delete y;
delete z;
```

- كل استدعاء لعملية delete يستدعي الهادم بالخاص بالصف
---

# العناصر الساكنة Static
- العناصر الساكنة هي عناصر (حقول وتوابع) معرفة على أنها ساكنة أي مسبوقة بالكلمة static
- تكون القيمة للحقل مشتركة بين كل الأغراض من الصف
- في حال كان تابعًا ساكنًا لن يتعامل مع مؤشر this
- لا يمكن للتابع الساكن أن يصل لعناصر غير ساكنة ضمن الغرض
---


```yaml
hideInToc: true
```
# العناصر الساكنة Static
<div grid="~ cols-2 gap-1">
<div>

- <v-click at="1">تعريف حقل ساكن</v-click>
- <v-click at="2">خلال بناء الموظف يتم زيادة عدد الموظفين</v-click>
- <v-click at="3">في الهادم يتم إنقاص عدد الموظفين</v-click>
</div>
<div>

```cpp{|12|7|8}
class Employee{
public:
	 static int getCount();
	Employee(string firstName,string LastName){
		this->firstName=firstName;
		this->lastName=lastName;
		++count;	}
	~Employee(){--count;}	
	// getters and setters
private:
	string firstName,lastName;
	static int count;	
};
```
</div>
</div>
---

```yaml
hideInToc: true
```
# العناصر الساكنة Static
<div grid="~ cols-2 gap-1">
<div>

- <v-click at="1">تهيئة عداد الموظفين بالقيمة 0 عند بدء تنفيذ الملف</v-click>
- <v-click at="2">تعريف تابع getCount الساكن</v-click>
</div>
<div>

```cpp{|1|2-3|}
int Employee::count=0;
int Employee::getCount(){
return count;}
```
</div>
</div>
---

```yaml
hideInToc: true
```
# العناصر الساكنة Static
- الاستدعاء
```cpp
int main(){
	Employee *e1=new Employee("James","Kirck");
	Employee *e2=new Employee("Han","Solo");
	cout<<Employee::getCount();
	delete e1;
	delete e2;
	cout<<Employee::getCount();
}
```
--- 

# التحميل الزائد للعلميات
- مثل السجلات، نمتلك القدرة على تنفيذ التحميل الزائد للعمليات على الصفوف
- سنطبق ذلك على صف (عوضًا عن سجل) يعبر عن الأعداد العقدية
```cpp
class Complex{
	private:
		double real;
		double imaginary;
	public:
		Complex(double real=0,double imaginary=0){
			this->real=real;
			this->imaginary=imaginary;		}
		//getters and setters
		Complex& operator+(Complex& other){
			this->real+=other.real;
			this->imaginary+=other.imaginary;
			return &this;}};
```

--- 

```yaml
hideInToc: true
```
# التحميل الزائد للعلميات

- قمنا بتنفيذ تحميل رائد للعملية + لتتقبل الأعداد العقدية (بشكل مشابه يمكننا تنفيذ التحميل الزائد لعمليات الطرح والضرب والقسمة ..الخ)
- في حال كانت العملية لا تعيد غرضًا من نفس الصف، نعرفه كتابع صديق
```cpp
class Complex{
	friend ostream& operator<<(ostream& out,Complex&c){
		out<<c.real<<" "<<((c.imaginary >=0)?"+":""<<c.imaginary<<"i"<<endl;
	}
// the otheres
}
```
---

```yaml
hideInToc: true
```
# التحميل الزائد للعلميات
- في حال كانت التحميل الزائد يعيد نمطاً اساسياً أو غرضاً من نفس الصف الذي نحمل العملية الزائدة عليه، يكون التابع عضواً
- في حال كان التحميل الزائد يعيد غرضاً من صف آخر يجب أن يكون صديقاً