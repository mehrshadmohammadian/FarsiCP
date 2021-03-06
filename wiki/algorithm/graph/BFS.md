---
layout: Wiki
---

# جست و جوی سطح اول(Breadth First Search )

BFS یکی از مهم ترین و پرکاربرد ترین الگوریتم ها در پیمایش گراف است. با BFS میتوان کوتاه ترین مسیر رسیدن به هر راس را پیدا کرد.کوتاه ترین مسیر در گراف بدون وزن ، کمترین تعداد یال هایی است که باید طی شود تا به آن راس رسید. اردر این الگوریتم (O(n+m است که n تعداد رئوس و m تعداد یال های گراف است.

## توضیح الگوریتم

در ابتدا یک گراف بدون وزن و یک راس ریشه مانند v به عنوان ورودی می گیریم. جهت دار بودن با نبودن گراف تاثیری در الگوریتم نخواهد داشت.
BFS را میتوان مانند پخش شدن آتش در یک گراف توضیح داد. بدین صورت که در ابتدا طبقه صفر ام که فقط شامل راس ریشه (v) است ، آتش میگیرد و در هر مرحله آتش که در هر راس است ، تمام همسایه های آن در طبقه بعدی را می سوزاند.
در واقع سطح بندی رئوس گراف در BFS این گونه است که در سطح صفر ام ریشه (v) وجود دارد و تمام راس های مجاور v را در سطح اول قرار می دهیم.(اگر گراف جهت دار باشد ، باید همسایه هایی از v را در سطح اول قرار بدهیم که یال v به آن ها وارد شده است)
و برای سطح i+1 ام راس u که همسایه یکی از رئوس سطح قبلی (iام) است را در این سطح قرار می دهیم به شرطی که راس u در هیچ سطر دیگری نیامده باشد. به عبارت دیگر راس ها را براساس کوتاه ترین فاصله از v سطح بندی می کنیم و برای پیمایش گراف به ترتیب سطح و در هر سطح به ترتیب دلخواهی وارد راس ها می شویم. پس اولین باری که یک راس را می بینیم، با کمترین فاصله از v به آن رسیده ایم.

## پیاده سازی

برای پیاده سازی یک صف(queue) که شامل تمام راس ها است و یک آرایه Boolean (که اسمش را []mark می گذاریم) شامل راس های دیده شده در نظر میگیریم.
در ابتدا راس v را در queue اضافه می کنیم (push) و mark[v]=true و برای بقیه رئوس مانند mark[u]=false،u.
برنامه تا زمانی که  queue خالی نشده ادامه می یابد و در هر مرحله راس ابتدایی را از queue برمیداریم (pop).
فرض می کنیم این راس u باشد. بعد به همسایه هایی از u می رویم که یال u به آن ها وارد شده( اگر گراف جهت دار بود) و اگر بعضی از این همسایه ها را قبلا ندیده بودیم ، mark آن ها را true کرده و به queue اضافه می کنیم.

```C++
const int MAXN = 1e5+5;
vector<int> adj[MAXN];  // adjacency list representation
int n; // number of nodes
int s; // source vertex

queue<int> q;
bool mark[MAXN];
int d[MAXN], p[MAXN];

//-------------

q.push(s);
mark[s] = true;
p[s] = -1;
while (!q.empty()) {
    int v = q.front();
    q.pop();
    for (int u : adj[v]) {
        if (!mark[u]) {
            mark[u] = true;
            q.push(u);
            d[u] = d[v] + 1;
            p[u] = v;
        }
    }
}
```

## کاربرد ها

۱. پیدا کردن کوتاه ترین مسیر از راس s به هر راس دیگری در گراف بدون وزن

۲. پیدا کردن مولفه های همبندی در گراف بدون جهت از (Order(n+m: برای این کار از هر راس یک BFS می زنیم ، به جز رئوسی که در BFS های قبلی mark آن 
ها true شده است ولی هر بار آرایه mark رو پاک نمی کنیم چون نمی خواهیم از رئوسی که mark آن ها true است دوباره BFS بزنیم.

۳. پیدا کردن راه حل برای مسائل یا بازی هایی که کمترین تعداد حرکت رو می خواهند ، اگر بتوان هر حالت (state) از بازی را به عنوان راس گراف و 
رسیدن از هر حالتی به حالت دیگر را با یال نشان داد.

۴. پیدا کردن کوتاه ترین مسیر در گراف با یال های وزن دار  ۰ یا ۱ : این کار ار می توان با کمی تغییر در DFS انجام داد. به این صورت که اگر وزن 
یال فعلی صفر است و طول مسیر از S به این راس کمتر از مسیر جدید پیدا شده است ، به جای اینکه این راس را پشت queue اضافه کنیم ، آن را در جلوی 
add queue می کنیم.

۵. پیدا کردن کوتاه ترین دور در گراف جهت دار بدون وزن: از هر راس BFS می زنیم و وقتی  که از راس فعلی به راسی رسیدیم که قبلا دیده شده پس یعنی 
دور داریم و این دور ، کوتاه ترین دور شامل راس منبع است و باید BFS متوقف شود و بعد بین تمام طول های پیدا شده ، کوتاه ترین طول را انتخاب می 
کنیم.

۶. پیدا کردن یالی که در حداقل یکی از کوتاه ترین مسیر های از a به b وجود دارد : برای انجام این کار یک بار از BFS ، a می زنیم و یک بار هم از b. آرایه 
[]Da شامل اندازه کوتاه ترین مسیر از a به هر راس دیگری است و آرایه Db شامل کوتاه ترین مسیر از b به بقیه راس ها است. حالا برای هر یال (u,v) 
باید چک کنیم که در کوتاه ترین مسیر a به b هست یا نه [Da[u]+1+Db[v]=Da[b

۷. پیدا کردن تمام راس هایی که در حداقل کوتاه ترین مسیر (a,b) : برای این کار همان آرایه های Da و Db را در نظر می گیریم و برای هر راس چک می کنیم که در 
هر کوتاه ترین مسیر از a به b هست یا نه : [Da[v]+Db[v]=Da[b

۸. پیدا کردن تمام راس هایی که در همه کوتاه ترین مسیر ها از
a
به
b
آمده اند: تمام راس هایی که در حداقل یک مسیر آمده اند را از روش بالا بدست آورید. حال تعداد راس هایی را بدست آورید که در حداقل یک مسیر آمده اند و فاصله شان از
a
برابر
x
است. ( به ازای تمام
x
ها ) اکنون اگر به ازای یک x خاص، تعداد به دست آمده ۱ باشد، راسی که از a فاصله x دارد باید در تمام کوتاه ترین مسیر ها آمده باشد. ( یال نیز مشابه است )

## مسائل تمرینی
* [SPOJ: AKBAR](http://spoj.com/problems/AKBAR)
* [SPOJ: NAKANJ](http://www.spoj.com/problems/NAKANJ/)
* [SPOJ: WATER](http://www.spoj.com/problems/WATER)
* [SPOJ: MICE AND MAZE](http://www.spoj.com/problems/MICEMAZE/)
* [Timus: Caravans](http://acm.timus.ru/problem.aspx?space=1&num=2034)
* [DevSkills - Holloween Party](https://devskill.com/CodingProblems/ViewProblem/60)
* [DevSkills - Ohani And The Link Cut Tree](https://devskill.com/CodingProblems/ViewProblem/150)
* [SPOJ - Spiky Mazes](http://www.spoj.com/problems/SPIKES/)
* [SPOJ - Four Chips (hard)](http://www.spoj.com/problems/ADV04F1/)
* [SPOJ - Inversion Sort](http://www.spoj.com/problems/INVESORT/)
* [Codeforces - Shortest Path](http://codeforces.com/contest/59/problem/E)
* [SPOJ - Yet Another Multiple Problem](http://www.spoj.com/problems/MULTII/)
* [UVA 11392 - Binary 3xType Multiple](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=2387)
* [UVA 10968 - KuPellaKeS](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1909)
* [Codeforces - Police Stations](http://codeforces.com/contest/796/problem/D)
* [Codeforces - Okabe and City](http://codeforces.com/contest/821/problem/D)
* [SPOJ - Find the Treasure](http://www.spoj.com/problems/DIGOKEYS/)
* [Codeforces - Bear and Forgotten Tree 2](http://codeforces.com/contest/653/problem/E)
* [Codeforces - Cycle in Maze](http://codeforces.com/contest/769/problem/C)
* [UVA - 11312 - Flipping Frustration](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=2287)
* [SPOJ - Ada and Cycle](http://www.spoj.com/problems/ADACYCLE/)

