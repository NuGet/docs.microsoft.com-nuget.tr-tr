Hataları `push` komutu, genellikle sorun gösterir. Örneğin, projenizdeki sürüm numarasını güncelleştirmek unutmuş olabilirsiniz ve bu nedenle zaten var olan bir paketi yayımlamaya çalışıyorsunuz.

Ayrıca konakta zaten var olan bir tanımlayıcı kullanılarak bir paketi yayımlamaya çalışırken hatalar görüyorsunuz. Örneğin, "AppLogger" adı zaten mevcut. Böyle bir durumda `push` komut şu hatayı verir:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Yeni oluşturduğunuz geçerli bir API anahtarı kullanıyorsanız, bu ileti hata "izni" bölümünden tamamen açık olmayan bir ad çakışması gösterir. Paket tanımlayıcısı değiştirmek için projeyi yeniden derleyin, yeniden `.nupkg` dosyasını açın ve yeniden deneme `push` komutu.