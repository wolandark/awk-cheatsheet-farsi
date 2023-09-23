<div align="right">
<a href="http://www.coffeete.ir/wolandark">
       <img src="http://www.coffeete.ir/images/buttons/lemonchiffon.png" style="width:260px;" />
</a>
</div>
<br>
<div align="center">
  <h1 style="text-align: center;">awk تک خطی‌های</h1>
	<h1>آک چیست؟</h1>
</div>
	
<div dir="rtl">
Awk یک ابزار پردازش متنی چندمنظوره است که برای پردازش و تحلیل
متن‌ها در سیستم‌های لینوکس و سیستم‌های مشابه یونیکس به کار
می‌رود. این ابزار به شما امکان می‌دهد تا متن‌ها را با استفاده از
الگوها و فیلترهای مختلف جستجو و تغییر دهید. به طور خاص، awk برای پردازش و
استخراج داده‌های جدولی یا فرمت‌دار بسیار مفید است. این ابزار دارای یک
زبان برنامه‌نویسی ساده برای تعریف الگوها و عملیات مورد نیاز است. به عبارت
دیگر، awk یک ابزار قدرتمند برای انجام وظایف پردازش متنی در خط فرمان لینوکس است.
</div>

<br>
<div dir="rtl">جهت شروع کار، ابتدا یک فایل متنی برای انجام دستورها روی آن نیاز
داریم. فایل مورد نظر باید دارای متن لاتین و با فرمت txt, asccidoc, md باشد. اگر
چنین فایلی در سیستم خود موجود دارید آن را کپی کرده و در پوشه‌ای مخصوص این
درس قرار دهید، اگر نه با دستور زیر می‌توانید یک متن Loremipsum برای خود
تولید کنید</div>
<br>

```
curl https://www.lipsum.com/feed/json | jq -r '.feed.lipsum' > dummy.txt
```
<br>
<div dir="rtl">می‌توانید جهت راحتی بیشتر و هماهنگی با این درس فایل تمرین را از آدرس زیر دانلود کنید.</div> 

[Gist](https://gist.github.com/wolandark/a559fcf94e47260f397b619ac472f1b1)

<div dir="rtl">متن حاصل از دستور را چند بار زیر خودش کپی کنید تا حجم بیشتری متن برای کار کردن داشته باشیم.</div> <br>

<div dir="rtl">
<h2>
استفاده از آک به چه صورت است؟
</h2>
آک به سه شکل قابل استفاده است. 
</div>

<div dir="rtl">نوع اول: اجرای دستورات آک از یک فایل</div>

```
awk -f myscript.awk inputfile.txt
```

<div dir="rtl">نوع دوم: پایپ کردن خروجی دستور دیگری به آک</div>


```
cat /etc/ssh/sshd_config | awk '/Port/'
```

<div dir="rtl">نوع سوم: اجرای دستور آک به صورت مستقیم روی فایل مورد نظر</div>


```
awk '/Port/' /etc/ssh/sshd_config
```

<br>
<br>
<div dir="rtl">
در این جزوه که در واقع برگ تقلبی برای آک و کاربردهای بیشمار آن است، ما بر روش سوم تمرکز خواهیم کرد.
</div>

<div dir="rtl">
آک بصورت کلی روی ستون‌های متنی کار می‌کند، این ستون‌ها فیلد (field) نامیده می‌شوند.
	
کلمات، رجکس و ترتیب کاراکترها در این جزوه الگو (pattern) نامیده می‌شوند.
</div>
<div dir="rtl"><h1>فرمت کردن پاراگراف</h1></div>
<div dir="rtl"><div dir="rtl"> اضافه کردن یک خط فاصله بین هر بند:</div></div>
‍

```
awk '1;{print ""}' dummy.txt
awk 'BEGIN{ORS="\n\n"};1' dummy.txt
```

<div dir="rtl"> اضافه کردن سه خط فاصله بین هر بند:</div>

```
awk '1;{print ""}' dummy.txt
```

<br>
 
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

```
Days    SSH Users    Offline    Idle Users    FTP Users
Sat	231           53          12              435
Sun	874           13          84	         9
Mon	837	      339         44              34
etc ...
```

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

<div align="center">
<br>
<a href="https://t.me/volandarkside"> Telegram Channel</a>
<br>
</div>
<hr>

- Sources:
  - awk One-Liners By Eric Pement
  - sed & awk, 2nd Edition, by Dale Dougherty and Arnold Robbins
    O'Reilly, 1997
  - UNIX Text Processing, by Dale Dougherty and Tim O'Reilly
    Hayden Books, 1987
  - Effective awk Programming, 3rd Edition. by Arnold Robbins
  O'Reilly, 2001

# Contact me
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/wolandarkside)
[![Protonmail](https://img.shields.io/badge/ProtonMail-8B89CC?style=for-the-badge&logo=protonmail&logoColor=white)](mailto:contact-woland@proton.me)
