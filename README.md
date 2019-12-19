## Yazılım Mimarisi ve Tasarımı


## Builder Design Pattern


Builder Tasarım Deseni karmaşık yapıdaki nesnelerin oluşturulmasında, istemcinin nesne tipini belirterek üretimi gerçekleştirilebilmesini sağlamak için kullanılır.Builder Design Pattern adı üzerinde bir inşaatçı görev üstlenen yaklaşım sergilemektedir. Projemiz inşa süresindeyken oluşturacağımız bazı nesnelerin üretimleri oldukça maliyetli olabilir, zamanla bu nesnelerin yapısı değişebilir yahut güncellenebilir. Yani nesne üzerinde her türlü dinamik süreç yaşanabilir. İşte bu tarz inşa durumlarında Builder Design Pattern ile ilgili nesneler genişletilebilir bir hale getirilmekte ve en önemlisi kod karmaşalığı minimize edilmektedir.
Yukarıda bahsettiğimiz o kompleks ve maliyetli nesnelerin oluşturulmasından Builder dediğimiz sınıf sorumlu tutulacaktır. Client, hangi nesnenin oluşturulacağını türü aracılığıyla belirteceğinden, oluşturulacak asıl nesneyle ve oluşturulmasıyla ilgilenmeyecektir. Dolayısıyla istemciyi maliyetli nesnelerin üretimsel sorumluluğu olan bu tarz bir işlevden kurtarmış olacağız. Ayriyetten, oluşturulacak nesnenin gerekli tüm donanımını ilgili desen halledeceği için istemciye sadece ne istediğini bilmek kalacaktır.

![](https://github.com/RukiyeSahin/yazilim-mimarisi-ve-tasarimi-2/blob/master/Builder.png)

Evet, yukarıdaki şemayı incelerseniz eğer gördüğünüz gibi "Builder", "ConcreteBuilder", "Product" ve "Director" isminde dört adet terimimiz mevcuttur. Şimdi bu terimlerden bahsedersek;

Product

İnşa sonucunda elde etmek istediğimiz nesnemizdir. Şemayı incelerseniz eğer ConcreteBuilder sınıfı tarafından üretilmektedir.

ConcreteBuilder

Gördüğünüz gibi Product ismini verdiğimiz nesneyi oluşturmaktadır. Oluşturulacak Product’ın temel özellik ve donanımını sağlayan sınıftır.

Builder

Product nesnesinin oluşturulması için gerekli arayüzü sağlar. Dikkat ederseniz ConcreteBuilder nesnesi ile kalıtsal bir durum söz konusudur.

Director

Yaptığımız tasarım sonucunda bir Builder referansı üzerinden Client tarafından nesne üretim talebine cevap verir.

Şimdi Builder Deseninine örnek verelim.

![](https://github.com/RukiyeSahin/yazilim-mimarisi-ve-tasarimi-2/blob/master/BuilderAraba.png)

Öncelikle ele alacağımız örnek birbirinden farklı özellik ve markalara sahip araba üretecek bir yapı oluşturmaktadır.

Burada oluşturmak istediğimiz ürün araba olacağı için Product nesnemiz Araba sınıfı olacaktır. Arabayı ürettirecek olan Opel, Ford, Mercedes  gibi birbirlerinden farklı özellik teşkil edecek olan tüm sınıflarımız ConcreteBuilder sınıfımız olacaktır.Şimdi bu örneğimizi kod kısımları ile birlikte açıklayalım.

Öncelikle Product Class’ımızı oluşturuyoruz.

```sh
//Product Class
class Araba
{
   public string Marka {get; set;}
   public string Model {get; set;}
   public double KM {get; set;}
   public bool Vites {get; set;}
   public override string ToString()
   {
     return $"{Marka} marka araba {Model} modelinde {KM} vites olarak üretilmiştir.";
   }
  }
   ```

Şimdi ise Builder arayüzümüzü oluşturalım.

```sh
//Builder
abstract class ArabaBuilder
{
   protected Araba araba;
   public Araba Araba 
   {
     get {return araba;}
   }
   public abstract void SetMarka();
   public abstract void SetModel();
   public abstract void SetKM();
   public abstract void SetVites();
   
 }
 ```
 
Burada dikkat etmemiz gereken husus, Builder sınıfımızda Araba referanssını protected olarak işaretlememizdir.Bunun sebebi, Bu Builder Class'ın uygulayacağı derived Class'lardan bu fieldea erişilebilmesi içindir.
 
Ardında Concrete builder nesnelerimizi oluşturalım.

```sh
//ConcreteBuilder Class

class OpelConcreteBuilder : ArabaBuilder
{
  public OpelConcreteBuilder()
  {
    araba = new Araba();
  }
  public override void SetKM() => araba.KM =100;
  public override void SetMarka () => araba.Marka ="Opel";
  public override void SetModel () => araba.Model ="Astra";
  public override void SetVites() => araba.Vites= true;
}
//ConcreteBuilder Class

class toyotaConcreteBuilder : ArabaBuilder
{
  public ToyotaConcreteBuilder()
  {
    araba = new Araba();
  }
  public override void SetKM() => araba.KM =150;
  public override void SetMarka () => araba.Marka ="Toyota";
  public override void SetModel () => araba.Model ="Corola";
  public override void SetVites() => araba.Vites= true;
}
//ConcreteBuilder Class

class BMWConcreteBuilder : ArabaBuilder
{
  public BMWConcreteBuilder()
  {
    araba = new Araba();
  }
  public override void SetKM() => araba.KM =25;
  public override void SetMarka () => araba.Marka ="BMW";
  public override void SetModel () => araba.Model ="X5";
  public override void SetVites() => araba.Vites= true;
}
```
Son olarak Director Class'ı oluşturalım.

```sh
//Director class
class ArabaUcret
{ 
   public void Ucret(ArabaBuilder Araba)
   { 
     Araba.SetKM();
     Araba.SetMarka();
     Araba.SetModel();
     Arba.SetVites();
    }
  }
  ```
  Araba üretimi için Builder Design Pattern'i uygulamış olduk. Şimdi bir Client tarafından araba talebinde bulunabiliriz.Bunun için aşağıda main metodu yazılmıştır
  
  ```sh
  //Client
  class Program
{
    static void Main(string[] args)
    {
        ArabaBuilder araba = new OpelConcreteBuilder();
        ArabaUret uret = new ArabaUret();
        uret.Uret(araba);
 
        Console.WriteLine(araba.Araba.ToString());
 
        araba = new ToyotaConcreteBuilder();
        uret.Uret(araba);
        Console.WriteLine(araba.Araba.ToString());
 
        Console.Read();
    }
}
```
