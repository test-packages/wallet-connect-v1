<div align="center">
<img src="https://github.com/Orange-Wallet/orangewallet-utils/raw/master/assets/images/walletconnect.png" alt="Wallet Connect Logo" width="70"/>
<h1>Wallet Connect</h1>
</div>


# Wallet Connect

[![İngilizce](https://img.shields.io/badge/Dil-Ingilizce-blue?style=for-the-badge)](README.md)    [![Türkçe](https://img.shields.io/badge/Dil-Turkce-red?style=for-the-badge)](README-TR.md)  ![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white)

* [Wallet Connect Hakkında](#wallet-connect-hakkında)
* [Önkoşullar](#önkoşullar)
* [Yükleme](#yükleme)
* [Kullanımı](#kullanımı)
### Wallet Connect Hakkında
Wallet Connect, cüzdanınızın DApp’ler ve diğer cüzdanlarla bağlantı kurmasını ve bunlarla etkileşim kurmasını sağlayan açık kaynaklı bir protokoldür . Wallet Connect, QR kodunu tarayarak veya bir bağlantı yardımıyla cüzdanınız ve DApp arasında şifreli bir bağlantı kurar. Protokol ayrıca kullanıcıları gelen işlemlerden haberdar etmek için anlık bildirim özelliklerine sahiptir. WalletConnect’i Trust Wallet ve MetaMask gibi Android veya iOS mobil cüzdanlarında görmüş olabilirsiniz . Wallet Connect’i destekleyen kripto para cüzdan uygulamalarının bir listesini bu [adresten](https://explorer.walletconnect.com/) ulaşabilirsiniz.
### Önkoşullar
[Flutter SDK](https://docs.flutter.dev/get-started/install) , [IDE](https://blog.logrocket.com/best-ides-flutter-2022/) ve [Xcode](https://developer.apple.com/xcode/) yüklü olmalıdır.

### Yükleme
Wallet connect paketini projeye eklemek için, pubspec.yaml dosyasına aşağıdaki satırları ekleyin:
``` YAML
  wallet_connect:
    git:
      url: https://github.com/test-packages/wallet-connect-dart
```
### Kullanımı
Wallet connect paketini aşağıdaki adımları uygulayarak dapp bağlantıları oluşturabilirsiniz.

1. Projeye import edilmesi

```dart
    import 'package:wallet_connect/wallet_connect.dart';
```

2. Wallet connect süreçleri için handler logici
```dart
    final wcClient = WCClient(
      onConnect: () {
        // bağlanma durumu
      },
      onDisconnect: (code, reason) {
        // bağlantının kopması durumu
      },
      onFailure: (error) {
        // başarısız aksiyon durumu
      },
      onSessionRequest: (id, peerMeta) {
        // session oluşturma isteği gelmesi durumu
      },
      onEthSign: (id, message) {
        // imzalama talebi durumu
      },
      onEthSendTransaction: (id, tx) {
        // tx gönderim talebi
      },
      onEthSignTransaction: (id, tx) {
        // tx imza talebi
      },
    );
```
3. Session Kabul etme
``` dart
  wcClient.approveSession(
        accounts: [], // cüzdandaki tüm adresler eklenir
        chainId: 1, // işlem yapılabileceği ağ belirlenir
    );
```
4. Session isteğini reddetme
``` dart
    wcClient.rejectSession();
```
5. İmza isteğini kabul etme
``` dart
    wcClient.approveRequest<String>(
        id: id,
        result: signedDataAsHex,
    );
```
6. Transaction isteğini kabul etme
``` dart
 wcClient.approveRequest<String>(
        id: id,
        result: transactionHash,
    );
```
7. Tx veya imza isteğini reddetme
``` dart
    wcClient.rejectRequest(id: id);
```
8. Yerel olarak bağlı bir oturumla bağlantıyı kesin.

```dart
    wcClient.disconnect();
```

9. Bağlı bir oturumu kalıcı olarak kapatın.

```dart
    wcClient.killSession();
```

10.  Bridge url den WCSession nesnesi.

```dart
    final session = WCSession.from(wcUri);
```

11.  Uygulamanız için meta verileri içeren WCPeerMeta objesi oluştur.

```dart
    final peerMeta = WCPeerMeta(
        name: 'Example Wallet',
        url: 'https://example.wallet',
        description: 'Example Wallet',
        icons: [],
    );
```

12.  Yeni bir oturuma bağlan.

```dart
    wcClient.connectNewSession(session: session, peerMeta: peerMeta);
```

13.  Veya kaydedilmiş bir oturuma bağlanın

```dart
    wcClient.connectFromSessionStore(sessionStore);
```


