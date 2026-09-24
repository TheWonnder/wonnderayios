<div align="center">

<img src="assets/logo.png" width="112" alt="Wonnderay">

# Wonnderay для iOS

**VPN-клиент на VLESS поверх официального ядра Xray.**
Только для устройств с джейлбрейком.

[![Версия](https://img.shields.io/github/v/release/TheWonnder/wonnderayios?style=for-the-badge&label=%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8F&color=9B6BFF&labelColor=130E1B)](../../releases/latest) [![Загрузок](https://img.shields.io/github/downloads/TheWonnder/wonnderayios/total?style=for-the-badge&label=%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BE%D0%BA&color=9B6BFF&labelColor=130E1B)](../../releases) [![iOS 12+ · arm64](https://img.shields.io/badge/iOS-12%2B%20%C2%B7%20arm64-9B6BFF?style=for-the-badge&labelColor=130E1B)](../../releases/latest)

[Android](https://github.com/TheWonnder/wonnderay4a) · [Windows](https://github.com/TheWonnder/wonnderaypc) · [Linux](https://github.com/TheWonnder/wonnderaylinux) · **iOS**

</div>

---

## Что это

Wonnderay подключает устройство к **вашему собственному** серверу и пропускает
через него трафик. Своих серверов у приложения нет и не продаётся ничего: вы
даёте ему ссылку `vless://` или адрес подписки, выданный панелью.

## Возможности

| Что умеет | Подробности |
| --- | --- |
| **Подписки и серверы** | Та же логика, что на Android и Windows: список с пингом, избранное, выбор лучшего сервера по результатам замера. |
| **Полный туннель** | Демон с правами root создаёт `utun` напрямую, пакеты разбирает `hev-socks5-tunnel`, дальше их забирает Xray. |
| **Демон запускается сам** | Пакет кладёт задание в launchd, а `postinst` делает `launchctl load -w` — поднимать отдельно ничего не нужно. Демон переживает падение: проверено на устройстве, `kill -9` и самому демону, и его shell-циклу — оба раза он вернулся. |

## Протоколы

| | |
| --- | --- |
| Протокол | VLESS |
| Транспорты | TCP · WebSocket · gRPC · XHTTP · HTTPUpgrade |
| Шифрование | TLS · Reality |
| Система | iOS 12 и новее, arm64 |

## Зачем джейлбрейк

Он снимает ровно два барьера, из-за которых обычной сборки быть не может.

Первый — entitlement **`packet-tunnel-provider`**: без него система не даст
поднять VPN, а получить его можно только с платным аккаунтом разработчика.
Второй — **лимит памяти для сетевых расширений**, около 15 МБ, в которые
Go-рантайм ядра Xray почти не помещается. Демон с root обходит оба.

## Скачать

Актуальная версия — на вкладке **[Releases](../../releases/latest)**.

| Файл | Что это |
| --- | --- |
| `wonnderay_<версия>_iphoneos-arm.deb` | Пакет для устройства с джейлбрейком |

Установка — через **Sileo**, **Zebra** или **Filza**, либо по SSH:

```sh
dpkg -i wonnderay_<версия>_iphoneos-arm.deb
```

## Другие платформы

| Платформа | Репозиторий | Что публикуется |
| --- | --- | --- |
| Android | [wonnderay4a](https://github.com/TheWonnder/wonnderay4a) | APK: `universal`, `arm64-v8a`, `armeabi-v7a`, `x86_64` |
| Windows | [wonnderaypc](https://github.com/TheWonnder/wonnderaypc) | Установщик и портативный zip |
| Linux | [wonnderaylinux](https://github.com/TheWonnder/wonnderaylinux) | Пакет `.pacman` и `.tar.gz` |
| **iOS** | [wonnderayios](https://github.com/TheWonnder/wonnderayios) | `.deb` для устройства с джейлбрейком |

## Поддержка

Telegram — [@neowixtg](https://t.me/neowixtg)
