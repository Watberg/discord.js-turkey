# Bot Yapımına Başlamak - Kısa Anlatım \(Linux\)

> **Bu Linux için kısa anlatımdır. **Eğer daha fazla açıklamaya ihtiyacınız olduğunu düşünüyorsanız lütfen [buradaki kılavuzu](/kodlamaya-baslarken/temel-bir-bot-yapimi.md) ziyaret edin.

## Uygulama Oluşturmak ve Bot Hesabı Açmak

* Discord sayfasına giderek [uygulama sayfası](https://discordapp.com/developers/applications/me)nı ziyaret edin.

* Bir isim verin ve bir uygulama oluşturun.

* **Create a bot account **butonuna tıklayın ve **Yes, do it. **tuşuna basın.

* [https://discordapp.com/oauth2/authorize?client\_id=APP\_ID&scope=bot](https://discordapp.com/oauth2/authorize?client_id=APP_ID&scope=bot) adresine giderek uygulama sayfasında verilen Application ID'yi linkin içine koyarak tıklayın. Ve botu sunucunuza davet edin. \(yada bunu yapması için sunucu sahibinize söyleyebilirsiniz.\)

* Sonrasında kullanabilmek için size verilen **Token**'ı bir yere not edin.

## Gerekli Yazılımlar

Paket menejerini kulanarak \(npm\) aşağıdakinileri yükleyin:

* nodejs \(versiyon 6.x yada daha yüksek gerekmektedir, [buradan](https://nodejs.org/en/download/package-manager/) bakabilirsiniz.\)

Kurulumunu bitirdikten sonra projeniz için bir dosya oluşturun ve dicord.js dosyalarını yükleyin:

* `mkdir mybot && cd mybot` `npm install discord.js`

**Ses desteği için **eklemeniz gereken `npm install opusscript` yada `npm install node-opus` \(çok daha iyi performansı var ancak `phyton 2.7.x` ve `build-essential` 'a ihtiyaç duyar.\) Bu iki seçenek de `ffmpeg` **gerektirir. **Bunun için de `sudo apt-get install ffmpeg`

## Örnek Kod

Aşağıdaki kod basitçe bir ping/pong etkileşimine giren bir bottur. Yazıyı `app.js` \(yada artık nasıl isterseniz\) kaydederek, aşağıdaki yere daha öncesinde almış olduğunuz **token**'ı yapıştırın.

```js
const Discord = require("discord.js");
const client = new Discord.Client();

client.on("ready", () => {
  console.log("Her şey hazır!");
});

client.on("message", (message) => {
  if (message.content.startsWith("zig")) {
    message.channel.send("zag!");
  }
});

client.login("AşırıGizliBotToken");
```

## Botu Çalıştırmak

Botunuzun olduğu klasorde terminal'e aşağıdaki komutu yazarak çalıştırabilirsiniz.

`node app.js`

Eğer hata görmediyseniz, botunuzun girmiş olduğu sunucu ya da sunucularda online olduğunu görebilirsiniz.

## Yardımcı Olabilecek Kaynaklar

* [Discord.js Dökümantasyonu](https://discord.js.org/#/docs/main/stable/general/welcome)
* [Resmi Discord.js Sunucusu](https://discord.gg/bRCvFy9)
* CodeBerry



