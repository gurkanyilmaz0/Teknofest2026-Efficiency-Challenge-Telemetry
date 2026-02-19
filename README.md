# Teknofest2026-Efficiency-Challenge-Telemetry
Ayyıldız Electromobile ekibi için Nextion Basic ekran ve Arduino tabanlı telemetri arayüzü
Bu proje, Karabük Üniversitesi Ayyıldız Electromobile takımı bünyesinde, TEKNOFEST Efficiency Challenge Elektrikli Araç Yarışları için geliştirilen yerli telemetri arayüz yazılımıdır.Araçtan alınan verilerin (hız, sıcaklık, voltaj) sürücüye anlık olarak görselleştirilmesi ve kritik durumlarda sesli/görsel uyarı verilmesini sağlar. Proje, donanım olarak Arduino ve Nextion Basic Serisi ekran kullanmaktadır.

Nextion Editör içindeki kodlar:

  Preinitialize event execute before component refresh:
    vis p1.1

    Timer Event(tm0):
          // Nextion tm0 (Timer) Olayı
      if(h0.val>70||n1.val>24||n2.val>450||j0.val<50)
        {
        if(sys1==0)
        {
        vis p1,1  // İkaz ışığını göster
        sys1=1
      }else
      {
        vis p1,0  // İkaz ışığını gizle
        sys1=0
      }
      }else
      {
      vis p1,0    // Şartlar düzelince gizle
      sys1=0
      }
      ref page0

      Timer Evemt(tm1):
          // 1. Açısal yay genişliği
sys0=h0.val*225
sys0=sys0/220
// 2. Başlangıç açısını 330'a düşürerek ibreyi belirgin şekilde aşağı alıyoruz
sys0=sys0+330
// 3. 360 derece devir kontrolü
if(sys0>=360)
{
  sys0=sys0-360
}
// 4. Sonucu ibreye aktar
z0.val=sys0
n0.val=h0.val


  Program.s:
    //The following code is only run once when power on, and is generally used for global variable definition and power on initialization data
int sys0=0,sys1=0,sys2=0     //At present, the definition of global variable only supports 4-byte signed integer (int), and other types of global quantity declaration are not supported. If you want to use string type, you can use variable control in the page to implement
baud=9600//Configure baudrate
dim=100//Configure bac
recmod=0//Serial data parsing mode:0-Passive mode;1-Active mode
printh 00 00 00 ff ff ff 88 ff ff ff//Output power on information to serial port
page 0                       //Power on start page 0


