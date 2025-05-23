<b>Архитектура базы данных</b><br>
🔧 Общая архитектура
База данных построена по реляционной модели и предназначена для обслуживания веб-приложения по управлению каталогом товаров и заказами. Вся структура разделена на логические сущности, каждая из которых отвечает за хранение конкретного типа информации: товары, заказы, пользователи, статусы и т.п.

Взаимосвязи между таблицами реализованы через внешние ключи (foreign keys), что обеспечивает целостность данных. Каждая сущность имеет уникальный первичный ключ и необходимый набор атрибутов.

🗂️ Таблицы и их назначение
products (Товары)
Содержит информацию о товарах, представленных в каталоге. Каждый товар привязан к категории и может участвовать в заказе.

id: PRIMARY KEY, автоинкремент

name: Название товара

model: Модель

material: Материал изготовления

price: Цена

category_id: Внешний ключ на таблицу categories

in_stock: Признак наличия

categories (Категории)
Список всех категорий товаров. Используется для группировки и фильтрации товаров в пользовательском интерфейсе.

id: PRIMARY KEY

name: Название категории

description: Текстовое описание

orders (Заказы)
Хранит общую информацию о заказах, включая клиента, статус, дату создания и сумму заказа.

id: PRIMARY KEY

client_id: Внешний ключ на clients

status_id: Внешний ключ на order_statuses

total_price: Итоговая сумма заказа

created_at: Дата и время создания

admin_id: Ответственный администратор

order_items (Состав заказа)
Множественные записи для каждого заказа, представляющие конкретные товары и их количество.

id: PRIMARY KEY

order_id: Внешний ключ на orders

product_id: Внешний ключ на products

quantity: Количество единиц товара

price_per_unit: Цена на момент оформления

clients (Клиенты)
Содержит персональные данные клиентов, оформивших заказы.

id: PRIMARY KEY

full_name: ФИО

email: Электронная почта

phone: Телефон

address: Адрес доставки

order_statuses (Статусы заказов)
Предоставляет список возможных состояний заказа, применяемых для отслеживания.

id: PRIMARY KEY

name: Название статуса (например: "Новый", "В процессе", "Завершён", "Отменён")

admins (Администраторы)
Информация о пользователях с правами управления системой.

id: PRIMARY KEY

username: Логин

password_hash: Хеш пароля

email: Электронная почта

role: Роль (например, менеджер, суперадмин)

🔄 Взаимосвязи (ER-уровень)
Один заказ принадлежит одному клиенту, но один клиент может иметь несколько заказов.

Один заказ содержит несколько позиций (order_items), каждая из которых относится к одному товару.

Один товар принадлежит одной категории, но категория может содержать множество товаров.

Один заказ имеет один статус и может быть обработан одним администратором.

🧩 Возможности расширения
Добавление таблицы product_photos для хранения изображений товаров.

Введение таблицы discounts для управления акциями.

Подключение таблицы delivery_methods для расчета доставки.
