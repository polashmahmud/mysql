# Section 2.3: VARCHAR(255) -- or not

#### Suggested max len

প্রথমে, আমি কিছু সাধারণ স্ট্রিং উল্লেখ করব যেগুলি সর্বদা hex, বা অন্যথায় ASCII-এর মধ্যে সীমাবদ্ধ। এইগুলির জন্য, আপনাকে CHARACTER <mark style="color:blue;">SET</mark> <mark style="color:orange;">ascii</mark> (latin1 ব‍্যবহার করতে পারেন) নির্দিষ্ট করতে হবে যাতে এটি স্পেস নষ্ট না করে:

```sql
UUID CHAR(36) CHARACTER SET ascii -- or pack into BINARY(16)
country_code CHAR(2) CHARACTER SET ascii
ip_address CHAR(39) CHARACTER SET ascii -- or pack into BINARY(16)
phone VARCHAR(20) CHARACTER SET ascii -- probably enough to handle extension 
postal_code VARCHAR(20) CHARACTER SET ascii -- (not 'zip_code') (don't know the max)
city VARCHAR(100) -- This Russian town needs 91:
country VARCHAR(50) -- probably enough
name VARCHAR(64) -- probably adequate; more than some government agencies allow
```

#### &#x20;কেন সবজায়গায় 255 লেন্থ ব‍্যবহার করা হয় না?&#x20;

সবকিছুর জন্য (255) ব্যবহার না করার  দুটি কারণ রয়েছেঃ

* যখন একটি <mark style="color:orange;">SELECT</mark>-এর অস্থায়ী টেবিল তৈরি করতে হয় (একটি সাবকোয়েরি চালানোর জন‍্য <mark style="color:orange;">UNION</mark>, <mark style="color:orange;">GROUP BY</mark>, ইত্যাদি ব‍্যবহার করতে হয়), এটি তখন মেমরি ইঞ্জিন ব্যবহার করে এবং ডেটাগুলোকে RAM এ রাখে৷ কিন্তু <mark style="color:blue;">VARCHAR</mark> গুলি প্রক্রিয়ায় <mark style="color:blue;">CHAR</mark>-এ পরিণত হয়। এটি <mark style="color:blue;">VARCHAR(255)</mark> কে utf8mb4 1020 bytes জায়গা নিতে বাধ্য করে। যা কুয়েরিকে অনেক স্লো করে ফেলে
* অনেক সময়, InnoDB একটি টেবিলের কলামের সম্ভাব্য আকার দেখে সিদ্ধান্ত নেয় যে এটি অনেক বড় হবে, তাই সে <mark style="color:blue;">CREATE TABLE</mark> করাই বাতিল করে দেয়।

#### <mark style="color:blue;">VARCHAR</mark> versus <mark style="color:blue;">TEXT</mark>

\*<mark style="color:blue;">TEXT</mark>, <mark style="color:blue;">CHAR</mark>, এবং <mark style="color:blue;">VARCHAR</mark> ব্যবহারের কিছু উদাহরণঃ

* কখনও <mark style="color:blue;">TINYTEXT</mark> ব্যবহার করবেন না৷
* প্রায় সময়ই <mark style="color:blue;">CHAR</mark> ব্যবহার করা থেকে বিরত থাকবার চেষ্টা করবেন -- এটি একটি ফিক্সড জায়গা দখল করে।
* <mark style="color:blue;">CHAR</mark> এর সাথে, CHARACTER <mark style="color:blue;">SET</mark> <mark style="color:orange;">ascii</mark> ব্যবহার করুন।
* <mark style="color:blue;">VARCHAR</mark><mark style="color:orange;">(</mark><mark style="color:blue;">n</mark><mark style="color:orange;">)</mark> <mark style="color:blue;">n</mark> অক্ষর পর্যন্ত ধারণ করতে পারবে। বাকি অক্ষরগুলো বাতিল করে দেওয়া হবে। আপনি তাই এখানে <mark style="color:blue;">n</mark> এর মান সর্বচ্চটা দেবার চেষ্টা করবেন
* <mark style="color:blue;">\*TEXT</mark> ফিল্ডগুলো জটিল কুয়েরির সময় কুয়েরি স্লো করে দিতে পারে
