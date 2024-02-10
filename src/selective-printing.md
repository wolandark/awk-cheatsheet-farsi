<div dir="rtl"><h1> نمایش انتخابی برخی از خطوط:</h1></div>
<div dir="rtl"> نمایش ۱۰خط  اول از فایل (شبیه‌سازی عملکرد head):</div>

```
awk 'NR < 11'
```

<div dir="rtl"> نمایش اولین خط از فایل (شبیه‌سازی head -1):</div>

```
awk 'NR>1{exit};1'
```

<div dir="rtl"> نمایش دو خط آخر یک فایل (شبیه‌سازی tail -2):</div>

```
awk '{y=x "\n" $0; x=$0};END{print y}' dummy.txt
```

<div dir="rtl"> نمایش آخرین خط یک فایل (شبیه‌ازی "tail -1):</div>

```
awk 'END{print}' dummy.txt
```

<div dir="rtl"> نمایش تنها خطوطی که با الگو تطابق دارند (شبیه‌سازی grep):</div>

```
awk '/Lorem/' dummy.txt
```

<div dir="rtl"> نمایش تنها خطوطی که با الگو تطابق ندارند (شبیه‌سازی grep -v):</div>

```
awk '!/Lorem/' dummy.txt
```

<div dir="rtl"> نمایش خط قبل از یک الگو، اما خط حاوی الگو را نمایش نمی‌دهد:</div>

```
awk '/Lorem/{print x};{x=$0}' dummy.txt
awk '/Lorem/{print (x=="" ? "تطابق در خط 1" : x)};{x=$0}'  dummy.txt
```

<div dir="rtl"> نمایش خط پس از یک الگو، اما خط حاوی الگو را نمایش نمی‌دهد:</div>

```
awk '/Lorem/{getline;print}' dummy.txt
```

<div dir="rtl"> گرفتن AAA و BBB و CCC (به هر ترتیب):</div>

```
awk '/AAA/; /BBB/; /CCC/' dummy.txt
```

<div dir="rtl"> گرفتن AAA و BBB و CCC (به همان ترتیب):</div>

```
awk '/AAA.*BBB.*CCC/' dummy.txt
```

<div dir="rtl"> نمایش تنها خطوطی با طول ۶۵ کاراکتر یا بیشتر:</div>

```
awk 'length > 64' dummy.txt
```

<div dir="rtl"> نمایش تنها خطوطی با طول کمتر از ۶۵ کاراکتر:</div>

```
awk 'length < 64' dummy.txt
```

<div dir="rtl"> نمایش بخشی از فایل از الگو تا انتهای فایل:</div>

```
awk '/Lorem/,0' dummy.txt
awk '/Lorem/,EOF' dummy.txt
```

<div dir="rtl"> نمایش بخشی از فایل بر اساس شماره‌های خط (خطوط ۸-۱۲):</div>

```
awk 'NR==8,NR==12' dummy.txt
```

<div dir="rtl"> نمایش شماره خط ۵۲:</div>

```
awk 'NR==52' dummy.txt
awk 'NR==52 {print;exit}' dummy.txt
   
در فایل‌های بزرگ بهتر عمل می‌کند

```

<div dir="rtl"> نمایش بخشی از فایل بین دو الگو :</h4></div>

```
awk '/Iowa/,/Montana/' dummy.txt         
    حساس به حروف کوچک و بزرگ است
```

<div dir="rtl"> پاک کردن تمامی خطوط خالی از فایل(مشابه grep '.'):</div>

```
awk NF dummy.txt
awk '/./' dummy.txt
```

<hr>
