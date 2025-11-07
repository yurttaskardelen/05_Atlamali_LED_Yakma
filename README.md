# 05_Atlamali_LED_Yakma_Uzun_Kod (v1)

Bu proje, **STM32F407-Discovery** kartı üzerinde 4 adet LED kullanarak 3 aşamalı, karmaşık bir animasyon senaryosu gerçekleştirir.

Bu deponun amacı, bu animasyonun **en temel ve açık** kodlama yöntemiyle nasıl yapılabileceğini göstermektir. Her komut, `HAL_GPIO_WritePin` ve `HAL_Delay` kullanılarak adım adım, tekrar edilerek yazılmıştır. Bu yaklaşım, kodun okunmasını kolaylaştırsa da uzun olmasına ve kod tekrarına (DRY prensibine aykırı) neden olur.

> **💡 Refactor Edilmiş Versiyon (Bitwise Operatörü)**
>
> Bu projenin, "Bitwise" operatörleri ve muhtemelen diziler/döngüler kullanılarak nasıl daha kısa, daha profesyonel ve verimli hale getirileceğini görmek için bir sonraki v2 deposunu inceleyebilirsiniz.
>
> ➡️ **[06_Atlamali_LED_Yakma_Bitwise_Operatoru](https://github.com/yurttaskardelen/06_Atlamali_LED_Yakma_Bitwise_Operatoru)**

---

### 🎯 Proje Senaryosu

Animasyon, 3 ana aşamadan oluşur ve `while(1)` içinde sürekli tekrar eder:

1.  **Aşama 1 (Sıralı Yanıp Sönme):**
    * Dört LED (`PA2`, `PA4`, `PA1`, `PA3`) sırayla 1'er saniye yanar ve bir sonrakine geçmeden önce söner.
2.  **Aşama 2 (İkili Yanıp Sönme):**
    * Önce `PA2` & `PA4` LED'leri birlikte 2 saniye yanar, sonra söner.
    * Ardından `PA1` & `PA3` LED'leri birlikte 2 saniye yanar, sonra söner.
3.  **Aşama 3 (Toplu Yanıp Sönme):**
    * Dört LED'in tümü (`PA1`, `PA2`, `PA3`, `PA4`) 4 saniye boyunca birlikte yanar.
    * Ardından tüm LED'ler 4 saniye boyunca sönük kalır.
4.  Döngü başa döner.

**Zamanlama:**
* **Sıralı Yanma (Aşama 1):** 1000 ms (1 saniye)
* **İkili Yanma (Aşama 2):** 2000 ms (2 saniye)
* **Toplu Yanma (Aşama 3):** 4000 ms (4 saniye)
* **Toplu Sönme (Aşama 3):** 4000 ms (4 saniye)

---

### 🛠️ Gerekli Donanım

* **1x** STM32F407-Discovery Geliştirme Kartı
* **4x** Tercih edilen renklerde LED
* **4x** 220 ya da 330 Ohm Direnç (LED'ler için ön direnç)
* Breadboard ve Jumper kablolar

---

### 🔌 Devre Şeması

LED'lerin anot (uzun) bacakları STM32 pinlerine, katot (kısa) bacakları ise direnç üzerinden GND hattına bağlanmalıdır.

| LED (Senaryo Sırası) | Direnç | STM32 Pini |
| :--- | :--- | :--- |
| LED 1 | 220 Ohm | `PA2` |
| LED 2 | 220 Ohm | `PA5` |
| LED 3 | 220 Ohm | `PA1` |
| LED 4 | 220 Ohm | `PA3` |
| (Tümü) | - | `GND` |

<img width="473" height="404" alt="Pin_Baglantilari" src="https://github.com/user-attachments/assets/d8d9caf0-01a1-43e4-945a-ec924c2ab757" />


### Kod Bloğu

<img width="836" height="844" alt="image" src="https://github.com/user-attachments/assets/83c8f1a9-c0b0-45eb-9f88-846d2281de65" />

---

### 🚀 Nasıl Kullanılır?

1.  Bu depoyu klonlayın (`git clone ...`).
2.  STM32CubeIDE yazılımını açın.
3.  `File > Open Projects from File System...` seçeneği ile proje klasörünü seçin.
4.  Proje içindeki `.ioc` dosyasını açarak pin yapılandırmasını inceleyebilirsiniz.
5.  Derleyin (Build) ve ST-Link V2 üzerinden kartınıza yükleyin (Run).
