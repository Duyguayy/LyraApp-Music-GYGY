# LyraApp - Tipografi Sistemi

> Bu dosya LyraApp uygulamasının tipografi sistemi için
> **tek doğruluk kaynağıdır** (single source of truth) ve
> doğrudan bir **Android Jetpack Compose** projesinde kullanılmak
> üzere düzenlenmiştir.

---

## 1. Temel Kural

> Hiçbir `@Composable` içinde ham `TextStyle(fontSize = X.sp)` yazılmaz.
> Tipler daima `MaterialTheme.typography.<slot>` üzerinden
> okunmak zorundadır.

Ham `TextStyle(..)` tanımı yalnızca `Type.kt` içinde, sabit değişken tanımlanırken kullanılır.

---

## 2. Yazı Tipi Ailesi

| Slot         | Değer                  | Notlar                            |
|--------------|------------------------|-----------------------------------|
| FontFamily   | `FontFamily.Default`   | Sistem fontu (Roboto / sans-serif) |

> Özel bir font entegre edildiğinde bu tablo güncellenmelidir.

---

## 3. `Type.kt` — TextStyle Token Tanımları

```kotlin
package com.turkcell.lyraapp.ui.theme

import androidx.compose.material3.Typography
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.sp

val LyraTypography = Typography(

    // ── Display ──────────────────────────────────────────────────────────
    displayLarge = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Bold,
        fontSize = 57.sp,
        lineHeight = 64.sp,
        letterSpacing = (-0.25).sp,
    ),
    displayMedium = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Bold,
        fontSize = 45.sp,
        lineHeight = 52.sp,
        letterSpacing = 0.sp,
    ),
    displaySmall = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Normal,
        fontSize = 36.sp,
        lineHeight = 44.sp,
        letterSpacing = 0.sp,
    ),

    // ── Headline ─────────────────────────────────────────────────────────
    headlineLarge = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.SemiBold,
        fontSize = 32.sp,
        lineHeight = 40.sp,
        letterSpacing = 0.sp,
    ),
    headlineMedium = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.SemiBold,
        fontSize = 28.sp,
        lineHeight = 36.sp,
        letterSpacing = 0.sp,
    ),
    headlineSmall = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.SemiBold,
        fontSize = 24.sp,
        lineHeight = 32.sp,
        letterSpacing = 0.sp,
    ),

    // ── Title ─────────────────────────────────────────────────────────────
    // Kullanım: Playlist adı, ekran başlığı (ör. "Gece Sürüşü", "Profil")
    titleLarge = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.SemiBold,
        fontSize = 22.sp,
        lineHeight = 28.sp,
        letterSpacing = 0.sp,
    ),
    // Kullanım: Bölüm başlıkları (ör. "Şarkı ekle", "Görünüm")
    titleMedium = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Medium,
        fontSize = 16.sp,
        lineHeight = 24.sp,
        letterSpacing = 0.15.sp,
    ),
    // Kullanım: Liste öğesi başlığı (ör. şarkı adı: "Neon Sokaklar")
    titleSmall = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Medium,
        fontSize = 14.sp,
        lineHeight = 20.sp,
        letterSpacing = 0.1.sp,
    ),

    // ── Body ──────────────────────────────────────────────────────────────
    // Kullanım: Playlist açıklaması (ör. "Karanlık yıldız için synthpop")
    bodyLarge = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Normal,
        fontSize = 16.sp,
        lineHeight = 24.sp,
        letterSpacing = 0.5.sp,
    ),
    // Kullanım: Sanatçı adı, meta bilgi (ör. "Zeynep Kaya · 6 şarkı · 23 dk")
    bodyMedium = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Normal,
        fontSize = 14.sp,
        lineHeight = 20.sp,
        letterSpacing = 0.25.sp,
    ),
    // Kullanım: İkincil meta bilgi, toggle açıklaması (ör. "Profilinizde görünsün")
    bodySmall = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Normal,
        fontSize = 12.sp,
        lineHeight = 16.sp,
        letterSpacing = 0.4.sp,
    ),

    // ── Label ─────────────────────────────────────────────────────────────
    // Kullanım: Buton metni (ör. "Çal", "Kaydet"), BottomNav etiketi
    labelLarge = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Medium,
        fontSize = 14.sp,
        lineHeight = 20.sp,
        letterSpacing = 0.1.sp,
    ),
    // Kullanım: Süre bilgisi (ör. "3:43"), rozet metni
    labelMedium = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Medium,
        fontSize = 12.sp,
        lineHeight = 16.sp,
        letterSpacing = 0.5.sp,
    ),
    // Kullanım: İstatistik değerleri (ör. "1.2B Takipçi"), çok küçük etiketler
    labelSmall = TextStyle(
        fontFamily = FontFamily.Default,
        fontWeight = FontWeight.Medium,
        fontSize = 11.sp,
        lineHeight = 16.sp,
        letterSpacing = 0.5.sp,
    ),
)
```

---

## 4. `Theme.kt` İçinde Kullanım

`MaterialTheme` çağrısında `typography` parametresine `LyraTypography` atanmalıdır:

```kotlin
MaterialTheme(
    colorScheme = colorScheme,
    typography = LyraTypography,
    content = content,
)
```

> `Type.kt` içindeki mevcut `Typography` değişkeni `LyraTypography` olarak yeniden adlandırılmalıdır.
> `Theme.kt` içindeki referans da buna göre güncellenmelidir.

---

## 5. Slot Kullanım Rehberi (UI Referansı)

Aşağıdaki tablo, ekran tasarımından türetilmiş kullanım önerileri içermektedir.

| Ekran Bileşeni                        | Typography Slot   |
|---------------------------------------|-------------------|
| Playlist / ekran başlığı              | `titleLarge`      |
| Playlist açıklaması                   | `bodyMedium`      |
| Şarkı adı (liste öğesi)               | `titleSmall`      |
| Sanatçı adı (liste öğesi)             | `bodySmall`       |
| Şarkı süresi (ör. 3:43)               | `labelMedium`     |
| Bölüm başlığı (ör. "Şarkı ekle")      | `titleMedium`     |
| Buton metni (ör. "Çal", "Kaydet")     | `labelLarge`      |
| BottomNav etiketi                     | `labelMedium`     |
| Toggle açıklaması                     | `bodySmall`       |
| Profil kullanıcı adı                  | `titleMedium`     |
| Profil istatistikleri (sayı)          | `titleSmall`      |
| Profil istatistikleri (etiket)        | `labelSmall`      |
| Ayar satırı başlığı                   | `bodyLarge`       |
| Ayar satırı değeri (ör. "Yüksek")     | `bodyMedium`      |

---

## 6. Kurallar

1. `@Composable` içinde ham `TextStyle` veya `fontSize` kullanımı yasaktır.
2. Her metin bileşeni `MaterialTheme.typography.<slot>` üzerinden stil almalıdır.
3. Yeni bir tipografik ihtiyaç doğduğunda önce bu dosyaya eklenmeli, ardından `Type.kt` güncellenmeli ve onay alınmalıdır.
4. `FontWeight` değerleri yukarıdaki tabloda tanımlanan değerlerle sınırlıdır; keyfi ağırlık kullanımı yasaktır.