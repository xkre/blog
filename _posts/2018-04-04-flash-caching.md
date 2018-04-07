---
layout: post
title:  "Analisis Prestasi HDD + Flash Caching"
date:   2018-04-04 1:18:11 +0800
categories: PC
---
[chart1]: /assets/pics/flash-caching/chart1.png "Peratusan peningkatan dalam masa membuka program-program"
[chart2]: /assets/pics/flash-caching/chart2.png "Peratusan peningkatan dalam masa membuka program-program"
[chart3]: /assets/pics/flash-caching/chart3.png "Peratusan peningkatan dalam masa membuka program-program"
[software]: https://www.romexsoftware.com/en-us/primo-cache/index.html

Caching merupakan salah satu langkah yang sering diambil untuk melajukan sesuatu sistem komputer. Terdapat banyak jenis caching dalam satu sistem komputer. Flash caching ialah satu proses dimana storan flash seperti SSD digunakan untuk melajukan HDD. Dalam sistem pengoperasian Windows, caching menggunakan flash drive sudah tersedia dengan fungsi _ReadyBoost_. Untuk lagi melajukan sistem, Windows juga menggunakan cache RAM. Proses ini dikenali sebagai _SuperFetch_.

Caching menggunakan flash storage untuk melancarkan sistem komputer yang menggunakan hard disk selalu disebut-sebut dalam perbincangan untuk melajukan komputer tanpa mengeluarkan wang yang banyak. Sebagai contoh, Apple dalam keluaran iMac menggunakan teknik ini yang dikenali sebagai __fusion drive__ untuk melancarkan prestasi sistem keluaran mereka, dimana HDD digunakan dengan SSD yang berperanan sebagai cache. Terdapat juga HDD di pasaran yang menggunakan teknik ini, dikenali segbagai Solid State Hybrid Drive, tetapi, harganya mahal jika mengambiil kira kapasiti SSD yang digunakan sebagai cache - yang biasanya dalam 8 GB sahaja.
  
Persoalannya, sebanyak mana penggunaan cache ini dapat meningkatkan prestasi sesuatu sistem? Untuk menjawab soalan tersebut, saya telah meguji kelajuan membuka program-program apabila menggunakan cache dan tanpa cache dengan menggunakan program [Primo Cache][software] bersama dengan USB drive. PrimoCache digunakan disebabkan kemampuannya untuk menghasilkan cache yang kekal. 

### Cache Menggunakan PrimoCache + USB Drive

Keputusannya adalah seperti berikut:
![Peratusan peningkatan dalam masa membuka program-program][chart1]
Merujuk carta di atas, peningkatan yang tertinggi ialah sebanyak 500%, dimana sistem sedia digunakan setelah di-boot. Peningkatan yang paling sedikit ialah Matlab, dimana program ini banyak menggunakan kitar CPU ketika dibuka. Dua program Universal Windows Platform (UWP): Groove music & Photos menunjukkan peningkatan sekitar 200%, dimana program-program tersebut direka untuk penggunaan SSD. 

Keseluruhan masa yang diambil adalah seperti dibawah:
![Peratusan peningkatan dalam masa membuka program-program][chart2]
Kelebihan perisian cache yang mempunyai cache kekal seperti Primo Cache adalah ianya dapat mempercepatkan proses boot. Hal ini disebabkan oleh caching module tersebut, yang juga merupakan kernel module, dimuatkan dalam proses boot. Kernel module (driver) adalah antara perkara yang paling awal dimuatkan dalam proses boot. Setelah driver untuk caching telah dimuatkan, ianya dapat mempercepatkan proses untuk memuatkan perkara-perkara yang berikutnya.

Sedia disini merujuk kepada masa yang diambil bagi HDD untuk memuatkan semua fail-fail yang diperlukan oleh sistem pengoperasion dan program-program ketika sistem dihidupkan. Masa yang dicatatkan disini merupakan masa di mana "Active Time" HDD surut dari 99% menjadi kurang dari 20%. Ketika fasa ini, komputer anda kebiasaanya slow.

