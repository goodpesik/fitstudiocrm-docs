[Back to home](/en/)

# ПРРО Offline-Mode Registers

This page covers the **Каси офлайн-режиму** card: the setup of the ПРРО registers of a till computer, the state of each register, the right to work offline, the offline cashier's key and the hand-over of documents to the tax service. Work of the till computer without internet is covered on the [Offline mode](/en/pages/offline-mode) page.

The card is shown in the admin panel: **Налаштування** → the **Офлайн-режим** tab, while offline mode is enabled on that computer. The card is available both in the online admin panel and in the offline till; in the online admin panel the requests reach the till through the Device Handler of that computer.

Below the card heading the line is shown: "Каси, якими цей компʼютер підписує фіскальні чеки без інтернету. Право на офлайн і перевірку ключа касира отримують, поки інтернет є; документи передаються в ДПС після закриття зміни каси."

When the offline till on that computer cannot sign documents, the warning is shown above the list: "Офлайн-каса на цьому компʼютері не може підписувати документи — зверніться в підтримку."

---

## The register list

Registers are listed in the order they were added. With no registers, "Кас офлайн-режиму ще немає" is shown. Above the list are the **Додати касу** and **Оновити** buttons.

| Column | Contents |
| --- | --- |
| **Каса** | The register name and the line **ПРРО {fiscal number}, локальний {local number}**. A register with no fiscal number shows `—` |
| **Стан** | The register state; below it the line **Тестовий режим ДПС** when the mode is enabled in the register settings |
| **Залишок офлайну** | For a register with an offline session: **Сесія: {remaining}** and **Місяць: {remaining}**. For a register without a session — `—` |
| **Ключ касира** | The state of the offline cashier's key; below it the moment of the last check against the tax service, when a check was done |
| **Документи в ДПС** | The number of documents not handed over to the tax service; below it the outcome of the last hand-over, when one was performed |
| **Дії** | The buttons available for that register |

### Register state

The state is read in this order; the first value whose condition holds is shown.

| Value | When shown |
| --- | --- |
| **Документи не передано в ДПС** | The register holds documents not handed over to the tax service |
| **Працює офлайн** | The register has an open offline session |
| **Реєструється в ДПС** | The register has no fiscal number yet |
| **Готова до офлайну** | The register holds the right to work offline and has no open session |
| **Немає права на офлайн** | The right to work offline has not been obtained |

### Offline time remaining

The remaining time is shown only for a register that has an offline session, and is counted against the limit set for a ПРРО.

| Limit | Value |
| --- | --- |
| Duration of one offline session | 36 hours |
| Total offline time per calendar month | 168 hours |

Format: **{hours} год {minutes} хв**; under an hour — **{minutes} хв**. A remainder that cannot be determined is shown as `—`. A remainder below zero is shown as zero.

### The offline cashier's key

| Value | When shown |
| --- | --- |
| **Не задано** | The offline cashier's key has not been added |
| **Сертифікат прострочено** | The certificate of the key is out of date |
| **Заявлено в ДПС** | The key is declared to the tax service |
| **Заявлено в ДПС, сертифікат скоро спливе** | The key is declared to the tax service, the certificate is about to expire |
| **Не заявлено в ДПС (5-ПРРО)** | The check was performed, the key is not declared to the tax service |
| **Не перевірено в ДПС** | No check has been performed |

### Documents at the tax service

Below the number of documents not handed over, the outcome of the last hand-over is shown.

| Line | When shown |
| --- | --- |
| **Передавання документів у ДПС триває** | The hand-over is running |
| **Документи не передано: {reason}** | The hand-over was not completed; the reason came from the till. With no reason, "Документи не передано: подивіться лог каси" is shown |
| **Документи передано в ДПС** | The hand-over is complete |
| **Документи передано, але право на офлайн не повернулось — отримайте його знову** | The hand-over is complete, the right to work offline was not granted after it |

---

## Register actions

| Button | When shown | Action and message |
| --- | --- | --- |
| **Право на офлайн** | The register has a fiscal number, is not being registered and has no offline session | Asks the tax service for the right to work offline. Message: "Право на офлайн отримано" |
| **Повернути в онлайн** | The register has an offline session (open, or closed with documents still to hand over) and the till shift is not open | Closes the offline session and hands the documents over to the tax service. Performed after confirmation |
| **Ключ касира** | Always | Checks the offline cashier's key against the tax service. Message: "Ключ касира перевірено в ДПС" |
| **Пристрій у ДПС** | Always | Registers that computer with the tax service for that register. Message: "Перевірку пристрою завершено"; separately, "ДПС тримає цей ПРРО за цим компʼютером" or "ДПС тримає цей ПРРО за іншим компʼютером" |
| **Налаштування** | Always | Opens the register settings window |
| **Відкинути тестову сесію** | For a register in the tax service's test mode with a closed offline session | Discards the session without handing the documents over. Message: "Тестову сесію відкинуто" |
| **Видалити** | The register has no offline session and no documents left to hand over | Removes the register from that computer. Performed after confirmation |

