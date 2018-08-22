# İlk Botunuz

Bu bölüm "Bot Yapımına Başlamak" kısımlarındaki anlatımları takip ederek buraya geldiğinizi varsayar. Eğer gördüğünüz kodlardan bir şey anlamıyorsanız, söylemek zorundayım ki belki de bir bot yapmak size göre değildir. Lütfen [w3schools](https://www.w3schools.com) ya da [CodeAcademy](https://www.codecademy.com/learn/javascript) sitelerine giderek JavaScript öğrenin.

Burada size bazı basit tekniklerle bot geliştirme mantığını sizlerle paylaşıyor olacağım. Bir önceki bölümde oluşturmuş olduğumuz örnekle devam edeceğiz:

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

## Events Nedir?

Başka bir şey yapmadan önce anlamanız gereken şeylerden bir tanesi `events` kısmıdır. Aşağıdaki kod ise bir event örneğidir:

```javascript
client.on('message', message => {
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

{% hint style="info" %}
Buradan sonra Discord.js'yi oluşturan ve başlatan kodları kaldırıp, kodun belirli kısımlarına yoğunlaşacağım.
{% endhint %}

```javascript
client.on('message', { content, channel } => {
  if (content.startsWith('zig')) return channel.send('zag!');
  if (content.startsWith('naber')) return channel.send('iyiyim!');
});
```

Yukarıdaki kodu kopyalayıp ilgili yere yapıştırarak, botunuzu yeniden başlatın. \(`node app.js`\) Aslında botunuzu yeniden başlatmanın çok daha pratik yöntemleri mevcut. Bu konulara dökümantasyonumuzun ilerleyen bölümlerinde değineceğim.

Şimdi botun olduğu sunucuya giredek, yeni komutumuz olan "naber"i deneyebilirsiniz. Bir yandan da hala "zig" yazdığımızda "zag!" cevabı alıyor olacaksınız.

## Prefix Kullanımı

Bir önek kullanılmazsa botun ne kadar çok şeye cevap vereceğini tahmin edebilirsiniz. Önek kullanmanın bu iki şeye gerçekten çok faydası vardır:

Bunların ilki, benzersiz bir önek kullanmazsanız sunucunuzda birden fazla bot varsa, hepsi birden mesajınıza yanıt vermek isteyecektir. İkincisi ise, yukarıdaki örnekte mesajımıza şu şekilde başlıyoruz "naber". Eğer şunu yazarsanız da bot size cevap verecektir: "naber ayşe bugün iyi misin?". Gördüğünüz gibi botumuz bu durumda size "iyiyim!" cevabını verdi. Oysa siz, bir başkasına söylemiştiniz.

Benzersiz bir prefix \(önek\) kullanırsak, bu iki büyük sorundan rahatça kurtulmuş olacağız. Hemen bir örnekle detaylandıralım.

```javascript
// Bir önek tanımlıyoruz.
const prefix = '!';

// Sonrasında bunu uyguluyoruz.
client.on('message', { content, channel } => {
  // Eğer mesaj önekle başlamıyorsa kodun geri kalanını durduruyoruz.
  if (!content.startsWith(prefix)) return;

  if (content.startsWith(prefix + 'zig')) return channel.send('zag!');
  if (content.startsWith(prefix + 'naber')) return channel.send('iyiyim!');
});
```

Yapmış olduğumuz değişiklik olduçka basitti. Hadi bunu biraz açıklayalım;

* `const prefix = '!';` önekin ne olduğunu tanımlar. Elbette bunu istediğiniz gibi değiştirebilirsiniz.
* Bu satır `if(!content.startsWith(prefix)) return;` kısaca şöyle okunabilir; "Eğer mesajın içeriği belirlenmiş olan önek ile başlamıyorsa, ne yapıyorsan durdur ve cevap verme." Bu kodunuzun geri kalanının çalışmasını engelleyerek daha duyarlı ve hızlı hale getirir.
* Artık bir komutunuz var. `startsWith(prefix + 'naber')` bu satırda önek ve yazıyı birleştirerek sadece `!naber` komutuna cevap vermesini sağladık.

{% hint style="warning" %}
Bir önek kullanmadığınızda RAM ve işlemci gücünü kalabalık sunucularda oldukça fazla harcanmasına neden olursunuz.
{% endhint %}

