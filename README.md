# -highload-cource-work-2025-2-amazon


## **1. Тема и целевая аудитория**

### **1.1 Тема**

**Amazon** – это крупнейшая в мире онлайн-платформа для электронной коммерции, предоставляющая пользователям возможность покупать и продавать товары, а также использовать широкий спектр дополнительных сервисов, включая доставку, подписки, облачные вычисления и цифровые товары.

---

### **1.2. Целевая аудитория**

- **Покупатели** – конечные пользователи, покупают товары
- **Продавцы** – предприниматели и компании
- **Партнеры по логистике** – службы доставки и возврата, службы ремонта

---

### **1.3. Анализ трафика и вовлеченности**

_(По данным SimilarWeb [1](https://www.similarweb.com/website/amazon.com/) и внутренних отчетов Amazon)_

- **Всего посещений (за месяц, данные за августь 2025):** 2.7B  [[1]](https://www.similarweb.com/website/amazon.com/)
- **Средняя продолжительность сеанса:** 6 минут [[1]](https://www.similarweb.com/website/amazon.com/)
- **Среднее количество просмотров страниц за посещение:** 9.4 [[1]](https://www.similarweb.com/website/amazon.com/)
- **Процент отказов:** ~31% [[1]](https://www.similarweb.com/website/amazon.com/)
- **Количество активных продавцов:** 9M+ на момент 2021 года [[2]](https://www.marketplacepulse.com/amazon/number-of-sellers)
- **Пользователи Amazon Prime:** 240M+ на момент лета 2025 года [[3]](https://salesduo.com/blog/amazon-statistics/)

### **1.4. Функционал MVP**

#### **Пользовательский функционал**

- **Регистрация и авторизация пользователей** (e-mail, телефон, социальные сети)
- **Каталог товаров и услуг**
  - Просмотр товаров по категориям
  - Фильтрация и сортировка
- **Карточка товара**
  - Описание, фотографии, характеристики
  - Отзывы и рейтинги
- **Корзина и оформление заказа**
  - Добавление товаров
  - Выбор способа доставки
  - Оплата (карты)
- **Личный кабинет**
  - История заказов
  - Адреса доставки

#### **Функционал для продавцов (Marketplace)**

- Регистрация и верификация
- Создание карточек товаров
- Управление заказами и возвратами

#### **Функционал для логистики и доставки**

- Интеграция с Amazon Logistics и партнерами
- Отслеживание заказов
- Управление складами (**FBA — Fulfillment by Amazon**)

---

<a name="block2"></a>

## **2. Расчет нагрузки**

### **2.1 Продуктовые метрики**

- #### MAU (Monthly Active Users) = 300M [[7]](https://analyzify.com/statsup/amazon)
- #### DAU (Daily Active Users) = 60M [[7]](https://analyzify.com/statsup/amazon)

Расчёт:
<i>DAU = 0.2×300M = 60M</i>

#### Действия пользователей

| Тип пользователя | Параметр (количество на 1 пользователя в день)   | Число                                                                                                                                                                                                                              |
| ---------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Покупатель       | Регистрация, авторизация, обновление профиля     | 0.003 [V]                                                                                                                                                                                                                          |
| Покупатель       | Среднее количество просмотров страниц за сессию  | 8                                                                                                                                                                                                                                  |
| Покупатель       | Количество сессий в день                         | 2                                                                                                                                                                                                                                  |
| Покупатель       | Количество оставленных отзывов за день           | 0.13 [[8]](https://meetanshi.com/blog/amazon-seller-statistics/)[[9]](https://www.powerreviews.com/wp-content/uploads/2023/10/2023-Ratings-Reviews-Report_-Amazon-Edition-1.pdf)                                                   |
| Покупатель       | Количество добавленных товаров в корзину за день | 3 [[12]](https://shopney.co/blog/ultimate-guide-to-increase-add-to-cart-rates/)                                                                                                                                                    |
| Покупатель       | Количество покупок за день                       | 0.19 [[11]](https://amzscout.net/blog/amazon-statistics/)                                                                                                                                                                          |
| Покупатель       | Количество платежей за день                      | 0.19 [[11]](https://amzscout.net/blog/amazon-statistics/)                                                                                                                                                                          |
| Продавец         | Регистрация, верификация, обновление профиля     | 0.003 [V]                                                                                                                                                                                                                          |
| Продавец         | Создание карточек товаров в день                 | 0.7                                                                                                                                                                                                                                |
| Продавец         | Количество отправляемых посылок в день           | 0.6 [[6]](https://www.feedough.com/amazon-statistics-usage-revenue-key-facts/)                                                                                                                                                     |
| Продавец         | Количество возвращаемых посылок в день           | 0.1 [[10]](https://nichesources.com/amazon-return-rate.html#:~:text=Amazon's%20return%20rate%20for%20online,support%20can%20help%20reduce%20returns.)                                                                              |
| Логистика        | Количество перемещаемых посылок в день           | 1.76M [[6]](https://www.feedough.com/amazon-statistics-usage-revenue-key-facts/) [[10]](https://nichesources.com/amazon-return-rate.html#:~:text=Amazon's%20return%20rate%20for%20online,support%20can%20help%20reduce%20returns.) |

<br><br>
Из рассчета, что за 2023 год было продано боле 4.5 млрд товаров [[8]](https://meetanshi.com/blog/amazon-seller-statistics/), а в среднем на карточку товара приходится 40 отзывов [[9]](https://www.powerreviews.com/wp-content/uploads/2023/10/2023-Ratings-Reviews-Report_-Amazon-Edition-1.pdf), то 4.5млрд x 40 = 180млрд<br>
180млрд/(MAU x 12) = 48 - примерное количество отзывов, оставляемое одним пользователем за год

Из рассчета 1,6M - количество посылок, отправляемых в день [[6]](https://www.feedough.com/amazon-statistics-usage-revenue-key-facts/), а активных продавцов 2.3M [[6]](https://www.feedough.com/amazon-statistics-usage-revenue-key-facts/), то <br>
1.6M/2.3M = 0.6 - количество посылок, отправляемых среднестатистич. продавцом в день

Процент возвратов на Amazon варируется между 5% и 15% --> среднее значение 10%<br>
Тогда количество возвращаемых посылок в день 10% от 0.6 = 0.06 = 0.1 [[10]](https://nichesources.com/amazon-return-rate.html#:~:text=Amazon's%20return%20rate%20for%20online,support%20can%20help%20reduce%20returns.)

Из рассчета 1,6M - количество посылок, отправляемых в день [[6]](https://www.feedough.com/amazon-statistics-usage-revenue-key-facts/), а возвращаемых - 10% от этого числа [[10]](https://nichesources.com/amazon-return-rate.html#:~:text=Amazon's%20return%20rate%20for%20online,support%20can%20help%20reduce%20returns.), то <br>
1.6M + 1.6M x 0.1 = 1.76M

Будем считать, что пользователь обновляет/подтверждает свои учетные данные один раз за год.<br>
Тогда 1/356 = 0.003

Из рассчета, что на сервисе в день 62M пользователей, и в день продается 12M товаров [[11]](https://amzscout.net/blog/amazon-statistics/), то<br>
12M/62M = 0.19 - количество покупаемых товаров пользователем в день = количество платежей в день

Из рассчета, что у пользователя 2 сессии в день, за которые он просматривает по 8 страниц по 35 товаров на странице, а конверсия с просмотра составляет 8% [[12]](https://shopney.co/blog/ultimate-guide-to-increase-add-to-cart-rates/), то<br>
2 x 8 x 35 x 0.08 x 0.08 = 3 товара в день пользователь добавляет в корзину

---


## **Список источников:**

0. https://www.amazon.com/
1. https://www.similarweb.com/website/amazon.com/
2. https://www.marketplacepulse.com/amazon/number-of-sellers
3. https://salesduo.com/blog/amazon-statistics/
4. https://amzscout.net/blog/amazon-statistics/#:~:text=It%20is%20estimated%20that%20the%20marketplace%20has%20over%20310%20million%20active%20users%20worldwide
5. https://www.demandsage.com/amazon-statistics/
6. https://www.feedough.com/amazon-statistics-usage-revenue-key-facts/
7. https://analyzify.com/statsup/amazon
8. https://meetanshi.com/blog/amazon-seller-statistics/
9. https://www.powerreviews.com/wp-content/uploads/2023/10/2023-Ratings-Reviews-Report_-Amazon-Edition-1.pdf
10. https://nichesources.com/amazon-return-rate.html#:~:text=Amazon's%20return%20rate%20for%20online,support%20can%20help%20reduce%20returns.
11. https://amzscout.net/blog/amazon-statistics/
12. https://shopney.co/blog/ultimate-guide-to-increase-add-to-cart-rates/

