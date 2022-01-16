

![What is Big O Notation Explained: Space and Time Complexity](https://www.freecodecamp.org/news/content/images/size/w2000/2021/06/0_NSxbYAwcC7Qzk7PP.jpg)

Do you really understand Big O? If so, then this will refresh your understanding before an interview. If not, don’t worry — come and join us for some endeavors in computer science.

هل تفهم الـ Big O حقًا؟ إن كنت تفهمها فهذا المقال سيجدد فهمك قبل أي مقابلة عمل. لو لم تسمع بها من قبل، لا تقلق. تعال و انضم إلينا ل في علوم الكمبيوتر.  

إذا كنت قد درست بعض الدورات المتعلقة بالخوارزميات Algorithms فعلى الأغلب قد سمعت بمصطلح صيغة O الكبير **Big O notation**. لو لم تكن فعلت؛ في هذا المقال سنمر عليها و ننتقل إلى فهم أعمق لما تعنيه حقًا.  


صيغة O الكبير Big O notation من الأدوات الأساسية لعلماء الحاسوب لتحليل مدي تعقيد و تكلفة الخوارزمية Algorithm، و ممارسة مهمة لمهندسي البرمجيات لفهم الخوارزميات بشكل أعمق.

كتب هذا المقال بافتراض أنك كتبت برامج بسيطة من قبل، أيضًا بعض الأجزاء المتعمقة تتطلب أساسيات الرياضيات في المرحلة الثانوية، مما قد يجعل هذا المقال يحتوى على قدر من الصعوبة للمبتدئين، لكن إذا كنت مستعدًا، فلنبدأ!

في هذا المقال، سنناقش بتعمق معنى Big O notation سنبدأ مع مثال لخوارزمية Algorithm كمدخل للفهم، بعد ذلك سندخل في الرياضيات قليلًا لنحصل على فهم حقيقي للنظريات، بعد ذلك سنستعرض بعض الأشكال المختلفة لـ Big O notation و في النهاية، سنناقش سيناريو عملي يوضح قيود الـ Big O. قائمة توضح المحتويات موجودة أدناه. 
### المحتويات

1. ما هو الـ Big O notation؟ و لماذا هو مهم؟ 
2. التعريف المتفق عليه (الرسمي) للـ Big O notation. 
3. Big O, Little O, Omega & Theta
4. مقارنة مستوى التعقيد بين الـBig Os الأساسية.
5. التعقيد الزمني و تعقيد المساحة.
6. التعقيد الأفضل، المتوسط، الأسوء، المتوقع.
7. لماذا لا يهم الـBig O notation؟
8. في النهاية..


إذًا لنبدأ.

### 1.  ما هو الـ Big O notation؟ و لماذا هو مهم؟

> “Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity. It is a member of a family of notations invented by Paul Bachmann, Edmund Landau, and others, collectively called Bachmann–Landau notation or asymptotic notation.”  
>   
> — Wikipedia’s definition of Big O notation

>" صيغة O الكبير Big O notation هو صيغة رياضية تصف الحدود المتاحة لدالة function عندما يميل المدخل إلى قيمة معينة أو مالا نهاية. و هو عضو في عائلة من الصيغ اخترعها بول باخمان Paul Bachmann و ادموند لاندو Edmund Landau و أخرون معروفة باسم صيغ باخمان-لاندو أو صيغ المقاربة." 
>   
> — تعريف موسوعة  ويكيبيديا للـBig O notation

بكلمات بسيطة، الـ Big O notation يصف تعقيد الكود الخاص بك باستخدام مصطلحات جبرية.  

لفهم ما هو الـ Big O لنبدأ بمثال تقليدي **_O(n²)_** و التي تُنطق O الكبير تربيع Big O squared الحرف n هنا يمثل حجم المدخلات، و الدالة  **_“g(n) = n²”_** داخل  **_“O()”_** تعطينا فكرة عن مستوى تعقيد الخوارزمية نسبة إلى حجم المدخلات.   

ستكون الخوارزمية النموذجية التي تملك تعقيد O(n²) هي خوارزمية الترتيب بالتحديد selection sort. ترتّب خوارزمية الترتيب بالتحديد selection sort المصفوفة عن طريق العثور على أصغر عنصر (بافتراض أنّ الترتيب سيكون ترتيبًا تصاعديًا) في الجزء غير المرتّب من المصفوفة ووضعه في بدايتها.  بمعنى أن في كل دورة من دورات خوارزمية الترتيب بالتحديد، يؤخذ العنصر ذو القيمة الأصغر (بافتراض الترتيب التصاعدي) من الجزء غير المرتّب ويوضع في الجزء المرتّب من المصفوفة. في الصورة أدناه شرح بصري لها. 

يمكن شرح الخوارزمية بالكود اللاحق، للتأكد أن العنصر في المكان i هو العنصر الأصغر في المصفوفة كلها، تدور الخوارزمية أولًا داخل المصفوفة باستخدام for loop و لكل عنصر تستخدم for loop أخرى لايجاد أصغر عنصر في الجزء المتبقى من المصفوفة. 

```js
SelectionSort(List) {
  for(i from 0 to List.Length) {
    SmallestElement = List[i]
    for(j from i to List.Length) {
      if(SmallestElement > List[j]) {
        SmallestElement = List[j]
      }
    }
    Swap(List[i], SmallestElement)
  }
}
```




في هذا السيناريو، نفترض أن List هي الداخل إلى الـ function و لذلك حجم المدخل n يعبر عن عدد العناصر داخل الـ List و افترض أن if الشرطية و الجزء المجاور لها يأخذان وقت ثابت و معروف، يمكننا تحديد مدى تعقيد (Big O notation) خوارزمية الـ SelectionSort عن طريق تحليل عدد المرات التي تنفذ فيها العمليات المكتوبة في الكود. 


أولًا، تقوم الحلقة الداخلية inner for loop بتشغيل العمليات المكتوبة عدد n مرة و بعد زيادة i ، تعمل الحلقة for الداخلية لـ n-1 مرة حتى يتم تشغيلها مرة واحدة، ثم تصل كلتا الحلقتين for إلى شروط التوقف الخاصة بهما. 

![](https://www.freecodecamp.org/news/content/images/2021/06/1_1ajbPJXjt3z7CofVODlaCw.png)

حلقات الخوارزمية Selection sort موضحة

إذا قمنا بحساب كل العمليات سيعطينا ذلك مجموعًا هندسيًا و مع بعض [رياضيات المرحلة الثانوية](https://en.wikipedia.org/wiki/1_%2B_2_%2B_3_%2B_4_%2B_%E2%8B%AF) سنجد أن الحلقة الداخلية تتكرر لمدة 1+2 … + n  مرة مما يساوي  n(n-1)/2 مرة. إذا قمنا بضرب ذلك سنتنهي بـ n²/2-n/2.


عندما نحسب الـ Big O notation نهتم فقط بالأجزاء السائدة **dominant terms** و لا نهتم بالمعاملات، مثال: لن نهتم بالاثنين المجاورة لـ n سنهتم بأكبر جزء في المعادلة فقط، فسنأخذ n² أنه Big O. و نكتبها O(n²) الذي يُنطق كما وضحت سابقًا Big O squared.

الآن قد تتساءل، ما هو **_"الجزء السائد dominant term "_**؟ ولماذا لا نهتم بالمعاملات؟ لا تقلق، سنمر بهم واحدًا تلو الآخر. قد يكون من الصعب بعض الشيء فهمه في البداية، لكن كل ذلك سيكون منطقيًا عندما تقرأ القسم التالي.  

### 2. التعريف المتفق عليه (الرسمي) للـ Big O notation

كان يا مكان، كان هناك ملك هندي أراد مكافأة رجل حكيم لتفوقه، لم يطلب الرجل الحكيم شيئًا سوى حبات قمح تكفي لملىء رقعة شطرنج.

و لكن كانت لديه قواعده: في المربع الأول يريد حبة قمح واحدة، في المربع الثاني يريد أربعة حبات، كل مربع يحتاج إلى أن يُملىء بمقدار ضعف عدد الحبات في السابق له. وافق الملك الساذج بدون تردد مفكرًا أنه طلب بسيط يمكن تحقيقه حتى ذهب و جربه..


![](https://www.freecodecamp.org/news/content/images/2021/06/0_em0jJ2rgj-ZapCef.jpg)

قمح و رقعة شطرنج، الصورة من: [Wikipedia](https://en.wikipedia.org/wiki/Wheat_and_chessboard_problem)

إذًا، كم حبة قمح يدين بها الملك للرجل الحكيم؟ نحن نعلم أن رقعة الشطرنج تتكون من 8 * 8 مربع، بمجموع 64 مربع، لذلك المربع الأخير يجب أن يحتوي على  2⁶⁴ حبة من القمح! إذا قمت بحساب العدد المطلوب ستحصل على  1.8446744*10¹⁹ و هو ما يساوي 18 متبوعة بـ 18 صفر، لنفترض أن كل حبة قمح تزن 0.01 جرام، هذا يعطينا 184467440737 طن من القمح! و 184 بليون طن كثير جدًا، أليس كذلك؟  

تزداد الأرقام بعد عدد من المربعات بزيادة أسية (تبعًا للدالة الأسية)، أليس كذلك؟ المنطق نفسه يسري على خوارزميات الحاسوب. إذا زادت الجهود المطلوبة لاكمال مهمة بطريقة أسية مع زيادة عدد المدخلات، يمكن أن تنتهي كبيرة للغاية حيث لا يستطيع الحاسوب (الموارد المتاحة عليه) اكمالها.  

الآن ضعف 64 هو 4096. إذا أضفت هذا الرقم إلى 2⁶⁴ سيفقد أهميته و ينضم إلى الأرقام غير المؤثرة على هذا الرقم الكبير، لهذا السبب عندما نحلل معدل الزيادة/النمو نهتم فقط بالأجزاء السائدة dominant terms. و نظرًا لأننا نريد تحليل معدل الزيادة بالنسبة لحجم المدخلات، فالمعاملات التي تضاعف الرقم فقط بدلًا من الزيادة مع زيادة حجم المدخلات لا تحتوى على معلومات قد تساعدنا.  

أدناه التعريف الرسمي للـ Big O:

![](https://www.freecodecamp.org/news/content/images/2021/06/0_cyqWw3UxODl-wqJi.jpg)

الصورة من جامعة واشنطن [CSE 373 Slides](https://slideplayer.com/slide/9739625/) 


يكون التعريف الرسمي مفيدًا عندما تحتاج إلى إجراء اثبات رياضي. على سبيل المثال، يمكن تحديد التعقيد الزمني لخوارزمية Selection sort من خلال الدالة f(n) = n²/2-n/2 كما ناقشنا في النقطة السابقة. 


إذا سمحنا للدالة  g(n) أن تكون n² يمكننا إيجاد ثابت c = 1 و أيضًا  N₀ = 0 طالما  N > N₀ ستكون N² دائمًا أكبر من  N²/2-N/2. يمكننا بسهولة اثبات ذلك بطرح N²/2 من الدالتين و يمكننا بسهولة أن نرى أن N²/2 > -N/2 ستكون صحيحة عندما تكون  N > 0 لذلك، يمكننا التوصل إلى استنتاج مفاده أن f (n) = O (n²)، بمعنى أخر أن الـ selection sort هو Big O squared. 


ربما لاحظت خدعة صغيرة هنا. بمعنى، إذا جعلت g (n) ينمو بسرعة كبيرة، بطريقة أسرع من أي شيء آخر ، فإن O (g (n)) ستكون دائمًا كبيرة بدرجة كافية. على سبيل المثال ، بالنسبة لأي دالة عديدة الحدود polynomial function ، يمكنك دائمًا أن تكون على صواب بالقول إنها O (2ⁿ) لأن 2ⁿ أكبر في التعقيد من أي عديدة حدود! 

رياضيًا، أنت على حق، لكن بشكل عام عندما نحدد الـ Big O نريد أن نعرف **الرابط المحصور(يتضمن الحد الأعلى و الأدنى) Tight bound** للدالة، ستفهم ذلك أكثر عند قرائتك للنقطة القادمة.

قبل أن نبدأ في القسم القادم لنختبر فهمنا بالسؤال التالي، ستكون الاجابة موجودة في النقاط اللاحقة. 

> **السؤال الأول:** لدينا صورة ممثلة على الحاسوب بمصفوفة ثنائية الأبعاد 2D Array من البيكسلز. لو استخدمت حلقة for مرتين متداخلتين (كما في selection sort) لتمر على كل بيكسل ( كأنك قمت بتقسيم الصورة لأعمدة و صفوف حلقة تمر على كل صف و حلقة داخلية تجعلك تمر على كل بيكسل في هذا الصف) ما التعقيد الزمني للخوارزمية عندما تكون الصورة هي المدخلات؟ 

### 3. Big O, Little O, Omega & Theta

> Big O: “f(n) is O(g(n))” iff for some constants c and N₀, f(N) ≤ cg(N) for all N > N₀  
>   
> Omega: “f(n) is Ω(g(n))” iff for some constants c and N₀, f(N) ≥ cg(N) for all N > N₀  
>   
> Theta: “f(n) is Θ(g(n))” iff f(n) is O(g(n)) and f(n) is Ω(g(n))  
>   
> Little O: “f(n) is o(g(n))” iff f(n) is O(g(n)) and f(n) is not Θ(g(n))  
>   
> —Formal Definition of Big O, Omega, Theta and Little O

بكلمات أوضح: 

-   **Big O (O())** تصف الحد الأعلى **upper bound** من التعقيد.
-   **Omega (Ω())** تصف الحد الأدنى **lower bound** من التعقيد.
-   **Theta (Θ())** تصف الحد المضبوط/الدقيق **exact bound** من التعقيد.
-   **Little O (o())** تصف الحد الأعلى بدون الحد المضبوط/الدقيق. 


![](https://www.freecodecamp.org/news/content/images/2021/06/1_O-dcXbYXojkAPEnDuVZMvA.png)

العلاقة بين Big O, Little O, Omega & Theta موضحة بالرسم. 

على سبيل المثال، الدالة g(n) = n² + 3n تمتلك تعقيد  O(n³) مما يعني: o(n⁴) و ثيتا Θ(n²) و اوميجا  Ω(n)، لكنك ستظل محقًا إذا قلت أيًا من Ω(n²)  أو    O(n²).

بشكل عام، عندما نتحدث عن Big O، فإن ما قصدناه في الواقع هو Theta. إنه نوعا ما بلا معنى عندما تعطي حدًا أعلى upper bound يكون أكبر بكثير من نطاق التحليل. سيكون هذا مشابهًا لحل المتباينات بوضع ∞ في الجانب الأكبر ، والذي سيجعلك دائمًا على صواب لكن بلا معنى.. 

لكن كيف نحدد أي من الدوال أكثر تعقيدًا؟ في النقطة التالية سنتعلم ذلك بالتفصيل.

### 4. مقارنة مستوى التعقيد بين الـBig Os الأساسية

عندما نحاول اكتشاف Big O لدالة معينة  g(n) نهتم فقط بالجزء السائد **dominant term** كما وضحت سابقًا، الجزء السائد هو الجزء الأسرع في الازدياد.  

على سبيل المثال، n² تزداد أسرع من n فإذا كنا نحاول تحليل دالة كـ g(n) = n² + 5n + 6 ستكون معقدة بدرجة O(n²)، إذا درست بعض التفاضل مسبقًا، فهذا يشبه للطريقة المختصرة عندما نحاول ايجاد الحدود لكثيرة الحدود الكسرية fractional polynomials عندما كنا نهتم فقط بالأجزاء السائدة للبسط و المقام في النهاية.   

![](https://www.freecodecamp.org/news/content/images/2021/06/0_MPwgKd4lgXACfuNt.png)

طريقة أخرى للنظر إلى Big O، صورة من: [Stack Overflow](https://stackoverflow.com/questions/1364444/difference-between-big-o-and-little-o-notation)

لكن، أي دالة تزداد أسرع من الدوال الأخرى؟ في الحقيقة يوجد بعض القواعد، لا تبدأ بالتحليل كل مرة من الصفر.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_KfZYFUT2OKfjekJlCeYvuQ.jpeg)

توضيح لازدياد التعقيد من  [Big O Cheatsheet](http://bigocheatsheet.com/)

#### 1. O(1) تمتلك أقل تعقيد
غالبًا ما يُطلق عليه **_" الوقت الثابت constant time"_** إذا استطعت صنع خوارزمية تحل المشاكل في O(1) أنت الأفضل. في بعض السيناريوهات يتجاوز التعقيد O(1) عندها يمكننا تحليلها من خلال ايجاد نظيره في حالة O(1/g(n))، على سبيل المثال: O(1/n) أكثر تعقيدًا من O(1/n²). 

#### 2. O(log(n)) أكثر تعقيدًا من O(1) لكنها أقل تعقيدًا من كثيرات الحدود polynomials 
نظرًا لأن تعقيد الخوارزميات غالبًا ما يتم قياسه في خوارزميات divide and conquer فـO(log(n)) بشكل عام هو درجة تعقيد جيدة يمكن الوصول إليها (تذكر أن هدفنا تقليل التعقيد) في خوارزميات الترتيب، و لاحظ أن O(log(n)) أقل تعقيدًا من O(√n) لأن دالة الجذر التربيعي يمكن اعتبارها كثيرة حدود، حيث تكون ذات أس يساوي 0.5 

#### 3. كلما زاد الأس exponent كلما زاد تعقيد كثيرة الحدود
على سبيل المثال،  O(n⁵) أكثر تعقيدًا من O(n⁴)، و نظرًا لسهولتها فنحن قد مررنا بالفعل على أمثلة لكثيرات الحدود في النقاط السابقة. 
#### 4. Exponentials have greater complexity than polynomials as long as the coefficients are positive multiples of n

O(2ⁿ) is more complex than O(n⁹⁹), but O(2ⁿ) is actually less complex than O(1). We generally take 2 as base for exponentials and logarithms because things tends to be binary in Computer Science, but exponents can be [changed](https://www.decodedscience.org/how-to-convert-the-base-of-an-exponent-with-logarithms/18524) by changing the coefficients. If not specified, the base for logarithms is assumed to be 2.

#### 5. مضروب العدد factorial أكثر تعقيدًا من الدالة الأسية
إذا كنت مهتمًا بالاثبات، فيمكن القراءة عن [**دالة جاما Gamma function**](https://en.wikipedia.org/wiki/Gamma_function) فهي  [**تحليل مستمر analytic continuation**](https://en.wikipedia.org/wiki/Analytic_continuation) لمضروب عدد. الاثبات المختصر أن كل من المضروب و الدالة الأسية لهما نفس عدد المضاعفات لكن الأرقام في المضروب العددي تتزايد بينما تبقى ثابتة في الدالة الأسية. (بمعنى أن 2⁶⁴ مهما كان الرقم في الأس سنظل نضرب 2 * 2 * 2 *2 ... لكن في المضروب العددي  الأرقام المضروبة تتغير مثال: 64! = 64 * 63 * 62 * 61 ..) 
#### 6. Multiplying terms

عند الضرب، سيكون التعقيد أكبر من الأصلي، لكن ليس أكبر من ما يعادل ضرب حد أكثر تعقيدًا، على سبيل المثال،  O(n * log(n)) أكثر تعقيدًا من O(n) لكن أقل تعقيدًا من  O(n²) لأن O(n²) = O(n * n) و n أكثر تعقيدًا من log(n).

لاختبار فهمك، جرب ترتيب الدوال التالية من الأكثر تعقيدًا إلى الأقل. الحلول مع شرح مفصل ستكون موجودة في نقطة لاحقة، بعض منهم قد يكون معقدًا/مخادعًا و يتطلب فهمًا أعمق للرياضيات، عندما تصل إلى الحل ستفهمهم بطريقة أفضل. 

> **سؤال:** رتب الدوال التالية من الأكثر تعقيدًا إلى الأقل

![](https://www.freecodecamp.org/news/content/images/2021/06/1_69bzUpQxBwZFLBimaMe7kQ.png)

الأمثلة مأخوذة من: [Textbook Problems](https://www.chegg.com/homework-help/questions-and-answers/problem-ask-refresh-knowledge-asymptotic-notations-rank-following-functions-order-growth-f-q23698273)


> **حل السؤال الأول (المذكور في النقطة الثانية):** 
>
>هذا السؤال هدفه أن يكون مخادعًا لاختبار مدى فهمك. يحاول السؤال جعلك تجيب O (n²) لأن هناك حلقة for متداخلة. ومع ذلك ، من المفترض أن يكون n هو حجم المدخلات. نظرًا لأن المصفوفة المعبرة عن الصورة هي المدخلات، و تم المرور على كل مربع (بيكسل) مرة واحدة فقط فإن الإجابة هي في الواقع O (n). ستتناول النقاط التالية أمثلة مثل هذا المثال 

### 5.التعقيد الزمني و تعقيد المساحة Time & Space Complexity

حتى الآن ناقشنا فقط التعقيد الزمني للخوارزميات، نهتم فقط كم سيستغرق البرنامج لانهاء المهمة المطلوبة. لكن مهم أيضًا أن نضع في الحسبان المساحة المأخوذة من البرنامج لانهاء المطلوب، تعقيد المساحة مرتبط بحجم الذاكرة التي سيستخدمها البرنامج لذلك فهي أيضًا عامل مهم للتحليل(قد تفشل المهمة بسبب عدم كفاية المساحة).

يعمل تعقيد المساحة بنفس طريقة التعقيد الزمني، على سبيل المثال، الترتيب بالتحديد selection sort يمتلك تعقيد مساحة O(1) لأنه يخزن فقط قيمة واحدة و ترتيبها للمقارنة كل مرة، المساحة المستخدمة لا تزيد مع حجم المدخلات. 

بعض الخوارزميات، مثل الترتيب بالدلو bucket sort تمتلك تعقيد مساحة O(n) لكن يمكننا تقليلها إلى O(1)، يقوم  Bucket sort يقوم بترتيب المصفوفة array عن طريق صنع قائمة مرتبة من كل العناصر المحتملة في المصفوفة و بعدها زيادة العداد عند مقابلة عنصر منهم، في النهاية المصفوفة المرتبة ستكون عناصر القائمة المصنوعة و مكررة بعددهم. (تابع الصورة الموضحة)

![](https://www.freecodecamp.org/news/content/images/2021/06/1_GfLWx2TXS55unwqZ5-X26w.png)

توضيح بصري للترتيب بالدلو Bucket sort 

### 6. Best, Average, Worst, Expected Complexity

The complexity can also be analyzed as best case, worst case, average case and expected case.

Let’s take **insertion sort,** for example. Insertion sort iterates through all the elements in the list. If the element is larger than its previous element, it inserts the element backwards until it is larger than the previous element.

![](https://cdn-media-1.freecodecamp.org/images/0*C9ork5K0ay7_CLBv.gif)

Insertion Sort Illustrated, Image from [Wikipedia](https://en.wikipedia.org/wiki/Insertion_sort)

If the array is initially sorted, no swap will be made. The algorithm will just iterate through the array once, which results a time complexity of O(n). Therefore, we would say that the **best-case** time complexity of insertion sort is O(n). A complexity of O(n) is also often called **linear complexity**.

Sometimes an algorithm just has bad luck. Quick sort, for example, will have to go through the list in O(n) time if the elements are sorted in the opposite order, but on average it sorts the array in O(n * log(n)) time. Generally, when we evaluate time complexity of an algorithm, we look at their **worst-case** performance. More on that and quick sort will be discussed in the next section as you read.

The average case complexity describes the expected performance of the algorithm. Sometimes involves calculating the probability of each scenarios. It can get complicated to go into the details and therefore not discussed in this article. Below is a cheat-sheet on the time and space complexity of typical algorithms.

![](https://www.freecodecamp.org/news/content/images/2021/06/0_XZsrnwao98R3dGTB.png)

[Big O Cheatsheet](http://bigocheatsheet.com/) for Common Algorithms

> **Solution to Section 4 Question:**

By inspecting the functions, we should be able to immediately rank the following polynomials from most complex to lease complex with rule 3. Where the square root of n is just n to the power of 0.5.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_RKlbisO36urUbi237TjyrQ.png)

Then by applying rules 2 and 6, we will get the following. Base 3 log can be converted to base 2 with [**log base conversions**](http://home.windstream.net/okrebs/page57.html). Base 3 log still grows a little bit slower then base 2 logs, and therefore gets ranked after.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_6R1jrWMGXpKxBqtEre9q8Q.png)

The rest may look a little bit tricky, but let’s try to unveil their true faces and see where we can put them.

First of all, 2 to the power of 2 to the power of n is greater than 2 to the power of n, and the +1 spices it up even more.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_eGLwpHDUJtr6CuALrpcQ2w.png)

And then since we know 2 to the power of log(n) with based 2 is equal to n, we can convert the following. The log with 0.001 as exponent grows a little bit more than constants, but less than almost anything else.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_4yo7najRBY_OaTnDpT3cIg.png)

The one with n to the power of log(log(n)) is actually a variation of the [**quasi-polynomial**](https://en.wikipedia.org/wiki/Time_complexity#Quasi-polynomial_time), which is greater than polynomial but less than exponential. Since log(n) grows slower than n, the complexity of it is a bit less. The one with the inverse log converges to constant, as 1/log(n) diverges to infinity.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_ZYUCFuiSbOibqdSfmuwdvA.png)

The factorials can be represented by multiplications, and thus can be converted to additions outside the logarithmic function. The “n choose 2” can be converted into a polynomial with a cubic term being the largest.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_cbrjlMGsWYCs36u831pLTA.png)

And finally, we can rank the functions from the most complex to the least complex.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_NHVggTVMGjGOe7SxtSgIpQ.png)

### Why BigO doesn’t matter

> **!!! — WARNING — !!!**  
>   
> Contents discussed here are generally **not accepted** by most programmers in the world. Discuss it **at your own risk** in an interview. People actually blogged about how they **failed** their Google interviews because they questioned the authority, like here.  
>   
> **!!! — WARNING — !!!**

Since we have previously learned that the worst case time complexity for quick sort is O(n²), but O(n * log(n)) for merge sort, merge sort should be faster — right? Well you probably have guessed that the answer is false. The algorithms are just wired up in a way that makes quick sort the _“quick sort”_.

To demonstrate, check out this [trinket.io](https://trinket.io/python/87a3166026) I made. It compares the time for quick sort and merge sort. I have only managed to test it on arrays with a length up to 10000, but as you can see so far, the time for merge sort grows faster than quick sort. Despite quick sort having a worse case complexity of O(n²), the likelihood of that is really low. When it comes to the increase in speed quick sort has over merge sort bounded by the O(n * log(n)) complexity, quick sort ends up with a better performance in average.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_UvDTlLjNnQurODtnCWjEJg.png)

Time Comparison between Quick Sort & Merge Sort

I have also made the below graph to compare the ratio between the time they take, as it is hard to see them at lower values. And as you can see, the percentage time taken for quick sort is in a descending order.

![](https://www.freecodecamp.org/news/content/images/2021/06/1_Zdm_8c-uU5941r7zJd4FPQ.png)

Time Ratio between Quick Sort & Merge Sort

The moral of the story is, Big O notation is only a mathematical analysis to provide a reference on the resources consumed by the algorithm. Practically, the results may be different. But it is generally a good practice trying to chop down the complexity of our algorithms, until we run into a case where we know what we are doing.

### In the end…

I like coding, learning new things and sharing them with the community. If there is anything in which you are particularly interested, please let me know. I generally write on web design, software architecture, mathematics and data science. You can find some great articles I have written before if you are interested in any of the topics above.

Hope you have a great time learning computer science!!!
