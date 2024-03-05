# Managing Resources

## Managing Disk Space

```
$ sudo lsof | grep deleted
```

<br>
<br>

Bu durumda, kayıtları daha sık döndüren araçların yapılandırmasını inceleyerek sadece ihtiyacınız olanı sakladığınızdan emin olmak isteyebilirsiniz. Başka durumlarda, disk büyük geçici dosyalar oluşturan ve ardından bunları temizleyemeyen bir program nedeniyle dolabilir. Örneğin, bir uygulama temiz bir şekilde kapanırken geçici dosyaları temizleyebilir, ancak çökerse geride bırakabilir. Veya basitçe geçici dosyalar oluşturur ve bunları asla temizlemez. Bu tür bir durumda, programı düzeltmek ve dosyaları doğru bir şekilde silmek için ideal olarak bir bakım süreciniz olacaktır. Ancak bu mümkün değilse, bunlardan kurtulacak kendi betiğinizi yazmanız gerekebilir. Debug etmesi zor olabilecek bir durum, alanı alan ancak silinmiş dosyaların alındığı durumlardır. Silinmiş dosyalar nasıl yer kaplayabilir, diye düşünüyor olabilirsiniz. Harika bir soru. Bir program bir dosyayı açtığında, OS, bu dosyayı silinmiş olarak işaretlenmiş olsa bile, programa dosyayı okuma ve yazma izni verir. Bu nedenle, birçok program, geçici dosyaları oluşturduktan hemen sonra bunları temizlemek için dosyayı siler. Bu şekilde, işlem, dosya açıkken dosyadan okuma ve yazma yapabilir. Ardından işlem tamamlandığında, dosya kapatılır ve gerçekten silinir. Bu sistem geniş bir şekilde kullanılır ve çoğu işlem için sorunsuz çalışır. Ancak bazı nedenlerden dolayı, bu geçici olarak silinen dosya aniden çok büyük hale gelirse, tüm kullanılabilir disk alanını kaplamaya neden olabilir. Bu durumda, verilerin çoğu nereye gittiğini anlamak için kafa karıştırıcı olabilir, çünkü bu silinmiş dosyaları görmeyiz. Belirli bir durumu kontrol etmek için, şu anda açık olan dosyaları listelememiz ve silindiğini bildiğimiz dosyaları aramamız gerekir.

![Ekran görüntüsü 2024-02-07 111130](https://github.com/kemda2/Google-Courses/assets/19648132/d9ffbe84-546a-4674-9850-9cd4e04edcfc)

<br>
<br>

## Dealing with Memory Leaks

```
$ uxterm &
[1] 16086 


$ od -cx /dev/urandom # Bir sürü sayı akmaya başladı.


$ top
```

```
$ cd contents_stats/


contents_stats$ ./contents_stats.py


contents_stats$ atom contents_stats_simple.py # Ram kullanımını gösteren memory profiler'ın aktif versiyonu.


contents_stats$ ./contents_stats_simple.py
```