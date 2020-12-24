#include <stdio.h>                       /* aciklama yapilmayan satirlar raporda detaylica aciklanmistir.*/
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <math.h>
#include <ctype.h>
#include <dos.h>
#include <dir.h>
#include <windows.h> // bazi kutuphaneler gorselligi arttirmak icin eklenmistir.

float calculated_frequencies[20];// bigram ve trigramlarin frekanslarinin atandigi veri kumesi.
float distances [2]={0,0};
const char matrix_bigram_strings[10][3] ={"th", "he", "in", "er", "an", "en", "ch", "de", "ei", "te"};
const char matrix_trigram_strings[10][4]={"the", "and", "ing", "ent", "ion", "der", "sch", "ich", "nde", "die"};
const char languages[2][8]={"english", "german"};
//ingilizce dilinin frekans degerleri
const float frequency_eng[20]={ 2.71, 2.33, 2.03, 1.78, 1.61, 1.13, 0.01, 0.01, 0.01, 0.01, 1.81, 0.73, 0.72, 0.42, 0.42, 0.01, 0.01, 0.01, 0.01, 0.01 };
 //almanca dilinin frekans degerleri
const float frequency_germ[20]={ 0.01, 0.89, 1.71, 3.90, 1.07, 3.61, 2.36, 2.31, 1.98, 1.98, 0.01, 0.01, 0.01, 0.01, 0.01, 1.04, 0.76, 0.75, 0.72, 0.62 };

void metni_al(char str[]); // bu fonksiyon gets() kullanimi sonucu, olusabilicek hatalari (copy-paste-error) giderecek sekilde tasarlandi.
void filter_str(char str[]); // metni temizlerken en minumum seviyede islemle amacimiza ulasmayi hedefledik.
void metinde_kelime_sayisi_bulucu(char str[]); // metinde kac adet kelime oldugunu hesaplar.
void calculate_frequencies_bi(char str[]); // her bir bigramdan kac adet bulundugunu hesaplar
void calculate_frequencies_tri(char str[]);// her bir trigramdan kac adet bulundugunu hesaplar.
void calculate_distances();
void detect_lang();// metnin diline karar veren fonkiyon.


int main()
{
    char ac_kapa;// birden fazla metin ile test edebileceginizi varsayip kolaylik olmasi acisindan sarta bagli sonsuz dongu kurduk.

    while(ac_kapa!='0')//sarta bagli sonsuz dongu
    {

        char str[10000];// 9999 char alir. //str[strlen(str)] indexinde '\0' karakteri bulunur.// '\0' karakterine bosluk karakteri atanmamaya ozen gosterilmistir.
        metni_al(str);// metin kullanicidan alinir.
        printf("\n");
        filter_str(str);// istenmeyen karakterler temizlenir.
        printf("\n");
        metinde_kelime_sayisi_bulucu(str);//Bu fonksiyon proje kapsaminin disinda bir fonksiyondur. Proje gelistirilirse gerekli olabilir.
        printf("\n");
        calculate_frequencies_bi(str);// metinde her bigram'in kac kez gectigi hesaplanir.
        printf("\n");
        calculate_frequencies_tri(str);// metinde her trigram'in kac kez gectigi hesaplanir.
        printf("\n");
        calculate_distances();// bu asamada gerekli hesaplamalar ile girilen metnin hangi dile yakin oldugu hesaplanir.
        printf("\n");
        detect_lang();// Bu fonksiyon girilen metnin hangi dilde olduguna karar verir. Bu kararin dogrulugu hakkinda bilgi verir.
        printf("\n");
        SetColor(2); // estetik icin en altta tanimladigimiz fonk. Proje kapsaminda degildir. Linux sistemlerde sorun cikarabilir !!! Win. isletim sisteminde calistirilmalidir.
        printf("\n\nmetin girmeye devam edicekseniz 'enter' tusuna basiniz \n");// sonsuz döngü icin bir uyari metni
        SetColor(4);
        printf("Programi kapatmak icin '0' yazip 'enter' tusuna tiklayiniz\n\n");
        ac_kapa=getchar();// donguyu kirmak ve donguye devam etmek arasinda secim yapilan asama.

        SetColor(15);
    }


    return 0; // sifir hata ile main dondurulur.
}

void metni_al(char str[])// bu fonksiyon gets() kullanimi sonucu olusabilicek hatalari (copy-paste-error) giderecek sekilde tasarlanmistir.
{
    char c;
    int i,uzunluk;
    SetColor(5);
    printf("\n***Hangi Dilde Yazildigini Bulmak Istediginiz Metni Giriniz***\n");
    SetColor(4);
    printf("\n--- NOT!!!---\nMetni girdikten sonra 'enter' tusu ile alt satira geciniz. \nSonra 'ctrl+z' tusuna basiniz ve ondan sonra 'enter' tusuna basiniz\n");
    SetColor(4);
    printf("!!!Programi kullanabilmek icin mutlaka bu NOT'a dikkat ediniz!!!\n\n");
    SetColor(8);
    for(i=0; c!=EOF ;i++) //eof karakter ^Z oldugundan bunuda metnin icine atar. Bu sebeble "determinating karakter" strlen(girilen_char_sayisi+3) konumunda bulunur.// strlen(girilen_char_sayisi+1)= ^ // strlen(girilen_char_sayisi+2)= Z //
    { // her bir karakter girildiginde dongu doner.
        c=getchar();
        str[i]=c;
    }
    //dizi[i+3]= Z // metni_al fonksiyonu , eof 2 adet chardan olustusgundan ( " ^ "  ve " Z " ) karakterden sayar.
    str[i-2]='\0'; //^Z yi karakterden saymamasi için determinating karakteri " ^ " isaretinin yerine atandi.
}

