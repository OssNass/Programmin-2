---
theme: ./slidev-theme-penguin-rtl
colorSchema: light
class: text-center
transition: slide-right
title: "المحاضرة 12: أمثلة إضافية"
mdc: true
author: Dr. Ossama Nasser
exportFilename: 12- أمثلة إضافية
layout: cover
hideInToc: true
---
# المحاضرة 12
## أمثلة إضافية
### د. أسامه ناصر
2025-2026
---

```yaml
hideInToc: true
```
# الفهرس
<toc mindepth="1" maxdepth="3" />

---

```yaml
hideInToc: true
```
# في الحلقة السابقة
- مثال عن الوراثة بالاعتماد على الأشكال
---

# مثال اليوم
- سنعمل على كتابة سجلان من نوعين مختلفين ضمن ملف
- النوع الأول: 
	- معلومات الصف، تتضمن:
		- رموز خاصة (غير ضرورية ولكن مفضلة)
		- اسم المدرس
		- عدد الطلاب
	- معلومات الطالب:
		- الاسم
		- الكنية
		- عام الولادة
		- المعدل
---

```cpp
// --- 1. FULLY ENCAPSULATED FILE HEADER ---
struct FileHeader {
    char magic[4] = {'S', 'T', 'U', 'D'};
    int majorVersion = 1;
    int minorVersion = 0;
    char teacherName[100] = {0};
    int studentCount = 0;
};
```

- معلومات الملف تحت مسمى FileHeader الترويسة
	- magic مجموعة من الرموز الخاصة التي تستخدم لتمييز الملف الخاص بنا عن بقية أنواع الملفات
	- majorVersion وminorVersion يعبران عن إصدار الملف (في حال طورنا نسخة جديدة بحقول إضافية)
	- teacherName اسم المدرس
	- studentCount عدد الطلاب
- الحقلين الأولين غير مهمين في حالتنا البسيطة، إلا أن الحقلين الأخيرين مهمان في مثالنا
---

```cpp
// --- 2. DATA BLOCK STRUCTURE ---
struct Student {
    char firstName[50];
    char lastName[50];
    int yearOfBirth;
    double gpa;
};
```

- معلومات الطالب
	- الاسم firstName
	- الكنية lastName
	- عام الولادة yearOfBirth
	- المعدل gpa
---

```cpp
class StudentClass {
private:
    std::string internalTeacherName;
    std::vector<Student> students;
public:
    StudentClass() : internalTeacherName("Unassigned") {}
    void setTeacher(const std::string& name) {
        internalTeacherName = name;    }
    void addStudent(const Student& student) {
        students.push_back(student);    }
```

- الصف StudentClass
	- الحقول
		- internalTeacherName اسم المدرس (نفس الحقل teacherName ضمن السجل FileHeaeder)
		- students شعاع vector يخزن ملعومات الطلاب
	- التوابع
		- setTeacher لتخزين اسم المدرس
		- addStudent لإضافة طالب للسجل بالاعتماد على التابع push_back الموجود ضمن الصف vector الذي يضيف لآخر المصفوفة
---

```cpp
   bool writeToFile(const std::string& filename) const {
        std::ofstream outFile(filename, std::ios::binary | std::ios::trunc);
        if (!outFile) return false;
        FileHeader header;
        std::strncpy(header.teacherName, internalTeacherName.c_str(), sizeof(header.teacherName) - 1);
        header.studentCount = static_cast<int>(students.size());
        outFile.write(reinterpret_cast<const char*>(&header), sizeof(FileHeader));
        if (header.studentCount > 0) {
            outFile.write(reinterpret_cast<const char*>(students.data()), header.studentCount * sizeof(Student));
        }
        outFile.close();
        return true;    }
```
---

## الكتابة للملف
- التابع writeToFile مسؤول عن كتابة المعلومات إلى ملف متضمنًا الخطوات التالية:
	- كتابة ترويسة الملف من خلال نسخ اسم المدرس من الصف string إلى مصفوفة char بالاعتماد على التابع strncpy والتابع c_str الموجود ضمن الصف string
		- internalTeacherName صف string بينما teacherName مصفوفة char لذلك نلجأ للتابع c_str لنأخذ محتوى الصف string كمصفوفة char ونسخها بالاعتماد على التابع strncpy إلى الحقل teacherName
	- بالإضافة لكتابة عدد الطلاب من خلال size ضمن الصف vector الذي يعطي عدد عناصر المصفوفة
- عمليات القصر static_cast وreinterpret_cast ممكن استبدالها بقصر مباشر (int) أو (*char)
- نكتب أولًا ترويسة الملف ومن ثم لدينا خيارين:
	- نحترج ضمن حلقة ونكتب كل سجل ضمن students بشكل إفرادي على الملف
	- نكتب كل السجلات دفعة واحدة من خلال التابع data ضمن الصف vector الذي يعيد لنا محتوى الشعاع كمصفوفة، ويكون الوسيط الثاني لتابع الكتابة حجم السجل * عدد السجلات
---


```cpp
    bool readFromFile(const std::string& filename) {
        std::ifstream inFile(filename, std::ios::binary);
        if (!inFile) return false;
        FileHeader header;
        inFile.read(reinterpret_cast<char*>(&header), sizeof(FileHeader));     
        if (std::strncmp(header.magic, "STUD", 4) != 0) return false;
        internalTeacherName = header.teacherName;
        students.clear();
                if (header.studentCount > 0) {
            students.resize(header.studentCount);
            inFile.read(reinterpret_cast<char*>(students.data()), header.studentCount * sizeof(Student));
        }
        inFile.close();
        return true;    }
```
---

## القراءة من الملف
- التابع readFromFile يسمح لنا بقراءة القيم من الملف من خلال:
	- قراءة ترويسة الملف والتأكد من الرموز الخاصة من خلال التابع strncmp
	- تحميل اسم المدرس وعدد الطلاب
	- قراءة الطلاب من الملف إما كل سجل لوحده ضمن حلقة أو دفعة واحدة
	- التابع resize ضمن الصف vector يهيئ المصفوفة الداخلية للتخزين بعدد خانات المطلوب
- ملاحظة أخيرة
	- التنقل في هذا الملف مختلف قليلًا، بالحالة العادية يكون الوصول لسجل معين ضمن ملف ثنائي (أو وصول عشوائي) يكون حجم الملف * رقمه في حالتنا النقل فيه تغير بسيط، هو أننا يجب أن نتقنل بحجم الترويسة + حجم السجل * رقمه