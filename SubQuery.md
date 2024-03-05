 # Subquery in Django
## AmirMohamadAsghari



[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://github.com/AmirMohamadmAsghari)





## معرفی
What is a Subquery?
- یک پرس و جو فرعی که به عنوان پرس و جوی تودرتو یا پرس و جو داخلی نیز شناخته میشود پرس و جوی تودرتو در داخل پرس جوی دیگری است
- امکان اجرای پرس و جوهای پیچیده را با تقسیم آنها به بخش های کوچیکتر و قابل مدیریت تر فراهم میکند



## Why Use Subqueries?

- Complex Filtering:فیلتر پیچیده:پرس و جوی فرعی فیلترینگ پیچیده را بر اسا نتایج یک پرس و جود دیگر فعال می کنند
- Annotations and Aggregations:حاشیه نویسی و تجمع: انها حاشیه نویسی و تجمع را با استفاده از داده های به دست امده از پرسش های فرعی تسهیل میکنند
- Reuse and Maintainability:استفاده مجدد و نگهداری: پرس و جو های فرعی قابلیت استفاده مجدد و نگهداری کد را با تجزیه عملیات پیچیده به اجزای کوچکتر و قایل استفاده مجدد افزایش می دهند



## Example

سناریویی را درنظر بگیرید که در ان ما دو مدل داریم:نویسنده و کتاب ما میخواهیم همه نویسندگانی که بیش از یک کتاب نوشته اند را پیدا کنیم



```python
from django.db.models import Count, Subquery

subquery = Book.objects.filter(author_id=OuterRef('id')).values('author_id').annotate(book_count=Count('id')).values('book_count')

authors_with_multiple_books = Author.objects.annotate(num_books=Subquery(subquery)).filter(num_books__gt=1)

```

در این مثال
- برای بازیابی تعداد کتاب های نوشته شده توسط هر نویسنده از یک پرسش فرعی استفاده میکنیم
- سپس پرس و جو بیرونی نویسندگان را بر اساس نتایج جست و جوی فرعی فیلتر میکند و فقط کسانی را انتخاب میکند که بیش از یک کتاب دارند


## نتیجه

- پرس و جو های فرعی مکانیزم قدرتمندی برای مدیریت عملیات پیچیده پایگاه داده فراهم میکند.
- توسعه دهندگان را قادر میسازد تا با تقسیم وظایف پیچیده به اجزای کوچکتر و قابل استفاده مجدد پرس جوهای گویا و کارآمد بنویسند.
- با استفاده از پرس و جو ها فرعی برنامه های جنگو می توانند به انعطاف پذیری قابلیت نگهداری و عملکرد بیشتری در عملیات پایگاه داده دست یابند.  