void filter_str(char str[])
{
    SetColor(8);
      for(int i=0;i<strlen(str);i++)
      {
          if(!((str[i]>64&&str[i]<91)||(str[i]>96&&str[i]<123)||(str[i]==32)||(str[i]==0)))  // Bosluk karakteri,buyuk ve kucuk 27 harf ve determinating karakterin olup olmadigi kontrol edilir.
            str[i]=' ';
          else
            str[i]=tolower(str[i]); //kucuk harfle yazilmis bi_gram'lar vb...  Metinde ki buyuk harfler ile eslesirken sorun yasayacagindan metindeki bütün harfler kucuk harf yapilir.
      }
   printf("\n\n***Metniniz Yabanci Karakterlerden Temizlendi***\n\n");
   puts(str);// metnin duzenlenmis hali yazdirilir.
}

 void metinde_kelime_sayisi_bulucu(char str[]) // ozetle : hizimizi alamadik :)
{
    SetColor(5);
    printf("\n***Metindeki toplam kelime sayisi hesapliniyor***\n");
    int i=0,j=0,s=strlen(str)-1,sayac_metin=0; // strlen(str)-1 islemininin amaci en son indiste bulunan '\0' karakterini korumaktir.
    if(str[0]==' ') // bu if en bastaki bosluklar icin // kelimenin (basinda ve/veya sonunda) bosluk varsa sayac +/- (1-2) tutarsizlik yapar.
    {
        for(j;str[j]==' ';j++)
            ;// j sayac gorevindedir.
        i=j;// bu islem ile en bastaki bosluk/bosluklar yok edilir.
    }
    if(str[s]==' ') // bu if en sondaki bosluklar icindir// en sondaki bosluklari bulup harften sonraki ilk bosluga '\0'  atanir.
    {
        for(str[s];str[s]==' ';str[strlen(str)-1]=s--)  // int s , '\0' karakterinin bulundugu indisi icermeyecek sekilde tasarlandi.

        str[s+1]='\0';
    }
    for(j=i;j<strlen(str);j++)
    {
      if(str[j]==' ')                // j sifirdan birer birer arttirilir.
      {                            // eger basta bosluk karakteri varsa for dongusune girilip art arda bosluk olup olmadigi kontrol edilir.
                                   // art arda gelen bosluklari kelimeden saymamak icin j ve i esitlenir
           for(j;str[j]==' ';j++) // i, j'ye esitlenerek art arda gelen bosluklar atlanir.
                i=j;             //ve j her yeni bosluk gördügünde sayac 1 artar . sayacin son degeri bize metindeki kelime sayisini verir.
            sayac_metin++;    // Kelimeler sayilirken "kelime = iki bosluk arasindaki karakterdir" tanimi ile haraket edildi.
       }



    }
    printf("\n\nMetinde %d adet kelime vardir\n",sayac_metin+1);

}

void calculate_frequencies_bi(char str[])
{
    SetColor(5);
    printf("\n***Bigramlarin Frekanslari Hesaplaniyor***\n\n");
    int i=0,k=0,a=0,sayac=0,toplam;
    for(i;i<10;i++) // i degerlerinin her biri, bigram matrisindeki i. satirindaki 2 harfli kelimeyi  temsil eder.
    {
        for(int j=0;j<strlen(str);j++) // butun metin taranir.
        {
            if(str[a]==matrix_bigram_strings[i][k])// str[a] != bigramin ilk harfiyse  döngü a'yi bir arttirip surekli döner . // bulamaz ise diger bigrama  gecip tekrardan tum metin taranir.
            {               //str[a] ,bigramin ilk harfine esit olur ise bir sonraki ardisik harf kontrol edilir.
              k++;        // sirali ardisik iki harf ("i" satir indisli) bigrama esit ise sayac 1 arttirilir.
                         // bu döngü strlen(str) kere doner ve i satir indisli bu bigramdan kac adet oldugu sayacta tutulur.
              if(k==2) // eger ilk harf uyar, 2. harf uymaz ise k sifirlanir , sayac artmaz ,a 1 artar ve program tarafindan siradaki harf ile ayni bigram tekrar test edilir.
              {
                  k=0;
                  sayac++;
              }

            }
            a++;  // metinde  1 harf ilerlenmesi saglanir ve son deger strlen(str) olur.
            if(str[a]!=matrix_bigram_strings[i][k]) //  ilk harfler uyusur fakat 2. harfler uyuşmaz ise k sifira esitlenir.
                k=0;


        }
        toplam+=sayac;
        calculated_frequencies[i]=sayac;  //"i. satirdaki  bigramdan kac adet oldugu sayacta tutulur.
        sayac=0; // sayac siradaki bigrami icin sifirlanir. // dongu basa doner ve yeni bigram icin calisir.
        a=0; //yeni bigrami  butun metinde tekrar taratmak icin a sifirlanir.
    }
    printf("                        {\n");
    for(int y=0;y<10;y++)
    {
        printf("%s's frequencies --> ",matrix_bigram_strings[y]);
            for(int g=0;g<3;g++)
                    printf(" ");
        printf("  %f,\n",calculated_frequencies[y]);


    }
    printf("                              }\n");

}


