## Yazılım Mimarisi ve Tasarımı


## Builder Design Pattern


Builder (Kurucu) Tasarım Deseni karmaşık yapıdaki nesnelerin oluşturulmasında, istemcinin nesne tipi belirterek üretimi gerçekleştirilebilmesini sağlamak için kullanılır.Builder Design Pattern adı üzerinde bir inşaatçı görev üstlenen yaklaşım sergilemektedir. Projemiz inşa süresindeyken oluşturacağımız bazı nesnelerin üretimleri oldukça maliyetli olabilir, zamanla bu nesnelerin yapısı değişebilir yahut güncellenebilir. Anlayacağınız nesne üzerinde her türlü dinamik süreç yaşanabilir. İşte bu tarz inşa durumlarında Builder Design Pattern ile ilgili nesneler genişletilebilir bir hale getirilmekte ve en önemlisi kod karmaşalığı minimize edilmektedir.Bu kompleks ve maliyetli nesnelerin oluşturulmasından Builder dediğimiz sınıf sorumlu tutulacaktır. Client, hangi nesnenin oluşturulacağını türü aracılığıyla belirteceğinden dolayı oluşturulacak asıl nesneyle ve oluşturulmasıyla ilgilenmeyecektir. Dolayısıyla istemciyi maliyetli nesnelerin üretimsel sorumluluğu olan bu tarz bir işlevden kurtarmış olacağız. Ayriyetten, oluşturulacak nesnenin gerekli tüm donanımını ilgili desen halledeceği için istemciye sadece ne istediğini bilmek kalacaktır.

![]()

Evet, yukarıdaki şemayı incelerseniz eğer gördüğünüz gibi “Builder”, “ConcreteBuilder”, “Product” ve “Director” isminde dört adet terimimiz mevcuttur. Builder paterninin senaryosunda kullanacağımız bu aktörler kimlermiş inceleyelim;

Product

İnşa sonucunda elde etmek istediğimiz nesnemizdir. Şemayı incelerseniz eğer ConcreteBuilder sınıfı tarafından üretilmektedir.

ConcreteBuilder

Gördüğünüz gibi Product ismini verdiğimiz nesneyi oluşturmaktadır. Oluşturulacak Product’ın temel özellik ve donanımını sağlayan sınıftır.

Builder

Product nesnesinin oluşturulması için gerekli arayüzü sağlar. Dikkat ederseniz ConcreteBuilder nesnesi ile kalıtsal bir durum söz konusudur.

Director

Yaptığımız tasarım sonucunda bir Builder referansı üzerinden Client tarafından nesne üretim talebine cevap verir.

Konuyla ilgili terminoloji aşamasından sonra sıra bir kaç senaryo üzerinden Builder desenini örneklendirmeye geldi.

