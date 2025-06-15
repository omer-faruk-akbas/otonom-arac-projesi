# 🚗 Raspberry Pi Tabanlı Otonom Araç Projesi

Bu proje, **Raspberry Pi 4 Model B** üzerinde çalışan, gerçek zamanlı görüntü işleme ile **şerit takibi** ve **trafik ışığı algılama** özelliklerine sahip otonom araç sistemidir. Araç, hem otonom hem de manuel sürüş modlarında çalışabilir.

---

## 🛠️ Kullanılan Donanım ve Yazılım Teknolojileri

### Donanım
- Raspberry Pi 4 Model B
- Raspberry Pi Camera Module (CSI bağlantılı)
- DRV8833 Motor Sürücü
- 3.7V Li-ion Batarya (Motor gücü için)
- Power Bank (Raspberry Pi güç kaynağı için)
- DC Motorlar
- GPIO bağlantıları için jumper kablolar

### Yazılım & Kütüphaneler
- Python 3
- OpenCV (Görüntü işleme)
- NumPy (Sayısal hesaplamalar)
- Picamera2 (Raspberry Pi kamera kontrolü)
- RPi.GPIO (GPIO pin kontrolü)

---

## ⚙️ Sistem Mimarisi ve İşleyiş

### 1. İşletim Sistemi ve Yazılım Altyapısı
- Raspberry Pi OS kurulumu gerçekleştirilmiştir.
- SSH ve uzak masaüstü erişimleri aktif edilmiştir.
- Python ve gerekli kütüphaneler (OpenCV, NumPy, Picamera2, RPi.GPIO) kurulmuştur.

### 2. Motor Sürücü ve Güç Bağlantıları
- DRV8833 motor sürücüsü, Raspberry Pi’nin GPIO pinlerine bağlanarak motor kontrolü sağlanmıştır.
- Motorlar için güç, 3.7V bataryadan sağlanırken Raspberry Pi ayrı bir Power Bank ile beslenmiştir.
- Motor hareketleri ileri/geri ve sağa/sola dönüş şeklinde GPIO çıkışları ile kontrol edilmektedir.

| İşlev          | Raspberry Pi GPIO | DRV8833 Pin |
|----------------|-------------------|-------------|
| Motor A İleri  | GPIO 17 (AIN1)    | AIN1        |
| Motor A Geri   | GPIO 27 (AIN2)    | AIN2        |
| Motor Standby  | GPIO 22 (STBY)    | STBY        |
| Motor B Sağa   | GPIO 23 (BIN1)    | BIN1        |
| Motor B Sola   | GPIO 24 (BIN2)    | BIN2        |

### 3. Kamera Entegrasyonu ve Görüntü İşleme
- Raspberry Pi Camera Module, CSI portu üzerinden bağlanmıştır.
- Picamera2 kütüphanesi ile kamera başlatılmış ve gerçek zamanlı görüntü alınmıştır.
- OpenCV ile görüntü işleme uygulanmış; şerit takibi ve trafik ışığı algılama gerçekleştirilmiştir.
- Trafik ışığı renk tespiti HSV renk uzayında maskeleme yöntemiyle yapılmıştır:
  - Kırmızı ışık: İki farklı HSV aralığında maske
  - Yeşil ışık: Tek bir HSV aralığında maske
- Maske içerisindeki aktif pikseller sayılarak ışığın durumu belirlenmiştir.

### 4. Araç Kontrolü
- Algoritma trafik ışığına göre aracı durdurma veya hareket ettirme kararları vermektedir.
- Manuel kontrol modu da geliştirilmiş, WASD tuşları ile klavyeden araç yönlendirme sağlanmıştır.
- Kullanıcı, sistem açılırken mod seçimi yapabilir:
  - **1:** Otonom Mod (trafik ışığına göre otomatik sürüş)
  - **2:** Manuel Mod (klavye ile kontrol)

### 5. Görsel Geri Bildirim
- Ekranda gerçek zamanlı olarak trafik ışığı durumu görsel olarak gösterilir.
- Modlar arası geçiş ve hata durumları için kullanıcıya bildirimler sağlanmaktadır.

---

## 📂 Proje Kurulum ve Çalıştırma

1. Raspberry Pi OS kurulumu tamamlanır.
2. Python 3 ve gerekli kütüphaneler aşağıdaki komutlarla yüklenir:
   ```bash
   sudo apt update
   sudo apt install python3-pip
   pip3 install opencv-python numpy picamera2 RPi.GPIO

3. Motor sürücü ve batarya bağlantıları yapılır.

4. Kamera Raspberry Pi’ye takılır ve aktif edilir.

5. Proje kodları indirilir ve çalıştırılır:

6. Başlangıçta mod seçimi yapılır (1 - Otonom, 2 - Manuel).

🎥 Proje Videosu
Projeye ait detaylı çalışma ve sonuçları içeren video buradan izlenebilir.
📺 [Proje Videosunu İzle](https://www.youtube.com/watch?v=EHhP65NESIM)

## 📂 Kod Durumu

> **Not:**  
> Şu an otomatik hareket eden, trafik ışığı ve şerit algılama fonksiyonlarına sahip otonom araç kodu, `otonom_arac_kodu.py` dosyası altında paylaşılmıştır.  
> Detaylı algoritma ve uygulama için bu dosyayı inceleyebilirsiniz.