### Taking a register back online

The **Повернути в онлайн** button opens the **Повернути касу в онлайн** confirmation window with the text: "Закрити офлайн-сесію каси «{name}» і надіслати її документи в ДПС? Після цього каса не працюватиме офлайн, доки не отримає право на офлайн знову." The window buttons are **Повернути в онлайн** and **Відміна**.

While the till shift is open, the button is not shown. Closing the shift is covered on the [Opening and closing a shift](/en/pages/shifts) page.

One action shows one message:

| Outcome | Message |
| --- | --- |
| Every document handed over | "Касу повернуто в онлайн" |
| Part of the documents not handed over | "Не передано документів: {count}. Спробуємо ще раз автоматично." |

### Removing a register

The **Видалити** button opens the **Видалити касу** confirmation window with the text: "Видалити касу «{name}» з цього компʼютера? Налаштування і право на офлайн буде втрачено." The window buttons are **Видалити** and **Відміна**. After removal the message "Касу видалено" is shown.

---

## Register settings

The **Додати касу** button opens the **Нова каса** window, the **Налаштування** button opens the **Налаштування каси** window.

| Field | Required | Value |
| --- | --- | --- |
| **Назва каси** | yes | The register name in the list |
| **Файл ключа каси** | yes | The key container file of the register |
| **Пароль ключа** | for a new register | The password of the register's key container |
| **Файл сертифіката ключа** | no | A certificate kept beside the container |
| **ПРРО з ДПС** | no | A ПРРО chosen from the list returned by the tax service |
| **Фіскальний номер ПРРО** | yes | The fiscal number of the ПРРО |
| **Локальний номер ПРРО** | yes | An integer from 1 |
| **ЄДРПОУ / ДРФО** | yes | The seller's code |
| **ІПН (за наявності)** | no | The individual tax number |
| **Назва продавця** | yes | The seller's name in a fiscal document |
| **Точка продажу** | yes | The name of the point of sale |
| **Адреса точки** | yes | The address of the point of sale |
| **Файл ключа офлайн-касира** | no | The key container file of the offline cashier |
| **Пароль ключа касира** | no | The password of the offline cashier's key container |
| **Сертифікат ключа касира** | no | The certificate of the offline cashier's key |
| **Тестовий режим ДПС** | no | The switch for working against the tax service's test environment |

The window buttons are **Зберегти** and **Відміна**. After saving the message "Касу збережено" is shown.

- A password left empty in the settings of an existing register does not change the stored password. The field carries the hint "Залиште порожнім, щоб не змінювати"; for a new register — "Потрібен для пошуку кас у ДПС".
- The **Знайти каси в ДПС** button fills the **ПРРО з ДПС** list from the register's key file and its password. Choosing a ПРРО from the list fills the register fields. When the tax service returns no ПРРО, "ДПС не повернула жодного ПРРО для цього ключа. Перевірте, що це ключ, зареєстрований для ПРРО." is shown.
- Adding another register key file clears the **ПРРО з ДПС** list.
- Saving is not performed while a key file is still being stored on the computer.

### Key files

A file is chosen with the **Вибрати файл** button; the field shows the file name or "Файл не вибрано". Below the register key field: "Підходять контейнери ключа та сертифікати. Файл залишається на цьому компʼютері — на наш сервер він не передається."

| Parameter | Value |
| --- | --- |
| File types | `.dat`, `.pfx`, `.p12`, `.jks`, `.zs2`, `.pem`, `.key`, `.pk8`, `.cer`, `.crt`, `.der` |
| Largest file size | 1 MB |

The file is stored in the offline till directory of that computer. After storing, the message "Файл {purpose} додано: {file name}" is shown, where the purpose is "ключа каси", "сертифіката ключа каси", "ключа офлайн-касира" or "сертифіката ключа касира".

### Form check refusals

