# 📘 Q&A Post: [Frequently Asked Questions]

Welcome to this Question & Answer post focused on **[Postgres SQL]**. Below you’ll find a curated list of questions and detailed answers meant to help you understand and master this topic.

## ❖ What is PostgreSQL?

**Ans:**  
PostgreSQL একটি ওপেনসোর্স অব্জেক্ট  রিলেশনাল ডেটাবেজ ম্যানেজমেন্ট সিস্টেম। এটি কাঠােমাবদ্ধভােব(Structured) তথ্য (Data) সংরক্ষণ, অনুসন্ধান ও ব্যবস্থাপনায় ব্যবহৃত হয়ে থাকে ! PostgreSQL তার ভাষা হিসেবে Postgres SQL নামের SQL এর ভেরিয়েন্ট  ব্যবহার করে ! এর ফাংশন ,ইনহেরিশনের মতো বৈশিষ্ট্য গুলো জনপ্রিয়তার মূল কারণ। 


PostgreSQL এর গুরুত্বপূর্ণ  কিছু বৈশিষ্ট্য হলো-

1) PostgreSQL এর অন্যতম বৈশিষ্ট্য ACID(Atomicity,Consistency,Isolation,Durability) প্রসেস ফলো করে।

2) উন্নত ডেটা টাইপ যেমনঃ JSON,XML সাপোর্ট করে ,তার সােথ ইউজার ডিফাইন্ড টাইপ ও সাপোর্ট করে থাকে।

3) মাল্টি ইউজার সিস্টেম সাপোর্ট করে ।

4) থার্ড পার্টি টূল্যস/এক্সটেনশন সাপোর্ট  থাকার কারেণ ব্যবহারকারীরা খুব সহেজই কাজগুেলা করেত পারে। 

---

## ❖ What is the purpose of a database schema in PostgreSQL?

**Ans:**  
Schema একটি অতিপ্রয়োজনীয়  namespace যেটি একটি ডাটােবেজর বিভিন্ন ধরণের অবেজক্ট(Object) এর গ্রুপ বহন কের থােক যারা একে অপরের সাথে সম্পর্ক যুক্ত থাকে।  একটি ডাটােবজ এর অধীনে এক বা একাধিক Schema থাকতে পারে, যেমনঃ কোন একটি কোম্পানি  সেলস, এইচআর, একাউন্টস এর জন্য আলাদা আলাদা schema থাকেত পাের। সাধারণত প্রতিটি ডাটােবজ এ public নােম একটি  ডিফল্ট  schema থাকে।

**Schema এর গুরুত্বপূর্ণ  কিছু বৈশিষ্ট্যঃ**

1. ডাটােবেজর অবেজক্ট গুলােকে একসােথ ম্যানেজ করা যায়  
2. এক সাথে একাধিক ব্যবহারকারী �ডটােবেজ কাজ/ব্যবহার করতে  পারে।   
3. Namespace সুবিধার কারণে একাধিক ব্যবহারকারীর একই তথ্য (নাম,ঠিকানা,পদবী ইত্যািদ) দটুি আলাদা schema �ত �রেখ আমরা কাজ করেত পারি!

**Schema তৈরী করার নিয়মঃ**

