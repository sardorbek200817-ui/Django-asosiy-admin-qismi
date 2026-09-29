1 ]  <!-- https://admin.ecoart.uz/dashboard/warehouse/products -->

bizning product uchun misol tariqasi korsatilgan

2 ] category = models.ManyToManyField(to="Category" , related_name="products")
    to='Category' bu qaysi Category modeliga boglanishini belgilaydi

ManyToMany qoydasi >>>>>  Bitta Product > bir nechta Category
Bitta Category > bir nechta Product







class Product(models.Model):
    name = models.CharField(max_length=50)
    img = models.ImageField(upload_to='products/img' , blank=True , null=True)
    category = models.ManyToManyField(to="Category" , related_name="products")
    unit = models.CharField( UNITS,default='piece')
    amout = models.IntegerField()



class Category(models.Model):
    name = models.CharField(max_length=30)


bu yerdas agarda     category = models.ManyToManyField(to="Category" , related_name="products")
ManyToManyField orniga Foreinkey bolganda   Product ni boshqa modellarga ulab bolmas edi ManyToMany shu modelni ham boshqa joylarda ishlashiga yordam beradi




3 ]


    {% for item in product %}
    <tr class="hover:bg-white/[0.02] transition-colors group">

        {% for i in item.category.all %}
        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-white">
        <a href="{% url 'product_detail' i.id %}">{{i.name}}a>
        </td>
        {% endfor %}

demak bu yerda har bitta productga tegishli categroyiadagi malumotlarni ovolib for ga solyabmiz , chunki bu yerda har bitta productga boshqa bir kategoriya boglangan



4 ] {% for i in product.product_in.all %}
yani bu yerda viewsdan kelyabdi product bu yerda product ga boglangan malumotlarni chaqirib olyabdi product_in 'related_nem'


modelga ga boshqa bir modelga boglangan boglangan modelning nomi bu relayted_name desak ham boladi, yani productga boglangan kopgina modellarni related_name orqali chaqirib olishdir teskari boglanish qilish


5 ] 


 def products(request):
    mahsulot = Kategoriya.objects.first()
    mahsulot2 = mahsulot.products.all()

bunda Kategorydagi birinchi Kategoryadagi hamma mahsulotlarni olyabmiz  products >>> 'related_name'


6 ] try:
        product = Product.objects.get(id=id)
    except:
        return render(request , "1.html"

Yani bu yerda agarda id hatolik bolganda shunchaki except ishlasin deyabdi yani try ning vazifasi
hato chiqarmaslik >>>>> if dan farqi if bu tenglab yuborishga qodir try esa shunchaki ohshamasa
keyingisiga otib ketaver degani


# 7 ]     related_name 

related_name nima uchun kerak bu teskari boglanish uchun kerak boladi yani bizning 
olma degan modelimiz bor uni biz mevalar degan kategoriyaga boglashimiz kerak boladi
foreinkey orqali uni mevalarga boglaymiz related_name shunday iboratki mevalarga bizning olma
banan va juda kop mevalar boglangan boladi masalan biz olmanig ozini chaqirib olmoqchimiz
buning uchun undagi related name dan foydalanamiz related nameni qisqasi modelimizga nom qoyib
qoyish va uni oddiygina chaqirib olish


#                            MISOL

for i in categoriya.mahsulotlar.all() >> html qismi

yani categoriya foreinkey orqali boglagan categoriyamiz mahsulot bu related_name


# 8 ]     select_related
select_related  >>> masalan biz select_related ishlatmay oddiy funksiya orqali masalan 
kitoblarni muallifi bilan olmoqchi bolsak N+1 problem yuzaga keladi select_related esa buni bartaraf etadi
yani select_related orqali muallifni kiritsak aynan shu muallifga doir kitoblarni hammasini bita query da 
olib beradi resuls kamroq sarf boladi


#                               MISOL

mahsulot = Mahsulot.objects.select_related("kategoriya_id").all()

"kategoriya_id" >>> bu yerda foreinkey orqali boglangan ozgaruvchi nomi 
yani shu ozgaruvchiga boglangan categoriya ni hamma malumotlarni olib beradi

class Product(models.Modela):
>> kategoriya_id = foreinkey(categoriya)


class categoriya(models.Model)


# html qismida >> 

for i in mahsulot >> {{i.kategoriya_id.name}}



#   ASOSIY MISOLLAR

#  views.py
  
mahsulot = Mahsulot.objects.select_related("kategoriya_id").all()



#  model.py
  
class Author(models.Model):
    name = models.CharField(max_length=100)


class Article(models.Model):
    title = models.CharField(max_length=200)
    # Har bir maqola 1 ta avtorga tegishli
    author = models.ForeignKey(Author, on_delete=models.CASCADE)


 
select_releted >> ha demak qaysi model author ga boglangan bolsa shu boglangan modellardagi
hamma malumotni chaqirib oladi yani bitta model sorovida


