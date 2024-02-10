<div dir="rtl"><h1> شماره گذاری و محاسبات</h1></div>
<div dir="rtl"> اضافه کردن شماره‌ی خطوط به متن و شمارش ناپیوسته‌ی خطوط تمام فایل‌ها:</div>
<div dir="rtl"><small>یعنی چنانچه بعد از dummy.txt فایل دیگری هم به آک بدهید، هنگامی که شمارش به فایل دوم برسد  دوباره از یک شروع به شمردن می‌کند.</small></div>

```
awk '{print FNR "\t" $0}' dummy.txt*
```

<div dir="rtl"> اضافه کردن شماره‌ی خطوط به متن و شمارش پیوسته‌ی خطوط تمام فایل‌ها:</div>

```
awk '{print FNR "\t" $0}' dummy.txt*
```

<div dir="rtl"> اضافه کردن شماره‌ی خطوط و مارجین از سمت چپ به متن :</div>

```
awk '{printf("%5d : %s\n", NR,$0)}' dummy.txt
```

<div dir="rtl"> اضافه کردن شماره‌ی خطوط به شرط خالی نبودن خطوط :</div>
 
```
awk 'NF{$0=++a " :" $0};{print}' dummy.txt
awk '{print (NF? ++a " :" :"") $0}' dummy.txt
```

<div dir="rtl"> شمارش خطوط یک فایل مانند wc -l:</div>

```
awk 'END{print NR}' dummy.txt
```

<div dir="rtl"> انجام عمیات ریاضی جمع بر روی تمام فیلدهای عددی یک فایل بصورت جداگانه:</div>
<div dir="rtl"><small>مناسب فایل‌های آماری </small></div>

<div dir="rtl"> برای مثال فایلی با محتوای زیر:</div>

<pre>
| Days | SSH Users | Offline | Idle Users | FTP Users
| Sat  | 231        | 53       | 12           | 435       
| Sun  | 874        | 13       | 849          | 56        
| Mon  | 837        | 339      | 4434         | 90        
</pre>

[دانلود این فایل](https://gist.github.com/wolandark/ec6400930e24be6823a8e55c27d84978)


```
awk '{s=0; for (i=1; i<=NF; i++) s=s+$i; print s}' stats.txt
```

<div dir="rtl"> انجام عمیات ریاضی جمع بر روی تمام فیلدهای عددی یک فایل و اعلام نتیجه‌ی کلی:</div>


```
awk '{for (i=1; i<=NF; i++) s=s+$i}; END{print s}' stats.txt
```

<div dir="rtl"> نمایش قدر مطلق هر فیلد عددی (Absolute Value):</div>

```
awk '{for (i=1; i<=NF; i++) if ($i < 0) $i = -$i; print }'
awk '{for (i=1; i<=NF; i++) $i = ($i < 0) ? -$i : $i; print }'
```

<div dir="rtl"> نمایش  تعداد کلی فیلدها - شمارش تغداد واژگان یک فایل:</div>

```
awk '{ total = total + NF }; END {print total}' dummy.txt
```

<div dir="rtl"> نمایش تعداد تمامی خطوطی که شامل یک الگوی خاص هستند:</div>
<div dir="rtl"><small>در اینجا از الگوی Lorem استفاده شده </small></div>
<div dir="rtl"><small> مناسب شمارش تعداد سایتیشن در متن علمی یا تعداد لاگین یک کاربر در یک لاگ فایل</small></div>

```
awk '/Lorem/{n++}; END {print n+0}' dummy.txt
```

<div dir="rtl"> نمایش تعداد فیلد در هر خط:</div>

```
awk '{ print NF ":" $0 } ' dummy.txt
```

<div dir="rtl"> نمایش آخرین فیلد هر خط:</div>

```
awk '{ print $NF }' dummy.txt
```

<div dir="rtl"> نمایش آخرین فیلد آخرین خط:</div>

```
awk '{ field = $NF }; END{ print field }' dummy.txt
```

<div dir="rtl"> نمایش اولین فیلد هر خط:</div>

```
awk '{ print $1 }' dummy.txt
```

<div dir="rtl"> نمایش چهارمین فیلد هر خط:</div>

```
awk '{ print $4 }' dummy.txt
```

<div dir="rtl"> نمایش تمام خطوطی که بیش از چهار فیلد دارند:</div>
 
```
awk 'NF > 4' dummy.txt
```