```sql
CREATE SCHEMA ph;
CREATE TABLE ph.instructors (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
````

---

## ❖ Explain the Primary Key and Foreign Key concepts in PostgreSQL.

**Ans:**

### Primary key:

প্রাইমারি কি ডেটাবেজ টেবিলের একটি নির্দিষ্ট বা একাধিক সমন্বিত কলাম যার মাধ্যমে টেবিলের প্রতিটি সারি কে আলাদাভাবে চিহ্নিত করা যায়। এটি অবশ্যই ইউনিক হতে হবে এবং কখনৈ খালি হতে পারবেনা। একটি টেবিলের নির্দিষ্ট একটি প্রাইমারি কি থাকতে পারে। 

**প্রাইমারি কি তৈরীর নিয়ম**

```sql
CREATE TABLE ph (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```

উপরের কোডটিতে  আমরা ph টেবিলের মধ্যে PRIMARY KEY কি ওয়ার্ড ববহার করে id কে টেবিলের PRIMARY KEY হিসেবে সেট করে দিয়েছি ।

তবে কখনো টেবিলে primary key যুক্ত করতে ভুলে গেলে সেইক্ষেত্রে alter এর মাধমে প্রাইমারি কি যুক্ত করা যায় ! যেমনঃ

```sql
ALTER TABLE hero ADD PRIMARY KEY (id);
```

প্রয়োজনে আমরা প্রাইমারি কি রিমোভ ও করতে পারি !

```sql
ALTER TABLE hero DROP CONSTRAINT hero_pkey;
```

---

### Foreign Key:

Foreign key হলো একটি  নির্দিষ্ট  কলাম বা কলামের সমষ্টি যা রিলেশনাল ডেটাবেজের অন্য
আরেকটি প্রাইমারি কি কে রেফার করে বা সংযুক্ত করে থাকে । এক টেবিলের এক বা একাধিক ফরেন কি
থাকতে পারে । তবে এর ভ্যালু খালি (Null) ও হতে পারে ।

Foreign key ববহারের মলূ উদ্দেশ মূল টেবিলের সাথে চাইল্ড টেবিলের এক সম্পর্ক বজাই রাখা
যায়। এ Null ছাড়াও, Default, Restrict, No action ও সাপ োর্ট করে থাকে ।


**ফরেনকি তৈরীর নিয়ম **

```sql
CREATE TABLE ph table(
   column1 datatype,
   column2 datatype,
   ...
   CONSTRAINT fk_name FOREIGN KEY (foreign_key_column)
   REFERENCES parent_table(primary_key_column)
);
```

**উদাহরণঃ**

আমরা দু টেবিল তৈরি করব যেখানে টেবিল “Course” এবং “Student” , Student টেবিলের রেফারে course টেবিলে যুক্ত থাকবে ।


```sql
CREATE TABLE course(
   course_id SERIAL PRIMARY KEY,
   course_name VARCHAR(100) NOT NULL
);

CREATE TABLE students(
   student_id SERIAL PRIMARY KEY,
   student_name VARCHAR(100) NOT NULL,
   course_id INT,
   CONSTRAINT fk_course FOREIGN KEY (course_id )
   REFERENCES courses(course_id )
);
```
এখানে students টেবিলের course_id  course টেবিলের course_id কে রেফার করছে যাতে শুধু কোর্স আইডি ই উপস্থিত থাকে ।

---

## ❖ What is the difference between the VARCHAR and CHAR data types?

**Ans:**
CHAR এক কি ওয়ার্ড যেটি মূলত নির্দিষ্ট  সংখার কারেক্টার স্টোর বা জমা রাখে নিজের মধ্যে ,
CHAR মলুত n byte সংখক কারেক্টার স্টোর বা জমা রাখতে পারে যেমনঃ CHAR(100) মানে
হচ্ছে এখানে 100  কারেক্টার বা কারেক্টার স্ট্রি ং স্টোর বা জমা রাখতে পারবে ।


অনদি কে VARCHAR যা মূলত ভ্যারিয়েবল  কারেক্টার বঝু ায় যা নির্দিষ্ট  সংখ্যক ভ্যারিয়েবল
কারেক্টার স্ট োর বা জমা রাখে । VARCHAR কারেক্টার স্টোড় করার ক্ষেত্রে যতটু প্রয় োজন
ততটূ জায়গা দখল করে , যেমনঃ VARCHAR(100) , যার মধ্যে 100 byte তথ/কারেক্টার রাখা
গেলে ও ইনপুট করা ডেটা  যদি 2 byte এর হয় সেক্ষেত্রে 2 byte সমান জায়গা ই দখল করবে !


**CHAR এবং VARCHAR এর মেধ্য অন্যতম পার্থক্য হলো**
ডাটাবেজ এর স্টোরেজ ব্যবহার করা,যেখানে CHAR নির্দিষ্ট  সংখ্যক পরিমাণ জায়গা দখল করে নেয় যদি ও তত পরিমাণ ডেটা তার কাছে না থাকে , কি  VARCHAR সেইক্ষেত্রে শুধু প্রইয়োজনীয় জায়গা  ই দখল করে , যার কারণে ডেটাবেজের জায়গার সঠিক ব্যবহার হয়ে থাকে , সাথে পারফর্মেন্স ও উন্নত হয় ডেটাবেজের।


---

## ❖ Explain the purpose of the WHERE clause in a SELECT statement.

**Ans:**
SELECT স্টেটমেন্ট  এর WHERE ব্যবহারের মাধ্যমে আমরা শর্তমতে নিদিষ্ট  পরিমাণ সারি আউটপুট হিসেবে নিতে পারি , উদাহরণস্বরুপ-

ধরি , আমাদের এক টেবিল যার নাম ph যার মধ্যে অনেকগুলো  course_id বিদ্যমান, এখন নির্দিষ্ট  এক বা একাধিক course_id পাওয়ার ক্ষেত্রে শর্তমতে আমরা WHERE ববহার করতে পারি ।

```sql
SELECT * FROM ph WHERE course_id = 2;
```
যে  শুধুমাত্র ৩ নং ক োর্স আউটপুট  পাবো!

WHERE এ ব্যবহৃত কিছু অপারেটর -
=, <>, <, >, <=, >=
AND, OR, NOT
LIKE, IN, BETWEEN, IS NULL

---

```

---

}
