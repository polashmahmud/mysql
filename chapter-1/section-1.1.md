---
description: Getting Started
---

# Section 1.1:

#### MySQL এ একটি ডাটাবেস তৈরি করা

```sql
CREATE DATABASE mydb;
```

Return value:

> Query OK, 1 row affected (0.05 sec)

#### তৈরি ডাটাবেস mydb ব্যবহার করা

```sql
USE mydb;
```

Return value:

> Database Changed

#### MySQL এ একটি টেবিল তৈরি করা

```sql
CREATE TABLE mytable 
(
id int unsigned NOT NULL auto_increment,
username varchar(100) NOT NULL,
email varchar(100) NOT NULL,
PRIMARY KEY (id) 
);
```

<mark style="color:blue;">CREATE TABLE</mark> mytable একটি নতুন টেবিল তৈরি করবে যার নাম mytable।

id <mark style="color:blue;">int unsigned</mark> <mark style="color:orange;">NOT NULL</mark> <mark style="color:blue;">auto\_increment</mark> এখানে id নামে একটা কলাম তৈরি করে এবং mySql এই কলামের একটা ইউনিক নম্বর নির্ধারণ করে প্রতিবার নতুন ডাটা ইনপুট হলে। অথ‍্যাৎ এই ক্ষেত্রে দুটি সারিতে একই id নম্বর থাকতে পারবে না আর এটা স্বয়ংক্রিয় ভাবে mySql নিয়ন্তন করে থাকে।

Return value:

> Query OK, 0 rows affected (0.10 sec)

#### mySql এ নতুন রো/ডাটা যুক্ত করা

```sql
INSERT INTO mytable (username, email)
VALUES ("John Dow", "john@example.com");
```

Example return value:

> Query OK, 1 row affected (0.06 sec)

<mark style="color:blue;">varchar</mark> (String) ভ‍্যালুগুলো আপনি চাইলে সিংগেল কোট দিয়েও লিখতে পারেন

```sql
INSERT INTO mytable (username, email)
VALUES ('Username', 'name@example.com');
```

#### mySql এ একটি রো/ডাটা আপডেট/এডিট করা

```sql
UPDATE mytable SET username="myuser" WHERE id=2;
```

Example return value:

> Query OK, 1 row affected (0.06 sec)

int ভ‍্যালুগুলোর সময় কোন প্রকার কোটেশন ব‍্যবহার করতে হয় না। Strings এবং Dates ভ‍্যালুগুলোর সময় অবশ‍্যই আপনাকে সিংগেল কোটেশন অথবা ডাবল কোটেশন ব‍্যবহার করতে হবে

#### mySql এ একটি রো/ডাটা ডিলিট/মুছে ফেলা

```sql
DELETE FROM mytable WHERE id=2
```

Example return value:

> Query OK, 1 row affected (0.06 sec)

এটি ২ নম্বর আইডি থাকা সারিটি/রোটি মুছে ফেলবে।

#### MySQL-এ শর্তের উপর ভিত্তি করে সারি/ডাটা নির্বাচন করা&#x20;

```sql
SELECT * FROM mytable WHERE username="myuser";
```

Return value:

![](<../.gitbook/assets/Screenshot 2021-12-28 at 12.41.17 AM.png>)

> 1 row in set (0.00 sec)

#### সকল ডাটাবেসের তালিকা দেখা

```sql
SHOW databases;
```

Return value:

```
+-------------------+
| Databases         |
+-------------------+
| information_schema|
| mydb              |
+-------------------+
```

> 2 rows in set (0.00 sec)

আপনি "information\_schema" কে একটি "মাস্টার ডাটাবেস" হিসেবে ভাবতে পারেন যা ডাটাবেস মেটাডেটাতে অ্যাক্সেস প্রদান করে।

#### একটি ডাটাবেসের সকল টেবিল দেখা

```sql
SHOW tables;
```

Return value:

```
+----------------+
| Tables_in_mydb |
+----------------+
| mytable        |
+----------------+
```

> 1 row in set (0.00 sec)

#### একটি টেবিলের সমস্ত fields গুলো দেখা

