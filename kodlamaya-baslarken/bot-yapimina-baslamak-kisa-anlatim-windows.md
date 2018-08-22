# Bot Yapımına Başlamak - Kısa Anlatım \(Windows\)

> **Bu Windows için kısa anlatımdır.** Eğer daha fazla açıklamaya ihtiyacınız olduğunu düşünüyorsanız lütfen [buradaki kılavuzu](temel-bir-bot-yapimi.md) ziyaret edin.

## Uygulama Oluşturmak ve Bot Hesabı Açmak

* Discord sayfasına giderek [uygulama sayfası](https://discordapp.com/developers/applications/me)nı ziyaret edin.
* Bir isim verin ve bir uygulama oluşturun.
* **Create a bot account** butonuna tıklayın ve **Yes, do it.** tuşuna basın.
* [https://discordapp.com/oauth2/authorize?client\_id=APP\_ID&scope=bot](https://discordapp.com/oauth2/authorize?client_id=APP_ID&scope=bot) adresine giderek uygulama sayfasında verilen Application ID'yi linkin içine koyarak tıklayın. Ve botu sunucunuza davet edin. \(yada bunu yapması için sunucu sahibinize söyleyebilirsiniz.\)
* Sonrasında kullanabilmek için size verilen **Token**'ı bir yere not edin.

## Gerekli Yazılımlar

Windows için aşağıdaki yazılımları yüklemeniz gerekmektedir:

* nodejs \(versiyon 6.x yada daha yüksek gerekmektedir, [buradan](https://nodejs.org/en/download/package-manager/) bakabilirsiniz.\)

Eğer ses desteği istiyorsanız 2 şeye daha ihtiyacınız olacak:

* ffmpeg'i [bu sayfadan](http://adaptivesamples.com/how-to-install-ffmpeg-on-windows/) indirebilrsiniz.
* Yeni Windows araçları:
  * Komut İstemcisini ya da PowerShell'i ADMİN olarak açın.
  * Sonrasında şu komutu çalıştırın: `npm i -g --production windows-build-tools`
  * Bu işlem Python 2.7 ve C++ yapı araçlarını yükleyecektir.

İşlemler bittikten sonra proje dosyasını oluşturun ve discord.js'yi yükleyin:

`md bot` `cd bot` `npm install discord.js`

## Örnek Kod

Aşağıdaki kod basitçe bir ping/pong etkileşimine giren bir bottur. Yazıyı `app.js` \(yada artık nasıl isterseniz\) kaydederek, aşağıdaki yere daha öncesinde almış olduğunuz **token**'ı yapıştırın.

```javascript
const { Client } = require('discord.js');
const client = new Client();

client.on('ready', () => {
  console.log('Her şey hazır!');
});

client.on('message', { content, channel } => {
  if (content.startsWith('zig')) {
    channel.send('zag!');
  }
});

client.login('AşırıGizliBotToken');
```

## Botu Çalıştırmak

Botunuzun olduğu klasorde terminal'e aşağıdaki komutu yazarak çalıştırabilirsiniz.

`node app.js`

Eğer hata görmediyseniz, botunuzun girmiş olduğu sunucu ya da sunucularda online olduğunu görebilirsiniz.

## Yardımcı Olabilecek Kaynaklar

* [Discord.js Dökümantasyonu](https://discord.js.org/#/docs/main/stable/general/welcome)
* [Resmi Discord.js Sunucusu](https://discord.gg/bRCvFy9)
* CodeBerry

