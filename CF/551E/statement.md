---
title : گوکیز و گوکیزیانا
layout : CF
---
پروفسور گوکیز در حال بازی کردن با آرایه است و تابعی تعریف کرده به نام
$GukiZiana$
.
برای آرایه 
$a$
و عدد
$y$
،
$GukiZiana(a,y)$
برابر است با بزرگترین مقدار
$j - i$
، 
به طوری که
$a_i = a_j = y$
.
اگر عدد
$y$
در آرایه وجود نداشت نیز
$GukiZiana(a,y)$
، 
برابر است با
-1.
گوکیز همچنین سوالی برای شما آماده کرده است
،
این بار شما باید عملیات هایی را روی آرایه انجام دهید 
:

1.
نوع اول عملیات به شکل
$1 l r x$
می باشد و به شما می گوید که تمام اعضای آرایه از
$l$
تا 
$r$
را
$x$
واحد افزایش دهید
.

2.
نوع دوم به صورت 
$2 y$
می باشد و در پاسخ به آن شما باید مقدار
$GukiZiana(a,y)$
را خروجی دهید
.

## ورودی

در اولین خط ورودی دو عدد
$n q$
آمده اند که به ترتیب نشان دهنده تعداد اعضای آرایه و تعداد عملیات ها می باشند
.
$(1 \le n \le 10^5,1 \le q \le 5 * 10^4)$

خط دوم ورودی شامل 
$n$
عدد که نشان دهنده اعضای آرایه اند می باشد
.
$(1 \le a_i \le 10^9)$

هر کدام از 
$q$
خط بعدی شامل دو یه چهار عدد هستند به نحوی که در متن سوال توضیح داده شده
:

اگر عدد
$1$
در ابتدای خط آمده به معنای عملیات نوع اول است
.
$(1 \le l \le r \le n,0 \le x \le 10^9)$

اگر عدد
$2$
در ابتدای خط آمده به معنای عملیات نوع دوم است که شما باید در پاسخ به آن مقدار
$GukiZiana(a,y)$
را در خروجی چاپ کنید
.

## خروجی

به ازای هر عملیات نوع دوم مقدار
$GukiZiana(a,y)$
را در خروجی چاپ کنید
.
