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
 