Maklumat terperinci pembukaan program-program adalah seperti berikut:
![Peratusan peningkatan dalam masa membuka program-program][chart3]
Disini, program yang di-bottle-neck oleh kelajuan storan akan menunjukkan peningkatan yang tinggi, manakala program yang bergantung kepada pekakas lain seperti CPU menunjukkan peningkatan yang lebih sedikit.

Warm Startup pula merujuk kepada program yang dimulakan untuk kali kedua dalam satu sesi. Ianya lebih laju kerana sistem pengoperasian telah mengcachekan data-data mereka di dalam RAM. Cache ini kekal dalam RAM selagi mana RAM tersebut tidak diperlukan oleh program lain dan sistem tidak dimatikan.

### Perbandingan HDD, SSD and USB flash drive

Benchmark adalah seperti berikut:
1. HDD:  
![HDD](/assets/pics/flash-caching/benchmark-hdd.png)
2. USB Drive:  
![HDD](/assets/pics/flash-caching/benchmark-usb.png)
3. SSD SATA:  
![HDD](/assets/pics/flash-caching/benchmark-ssd.png)

### Mengapa Flash Caching Melajukan Komputer

Seperti dalam bechmark diatas, HDD adalah sangat perlahan apabila membaca fail secara rawak (4KB read, terutamanya Queue depth = 1 & Thread = 1 ; yang biasa digunakan oleh penggunaan PC yang biasa ketika membuka program). Bacaan rawak HDD adalah dalam kebiasaan 1 MB/s. Terdapat HDD yang lagi laju, iaitu HDD yang beroperasi pada 7200 RPM & 10000 RPM, namum peningkatannya adalah terlalu sedikit jika dibandingkan dengan SSD. Tambahan pula, HDD tersebut juga tidak digunakan di laptop kerana tidak mesra batteri. 

Selain itu, kelajuan HDD bergantung kepada posisi fail tersebut di dalam platter HDD. Posisi yang awal adalah laju, manakala posisi yang akir-akhir adalah perlahan. Untuk HDD 1TB desktop, kebiasaannya kelajuannya antara 150 MB/s sehingga 50 MB/s. Ini adalah disebabkan oleh kelajuan putaran piring yang sama (Constant Angular Velocity), dimana kelajuannya linearnya lain di kawasan piring yang tengah dengan yang luar.

Jika dibandingkan dengan USB drive, usb drive mempunyai random write yang lagi laju berbanding HDD. Tahap kelajuan ini adalah bergantung kepada kualiti drive tersebut. Kelajuan bacaan berturut USB drive juga kebiasaannya lebih konsisten berbanding HDD. Kelemahan USB drive ialah kelajuan menulisnya. Menulis fail di USB drive kebiasaanya laju untuk seketika, dan perlahan seterusnya.

Dengan caching, USB drive tersebut membantu HDD ketika membaca fail-fail secara rawak. Algoritma caching yang baik dapat membezakan fail-fail yang selalu dibaca secara rawak dan berterusan, dan dapat mengisi cache dengan fail yang selalu dibaca secara rawak. Apabila membaca fail tersebut, kelajuan HDD digabungkan dengan kelajuan USB drive.

#### Perkakasan yang digunakan

* Laptop Asus N55SF
    * Intel Core i7-2630QM (4 Core 2.0 GHZ - 2.9 GHz)
    * 8 GB RAM (1333 MT/s) dual-channel
* 500 GB 2.5" 5400 Toshiba RPM HDD (external)
* Widows 10 1709
* Sandisk CZ73 32GB USB 3
![Sandisk](/assets/pics/flash-caching/usb.png)

### Kesimpulan

Dengan menggunakan USB drive yang kurang dari RM 50, kelajuan PC yang menggunakan HDD dapat ditingkatkan.