```sql
DESCRIBE databaseName.tableName;
```

অথবা, যদি ইতিমধ্যে একটি ডাটাবেস ব্যবহার করে থাকেন

```sql
DESCRIBE tableName;
```

Return value:

![](<../.gitbook/assets/Screenshot 2021-12-28 at 12.53.19 AM.png>)

#### ব্যবহারকারী/ইউজার তৈরি করা&#x20;

প্রথমত, আপনাকে একটি ব্যবহারকারী তৈরি করতে হবে এবং তারপরে নির্দিষ্ট ডেটাবেস/টেবিলে ব্যবহারকারীকে অনুমতি দিতে হবে। ব্যবহারকারী তৈরি করার সময়, এই ব্যবহারকারী কোথা থেকে সংযোগ করতে পারে তাও আপনাকে নির্দিষ্ট করে দিতে হবে৷q

```sql
CREATE USER 'user'@'localhost' IDENTIFIED BY 'some_password';
```

এই কমান্ডটি দিয়ে এমন একজন ব্যবহারকারী/ইউজার তৈরি হবে যা শুধুমাত্র স্থানীয় (local) মেশিনে সংযোগ করতে পারবে।

```sql
CREATE USER 'user'@'%' IDENTIFIED BY 'some_password';
```

এই কমান্ডটি দিয়ে এমন একজন ব্যবহারকারী/ইউজার  তৈরি হবে যা যেকোনো জায়গা থেকে সংযোগ করতে পারবে (স্থানীয় (local) মেশিন ছাড়া)।

Example return value:

> Query OK, 0 rows affected (0.00 sec)

#### Adding privileges

নির্দিষ্ট ডাটাবেসের সমস্ত টেবিলের জন্য ব্যবহারকারীকে সাধারণ, মৌলিক সুবিধা প্রদান করা

```sql
GRANT SELECT, INSERT, UPDATE ON databaseName.* TO 'userName'@'localhost';
```

সমস্ত ডাটাবেসের সমস্ত টেবিলের জন্য ব্যবহারকারীকে সমস্ত সুবিধা প্রদান করা (এতে মনোযোগ দিন)

```sql
GRANT ALL ON *.* TO 'userName'@'localhost' WITH GRANT OPTION;
```

উপরে, <mark style="color:orange;">\*</mark>_.<mark style="color:orange;">\*</mark>_  দিয়ে সমস্ত ডাটাবেস এবং টেবিলকে বুঝানো হয়েছে।&#x20;

<mark style="color:blue;">WITH GRANT OPTION</mark> যদি ব্যবহারকারী/ইউজার অন্য ব্যবহারকারীদের/ইউজারদের বিশেষ একসেস প্রদান করতে সক্ষম না হলে এটা বাদ দেওয়া উচিত।

বিশেষাধিকার হতে পারে / Privileges can be either

```sql
ALL
```

অথবা আপনি আলাদা আলাদা ভাবেও বিশেষাধিকার দিতে পারেন। এ ক্ষেত্রে আপনি কমা কমা করে ব‍্যবহার করতে পারেন

```sql
SELECT
INSERT
UPDATE
DELETE
CREATE
DROP
```

#### Note

সাধারণত, আপনার স্পেস সম্বলিত কলাম বা টেবিলের নাম ব্যবহার করা বা SQL-এ সংরক্ষিত শব্দ ব্যবহার করা এড়ানোর চেষ্টা করা উচিত। উদাহরণস্বরূপ, table বা first নামের মতো নামগুলি এড়ানো ভাল।

আপনি যদি এই ধরনের নামগুলি ব্যবহার করতেই চান, তাহলে সেগুলিকে ব্যাক-টিক \`\` ডিলিমিটারের মধ্যে রাখুন। উদাহরণ স্বরূপ

```sql
CREATE TABLE `table` (
`first name` VARCHAR(30) );
```

ব্যাক-টিক ডিলিমিটার সমন্বিত একটি query উদাহরণ

```sql
SELECT `first name` FROM `table` WHERE `first name` LIKE 'a%';
```
