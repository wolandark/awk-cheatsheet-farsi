<div dir="rtl"><h1> جایگزینی متن</h1></div>
<div dir="rtl"> حذف فضاهای سفیدی ابتدایی (فاصله‌ها، تب‌ها):</div>

```
awk '{sub(/^[ \t]+/, ""); print}' dummy.txt 
```

<div dir="rtl"> حذف فضاهای سفید انتهایی (فاصله‌ها، تب‌ها) از انتهای هر خط:</div>

```
awk '{sub(/[ \t]+$/, "");print}'
```

<div dir="rtl"> حذف هم فضای سفید ابتدایی و انتهایی از هر خط:</div>

```
awk '{gsub(/^[ \t]+|[ \t]+$/,"");print}' dummy.txt
```

<div dir="rtl">این دستور فاصله‌ی اضافی بین فیلد‌ها را هم حذف می‌کند</div>

```
awk '{$1=$1;print}' dummy.txt
```

<div dir="rtl"> درج 5 فضای خالی در ابتدای هر خط (ساخت ترتیب صفحه):</div>

```
awk '{sub(/^/, "     ");print}' dummy.txt
```

<div dir="rtl"> راست‌چین کردن تمام متن با عرض ۷۹ کاراکتر:</div>

```
awk '{printf "%79s\n", $0}' dummy.txt*
```

<div dir="rtl"> وسط‌چین کردن تمام متن با عرض ۷۹ کاراکتر:</div>

```
awk '{l=length();s=int((79-l)/2); printf "%"(s+l)"s\n",$0}' dummy.txt*
```

<div dir="rtl"> یافتن و جایگزینی الگوی اول با دوم:</div>

```
awk '{sub(/Lorem/,"foo");print}' dummy.txt
```

<div dir="rtl"><small>برای بهتر دیدن خروجی این دستور می‌توانید از grep استفاده کنید</small></div>

```
awk '{sub(/Lorem/,"foo");print}' dummy.txt | grep --color=always foo
```

<div dir="rtl"> یافتن و جایگزینی، تنها در خطوطی که شامل یک الگوی  خاص هستند:</div>
<div dir="rtl"><small> در این دستور خطوطی که شامل الگوی Lorem هستند هدف‌گیری می‌شوند و در آن خطوط، الگوی ipsum با foo جایگزین خواهند شد. </small></div>

```
awk '/Lorem/{gsub(/ipsum/, "foo")};{print}' dummy.txt
```

<div dir="rtl"> یافتن و جایگزینی در تمام خطوطی که شامل یک الگوی  خاص نیستند (عکس دستور قبل):</div>
 
```
awk '!/Lorem/{gsub(/sit/, "foo")};{print}' dummy.txt
```

<div dir="rtl"> جایگزینی گروهی  واژگان با الگویی خاص:</div>
 
```
awk '{gsub(/Lorem|ipsum|dolor/, "foo"); print}' dummy.txt
```

<div dir="rtl"> برعکس کردن  ترتیب خطوط (مشابه tac):</div>

```
awk '{a[i++]=$0} END {for (j=i-1; j>=0;) print a[j--] }' dummy.txt*
```

<div dir="rtl"> اگر یک خط با یک علامت \ پایان می‌یابد، خط بعدی را به آن اضافه کن:</div>

```
awk '/\\$/ {sub(/\\$/,""); getline t; print $0 t; next}; 1' dummy.txt*
```

<div dir="rtl"> نمایش و مرتب سازی نام‌های ورودی تمام کاربران:</div>

```
awk -F ":" '{ print $1 | "sort" }' /etc/passwd
```

<div dir="rtl"> نمایش دو فیلد اول، به ترتیب معکوس، از هر خط:</div>

```
awk '{print $2, $1}' dummy.txt
```

<div dir="rtl"> تعویض دو فیلد اول از هر خط:</div>

```
awk '{temp = $1; $1 = $2; $2 = temp}' dummy.txt
```

<div dir="rtl"> نمایش همه‌ی خطوط و حذف دومین فیلد آن خط:</div>
 
```
awk '{ $2 = ""; print }' dummy.txt
```

<div dir="rtl"> نمایش همه‌ي خطوط با ترتیب معکوس فیلدها:</div>

```
awk '{for (i=NF; i>0; i--) printf("%s ",i);printf ("\n")}' dummy.txt
```

<div dir="rtl"> حذف خطوط تکراری و متوالی (شبیه‌سازی uniq):</div>

```
awk 'a !~ $0; {a=$0}'
```

<div dir="rtl"> حذف خطوط تکراری و غیر متوالی :</div>

```
awk '! a[$0]++'                
awk '!($0 in a) {a[$0];print}'      
```
