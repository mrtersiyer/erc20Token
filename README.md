# TokenPayToken!
İletişim, Destek ve diğer herşey için mrtersiyer@gmail.com
Son zamanlar uzun uzun bitcointalk.org u inceledim ve gördüğüm kadarı ile işi iyi bilen yazılımcı kitleri eksik kalmış. İşi bilen 3,5 kişi ise projelerini kendilerine saklıyorlar. Velakin ben buna çıkarak TokenPay adı altında oluşturduğum tokenin Ethereum Solidity kodlarını sizlerle paylaşmak istiyorum. Kodların açıklamalarını kurallarına uygun biçimde her fonksiyon ve değişkenin üzerine tanımladım.

# Detaylar
Bir ICO süreci için tüm detayları ile yönetmenizi sağlıyor. TGE kontratı Toplam arz, kurucu ekip ayrılan token, danışmanlara ayrılan token, ekibe ayrılan token, referans & bounty giderlerine ayrılan token, ön satışa ayrılan token ve ana satışa ayrılan tokeni ilgili adreslere dağıtıyor. TokenPayToken kontratı tokenin yakma ve kilidini açma gibi işlevleri sağlıyor. CrowdsalePre kontratı ön satışı gerçekleştiriyor (white list ve havuz yatırımları için adresleri kurucu tarafından set edebiliyorsunuz). CrowdsaleMain kontratı CrowdsalePre ile aynı işleri yapıyor tabi oranları farklı :). TokenVesting kontratı TGE dağıtımı yapılmadan önce imzalandığında verilen zaman dilimleri içerisinde kurucular danışmanlanlar v.s tokeni kilitli tutuyor. 

# Dosyalar

 1. TokenPayToken.sol  (Tokenin ana kontratı. Yani token diyebiliriz.)
 2. TokenPayTokenTGE.sol  (Tokeni adreslere dağıtacak kontrat. Yani Şöyle ki token imzalandıktan hemen sonra TGE kontratı oluşturulur. Tokenin arz miktrarı girilip TGE kontratına oluşturulan token transfer edilir. Bu işlemden sonra TGE kontratına crowedSale adresleri vesting te kalacak adresler girilir. ve token dağıtılır.)
 3. CrowdsaleMain.sol (Bu kontrat ana satışı gerçekleştirir. x-y süresi altında z fiyata sat gibi konfigurasyonları içerir. Satış bittikten sonra TokenPayToken dan burn yetkisi verileren kontrat üzerindeki tokenin süre bittikten sonra yanmasını otomatik olarak sağlaya bilirsiniz.)
 4. CrowdsalePre.sol  (Bu kontrat ön satışı gerçekleştirir. x-y süresi altında z fiyata sat gibi konfigurasyonları içerir. Satış bittikten sonra TokenPayToken dan burn yetkisi verileren kontrat üzerindeki tokenin süre bittikten sonra yanmasını otomatik olarak sağlaya bilirsiniz.)
 5. TokenVesting.sol (Bu kontrat ile danışmanlar & kurucular ve ekip üyeleri gibi tokenin zaman kilidinde kalması gerektiği hesapları tanımlaya bilirsiniz. Şöyle ki TGE kontratı ile dağıtım yapılmadan önce TokenVesting kontratı imzalanır. Owner tarafından ilgili adreslere kaç birim token gideceği ve zaman kilidinin timestamp olarak ne zaman açılacağı belirtilir. Zaman kilidi dolduktan sonra herhangi bir adresten tetikleme sağlandığında ilgili adreslere token dağıtımı yapılır.)

# Kurulum aşamaları
Aşağıdaki işlemlerin hepsi remix ide de yapılacaktır. https://remix.ethereum.org/
 1.  token derle
 2.  ön satış derle
 3.  ana satış derle
 4.  kilitler derle
 5.  TGE derle
 6.  TGE setUp funtion doldur
 7.  TOKEN distribute TGE adres gir
 8.  TGE distbrute et
 9.  TOKEN addWhitelistedBurn ekle ana satış
 10. TOKEN addWhitelistedBurn ekle ön satış
 11.  TOKEN addWhitelistedTransfer ekle ana satış
 12.  TOKEN addWhitelistedTransfer ekle ön satış
 13.  Ön satış owner transfer et
 14.   Ana satış owner transfer et
 
