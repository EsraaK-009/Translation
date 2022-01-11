
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




