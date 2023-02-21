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
      </ul>
  </li>
  <li>
      <h3 color="Red">Oyundan Görseller:</h3>
      <ul>
        <li><img src="GorsellerReadme/1.png"></li> 
        <li><img src="GorsellerReadme/2.png"></li>
      </ul>
  </li>
</ol>

 
