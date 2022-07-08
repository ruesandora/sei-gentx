# <h1 align="center"> Sei Network gentx dosyası alma, pull request ve form doldurma 3</h1> 

## Arkadaşlar öncelikle bu işlemleri mevcut sunucunuzda yani sei veya herhangi bir validatorün çalıştığı sunucuda yapamıyorsunuz maalesef boş sunucuya ihtiyacınız var.


# Öncelikle Sunucumuzu güncelliyoruz:
```
sudo apt update && sudo apt upgrade -y
```

# Kütüphaneleri yüklüyoruz:
```
sudo apt-get install make build-essential gcc git jq chrony -y
```

# Go kurulumu yapıyoruz
```
ver="1.18.2"
cd $HOME
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
source ~/.bash_profile
```

# Binary kurulumu yapıyoruz
```
cd $HOME
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.6beta
make install
```

# Uygulama konfigrasyonu
```
seid config chain-id  atlantic-1
seid config keyring-backend test
```

# İnitialize işlemi, altta bir kaç komut dahil rues yazan yeri kendi validator isminizi girin.
```
seid init rues --chain-id atlantic-1
```

# Eğer yoksa cüzdan oluşturuyoruz. (yeni dahil olduysanız)
```
seid keys add rues
```

# Daha önceden cüzdan oluşturduysak mnemonic'ler ile recover ediyoruz
```
seid keys add rues --recover
```

# Genesis'i ekliyoruz (burada cüzdan adresini giriyoruz wallet adres yazan yere, örn: sei565...)
```
seid add-genesis-account walletAddress 10000000usei
```

# Gentx dosyası oluşturuyoruz, değiştirilmesi gereken yerleri yazıyorum:

Wallet name kısmına wallet ismimizi, NODENAME kısmına kendi node ismimizi giriyoruz, your_validator_description kısmına validator açıklamamızı yazıyoruz, your_email kısmına iletişim bilgilerimizi yazıyoruz, your_website kısmına websitemizi yazıyoruz, websiteniz yoksa bizim forum'u yazabilirsiniz.

```
seid gentx Walletame 10000000usei \
--chain-id  atlantic-1\
--moniker=NODENAME \
--commission-max-change-rate=0.01 \
--commission-max-rate=0.20 \
--commission-rate=0.05 \
--details="your_validator_description" \
--security-contact="your_email" \
--website="your_website"
```

