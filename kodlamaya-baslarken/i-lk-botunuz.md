# İlk Botunuz

Bu bölüm "Bot Yapımına Başlamak" kısımlarındaki anlatımları takip ederek buraya geldiğinizi varsayar. Eğer gördüğünüz kodlardan bir şey anlamıyorsanız, söylemek zorundayım ki belki de bir bot yapmak size göre değildir. Lütfen [w3schools](https://www.w3schools.com) ya da [CodeAcademy](https://www.codecademy.com/learn/javascript) sitelerine giderek JavaScript öğrenin.

Burada size bazı basit tekniklerle bot geliştirme mantığını sizlerle paylaşıyor olacağım. Bir önceki bölümde oluşturmuş olduğumuz örnekle devam edeceğiz:

```javascript
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

## Events Nedir?

Başka bir şey yapmadan önce anlamanız gereken şeylerden bir tanesi `events` kısmıdır. Aşağıdaki kod ise bir event örneğidir:

```javascript
client.on("message", (message) => {
// Buradaki kod message event'ı tetiklendiğinde çalışır.
});
```

Bu örnek bize discord.js'nin event ile API'yi nasıl kullandığının basitçe göstermektedir. Bu event her mesaj atıldığında tetiklenir. Bu botun girmiş olduğu tüm sunucuları, erişiminin olduğu tum kanalları ve hatta özel mesajları kapsar. Eğer bir kanala 10 mesaj atılırsa, yukarıdaki event 10 kez tetiklenmiş olur.

Peki bunu bilmeniz neden önemli? Eğer botunuzu büyük bir sunucuda kullanmayı düşünüyorsanız ya da birden fazla sunucuda olacaksa, bu, her an tetiklenen bir event olur. Discord.js belirli durumlarda her an tetiklenebilecek bir çok event barındırır. Bunlardan bazıları:

`ready` : Bot her çevrimiçi olduğunda tetiklenir.

`guildMemberAdd` : Sunucunuza gelen her yeni kullanıcıda tetiklenir.

Bu event'ların tam listesini görmek istiyorsanız [buradaki sayfa](https://discord.js.org/#/docs/main/stable/class/Client?scrollTo=channelCreate)yı ziyaret edebilirsiniz.

## İkinci Komutu Eklemek

Öğrenmek isteyeceğiniz en mantıklı şeylerden biri de, botunuz için ikinci bir komutu nasıl ekleyeceğinizdir. Bu vermiş olacağım örnekten çok daha iyileri mevcut olsa da, şimdilik senin işini görecektir.

> Bundan sonra kodun belirli yerlerini ele alarak açıklama yapacağım.

```javascript
client.on("message", (message) => {
  if (message.content.startsWith("zig")) {
    message.channel.send("zag!");
  } else

  if (message.content.startsWith("naber")) {
    message.channel.send("iyiyim!");
  }
});
```

Yukarıdaki kodu kopyalayıp ilgili yere yapıştırarak, botunuzu yeniden başlatın. \(`node app.js`\) Aslında botunuzu yeniden başlatmanın çok daha pratik yöntemleri mevcut. Bu konulara dökümantasyonumuzun ilerleyen bölümlerinde değineceğim.

Şimdi botun olduğu sunucuya giredek, yeni komutumuz olan "naber"i deneyebilirsiniz. Bir yandan da hala "zig" yazdığımızda "zag!" cevabı alıyor olacaksınız.

## Prefix Kullanımı

Bir önek kullanılmazsa botun ne kadar çok şeye cevap vereceğini tahmin edebilirsiniz. Önek kullanmanın bu iki şeye gerçekten çok faydası vardır:

Bunların ilki, benzersiz bir önek kullanmazsanız sunucunuzda birden fazla bot varsa, hepsi birden mesajınıza yanıt vermek isteyecektir. İkincisi ise, yukarıdaki örnekte mesajımıza şu şekilde başlıyoruz "naber". Eğer şunu yazarsanız da bot size cevap verecektir: "naber ayşe bugün iyi misin?". Gördüğünüz gibi botumuz bu durumda size "iyiyim!" cevabını verdi. Oysa siz, bir başkasına söylemiştiniz.

Benzersiz bir prefix \(önek\) kullanırsak, bu iki büyük sorundan rahatça kurtulmuş olacağız.

