# Wonnderay для iOS

VPN-клиент на VLESS/Xray. **Только для устройств с джейлбрейком.**

## О приложении

- **Подписки и серверы** — та же логика, что на Android и Windows: список с
  пингом, избранное, выбор лучшего сервера.
- **Полный туннель.** Демон с правами root создаёт `utun` напрямую, пакеты
  разбирает `hev-socks5-tunnel`, дальше их забирает Xray.
- **Демон запускается сам.** Пакет кладёт задание в launchd, и `postinst`
  делает `launchctl load -w` — отдельно поднимать ничего не нужно. Демон
  переживает падение: проверено на устройстве, `kill -9` и самому демону, и
  его shell-циклу, оба раза он вернулся.
- **Протоколы:** VLESS поверх TCP / WS / gRPC / XHTTP, TLS и Reality.
- iOS 12 и новее, arm64.

## Зачем джейлбрейк

Он снимает ровно два барьера, из-за которых обычной сборки быть не может.
Первый — entitlement `packet-tunnel-provider`: без него система не даст поднять
VPN, а получить его можно только с платным аккаунтом разработчика. Второй —
лимит памяти для сетевых расширений, около 15 МБ, в которые Go-рантайм ядра
Xray почти не помещается. Демон с root обходит оба.

## Скачать

Актуальная версия — на вкладке [Releases](../../releases/latest).

| Файл | Что это |
| --- | --- |
| `wonnderay_<версия>_iphoneos-arm.deb` | Пакет для устройства с джейлбрейком |

Установка — через Sileo, Zebra или Filza, либо по SSH:

```
dpkg -i wonnderay_<версия>_iphoneos-arm.deb
```

## Другие платформы

| Платформа | Репозиторий |
| --- | --- |
| Android | [wonnderay4a](https://github.com/TheWonnder/wonnderay4a) |
| Windows | [wonnderaypc](https://github.com/TheWonnder/wonnderaypc) |
| iOS | [wonnderayios](https://github.com/TheWonnder/wonnderayios) |

## Поддержка

Telegram — [@neowixtg](https://t.me/neowixtg)
