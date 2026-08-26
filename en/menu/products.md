<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.7 Products

> The **Products** section — selling ancillary goods (water, protein, merch, etc.) and tracking stock.

![](../../_media/products.png ':size=400x241')

The section has two tabs:

- **[Products](#_371-Products)** — the list of products and the actions available on them.
- **[History](#_372-Stock-history)** — stock movements (who added/removed how much, and when).

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
  - **📦 Restock** ("Поповнити склад", box icon) — see [3.7.3](#_373-Restocking)
  - **✎ Edit** (pencil icon) — name, price

> ℹ️ When a sale is made through [Point of sale](/en/menu/pos) or through [client registration](/en/menu/clients#_3-2-9-registration), stock is decreased automatically. If stock is 0, the sale is blocked.

### Adding a product

> The **+** button above the list of cards is available to the SuperAdmin and Admin roles regardless of whether a shift is open.

![](../../_media/add-product.png ':size=300x180')

**Fields:**

- **Name**
- **Price**
- **Quantity** — the starting stock when the product is created. Further restocking is done via [Restock](#_373-Restocking).

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

> Clicking the **📦 Restock** ("Поповнити склад", box icon) button on a card opens the **Restock** modal.

![](../../_media/product-restock-modal.png ':size=300x181')

**Fields:**

- **Quantity to add** — a positive number (min. 1).

Saving immediately increases **Stock** and adds a row to the [History](#_372-Stock-history) with the reason **Restock** and the user's name.

> ⚠️ If you need to **write off** a product without a sale (damage, personal use), this is handled via a sale with refund status — there is no direct "negative" restock.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)
