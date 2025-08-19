Bu depo, Siemens TIA Portal ile geliştirilmiş, PLC programlamanın temel kavramlarını gösteren çeşitli bağımsız projeleri içerir. Her bir proje, farklı bir kontrol senaryosunu ele alır ve bu senaryoları gerçekleştirmek için kullanılan temel PLC komut ve bloklarını (SET, RESET, TON, NORM_X, SCALE_X vb.) uygulamalı olarak gösterir. Bu projeler, PLC programlamaya yeni başlayanlar ve temel otomasyon mantıklarını pekiştirmek isteyenler için ideal bir kaynak niteliğindedir.

Çalışma Mantığı
Bu depodaki projeler, her biri farklı bir amaca hizmet eden birden fazla bağımsız senaryoyu kapsar. Çalışma mantıkları aşağıda her bir senaryo için ayrı ayrı açıklanmıştır.

1. Analog Sinyal İşleme ve Ölçekleme
Bu senaryo, bir sensörden gelen analog sinyali okumayı ve işleyerek daha anlamlı bir değere dönüştürmeyi gösterir.

Sinyal Dönüşümü: NORM_X bloğu, analog girişten (%MW100, AnalogGiris) gelen ham tamsayı (INTEGER) değerini (0-27648) normalize edilmiş bir ondalıklı (REAL) değere (%MD102, AnalogYuzde) çevirir. Bu, sensörün tam aralığını 0.0-1.0 arasına sıkıştırmak için yapılır.

Ölçekleme: SCALE_X bloğu, normalize edilmiş değeri (%MD102) istenen bir aralığa (örneğin 0.0-100.0) ölçekler. Bu, sıcaklık, basınç veya seviye gibi fiziksel bir değerin yüzdesel karşılığını elde etmek için yaygın olarak kullanılır.

2. Tek Butonla Start/Stop Kontrolü
Bu senaryo, bir start/stop butonunun nasıl tek bir input ile kontrol edileceğini gösterir.

Set/Reset Mantığı: Program, %I0.0 (START-STOP) girişinin her pozitif kenar tetiklemesinde (P_TRIG), bir dahili hafıza biti olan %M50.0'ı toggle (açık/kapalı) eder.

Motor Kontrolü: %M50.0'ın durumuna bağlı olarak, %Q0.0 (MOTOR) çıkışı aktif veya pasif hale gelir. Bu, tek bir butona her basıldığında motorun durumunun değişmesini sağlar.

3. Tek Butonla Motoru Devreye Alma ve Durdurma
Bu senaryo, bir motoru farklı butonlarla kontrol etmek için SET_BF ve RESET_BF komutlarının kullanımını gösterir.

Motoru Devreye Alma: %I0.0 (START) butonu basıldığında, %Q0.0 (MOTOR) çıkışı SET_BF komutu ile aktif hale gelir. SET_BF komutu, çıkışı kalıcı olarak "1" (true) durumunda tutar.

Motoru Durdurma: %I0.1 (STOP) butonu basıldığında, aynı MOTOR çıkışı RESET_BF komutu ile pasif hale gelir. Bu, endüstriyel uygulamalarda en yaygın kullanılan motor kontrol mantıklarından biridir.

Ek olarak, bir başka görüntüde SR (Set-Reset) ve RS (Reset-Set) blokları kullanılarak da aynı mantığın nasıl oluşturulabileceği gösterilmiştir.

4. Motorların ve Pistonun Kontrolü
Bu senaryo, birden fazla motorun ve bir pistonun nasıl kontrol edileceğini gösterir.

Basit Lojik: Network 1 ve Network 2'de, %I0.0 ve %I0.1 giriş sinyallerine bağlı olarak %Q0.0, %Q0.1, %Q0.2 ve %Q0.3 çıkışları aktif veya pasif hale gelir. Bu, temel lojik kapıların kullanımını gösterir (AND, OR vb.).

Dahili Bitler: %M500.1 gibi dahili hafıza bitleri, programın bir ağındaki durumu tutmak ve başka bir ağdaki lojiği kontrol etmek için kullanılır.

SET/RESET Uygulaması: Diğer bir görüntüde, MOTOR-1 çıkışı için SET ve RESET_BF komutları kullanılarak kalıcı kontrol mantığı kurulur. %M500.4 adında bir dahili hafıza biti, Tag_3 değişkeni ile birlikte bu kontrol için kullanılır.
