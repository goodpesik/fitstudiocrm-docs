[Back to home](/en/)

# ПРРО Fiscal Shift

This page covers opening and closing a shift on a till computer that has ПРРО offline-mode registers set up. Registers, cashier keys and the right to work offline are set in the admin panel: **Налаштування** → the **Офлайн-режим** tab. Work of the till computer without internet is covered on the [Offline mode](/en/pages/offline-mode) page, and the general shift procedure on the [Opening and closing a shift](/en/pages/shifts) page.

The till shift and the fiscal shift of the ПРРО registers are opened and closed by one press: **Відкрити зміну** opens the fiscal shift on the selected registers, **Закрити зміну** closes the fiscal shift on every register that has one open and issues the Z-report of each of them.

---

## Opening a shift

The list of registers offered for selection when a shift is opened is formed by the ПРРО till. A register on which a shift cannot be opened is not offered for selection; the reason for the refusal is shown for it.

Two registers may use one offline cashier's key file, but not at the same time. When two registers with one cashier's key are selected, opening a shift is unavailable: the names of those registers and the requirement to leave only one of them selected are shown. By default one register of such a pair is selected.

When no register can open a shift, the shift opens without fiscalization of receipts.

### The register selection window

Pressing **Відкрити зміну** opens the **Відкрити зміну** window with the **Каси ПРРО** block. Only the registers fit to open a shift are offered for selection. The fitness of each register is reported by the offline till of this computer together with the state of the register; the admin panel only displays it.

When more than one register is set up on the computer, the list carries selection boxes and the line:

> Зміна відкриється на позначених касах. Якщо хоч одна з них не зможе відкрити зміну, зміна не відкриється на жодній.

When one register is set up, there are no selection boxes: the shift opens on that register.

List columns:

| Column | Contents |
| --- | --- |
| **Каса** | The register name and the line **ПРРО {fiscal number}, локальний {local number}**. A register with no fiscal number shows `—` |
| **Стан** | The register state; below it the line **Тестовий режим ДПС** when the mode is enabled in the register settings |
| **Ключ касира** | The state of the offline cashier's key of that register |

Values of the **Стан** column:

| Value | When shown |
| --- | --- |
| **Готова до офлайну** | The register holds the right to work offline and has no open session |
| **Працює офлайн** | The register has an open offline session; the shift opens inside that session |
| **Документи не передано в ДПС** | The register holds documents not handed over to the tax service |
| **Реєструється в ДПС** | The register has no fiscal number yet |
| **Немає права на офлайн** | The right to work offline has not been obtained |

Values of the **Ключ касира** column:

| Value | When shown |
| --- | --- |
| **Заявлено в ДПС** | The key is declared, the certificate is in date |
| **Заявлено в ДПС, сертифікат скоро спливе** | The key is declared, the certificate is running out |
| **Не заявлено в ДПС (5-ПРРО)** | The key is not among the operators the tax service lists |
| **Не перевірено в ДПС** | The key has not been checked with the tax service, or was replaced after the check |
| **Сертифікат прострочено** | The certificate of the cashier's key has run out |
| **Не задано** | No offline cashier's key has been added for the register |

### Selecting registers

Every register of the list is selected, except where two registers use one cashier's key: the first of them is selected. The selection may be changed.

At least one register must be selected: while none is selected, the **Відкрити зміну** button in the window is unavailable.

### Two registers on one cashier's key

One cashier's key works on one registrar at a time. When two registers with one key are selected, the window shows the line:

> Позначені каси використовують один ключ касира: {register names}. Один ключ працює на одному реєстраторі, тому залиште позначеною лише одну з них.

The **Відкрити зміну** button is unavailable. To proceed, one of the named registers must be unselected.

### A register not fit to open a shift

A register not fit to open a shift is not offered for selection: it cannot be marked, and no shift is opened on it. The reason for the refusal is shown for every such register.

The fitness and the reason are reported by the offline till for each register separately. A reason carries a code and a message: the code is the machine value, the message is the text shown to the user. The set of codes is closed and given below.

