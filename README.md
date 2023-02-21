# Natural Language Processing Basic With C Language 
 
@Bu program kullanıcının girdiği metnin, hangi dilde yazıldığını bulmaktadır.
@Bursa_Technical_University/Computer_Engineering First year First semester

<h3 align="center" color="Darkblue">Ahmet Bahadır Aksakal - İrem Atak</h3>
<h4 align="center" color="Darkblue">20360859079</h4>

<ol>
  <li>
      <h3 color="Red">Projede Kullanılan Teknoloji Ve Diller:</h3>
      <ul>
        <li>C</li>
      </ul>
  </li>
  <li>
      <h3 color="Red">Nasıl Kullanılır</h3>
      <ul>
        <li>Program komut sistemi üzerinden çalıştırılır.</li>
        <li>İlgili metin konsola girilir.</li>
        <li>Metin girildikten sonra 'enter' tuşuna basınız.</li>
        <li>ctrl+z' tuşuna basınız sonra 'enter' tusuna tekrar basınız. Program gerekli hesaplamaları yapıp sonucu size döndürecektir.</li>
      </ul>
  </li>
  <li>
      <h3 color="Red">Genel Çalışma Yapısı</h3>
      <ul>
        <li>10000 karakteri aşmayacak bir metin kullanıcı tarafından girilir.</li>
        <li>Girilen metin yabancı karakterlerden temizlenir.</li>
        <li>Bigram ve trigramlarin metinde kaç kez geçtiği hesaplanır.</li>
        <li>Verilen frekans değerleriyle hesaplama yapılır ve metnin dilinin Almanca mı yoksa İngilizce mi olduğu ekrana yazdırılır.</li>
      </ul>
  </li>
  <li>
      <h3 color="Red">Detaylı Çalışma Yapısı Ve Fonksiyon Açıklamları</h3>
      <ul>
        <li>
         <h4 color="Darkblue">Adım 1:</h4>
            <p>
               Metin alınırken kullanılan void metni_al(char str[]) fonksiyonu gets() 
               kullanımı sonucu oluşabilecek hataları (copy-paste-error) gidermek için  
               getchar() isimli fonksiyonu for döngüsü içinde kullandık. Böylece copy-
               paste sorununu çözdük. Daha farklı fonksiyonları da denedik ama 
               tekrardan hata aldık. En doğru yöntemin for döngüsünü kullanmak 
               olduğuna karar verdik. Art arda metin girilmesi durumunda her seferinde 
               build and run yapmak  yerine maindeki bütün fonksiyonlarımızı sonsuz 
               bir döngünün içine aldık ve bu döngüde bir devam koşulu koyduk .
               O koşul gerçekleşmediği sürece yeni metin girilebiliyor. Koşul 
               gerçekleştiğindeyse yeni metin girilemiyor .Metnin tamamı girildikten 
               sonra enter ile alt satıra geçip eof karakter  tuşlanır ve tekrardan entera 
               tıklanır . Böylece program çalışır.
            </p>
        </li>
        <li>
         <h4 color="Darkblue">Adım 2:</h4>
            <p>
               Girilen metin void filter_str(char str[]) fonksiyonu ile yabancı karakterlerin 
               yerine boşluk karakteri yerleştirilir. Böylece metin yabancı karakterlerden 
               temizlenmiş olur. Metni temizledikten sonra bütün karakterleri küçük harfe
               dönüştürdük. Amacımız bigram ve trigramlar aranırken sorun çıkmamasıydı.
            </p>
        </li>
       <li>
         <h4 color="Darkblue">Adım 3:</h4>
            <p>
               Girilen metinde void calculate_frequencies_bi(char str[]) fonksiyonu ile 
               her bir bigramın metinde kaç kez tekrar ettiğini hesapadık. Şöyle bir sorunla 
               karşılaştık. Örneğin “the” kelimesinde hem “th” bigramı hem de “he” bigramı 
               var. İlk yazdığımız fonksiyonda ilk bigramı saydıktan  sonra ikinci bigramı 
               saymıyordu. Yani bigramları eksik hesaplıyordu. Projede yazdığımız 
               fonksiyonla bu sorunu çözdük ve minimum düzeyde RAM kullanımına dikkat 
               ettik. Hesaplanan frekansaları calculated_frequencies[i] dizisine sırasıyla 
               yerleştirdik.
            </p>
        </li>
       <li>
         <h4 color="Darkblue">Adım 4:</h4>
            <p>
               Girilen metinde void calculate_frequencies_tri(char str[])  fonksiyonu ile 
               her bir trigramın metinde kaç kez tekrar ettiğini hesapladık. Hesaplanan 
               frekansaları 10. elemandan başlayacak şekilde calculated_frequencies[i+10] 
               dizisine sırasıyla yerleştirdik.
            </p>
        </li>
       <li>
         <h4 color="Darkblue">Adım 5:</h4>
            <p>
              void calculate_distances() fonksiyonu ile İngilizce ve Almanca dilleri için ayrı ayrı puanlama yaptık . 
              Distances[0] dizisine İngilizce için hesaplananpuan atanır.  distances[1] dizisineyse Almanca için hesaplanan puan atanır.
              Projede bizden öklit hesaplaması yapmamız isteniyordu ama bu
              hesaplama kısa metinlerde hatalı sonuç veriyordu. Özellikle 3 satırı geçmeyen
              metinlerde ciddi sorunlar oluyordu. Doğruluk oranı nerdeyse %70’in
              altındaydı. Bu sorunu çözecek yeni bir yöntem geliştirdik. Yöntemimiz şu
              şekilde frekansı 1’den yüksek olan bigram ve trigramları seçtik. İngilizce için
              bunların tekrar sayısını toplayıp distances[0] dizisine yerleştirdik. Almanca
              içinse aynı şekilde toplayıp distances[1] dizisine yerleştirdik.
            </p>
        </li>
       <li>
         <h4 color="Darkblue">Adım 6:</h4>
            <p>
               void detect_lang() fonksiyonunda distances[0] ve distances[1]’in değerlerini
               karşılaştırdık . Distances dizisinin 0. indeksteki değeri daha büyükse metnin
               dilinin İngilizce olduğu ekrana yazdırılıyor, değilse Almanca olduğu 
               yazdırılıyor. Belirlenen dilin doğruluğunu arttırmak için bir algoritma
               kullandık. Bir sayaç ekledik. Bu sayaç tekrar sıklığı 1’den az olan bigram ve  
               trigramları sayıyor. Eğer  sayaç 20 ise girilen metin çok kısadır ve sonuç doğru 
               olmayabilir. Bunu  kullanıcıya da belirtmek için uyarı mesajı gönderdik. 2. bir
               sayaç ekledik. Bu sayaç bigram ve  trigramların tekrar sıklığı 5’den az 
               olanlarını sayıyor. 2. sayaç 20 ise girilen metin muhtemelen bir cümledir. 
               Metinse de farklı bir dil olabilir. Bunu belirtmek için de kullanıcıya bir uyarı
               mesajı gönderiyoruz. Projemiz geliştirilmeye açık. Farklı dilde daha uzun bir 
               metin girildiğinde sayac1 ve sayac2 işlevsiz kalacaktır.
            </p>
        </li>
       <li>
         <h4 color="Darkblue">Not 1:</h4>
            <p>
               Bizden bigram ve trigramların frekanslarının hesaplanması istendi.
               Frekansları ,bigram ve trigramların tekrar sayılarını toplam kelime sayısına 
               bölüp hesaplamayı planladık. void metinde_kelime_sayisi_bulucu(char str[]) 
               fonksiyonunu metindeki toplam kelimeyi bulmak için kullandık. Bu 
               fonksiyonun çalışma mantığı şöyledir: 2 boşluk arasındaki char dizisini kelime 
               olarak tanımlar ve bundan yola çıkarak metindeki kelime sayısını hesaplar. Bu 
               yöntemin her zaman doğru sonuç vermediğini fark ettik ve yöntemimizi 
               değiştirdik. Bu fonksiyonu herhangi bir yerde kullanmadık. Fonksiyonun 
               projemizde bulunmasını istedik çünkü proje geliştirilirse ihtiyaç 
               duyulabileceğini düşündük.
            </p>
        </li>
       <li>
         <h4 color="Darkblue">Not 2:</h4>
            <p>
               void SetColor(int ForgC) bu fonksiyonun yerine ilk başta System(“COLOR D”);
               fonksiyonunu kullanarak bütün metnin rengini değiştirebiliyorduk ama 
               istediğimiz yerlerde değişiklik yapamıyorduk. İstediğimiz kısımlarda metnin
               rengini değiştirebileceğimiz bir fonksiyon bulmak istedik . Yeterli bilgimiz 
               olmadığından çeşitli forumlardan yardım alarak bu fonksiyonu bulduk.
               Fonksiyonun kütüphanelerini ve fonksiyonu metnimize ekleyerek 
               istediğimiz renklendirme işlemlerini yaptık. Bu fonksiyonu kullanmamızın
               nedeni kullanıcının dikkatini çekmek ve görsel bir estetiklik katmaktır.
               Projenin işlevi kadar tasarımının da önemli olduğunu düşünüyoruz.
            </p>
        </li>
      </ul>
  </li>
  <li>
      <h3 color="Red">Programdan Görseller:</h3>
      <ul>
        <li><img src="GorsellerReadme/1.png"></li> 
        <li><img src="GorsellerReadme/2.png"></li>
      </ul>
  </li>
</ol>

 
