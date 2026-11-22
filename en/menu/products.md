<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.7 Products

> The **Products** ("Товари") section — selling ancillary goods (water, protein, merch, etc.) and tracking stock.

![](../../_media/products.png ':size=400x241')

The section has two tabs:

- **[Products](#_371-products)** — the list of products and the actions available on them.
- **[History](#_372-stock-history)** — stock movements (who added/removed how much, and when).

---

## 3.7.1 Products

> A product card contains:

- **Name**
- **Price** (UAH)
- **Stock** — current quantity on hand. Color coding:
  - **Normal** — stock ≥ 3
  - **Yellow (warning)** — low (1 or 2 units)
  - **Red (danger)** — out of stock (0)
- **Buttons** (for the **SuperAdmin** and **Admin** roles):
  - **🗑 Delete** (trash-can icon)
  - **📦 Restock** ("Поповнити склад", box icon) — see [3.7.3](#_373-restocking)
  - **✎ Edit** (pencil icon) — the **Edit product** ("Редагувати товар") modal with the **Name** and **Price** fields. Stock is not changed in this modal.

Before deleting, the system asks for confirmation (**Cancel** ("Відміна") / **Continue** ("Продовжити") buttons). After deletion the notification "Товар успішно видалено" (product deleted) is shown.

The card list is paginated (10, 20 or 50 cards per page).

> ℹ️ When a sale is made through [Point of sale](/en/menu/pos) or through [client registration](/en/menu/clients#_329-registration), stock is decreased automatically. In the product picker a product with stock 0 cannot be selected; when stock is below 3, "(залишилось N шт.)" (N left) is shown next to the name.

### Adding a product

> The **+** button above the list of cards opens the **Add product** ("Додати товар") modal. The button is available to the SuperAdmin and Admin roles regardless of whether a shift is open.

![](../../_media/add-product.png ':size=300x180')

**Fields:**

- **Name** — required.
- **Price** — integer, required.
- **Quantity** — the starting stock, an integer from 0. Optional; shown only when creating. Further restocking is done via [Restock](#_373-restocking).

Modal buttons: **Close** ("Закрити"), **Save** ("Зберегти").

---

## 3.7.2 Stock history

> The **History** tab shows all stock movements.

![](../../_media/products-history.png ':size=420x253')

**Columns:**

| Column | Description |
|---|---|
| **Date** | Time of the event |
| **Product** | Product name |
| **Change** | `+N` (added) or `−N` (removed). Green / red color. |
| **Reason** | `Restock` / `Sale` / `Refund` |
| **By** | Name of the user who made the change |

---

## 3.7.3 Restocking

> Clicking the **📦 Restock** ("Поповнити склад", box icon) button on a card opens the **Restock: <product name>** ("Поповнити склад: <назва товару>") modal.

![](../../_media/product-restock-modal.png ':size=300x181')

**Fields:**

- **Quantity to add** ("Скільки додати") — an integer, minimum 1. The **Save** button is disabled when the value is below 1.

Saving immediately increases **Stock** and adds a row to the [History](#_372-stock-history) with the reason **Restock** and the user's name; the notification "Склад поповнено" (stock replenished) is shown.

> ⚠️ Writing off a product without a sale (damage, personal use) is not supported: stock decreases only through a sale, and restocking accepts only positive values. Refunding a sale increases stock.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)
