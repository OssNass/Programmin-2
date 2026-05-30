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
- <v-click at="6">
</div>

</div>