![image](https://user-images.githubusercontent.com/101149671/178025849-89c286cd-22e4-4740-b687-acbc897ed365.png)


# Gentx oluşturduktan sonra aşağıdaki gibi bir çıktı alıyoruz:

![image](https://user-images.githubusercontent.com/101149671/178025901-bf48ad66-7f1b-4967-813a-d8f2c153da49.png)

# Şimdi gentx'imizi kopyalamak için winscp'ye ihtiyacımız var.

WinSCP: https://winscp.net/eng/download.php

# İndirdikten sonra sol üstten yeni oturum diyip, sunucu bilgilerimizi buraya giriyoruz, Linux eğitimi-1'de, anlatmıştık kullanımını youtube'da var:

![image](https://user-images.githubusercontent.com/101149671/178026247-d2c0bf47-dd47-4e94-9334-e2122cde2e45.png)

# Confing dosyamızın içine giriyoruz. (confing gözükmüyorsa ctrl+alt+H butonu) ve gentx dosyamızı sol tarafta windows makinemize kopyalıyoruz/aktartıyoruz.

![image](https://user-images.githubusercontent.com/101149671/178026654-a2839240-4e41-4b15-bea7-62f8d4ff5191.png)

# Ardından bu siteye gidiyoruz: https://github.com/sei-protocol/testnet ve sağ üstten forklama işlemi yapıyoruz.

Forkalama işlemini yaptıktan sonra sağ üstten Profile tıklayıp, Your repository kısmına gelelim.

# Forkladığımız repoya tıklıyoruz ve sei-incentivized-testnet/gentx kısmına giriyoruz:

![image](https://user-images.githubusercontent.com/101149671/178027108-c75398be-457b-44fc-9c6b-dc7c7e5f9857.png)

![image](https://user-images.githubusercontent.com/101149671/178027280-90029866-7e8d-4be1-ad89-e07ee874b754.png)

# Daha sonra add file kısmından create new file diyelim:

![image](https://user-images.githubusercontent.com/101149671/178028736-26f639de-a223-4cf6-a0e3-9089caaf4350.png)

# Dosyanın ismi gentx-validatorisminiz.json formatında olacak (1. görsel) - gentx dosyasını ekleme (2. görsel)

![image](https://user-images.githubusercontent.com/101149671/178028347-7009c306-1943-4805-a00f-c2a8ab0279e0.png)

# Nereye kaydettiyseniz artık ordan alıp sürüklüyoruz github'a ve bunu sol alttan yeşil butonla kaydediyoruz.

![image](https://user-images.githubusercontent.com/101149671/178028592-d1d864b7-6217-456a-8bda-bb233874a986.png)

# Daha sonra sol üstten pull request diyip sağ taraftan yeşil butona basalım:

![image](https://user-images.githubusercontent.com/101149671/178029077-e3bb011c-55b0-4487-92da-573a102aa202.png)

# Create pull request diyoruz ve write kısmı açılıyor.

![image](https://user-images.githubusercontent.com/101149671/178029316-7d5d7249-124a-4339-b3eb-96357e98a2d9.png)

# Write kısmı için bu sefer gentx dosyamızı not defteri ile açıyoruz:

Not: Not defteri gözükmüyorsa başka bir uygulama seç butonuna tıklayıp not defterini seçin.

![image](https://user-images.githubusercontent.com/101149671/178029679-bc7e405d-cdea-45fe-8c91-423978d36092.png)

# Not defteri ile açtığımız dosyayı kopyalayıp yapıştırıyopruz ve pull oluştu:

Not isminizi buradan görebilirsiniz en üstlerde gözükür: https://github.com/sei-protocol/testnet/pulls

![image](https://user-images.githubusercontent.com/101149671/178030023-994cdc18-c6b1-4e71-8b43-094b29fb6b81.png)


# Son olarak formu doldurmanız gerekiyor, formun ilerleyen aşamalardaki soruların cevaplarını söylemem yasak kusura bakmayın:

Bir tüyo verebilirim sadece, en sonda ki memo sorusu gentx dosyasında bulunuyor: 

https://docs.google.com/forms/d/e/1FAIpQLSfFm2ATsspXI7Vv915TwoApbFICBjEwW1VXFvK8NyXxCsup_w/viewform?fbzx=-4206818241420982188

![image](https://user-images.githubusercontent.com/101149671/178037073-280a8a5e-d108-4c94-b4e4-2fc747a1fe83.png)


<h1 align="center"> Elimden geldiğince detaylı yazmya çalıştım, arkadaşlar formda 2. kısımda ki bilmediğiniz soruları kendiniz discordda araştırarak bence öğrenin, başka gruplara sorup sizi yanıltabilirler, herkes yapamayacak bunu ve arzın %1'i ödül çok yüksek bir ödül, ve az sayıda katılan olacak. 3</h1> 

Sei Network Türkiye: https://t.me/SeiNetworkTurkish

Sei Network discord: https://discord.gg/gxBxGGcv

# Hesaplar:

[<img src="https://cdn-icons-png.flaticon.com/512/733/733579.png" width="16px"> Twitter   ](https://twitter.com/Ruesandora0) 

[<img src="https://cdn-icons-png.flaticon.com/512/1336/1336494.png" width="16px"> Forum   ](https://forum.rues.info/index.php)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Announcement   ](https://t.me/RuesAnnouncement)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Chat   ](https://t.me/RuesChat)

[Discord](https://discord.gg/ruescommunity)