| Message | When shown |
| --- | --- |
| "Вкажіть назву каси." | The name is empty |
| "Вкажіть фіскальний номер ПРРО." | The fiscal number is empty |
| "Вкажіть локальний номер ПРРО — ціле число від 1." | The local number is not an integer from 1 |
| "Вкажіть ЄДРПОУ або ДРФО продавця." | The seller's code is empty |
| "Вкажіть назву продавця." | The seller's name is empty |
| "Вкажіть назву точки продажу." | The point of sale name is empty |
| "Додайте файл ключа каси." | The register key file has not been added |
| "Додайте файл ключа каси і вкажіть його пароль." | A ПРРО lookup was asked without a key file or without a password |

### File choice refusals

| Message | When shown |
| --- | --- |
| "Файл не вибрано." | No file was chosen |
| "Цей тип файлу не підходить для ключа. Підходять контейнери ключа та сертифікати: {list}." | The file type is not in the list |
| "Файл порожній." | The file holds no data |
| "Файл завеликий для ключа — контейнер ключа важить кілька кілобайтів." | The file size is over 1 MB |
| "Не вдалося прочитати вибраний файл — можливо, його перемістили, видалили або він зайнятий іншою програмою. Виберіть файл ще раз." | The file was not read on that computer |

---

## Refusals of a request to the till

| Message | When shown |
| --- | --- |
| "Device Handler не відповідає — перевірте, чи він запущений на цьому компʼютері." | Device Handler did not answer |
| "Device Handler не відповів за {seconds} с, тому запит скасовано. Перевірте, чи він працює на цьому компʼютері, і спробуйте ще раз." | No answer arrived within the time allowed |
| "Ця версія Device Handler не вміє працювати з офлайн-касою — оновіть його." | The installed Device Handler version does not support offline-mode registers |
| "Не вдалося прочитати налаштування цього компʼютера, тому адреса Device Handler невідома. Перевірте, чи браузер не блокує дані цього сайту." | The computer settings were not read |
| "Не вказано адресу Device Handler — вкажіть «URL менеджера» в налаштуваннях інтеграцій." | The Device Handler address is not set |
| "Адресу Device Handler вказано неправильно — потрібна повна адреса, наприклад http://localhost:9999. Виправте «URL менеджера» в налаштуваннях інтеграцій." | The Device Handler address is not a full address |
| "Браузер не пропускає звернення з цієї сторінки на адресу Device Handler без шифрування. Вкажіть у «URL менеджера» адресу цього компʼютера або адресу з https." | The browser does not allow a request to the address given |
| "Ключ каси не відкривається. Перевірте в налаштуваннях каси, чи вказано правильний файл ключа та пароль до нього, і спробуйте ще раз." | The register's key container was not opened |
| "Ключ офлайн-касира не відкривається." | The offline cashier's key container was not opened |
| "Офлайн-каса відмовила у цій дії. Спробуйте ще раз, а якщо відмова повториться, зверніться до технічної підтримки." | The till refused without a separate reason |

---

## Stale tax settings of a till

The studio's tax group and the moment it last changed are part of every till data package; the tax group itself is part of the full package.

- While the moment of the tax group change is newer than the till data, the till refuses a sale.
- The **Синхронізувати** button in the Device Handler **Офлайн режим** window pulls the full data package while the till data is older than that moment, and the refusal is cleared.
- The shift opening and closing documents and the Z-report are not subject to that refusal.

---

## Switching offline mode off with documents not handed over

Switching offline mode off removes the studio's local data from the computer, including the fiscal documents of the ПРРО registers. Switching off is not performed in these cases:

| Message | When shown |
| --- | --- |
| "Офлайн-операцій, що ще не надійшли на сервер: {count}. Вимкнення можливе після синхронізації." | The queue holds operations not sent to the server |
| "Офлайн-каса ще працює в офлайн-сесії. Вимкнення можливе після повернення каси в онлайн." | The register has an open offline session |
| "Фіскальних документів, ще не переданих до ДПС: {count}. Вимкнення можливе після їх передачі." | There are documents not handed over to the tax service |
| "Фіскальних документів на цьому комп'ютері: {count}, і немає даних про їх передачу до ДПС. Вимкнення можливе після повернення каси в онлайн." | The computer holds fiscal documents with no record of their hand-over |

A copy whose state cannot be read does not block switching off.

---

## Related pages

- [Offline mode](/en/pages/offline-mode) — work of the till computer without internet, Device Handler, the sync.
- [Opening and closing a shift](/en/pages/shifts) — opening and closing the till shift.
- [Налаштування](/en/login/settings) (Settings) — the studio settings tabs, fiscal integrations, "URL менеджера".
