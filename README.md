# Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet — сборка под War Dogs + Discord

Форк [Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet](https://github.com/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet), заранее настроенный так, чтобы работали **War Dogs** и **Discord** одновременно.

Главное отличие от оригинала — файл **`AUTO-PICK-ZAPRET.bat`**: он сам перебирает стратегии и останавливается на той, что работает сегодня. Руками по одной запускать больше не нужно.

## Как пользоваться

1. Скачать репозиторий: зелёная кнопка **Code → Download ZIP**
2. ПКМ по архиву → **Свойства** → галочка **«Разблокировать»** → ОК
3. Распаковать в путь **без кириллицы и пробелов** — например `C:\zapret`
4. ПКМ по **`AUTO-PICK-ZAPRET.bat`** → **«Запуск от имени администратора»**

Скрипт перебирает стратегии и на каждой проверяет три адреса Discord — сайт, gateway и CDN. Останавливается на первой, где отвечают все три, и оставляет её работать. Занимает от нескольких секунд до пары минут.

Доступность античита War Dogs проверяется отдельно и **на выбор стратегии не влияет** — почему, см. ниже.

Первой всегда пробуется `general (ALT11)` — она подтверждённо работает с War Dogs.

Результат последнего запуска пишется в `auto-pick-last-run.txt`.

## Что уже настроено

| Настройка | Значение | Зачем |
|---|---|---|
| Game Filter | `enabled (UDP)` | War Dogs использует UDP на портах выше 1023 |
| IPSet Filter | `any` | под фильтр попадает любой IP игры |
| `lists/list-general.txt` | 105 строк | штатные домены + Cloudflare + `codefusion.technology` (античит) |
| `lists/list-exclude.txt` | 129 строк | штатные исключения + Яндекс, Teams и прочее |

Списки — **надстройка** над оригинальными: все домены Discord и YouTube из штатной сборки на месте, ничего не удалено. Поэтому Discord не ломается.

### Почему античит не влияет на выбор стратегии

Все 8 доменов античита (`ac-*.codefusion.technology`) присутствуют **одновременно** в `list-general.txt` и в `list-exclude.txt`. В winws исключения имеют приоритет над списком обхода, поэтому zapret пропускает этот трафик нетронутым — при любой стратегии.

Скорее всего так и задумано: вмешиваться в трафик античита — плохая идея. Но следствие важно понимать: **по доступности античита нельзя отличить одну стратегию от другой**, результат будет одинаковым хоть с обходом, хоть без него. Поэтому `AUTO-PICK` выбирает стратегию по Discord, а античит показывает справочно — если он не отвечает, менять стратегию бессмысленно, проблема в сети.

Если захотите, чтобы античит всё же обходился, удалите строки `codefusion` из `lists/list-exclude.txt`. Конфиг из Discord-гайда я оставил как есть, потому что он у вас рабочий.

## Если не работает

- **Ни одна стратегия не прошла** — скрипт напишет, какая была лучшей, и запустит её. Часто этого достаточно.
- **`winws.exe` не стартует** — почти всегда антивирус забрал `WinDivert`. Добавьте папку в исключения или отключите детект PUA.
- **Нет прав администратора** — без них WinDivert не загрузится, обход не заработает в принципе.
- **Голосовой чат Discord висит на «подключении»** — нужны записи в `hosts`: запустите `service.bat` → пункт **9. Update Hosts File**. На машине, где диск откатывается после сессии, это придётся делать каждый раз.
- **Тормозят посторонние сайты** — это цена режима `IPSet any`. Вернуть: `service.bat` → **5. IPSet Filter**. Полный список лежит в `lists/ipset-all.txt.backup`.

## Ручной режим

Автоподбор ничего не ломает в оригинальной сборке — все штатные файлы на месте. Если хочется по-старому, просто запускайте `general (ALT11).bat` или любой другой напрямую, как раньше.

## Откуда взялся конфиг

Связку «ALT11 + Game Filter UDP + IPSet any + подменённые списки» подсказали на официальном Discord-сервере War Dogs. Стратегии со временем перестают работать и зависят от провайдера — поэтому и нужен автоподбор.

## Лицензия и происхождение

Оригинальный README сохранён рядом — [README-UPSTREAM.md](README-UPSTREAM.md), там полная документация по всем стратегиям и настройкам.

Оригинальный проект — [Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet](https://github.com/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet), лицензия MIT. Бинарники в `bin/` взяты из [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle) — их можно сверить по контрольным суммам с оригиналом.

Отдельная благодарность [bol-van](https://github.com/bol-van) — автору [zapret](https://github.com/bol-van/zapret).

---

<details>
<summary><b>NEW</b></summary>

*   🎉 **Автоматический выбор стратегии:** `AUTO-PICK-ZAPRET.bat` сам найдёт работающую конфигурацию.
*   🚀 **War Dogs + Discord:** одновременная работа двух приложений.
*   💡 **UDP Game Filter:** для War Dogs.

</details>

<div align="center">
  <img src="https://img.shields.io/github/v/tag/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet?label=Release&style=flat-square" alt="Release">
  <a href="https://github.com/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet/releases/tag/1.10.3">
    <img src="https://img.shields.io/github/v/release/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet?include_prereleases&label=Latest&style=flat-square" alt="Latest">
  </a>
  <a href="https://github.com/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet/issues">
    <img src="https://img.shields.io/github/issues/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet?style=flat-square" alt="Issues">
  </a>
  <a href="https://github.com/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet/blob/main/LICENSE.txt">
    <img src="https://img.shields.io/github/license/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet?style=flat-square" alt="License">
  </a>
</div>

---

## ⚠️ ФЕЙКИ И АНТИВИРУСЫ

*   **WinDivert.dll** и **WinDivert64.sys** могут детектироваться антивирусами как вредоносное ПО (PUA/UAC). Это ложное срабатывание. Добавьте папку с zapret в исключения антивируса.
*   Если `winws.exe` не стартует, скорее всего, антивирус заблокировал `WinDivert`.

---

## 💖 ПОДДЕРЖКА ПРОЕКТА

*   **Звёзды:** если репозиторий оказался полезен, поставьте звезду ⭐.
*   **Баги:** сообщения об ошибках и предложения по улучшению оставляйте в [Issues](https://github.com/Vaulttrashine/WArdOgS-GItHUb_DIscOrD_ZapRet/issues).
*   **Донат:** любая помощь приветствуется! [Buy me a coffee](https://www.buymeacoffee.com/vaulttrashine) ☕.

---

<details>
<summary><b>Содержимое репозитория</b></summary>

```
.
├── AUTO-PICK-ZAPRET.bat
├── LICENSE.txt
├── README.md
├── SHA256SUMS.txt
├── bin
│   ├── WinDivert.dll
│   ├── WinDivert64.sys
│   ├── cygwin1.dll
│   ├── quic_initial_dbankcloud_ru.bin
│   ├── quic_initial_www_google_com.bin
│   ├── stun.bin
│   ├── tls_clienthello_4pda_to.bin
│   ├── tls_clienthello_max_ru.bin
│   ├── tls_clienthello_www_google_com.bin
│   └── winws.exe
├── general (ALT).bat
├── general (ALT10).bat
├── general (ALT11).bat
├── general (ALT12).bat
├── general (ALT2).bat
├── general (ALT3).bat
├── general (ALT4).bat
├── general (ALT5).bat
├── general (ALT6).bat
├── general (ALT7).bat
├── general (ALT8).bat
├── general (ALT9).bat
├── general (FAKE TLS AUTO ALT).bat
├── general (FAKE TLS AUTO ALT2).bat
├── general (FAKE TLS AUTO ALT3).bat
├── general (FAKE TLS AUTO).bat
├── general (SIMPLE FAKE ALT).bat
├── general (SIMPLE FAKE ALT2).bat
├── general (SIMPLE FAKE).bat
├── general.bat
├── lists
│   ├── ipset-all.txt
│   ├── ipset-all.txt.backup
│   ├── ipset-exclude.txt
│   ├── list-exclude.txt
│   ├── list-general.txt
│   └── list-google.txt
├── serivce.bat
├── utils
│   ├── check_updates.enabled
│   ├── targets.txt
│   └── test zapret.ps1
└── README-UPSTREAM.md
```

</details>