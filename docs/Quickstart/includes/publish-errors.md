Hataları `push` komut genellikle sorun olduğunu gösteriyor. Örneğin, projenizdeki sürüm numarasını güncelleştirmek unutmuş ve bu nedenle zaten mevcut bir paketi yayımlamaya çalışırken.

Konakta zaten mevcut bir tanımlayıcı kullanılarak bir paketi yayımlamaya çalışırken de hatalarına bakın. Örneğin, "AppLogger" adı zaten mevcut. Böyle bir durumda `push` komut şu hata verir:

```output
Response status code does not indicate success: 403 (The specified API key is invalid, has expired, or does not have permission to access the specified package.).
```

Yeni oluşturduğunuz geçerli bir API anahtarı kullanıyorsanız, bu ileti hata "izni" bölümünden tamamen NET değildir bir ad çakışması gösterir. Paket tanımlayıcısı değiştirmek, projeyi oluşturmak, yeniden `.nupkg` dosya ve yeniden deneme `push` komutu.