| Code | Message | When shown |
| --- | --- | --- |
| `REGISTER_NOT_REGISTERED` | **Касу ще реєструють у Державній податковій службі. Працювати на ній можна буде після того, як реєстрація завершиться і каса отримає фіскальний номер, — зачекайте та оновіть сторінку.** | The register has no fiscal number yet |
| `TEST_MODE_DEV_ONLY` | **Каса працює в тестовому режимі Державної податкової служби, а цей режим доступний лише на тестовому сервері. Закрийте зміну каси й вимкніть тестовий режим у налаштуваннях каси.** | The tax service's test mode is on in the register settings and the computer is not the test server |
| `OFFLINE_SESSION_CLOSED` | **Офлайн-сесію цієї каси вже закрито. Документи цієї сесії ще потрібно надіслати до Державної податкової служби — дочекайтесь, поки каса їх надішле.** | The offline session of the register is closed and its documents have not reached the tax service |
| `OFFLINE_GRANT_NONE` | **Ця каса не має права працювати в офлайні. Отримайте його в налаштуваннях каси, поки є звʼязок з інтернетом.** | The register has no open session and holds no right to work offline |
| `CASHIER_KEY_NOT_SET_UP` | **Додайте ключ офлайн-касира — без нього каса не працює в офлайні.** | No offline cashier's key is set up on the register |
| `CASHIER_KEY_NOT_DECLARED` | **Ключ офлайн-касира не заявлено в Державній податковій службі. Подайте повідомлення про касира за формою 5-ПРРО і перевірте ключ ще раз.** | The key is not among the operators the tax service lists, or was not checked after being replaced |
| `CASHIER_KEY_SAME_AS_HEAD` | **Ключ офлайн-касира — це головний ключ каси. Для роботи в офлайні потрібен окремий ключ касира: отримайте його в будь-якого кваліфікованого надавача електронних довірчих послуг і вкажіть у налаштуваннях каси.** | The offline cashier's key is the head key of this or another register of the computer |
| `CASHIER_KEY_IN_USE` | **Ключем офлайн-касира цієї каси зараз працює каса «назва іншої каси». Один ключ працює лише на одній касі одночасно: закрийте зміну на тій касі або вкажіть цій касі окремий ключ касира.** | The offline cashier's key signs the open offline session of another register of the computer |
| `CASHIER_CERTIFICATE_EXPIRED` | **Строк дії сертифіката ключа офлайн-касира закінчився, а головний ключ не відкривається. Отримайте новий ключ касира та вкажіть його в налаштуваннях каси.** | The certificate of the offline cashier's key has run out |
| Codes of the key container, beginning with `KEY_` | Messages about the state of the key or certificate file; given on the [ПРРО offline-mode registers](/en/pages/prro-registers) page | The container of the key that signs the documents of the register did not open |

The name of the other register is filled in by the till; when no name is given, «інша каса цього компʼютера» is shown.

When the computer has no ПРРО register at all, the line shown is:

> Кас офлайн-режиму ще немає. Зміна відкриється без фіскалізації чеків.

### The registers could not be read

When the register list could not be read, the window shows a line and the **Оновити** button:

> Не вдалося прочитати каси офлайн-режиму. Перевірте, що служба каси працює на цьому комп'ютері, і спробуйте ще раз.

The **Відкрити зміну** button in the window is unavailable until the list has been read. The **Оновити** button repeats the read; the window does not have to be closed.

### A shift opened without fiscalization

A register's refusal does not hold the shift closed: the shift opens and receipts are issued. When the shift has opened and no register opened a fiscal shift, the message **Зміну відкрито без фіскалізації** is shown with the text:

| Text | When shown |
| --- | --- |
| **Жодна каса ПРРО не змогла відкрити зміну, тому чеки цієї зміни не фіскалізуються.** | The window held no register a shift could be opened on |
| **Жодна каса ПРРО не відкрила зміну, тому чеки цієї зміни не фіскалізуються.** | Every selected register refused at the opening |

In these cases the successful-opening message is not shown.

### One register's refusal

When the fiscal shift was not opened on every selected register, a separate message is shown for each register that refused: the register name in the heading, the reason in the text. The shift stays open and the remaining registers work.

| Message | Meaning |
| --- | --- |
| **Офлайн-сесія вичерпала свої 36 годин.** | The register's offline session is spent |
| **Місячний запас офлайну (168 годин) вичерпано.** | The monthly offline allowance is spent |
| **Ця каса не має права працювати в офлайні. Отримайте його в налаштуваннях каси, поки є звʼязок з інтернетом.** | The right to work offline is absent or already spent |
| **Каса не перейшла в офлайн. Щоб спробувати ще раз, закрийте зміну й відкрийте її знову.** | The document was not signed |
| **Зміна на цій касі вже відкрита.** | The register's fiscal shift was already open |
| **Додайте ключ офлайн-касира — без нього каса не працює в офлайні.** | No offline cashier's key has been added for the register |
| **Ключ офлайн-касира не заявлено в Державній податковій службі. Подайте повідомлення про касира за формою 5-ПРРО і перевірте ключ ще раз.** | The key is not declared to the tax service |
| **Строк дії сертифіката ключа офлайн-касира закінчився, а головний ключ не відкривається. Отримайте новий ключ касира та вкажіть його в налаштуваннях каси.** | The certificate of the cashier's key has run out |
| **Ключ офлайн-касира — це головний ключ каси. Для роботи в офлайні потрібен окремий ключ касира: отримайте його в будь-якого кваліфікованого надавача електронних довірчих послуг і вкажіть у налаштуваннях каси.** | The cashier's key is the head key of a register |
| **Ключем офлайн-касира цієї каси зараз працює каса «назва іншої каси». Один ключ працює лише на одній касі одночасно: закрийте зміну на тій касі або вкажіть цій касі окремий ключ касира.** | The cashier's key signs the open session of another register |