void calculate_frequencies_tri(char str[])
{
    SetColor(5);
    printf("\n***Tri_gramlarin Frekanslari Hesaplaniyor***\n\n");
    int i=0,k=0,a=0,sayac=0;

    for(i=0;i<10;i++)
    {
        for(int j=0;j<strlen(str);j++)
        {
            if(str[a]==matrix_trigram_strings[i][k])
            {
                k++;
                if(k==3)
                {
                    k=0;
                    sayac++;
                }
            }

            a++;
            if(str[a]!=matrix_trigram_strings[i][k])
            k=0;
        }

        calculated_frequencies[i+10]=sayac; // i+10 dan baslanir cunku 9. indiste bigramlarin son elemani olan "te" bulunur.
        sayac=0; // her seferinde sayac bir sonraki trigrami saymak icin sifirlanir.
        a=0; // metni en bastan taramak icin a sifira esitlenir.
    }

    printf("                        {\n");
    for(int y=0;y<10;y++)
    {
        printf("%s's frequencies --> ",matrix_trigram_strings[y]);
        for(int g=0;g<3;g++)
                printf(" ");
        printf("  %f,\n",calculated_frequencies[y+10]);


    }
    printf("                              }\n");



}

void calculate_distances()
{


    //ing. icin tek tek uzaklik hesaplanip hepsi toplanir.
    for(int i=0;i<5;i++)
    {

           distances[0]=distances[0]+calculated_frequencies[i]+calculated_frequencies[i+10]; // Ing. de frekansi en yuksek olan 5 bigram ve 5 trigram toplanir ve distances[0] a atanir.
           distances[1]=distances[1]+calculated_frequencies[i+5]+calculated_frequencies[i+15]; // Alm. da frekansi en yuksek olan 5 bigram ve 5 trigram toplanir ve distances[1] e atanir.
            // distances[0]'in degeri yuksek ise metin Ing. , distances[1]'in degeri yuksek ise metin Almancadir.
    }
}



void detect_lang()  // Bu fonksiyon metnin hangi dilde yazildigini bulur.
{
    int sayac=0,sayac2=0;
    for(int i=0;i<20;i++)
    {
        if(calculated_frequencies[i]<=1)  //  belli bir degerin altindaki sonuclar icin uyari mesaji verilir.
            sayac++;
        if(calculated_frequencies[i]<=5)
            sayac2++;

    }
    printf("\ntotal_point_ing: %.1f\ntotal_point_ger: %.1f\n",distances[0],distances[1]);
    SetColor(1);
        if(distances[0]>distances[1])
            printf("\ngirilen metin ingilizcedir\n");
        else
            printf("\ngirilen metin almancadir\n");

    SetColor(4);

        if(sayac==20) // kararin dogrulugunun degerlendirilmesi gerekli ise uyari verilir
            printf("\nmuhtemelen cumle yada metin girmediniz ya da girdiginiz dil sistemimizde tanimli degil\n sonuclar hatali olabilir\n");
        else if(sayac2==20) // kararin dogrulugunun degerlendirilmesi gerekli ise uyari verilir
            printf("\nmuhtemelen kisa bir cumle girdiniz ya da girdiginiz dil sistemimizde tanimli degil\n sonuclar hatali olabilir\n");


        distances[0]=0; // her seferinde sifirlanir cunku mainde sonsuz dongu vardir.
        distances[1]=0; // sonsuz dongu icin sifirlanir.
}

void SetColor(int ForgC)  // estetik gorunum icin yazilmistir.
{
	 WORD wColor;

      HANDLE hStdOut = GetStdHandle(STD_OUTPUT_HANDLE);
      CONSOLE_SCREEN_BUFFER_INFO csbi;

                       //We use csbi for the wAttributes word.
     if(GetConsoleScreenBufferInfo(hStdOut, &csbi))
     {
                 //Mask out all but the background attribute, and add in the forgournd    color
          wColor = (csbi.wAttributes & 0xF0) + (ForgC & 0x0F);
          SetConsoleTextAttribute(hStdOut, wColor);
     }
     return;
}
/*
BLACK	     0
BLUE	     1
GREEN	     2
CYAN	     3
RED	         4
MAGENTA      5  // purple
BROWN	     6
LIGHTGRAY	 7
DARKGRAY	 8
LIGHTBLUE	 9
LIGHTGREEN	 10
LIGHTCYAN	 11
LIGHTRED	 12
LIGHTMAGENTA 13
YELLOW	     14
WHITE	     15
*/


