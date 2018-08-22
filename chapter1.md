# Sık Sorulan Sorular

Burada bazı çok temel sık sorulan sorulara yanıt veriyor olacağım. Ancak bu örneklerin sadece kopyala-yapıştır usulü ile yaptığınız bota eklemenizin size bir faydasının olmayacağını belirtmek isterim. Lütfen burada yazılan satırları anlamaya çalışın ve körü körüne kodlarınıza eklemeyin.

## Kod Örnekleri

### Bot Durumu

```javascript
// Botun aktivite durumunu ayarlamak için. (Bir event içinde olmalıdır.)

client.on('ready', () => {
    client.user.setActivity('Benimle', { type: 'WATCHING' });
});
```

```javascript
// Botun çevrimiçi/çevirimdışı/rahatsız etme ve boşta durumu için. (online/dnd/invisible/idle)

client.on('ready', () => {
    client.user.setStatus('online');
});
```

```javascript
// Hem aktivite hem de statüsünü değiştirmek için.

client.user.setPresence({ activity: { name: 'benimle', type: 'PLAYING' }, status: 'dnd' });
```

### Users ve Members

```javascript
// ID ile bir kullanıcı çağırmak için.

client.users.get('Kullanıcı ID\'si');

// <User> olarak döner.
```

```javascript
// ID ile bir üye çağırmak için.

message.guild.members.get('Kullanıcı ID\'si');

// <Member> olarak döner.
```

```javascript
// Bir mesaja mention edilmiş ilk kullanıcıyı çağırmak için.

message.mentions.members.first();

// <Member> olarak döner.
```

```javascript
// Bir kullanıcıya özel mesaj atmak için.

message.author.send("Naber?");
```

```javascript
// Mesajda bir kullanıcıyı mention etmek için.

message.channel.send(`Merhaba ${user}, hoşgeldin!`);

// ya da

message.channel.send('Merhaba ' + message.author.toString() + ', hoşgeldin!');
```

### Channels ve Guilds

```javascript
// ID'ye göre sunucu çağırma.

client.guilds.get('Sunucu ID\'si');

// message.guild olarak döner.
```

```javascript
// ID'ye göre kanal çağırma

client.channels.get('Kanal ID\'si');

// message.channel olarak döner.
```

```javascript
// İsme göre bir kanal çağırma. (not: BU METOD ÖNERİLMEZ -bir taneden daha 
// fazla aynı ada sahip kanalınız varsa ya da bu kanalların isimleri sonra değiştirilirse, sorun yaratabilir!)

message.guild.channels.find('name', 'kanal adı');

// message.channel olarak döner.
```

## Genel Hatalar ve Düzeltmeler

### Can not find module `discord.js`

#### Sorun:

Ya Discord.js'yi yüklemediniz ya da yanlış klasöre yüklediniz.

#### Çözüm:

* Bot dosyalarınız neredeyse, discord.js'yi de o klasörün içine indirmiş ya da koymuş olduğunuzdan **emin** olun.
* Bot klasörünün içinde SHIFT+Sağ-Tık yaparak **Komut penceresini burada aç** diyin.
* `npm init -y` komutunu çalıştırın ve enter'a basarak tamamlayın.
* `npm i -S discord.js` komutu ile Discord'u tekrar yükleyin.

### Unexpected End of Input Hatası

#### Sorun:

```text
});

  ^

SyntaxError: Unexpected end of input
```

#### Çözüm:

Anlaşılan kodunuz bir yerde hata veriyor. Bunu kodlarınızı incelemeden hatanın nerede olduğunu anlamak neredeyse _imkansız_. \(Genel olarak bu tarz hatalar yazım yanlışlarından dolayı olur ve kodların sonlarında gerçekleşir\).

Bu kısım gerçekten hayatınızı kurtarabilir. Bu yüzden dikkatinizi verin. Kod editörleri sizlere yardımcı olmaya çalışır. Hangi editör'ü kullanıyorsanız \(Notepad++ kullanmayın o hariç!\), size hatanın nerede olabileceği ile ilgili bilgiler vermeye çalışır. Köşeli parantezler, parantezler ve kıvrımlı parantezlerin üzerine tıkladığınızda nerede açılıp nerede kapandığına dair bilgiler verir. Bu tarz hataları bunu gösteren editörler ile yapmanız çok daha iyi olacaktır. Zaman bizim için çok önemli!

Bir bot kodlamaya başlamadan önce ya da botunuzu çalıştırmaya başlamadan önce [Bir Editör Yüklemek ve Kullanmak](kodlamaya-baslarken/bir-editor-yuklemek-ve-kullanmak.md) isimli yazıma bakmanızı tavsiye ederim.

