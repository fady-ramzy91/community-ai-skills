# Clean Classes — examples

## How to invoke

```
Run clean-classes on <Type or file>. Apply Clean Code Chapter 10:
naming test, reasons to change, cohesion, Open/Closed, DIP.
Split if it has more than one responsibility. Then re-audit every new type.
```

## Messy → split (SRP)

**Input (god ViewModel):** load user, cache, format date, track screen, validate email.

**Audit:** naming test fails ("and"). Five reasons to change.

**Split:**

- `UserLoading` — fetch user
- `UserCaching` — persist user
- `JoinDateFormatting` — presentation
- `AnalyticsTracking` — events
- `EmailValidating` — rules
- `ProfileViewModel` — orchestrates on appear (inject the others)

ViewModel does not own those jobs.

## Messy → split (cohesion)

**Input:** `OrderReport` with `orders`, `html`, `csv`; methods `fetchOrders`, `renderHtml`, `exportCsv`.

**Audit:** three field clusters.

**Split:**

- `OrderFetching` — load orders
- `HTMLOrderRenderer` — HTML from orders
- `CSVOrderExporter` — CSV from orders

## Messy → split (Open/Closed)

**Input:** `process(payment)` switches on `.card` / `.applePay` / `.paypal`.

**Audit:** never closed; new method = edit a working function.

**Split:**

- `PaymentCharging` protocol/interface
- `CardCharger`, `ApplePayCharger`, `PayPalCharger`
- `process` takes `PaymentCharging` and calls `charge`

## Messy → split (DIP)

**Input:** `LoginUseCase` calls `URLSession.shared` / Retrofit directly.

**Audit:** policy glued to a concrete; untestable without network.

**Split:**

- `AuthClient` protocol/interface
- `LoginUseCase(client: AuthClient)`
- Concrete client at composition root; `FakeAuthClient` in tests

## Pass (do not split)

A `Stack` with `elements` and `push` / `pop` / `size` — one concept, one cluster, no kind-switch, no I/O concrete. Report `Split: no` and stop.
