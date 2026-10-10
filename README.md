# VPN Manager

Windows, macOS ve Linux için OpenVPN masaüstü istemcisi. Bu depo kurulum dosyalarını ve otomatik güncellemeleri tutar. Kaynak kodu burada değildir.

Güncel sürüm **1.0.4**.

| Sistem | Dosya |
| --- | --- |
| Windows 64 bit | [VPNManager-1.0.4-win-x64-Setup.exe](https://github.com/omeruygun/omura-vpn-manager-releases/releases/download/v1.0.4/VPNManager-1.0.4-win-x64-Setup.exe) |
| macOS Apple silicon | [VPNManager-1.0.4-osx-arm64.pkg](https://github.com/omeruygun/omura-vpn-manager-releases/releases/download/v1.0.4/VPNManager-1.0.4-osx-arm64.pkg) |
| Linux 64 bit | [VPNManager-1.0.4-linux-x64.AppImage](https://github.com/omeruygun/omura-vpn-manager-releases/releases/download/v1.0.4/VPNManager-1.0.4-linux-x64.AppImage) |

Tüm dosyalar [Releases](https://github.com/omeruygun/omura-vpn-manager-releases/releases/tag/v1.0.4) sayfasındadır. Paketler imzasızdır. OpenVPN bu pakete konmaz.

## Kurulum

### Windows

1. `VPNManager-1.0.4-win-x64-Setup.exe` dosyasını indirin.
2. SmartScreen uyarırsa **Daha fazla bilgi** ve ardından **Yine de çalıştır** deyin. Paket imzasız olduğu için bu uyarı beklenir.
3. Kurulumu bitirin. Masaüstüne ve Başlat menüsüne **VPN Manager** kısayolu gelir.
4. Kısayoldan açın. Pencerenin kendisi yönetici olarak çalışmaz.

Pencere açılmazsa Görev Yöneticisi'nde kalan `VPNManager` sürecini sonlandırıp yeniden açın. Açılış satırları `%LOCALAPPDATA%\VPNManager\logs\startup.log` dosyasındadır.

### macOS

1. `VPNManager-1.0.4-osx-arm64.pkg` dosyasını indirin. Bu paket Apple silicon içindir.
2. Paketi açın. Gatekeeper engellerse Sistem Ayarları > Gizlilik ve Güvenlik bölümünden açılmasına izin verin.
3. Kurulum bitince VPN Manager'ı açın.

### Linux

1. `VPNManager-1.0.4-linux-x64.AppImage` dosyasını indirin.
2. Çalıştırma izni verin: `chmod +x VPNManager-1.0.4-linux-x64.AppImage`
3. Gerçek tünel için uygulamayı root olarak açın. Root değilse bağlantı kurulmuş gibi gösterilmez.

## OpenVPN

VPN Manager tüneli kendisi kurmaz. Community OpenVPN sürecini başlatır.

OpenVPN yoksa durum çubuğunda **OpenVPN kur** görünür. Onaylarsanız:

- Windows'ta `winget` ile `OpenVPNTechnologies.OpenVPN` kurulur.
- macOS ve Linux'ta Homebrew ile `openvpn` kurulur.

Paket yöneticisi yoksa kurulum başlamaz. Bilgisayarda zaten bir `openvpn` varsa üzerine yazılmaz. Sessiz indirme yoktur.

OpenVPN'i kendiniz de kurabilirsiniz. Yolunu sol alttaki **Ayarlar** ekranından seçin. Windows'ta dosya adı `openvpn.exe`, macOS ve Linux'ta `openvpn` olmalıdır.

Bağlanırken Windows ve macOS yalnızca OpenVPN sürecine izin sorar. Bu, VPN parolası değildir. Linux'ta uygulamanın root olması gerekir.

## Kullanım

Aynı anda tek bağlantı vardır. Çok profil tutulabilir. Listeden başka bir profil seçmek açık tüneli kesmez.

### Profil eklemek

Sol üstteki artı, boş bir profil açar. İndirme simgesi bir veya birden çok `.ovpn` dosyası alır. Klasör simgesi bir klasörün içindeki profilleri alır.

Profilde kullanıcı adı ve parola istenebilir. Parola profil dosyasına yazılmaz. OTP kullanıyorsanız **QR yükle** ile kodu bir kez ekleyin; bağlanırken kod üretilir. Kayıtlı OTP, **QR'ı göster**, **QR değiştir** ve **Sil** ile yönetilir.

Statik ek doğrulama isteyen profiller bağlanmadan reddedilir.

### Bağlanmak

1. Listeden profili seçin.
2. İsteniyorsa kullanıcı adını, parolayı ve OTP kodunu yazın.
3. **Bağlan** deyin.
4. Sistem OpenVPN için izin isterse onaylayın.
5. Durum **Bağlantı aktif** olunca süre, VPN adresi, sunucu ve trafik görünür.

**Bağlı** yazısı, motor `CONNECTED` ve `SUCCESS` bildirince gelir. Motor yokken veya izin verilmezken bağlı gösterilmez.

Kesmek için **Bağlantıyı kes** deyin. Başka bir profile bağlanmak, açık tüneli kesmek için ayrıca onay ister.

Hata olursa kart **Bağlantı kurulamadı** der ve düğme **Tekrar dene** olur.

### Profil işlemleri

Profil satırındaki veya karttaki menüden düzenleyebilir, yeniden adlandırabilir, çoğaltabilir, dışa aktarabilir veya silebilirsiniz. Dışa aktarılan zip içinde `.ovpn` vardır. OTP için QR kayıtlıysa görseli de konur. Kayıtlı parola zip'e girmez.

**Profil ayarları** sekmesinde **Açılışta bağlan** ve **Bağlantı koparsa yeniden dene** vardır. Yeniden deneme 2, 5, 10 ve 30 saniye aralıklarıyla yapılır, sonra durur. Siz keserseniz, iptal ederseniz veya parola yanlışsa yeniden denenmez.

### Günlük ve istatistik

**Bağlantı günlükleri** sekmesi motor satırlarını gösterir. Arama, otomatik kaydırma ve dışa aktarma vardır. **Görünümü temizle** ekranı boşaltır; kayıt dosyasını silmez. Günlüğe parola, sertifika, anahtar ve kimlik komutu yazılmaz.

Sol alttaki **İstatistik**, tamamlanmış bağlantı sürelerini açar. Oturum, bağlantı kurulduktan sonra sayılır.

## Ayarlar

Sol alttaki **Ayarlar**:

- OpenVPN dosyasının yolu
- Başlangıçta tepsiye küçültme
- Kapatınca tepside kalma
- Windows açılışında başlatma. Bu seçenek yalnızca Windows'ta açıktır.
- Yeniden bağlanma gecikmeleri, saniye olarak ve virgülle

Güncelleme anahtarı gerekmez. Sürümler bu herkese açık depodan okunur.

## Güncelleme

1.0.4 ve sonraki kurulu kopyalar açılışta bu depoya bakar. Yeni sürüm varsa **Güncelle** veya **Sonra** diye sorar. Güncelle derseniz paket iner, açık tünel kapanır ve uygulama yeniden başlar.

1.0.3 ve daha eski kurulumlar bu depoyu bilmez. Onlar için 1.0.4'ü bu sayfadan bir kez elle kurun. Sonraki sürümler açılışta sorulur.

## Veriler

Profiller, ayarlar ve günlükler şu klasördedir:

- Windows: `%LOCALAPPDATA%\VPNManager`
- macOS: `~/Library/Application Support/VPNManager`
- Linux: `~/.local/share/VPNManager`

Parolalar JSON dosyasında durmaz. Windows'ta DPAPI ile, macOS ve Linux'ta yalnızca sizin okuyabildiğiniz bir dosyada saklanır.