# Default tanımlar
 
```Token için default tanımlar...
+--------------+-------------------------------+
| Name         | TokenPay                      |
+--------------+-------------------------------+
| Symbol       | TKN                           |
+--------------+-------------------------------+
| Decimal      | 18                            |
+--------------+-------------------------------+
| Total Supply | 10.000.000,000000000000000000 |
+--------------+-------------------------------+

Anasatış 4. hafta fiyatı yani indirimsiz arz fiyatı
+---------------------+------------------------+
| 1 Ether / TKN %0	250.000000000000000000 tkn |
+---------------------+------------------------+

Satış tablosu örneği
+------------------+------------------------+----------------------------+----------------------------+
| Satış Türü       | İndirim Oranı          | 1 ETH Gidecek Token        | Fiyat                      |
+------------------+------------------------+----------------------------+----------------------------+
| PreSale 1. Week  | 60,000000000000000000% | 400,000000000000000000 tkn | 0,002500000000000000 ether |
+------------------+------------------------+----------------------------+----------------------------+
| PreSale 2. Week  | 60,000000000000000000% | 400,000000000000000000 tkn | 0,002500000000000000 ether |
+------------------+------------------------+----------------------------+----------------------------+
| PreSale 3. Week  | 60,000000000000000000% | 400,000000000000000000 tkn | 0,002500000000000000 ether |
+------------------+------------------------+----------------------------+----------------------------+
| PreSale 4. Week  | 60,000000000000000000% | 400,000000000000000000 tkn | 0,002500000000000000 ether |
+------------------+------------------------+----------------------------+----------------------------+
| MainSale 1. Week | 30,000000000000000000% | 325,000000000000000000 tkn | 0,003076923076923080 ether |
+------------------+------------------------+----------------------------+----------------------------+
| MainSale 2. Week | 20,000000000000000000% | 300,000000000000000000 tkn | 0,003333333333333330 ether |
+------------------+------------------------+----------------------------+----------------------------+
| MainSale 3. Week | 10,000000000000000000% | 275,000000000000000000 tkn | 0,003636363636363640 ether |
+------------------+------------------------+----------------------------+----------------------------+
| MainSale 4. Week | 0,000000000000000000%  | 250,000000000000000000 tkn | 0,004000000000000000 ether |
+------------------+------------------------+----------------------------+----------------------------+


| Name         | ARZ                        | %      | 18 Decimal                    |
|--------------|----------------------------|--------|-------------------------------|
| Total Supply | 10000000000000000000000000 | 100%   | 10.000.000,000000000000000000 |
| Founder Team | 1000000000000000000000000  | 10%    | 1.000.000,000000000000000000  |
| Counselors   | 400000000000000000000000   | 4%     | 400.000,000000000000000000    |
| Team         | 300000000000000000000000   | 3%     | 300.000,000000000000000000    |
| Reference    | 700000000000000000000000   | 7%     | 700.000,000000000000000000    |
| PreSale      | 1000000000000000000000000  | 10%    | 1.000.000,000000000000000000  |
| MailSale     | 6600000000000000000000000  | 66%    | 6.600.000,000000000000000000  |
| Total Supply | 10000000000000000000000000 | 100%   | 10.000.000,000000000000000000 |
```

Vesting Örneği
```plain
+------------------------------+--------------------------------------------+---------------------------+
| Start Time	1519221600	Çarşamba | 21 Şubat 2018 17:00:00 GMT+03:00	Wednesday  | 21 February 2018 14:00:00 |
+------------------------------+--------------------------------------------+---------------------------+
| Duration	15780000		182 days     | 15 hours                                   | 20 minutes and 0 seconds. |
+------------------------------+--------------------------------------------+---------------------------+
| Final	1535001600	Perşembe      | 23 Ağustos 2018 08:20:00 GMT+03:00	Thursday | 23 August 2018 05:20:00   |
+------------------------------+--------------------------------------------+---------------------------+
```