When a selected register could not be taken into the shift because of its settings, its key or its right to work offline, the shift opens on no register and the reason for the refusal is shown.

---

## A repeated press and a shift opened by another user

While the request to open or close the shift is running, the action button in the window is unavailable and the window does not close. A repeated press does not open or close the shift a second time.

| Message | Text | When shown |
| --- | --- | --- |
| **Зміна в обробці** | Попередній запит ще виконується. Дочекайтеся відповіді: повторне натискання не відкриє і не закриє зміну вдруге. | Pressed again while the previous request is running |
| **Зміну вже відкрито** | Зміну вже відкрито користувачем {name}. | Another user opened the shift; the name is known |
| **Зміну вже відкрито** | Зміну вже відкрито іншим користувачем. | The shift is open and the name is not known |

A shift opened by another user is not opened again here: no fiscal shift is opened on the registers and no success message is shown.

### The action did not finish

When the action over the shift did not finish, the message **Дію не завершено** is shown with the text:

> Дію над зміною не завершено. Перевірте стан зміни та повторіть спробу.

The window stays open and the action button becomes available again. Z-reports the registers already issued in that attempt are kept and sent in the next closing attempt: a second Z-report of the same shift is not issued.

---

## Closing a shift

Pressing **Закрити зміну** closes the fiscal shift on every register of the computer that has one open and issues the Z-report of each of them. No registers are selected at closing.

### Z-reports in the shift closing window

When the shift has Z-reports, the Z-report window is shown after closing. For each ПРРО Z-report it shows:

| Line | Contents |
| --- | --- |
| **Z-звіт зміни — {register name}** | The heading with the register name |
| **ФН ПРРО {number}** | The register's fiscal number with the tax service |
| **Звіт № {number}** | The fiscal number of the Z-report document |
| Date and time | The instant the Z-report was issued, in the studio's time zone |

When the shift has no Z-report, the line **Дані Z-звіту відсутні** is shown and the shift closing window stays the working-hours window.

The Z-report window also shows the Z-reports of this computer that no shift report has carried yet. One Z-report is carried by exactly one shift report.

### One register's refusal at closing

A register's refusal does not hold the shift open: the shift closes, and for each register that refused a separate message is shown — the register name in the heading, the reason in the text.

| Message | Meaning |
| --- | --- |
| **Фіскальну зміну цієї каси не закрито — перевірте ключ каси. Z-звіт буде сформовано при наступному закритті зміни або при поверненні каси в онлайн.** | The register's fiscal shift was not closed |
| **Не вдається скласти Z-звіт: в одного з чеків зміни не збереглися суми.** | A receipt of the shift carries no amounts |
| **Не вдається скласти Z-звіт: у зміні є документ, якого ми не вміємо підсумувати.** | The shift holds a document the Z-report does not cover |

A fiscal shift that stayed open is closed at the next shift closing or when the register is brought back online.

### The shift was not closed

When the request to close the shift was not carried out, the message **Зміну не закрито** is shown with the text:

> Запит на закриття зміни не виконано, тому зміна залишається відкритою. Повторіть закриття.

The shift stays open and the shift closing window is not shown. The successful-closing message is not shown in this case.

### A sale in a shift whose Z-report has been issued

When the Z-report of a register's shift has been issued, a sale in that shift is refused with the message:

> Z-звіт цієї зміни вже сформовано, тож продаж у ній неможливий. Закрийте зміну каси й відкрийте її знову.

---

## Handing documents over to the tax service

The hand-over state of a register is shown on the register card in the offline-mode settings tab.

| Line | When shown |
| --- | --- |
| **Передавання документів у ДПС триває** | The hand-over is running |
| **Документи передано в ДПС** | The documents have been handed over |
| **Документи передано, але право на офлайн не повернулось — отримайте його знову** | The documents have been handed over and the right to work offline has not been obtained |
| **Документи не передано: {reason}** | The hand-over was not carried out |

### The hand-over was interrupted

When the hand-over of documents was interrupted — the till service was restarted or the computer was switched off during the hand-over — the register state after the service starts shows:

> Документи не передано: Передачу перервано — спробуємо ще раз

The **Передавання документів у ДПС триває** state does not survive a restart. The hand-over is repeated automatically; no documents are lost.

---

## An incomplete plan list above the clients list

When the plan data could not be read whole, the notice above the clients list reads:

> Перелік абонементів у цьому списку може бути неповним. Перевірте абонементи клієнта перед продажем або допуском на заняття.

While the notice is shown, the client's plans must be checked on the client card before a plan is sold and before the client is admitted to a class. The clients list itself works: search, opening a card and selling are available.

---

## Related pages

- [Opening and closing a shift](/en/pages/shifts)
- [Offline mode](/en/pages/offline-mode)
- [Point of sale](/en/menu/pos)

[Back to home](/en/)
