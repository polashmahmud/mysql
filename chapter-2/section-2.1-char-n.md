# Section 2.1: CHAR(n)

<mark style="color:blue;">CHAR</mark><mark style="color:orange;">(</mark><mark style="color:blue;">n</mark><mark style="color:orange;">)</mark> হল <mark style="color:blue;">n</mark> অক্ষরের একটি নির্দিষ্ট দৈর্ঘ্যের স্ট্রিং অথ‍্যাৎ <mark style="color:blue;">n</mark> এর মান যদি ১০ হয় তাহলে ১০ অক্ষরের একটা স্ট্রিং <mark style="color:blue;">n</mark> এর মান যদি ৫ হয় তাহলে ৫ অক্ষরের একটা স্ট্রিং। যদি এটি CHARACTER <mark style="color:orange;">SET</mark> utf8mb4 হয়, তার মানে এটি ঠিক 4\*n বাইট দখল করে, তাতে কোন টেক্সট থাকুক অথবা না থাকুক। বেশিরভাগ ক্ষেত্রে <mark style="color:blue;">CHAR</mark><mark style="color:orange;">(</mark><mark style="color:blue;">n</mark><mark style="color:orange;">)</mark> এর ক্ষেত্রে ইংরেজি অক্ষর রয়েছে এমন স্ট্রিং ব‍্যবহার করা হয়, তাই CHARACTER SET ascii হওয়া উচিত। (Latin1 হলেও ভাল।) কয়েকটি উদাহরনঃ

```sql
country_code CHAR(2) CHARACTER SET ascii,
```

```sql
postal_code CHAR(6) CHARACTER SET ascii,
```

```sql
uuid CHAR(39) CHARACTER SET ascii,
```
