# awk

AWK,  satır ve sütun bazlı metin işleme için kullanılan araçtır. Her satırı otomatik olarak işler ve satırdaki alanları (sütunları) $1, $2, …, $NF ile  kullanabilirz.

Satırdaki 1. sütunu yazdırmak için:
```
awk '{print $1}' access.log
```
 $1 -> 1. sütun, log dosyasında IP adresi genellikle 1. sütundadır

# Belirli bir koşula göre satırları filtreleme

 3. sütunu 200 olan satırların 1. sütununu yazdırma:
```
awk '$3 == "200" {print $1}' access.log
```
* $3 == "200" -> 3. sütun 200 ise satırı seçer
* {print $1} -> Seçilen satırın 1. sütununu yazdırır.


 # IP adreslerinin her birinin kaç istek yaptığını sayma
```
awk '{count[$1]++} END {for (ip in count) print ip, count[ip]}' access.log
```
* count[$1]++ -> Her IP için sayacı artırır.
* END {…} -> Dosya bittiğinde toplam sayıları yazdırma


 # Tüm satırı yazdırmak için:
```
awk '{print $0}' access.log
```
$0, Satırın tamamı 

Birden fazla sütunu birleştirip gösterme örneği IP -> URL:
```
awk '{print $1 " -> " $7}' access.log
```
$1 IP, $7  --> logdaki URL

# HTTP durum koduna göre toplam sayıyı hesaplama
```
awk '$9 == 200 {count++} END {print "200 OK toplam:", count}' access.log
```
* $9 : HTTP durum kodu sütunu
* count++ : Durum kodu 200 olan satırları sayar

# Değişken kullanarak belirli tarihe göre filtreleme yapma
```
awk -v day="21/Aug/2025" '$4 ~ day {print $0}' access.log
```
* -v day="21/Aug/2025", awk içine bir değişken geçirir
* $4 ~ day  4. sütunda day değerini içeren satırları seçer


# AWK 
* Satır ve sütun bazlı veri işleme,
* Filtreleme ve koşullu seçim,
* Sayma ve toplama işlemleri,
* Alan ayırıcı ile özel veri seçimi,
* Değişken kullanımı ile dinamik filtreleme yapabilriz
*  Bu, log analizi ve veri işleme işlerinde kullanışlıdır.
