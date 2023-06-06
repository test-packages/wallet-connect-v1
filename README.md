<div align="center">
<img src="https://github.com/Orange-Wallet/orangewallet-utils/raw/master/assets/images/walletconnect.png" alt="Wallet Connect Logo" width="70"/>
<h1>Wallet Connect</h1>
</div>


# Wallet Connect

[![İngilizce](https://img.shields.io/badge/Dil-Ingilizce-blue?style=for-the-badge)](README.md)    [![Türkçe](https://img.shields.io/badge/Dil-Turkce-red?style=for-the-badge)](README-TR.md)  ![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white)

* [About Wallet Connect](#about-wallet-connect)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Using](#using)
### About Wallet Connect
Wallet Connect is an open source protocol that allows your wallet to connect and interact with DApps and other wallets. Wallet Connect establishes an encrypted connection between your wallet and DApp by scanning the QR code or using a link. The protocol also has instant notification features to notify users of incoming transactions. You may have seen WalletConnect on Android or iOS mobile wallets like Trust Wallet and MetaMask. A list of cryptocurrency wallet apps that support Wallet Connect can be found [here](https://explorer.walletconnect.com/).

### Prerequisites
[Flutter SDK](https://docs.flutter.dev/get-started/install) , [IDE](https://blog.logrocket.com/best-ides-flutter-2022/) and [Xcode](https://developer.apple.com/xcode/) must be installed.

### Installation
To add the wallet connect package to the project, add the following lines to the pubspec.yaml file:
``` YAML
  wallet_connect:
    git:
      url: https://github.com/test-packages/wallet-connect-dart
```
### Using
You can create dapp connections with the wallet connect package by following the steps below.

1. Importing into the project

```dart
    import 'package:wallet_connect/wallet_connect.dart';
```

2. Handler logic for wallet connect processes
```dart
       final wcClient = WCClient(
      onConnect: () {
        // Respond to connect callback
      },
      onDisconnect: (code, reason) {
        // Respond to disconnect callback
      },
      onFailure: (error) {
        // Respond to connection failure callback
      },
      onSessionRequest: (id, peerMeta) {
        // Respond to connection request callback
      },
      onEthSign: (id, message) {
        // Respond to personal_sign or eth_sign or eth_signTypedData request callback
      },
      onEthSendTransaction: (id, tx) {
        // Respond to eth_sendTransaction request callback
      },
      onEthSignTransaction: (id, tx) {
        // Respond to eth_signTransaction request callback
      },
    );
```
3. Approve a session connection request.
``` dart
  wcClient.approveSession(
        accounts: [], 
        chainId: 1,
    );
```
4. reject a session connection request.
``` dart
    wcClient.rejectSession();
```
5. Approve a sign transaction request by signing the transaction and sending the signed hex data.

``` dart
    wcClient.approveRequest<String>(
        id: id,
        result: signedDataAsHex,
    );
```
6. Approve a send transaction request by sending the transaction hash generated from sending the transaction.
``` dart
 wcClient.approveRequest<String>(
        id: id,
        result: transactionHash,
    );
```
7. Or reject any of the requests above by specifying request id.
``` dart
    wcClient.rejectRequest(id: id);
```
8. Disconnect from a connected session locally.

```dart
    wcClient.disconnect();
```

9. Permanently close a connected session.

```dart
    wcClient.killSession();
```

10.  Create WCSession object from wc: uri.

```dart
    final session = WCSession.from(wcUri);
```

11.  Create WCPeerMeta object containing metadata for your app.

```dart
    final peerMeta = WCPeerMeta(
        name: 'Example Wallet',
        url: 'https://example.wallet',
        description: 'Example Wallet',
        icons: [],
    );
```

12.  Connect to a new session.

```dart
    wcClient.connectNewSession(session: session, peerMeta: peerMeta);
```

13.  Or reject a session connection request.

```dart
    wcClient.connectFromSessionStore(sessionStore);
```


