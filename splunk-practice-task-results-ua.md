# Результати практичного завдання Splunk

Аналітик з безпеки в компанії Buttercup Games досліджує невдалі спроби SSH-входу під обліковим записом root на поштовому сервері, використовуючи Splunk Cloud.

файл `tutorialdata.zip`, завантажений у Splunk Cloud, проіндексований як `index=main`.

 Усі пошуки виконані з однаковим фіксованим діапазоном:
`03/01/2023 12:00:00.000 PM` — `03/02/2023 12:00:00.000 PM`

---

Step 1–6: Підготовка (скріни з початку роботи)


> - Скрін сторінки "Set Source Type" / завантаження даних [Add Data](https://github.com/stacy007009/Splunk-/blob/main/IMG_2739.png)
> - Скрін першого базового пошуку `index=main’ [Screen](https://github.com/stacy007009/Splunk-/blob/main/IMG_2743.png)
> - Скрін панелі полів (`host`, `source`, `sourcetype`) зі значеннями (5 хостів, 8 джерел, 3 sourcetype) [Screen](https://github.com/stacy007009/Splunk-/blob/main/IMG_2744.png)
> - Скрін після звуження пошуку до `index=main host=mailsv` [Screen](https://github.com/stacy007009/Splunk-/blob/main/IMG_2740.png)

---

## Use Case 1 (приклад): Невдалий вхід під root

```
index=main host=mailsv fail* root
```
[Screen](https://github.com/stacy007009/Splunk-/blob/main/IMG_2762.png)

**Кількість подій:** 41

---

## Use Case 2: Невдалий вхід під root на хості "www1"

**Пошук:**
```
index=main host=www1 fail* root
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 67

---

## Use Case 3: Невдалий вхід під root на хості "www2"

**Пошук:**
```
index=main host=www2 fail* root
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 57

---

## Use Case 4 (приклад): HTTP-відповіді зі статусом "Client side error"

**Пошук:**
```
sourcetype=access_* status=40*
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 439

---

## Use Case 5: "Client side error" на хості "www1"

**Пошук:**
```
sourcetype=access_* status=40* host=www1
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 122

---

## Use Case 6: "Client side error" на хості "www3"

**Пошук:**
```
sourcetype=access_* status=40* host=www3
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 141

---

## Use Case 7 (приклад): HTTP-відповіді зі статусом "Server-side error"

**Пошук:**
```
sourcetype=access_* status=50*
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 306

---

## Use Case 8: "Server-side error" на хості "www2"

**Пошук:**
```
sourcetype=access_* status=50* host=www2
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 88

---

## Use Case 9: "Server-side error" на хості "www3"

**Пошук:**
```
sourcetype=access_* status=50* host=www3
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 113

---

## Use Case 10 (приклад): Успішні спроби SSH-входу

**Пошук:**
```
sourcetype="secure-2" accept*
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 229

---

## Use Case 11: Невдалі спроби SSH-входу (усі хости)

**Пошук:**
```
sourcetype="secure-2" fail*
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 5,034

---

## Use Case 12: Невдалі спроби SSH-входу на хості "www2"

**Пошук:**
```
sourcetype="secure-2" fail* host=www2
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 1,289

---

## Use Case 13: Успішні спроби SSH-входу на хості "www3"

**Пошук:**
```
sourcetype="secure-2" accept* host=www3
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 60

---

## Use Case 14: Успішні спроби SSH-входу на хості "mailsv"

**Пошук:**
```
sourcetype="secure-2" accept* host=mailsv
```
> 📌 **Вставте скрін тут**

**Кількість подій:** 39

---

## Підсумкова таблиця

| Use Case | Опис | SPL-запит | Кількість подій |
|---|---|---|---|
| 1 | Невдалий вхід під root | `index=main host=mailsv fail* root` | 41 |
| 2 | Невдалий вхід під root на www1 | `index=main host=www1 fail* root` | 67 |
| 3 | Невдалий вхід під root на www2 | `index=main host=www2 fail* root` | 57 |
| 4 | HTTP 4xx (client error) | `sourcetype=access_* status=40*` | 439 |
| 5 | HTTP 4xx на www1 | `sourcetype=access_* status=40* host=www1` | 122 |
| 6 | HTTP 4xx на www3 | `sourcetype=access_* status=40* host=www3` | 141 |
| 7 | HTTP 5xx (server error) | `sourcetype=access_* status=50*` | 306 |
| 8 | HTTP 5xx на www2 | `sourcetype=access_* status=50* host=www2` | 88 |
| 9 | HTTP 5xx на www3 | `sourcetype=access_* status=50* host=www3` | 113 |
| 10 | Успішні SSH-входи | `sourcetype="secure-2" accept*` | 229 |
| 11 | Невдалі SSH-входи | `sourcetype="secure-2" fail*` | 5,034 |
| 12 | Невдалі SSH-входи на www2 | `sourcetype="secure-2" fail* host=www2` | 1,289 |
| 13 | Успішні SSH-входи на www3 | `sourcetype="secure-2" accept* host=www3` | 60 |
| 14 | Успішні SSH-входи на mailsv | `sourcetype="secure-2" accept* host=mailsv` | 39 |

---

## Технічні деталі середовища

- Splunk Cloud інстанс: `prd-p-rgjoz.splunkcloud.com`
- Індекс: `main`
- Завантажений файл: `tutorialdata.zip` (через Settings → Add Data → Upload)
- Налаштування host: **Segment in path**, номер сегмента `1`
- Поля даних: `host`, `source`, `sourcetype`
  - Хости: `mailsv`, `www1`, `www2`, `www3`, `vendor_sales`
  - Ключове джерело: `/mailsv/secure.log`
  - Ключовий sourcetype: `secure-2`
- Часовий діапазон для всіх пошуків: `03/01/2023 12:00:00.000 PM` — `03/02/2023 12:00:00.000 PM`
