# BeGuard

Yasadışı bahis SMS'lerini ayıklayan iOS mesaj filtresi.

Türkiye'de telefon numaraları sızıntılar yüzünden neredeyse her bahis sitesinin
listesinde. Sonuç: günde birkaç tane "çark çevir", "bonus", "nakit iade" mesajı.
Gönderici numarası her seferinde değiştiği için numara engellemek işe yaramıyor.
Değişmeyen şey **kelimeler**.

BeGuard mesajın metnine bakıyor: listedeki kelimelerden biri geçiyorsa mesaj
gelen kutusuna değil, Mesajlar'daki spam klasörüne düşüyor.

**App Store:** [BeGuard](https://apps.apple.com/tr/app/beguard/id6759072061) · ücretsiz · iOS 18.5+

## Nasıl çalışıyor

İki parça var:

| Parça | Ne yapar |
| --- | --- |
| **Uygulama** | Kelime listesini bu repodan indirir, kullanıcının kendi eklediği kelimelerle birleştirir, uzantıyla paylaşılan alana (`group.pharex.BeGuard`) yazar |
| **Mesaj filtresi uzantısı** | iOS'un `IdentityLookup` altyapısıyla gelen her SMS'i sorar; metinde listedeki bir kelime varsa spam olarak işaretler |

Uzantı ağa çıkmıyor, listeyi sadece paylaşılan alandan okuyor. Mesaj içeriği cihazdan
dışarı gönderilmiyor.

iOS bu filtreyi yalnızca **rehberde kayıtlı olmayan** göndericilere uygular — bankadan,
kargodan, tanıdıktan gelen mesaja dokunmaz.

## Neden liste bu repoda

Bahis mesajları kelime değiştiriyor. Listeyi uygulamanın içine gömseydim her yeni
kelime için App Store'a yeni sürüm göndermem ve incelemeyi beklemem gerekirdi.

Liste burada durunca kelime eklemek **tek commit**: uygulama listeyi buradan çektiği için
yeni sürüm gerekmiyor.

Canlı liste: [`filter`](filter)

```json
{
  "keywords": ["cark", "çark", "spin", "dede", "bahis", "nakit", "bonus", "bet", "casino"]
}
```

"cark" ve "çark" ikisi de listede — SMS'lerin bir kısmı Türkçe karakter kullanmadan geliyor.

## Kurulum

1. App Store'dan BeGuard'ı indir, bir kez aç (liste ilk açılışta iniyor)
2. **Ayarlar → Uygulamalar → Mesajlar → Bilinmeyen ve Spam → SMS Filtreleme → BeGuard**
3. İstersen uygulamadan kendi kelimelerini ekle

## Kelime önermek

Filtreye takılmayan bir bahis mesajı aldıysan, içindeki ayırt edici kelimeyle bir issue
aç ya da `filter` dosyasına PR at. Tek kural: gündelik mesajlarda da geçen kelime
eklenmez ("para", "kazan" gibi) — yanlış pozitif, kaçan spam'den daha kötü.
