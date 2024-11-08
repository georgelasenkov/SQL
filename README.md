<h1 align="center">SQL</h1>
Здесь Вы сможете просмотреть мои навыки языка SQL на примере PostgreSQL, такие как: построение запросов для выборки данных, создания и изменения таблиц.

<h2 align="center">Вступление</h2>

#### Мы с Вами имеем автосалон по продаже б/у спортивных (и не только) автомобилей, а также базу данных с тремя таблицами:
1. Таблица 'brands', в которой содержится информация о марке автомобиля и стране производства.
2. Таблица 'customers', в которой содержится информация об имени и фамилии покупателя авто, а также его возраст и пол.
3. Таблица 'vehicles', в которой содержится подробная информация об автомобиле, например: модель, цена, пробег, мощность, когда автомобиль был приобретен в нашем салоне и так далее. Также указаны айди бренда автомобиля и айди покупателя.

Марки и модели автомобилей взяты из жизни, но все совпадения в данных с людьми совершенно случайны 😉

<h2 align="center">🏁 Начинаем 🏁</h2>

### 1️⃣ Создаем таблицы
#### brands
<details>
  <summary>запрос</summary>

  ```
CREATE TABLE IF NOT EXISTS brands (
	id SERIAL PRIMARY KEY,
	brand_name VARCHAR(30),
	country VARCHAR(30)
	);
  ```
</details>

| id | brand_name      | country  |
|----|-----------------|----------|

customers
<details>
  <summary>запрос</summary>

  ```
CREATE TABLE IF NOT EXISTS customers (
	customer_id SERIAL PRIMARY KEY,
	first_name VARCHAR(30) NOT NULL,
	last_name VARCHAR(30) NOT NULL,
	age INT,
	sex VARCHAR(10)
	);
  ```
</details>

| customer_id | first_name | last_name | age | sex |
|--------------|------------|-----------|-----|-----|

vehicles
<details>
  <summary>запрос</summary>

  ```
CREATE TABLE IF NOT EXISTS vehicles (
	vehicle_id SERIAL PRIMARY KEY,
	customer_id INT NOT NULL REFERENCES customers (customer_id),
	brand_id INT NOT NULL REFERENCES brands (id),
	model VARCHAR (30),
	body_type VARCHAR (20),
	production_date DATE,
	price INT NOT NULL,
	mileage INT NOT NULL,
	color VARCHAR(15),
	powertrain VARCHAR(10),
	transmission VARCHAR(15),
	fuel_type VARCHAR(10),
	engine_capacity NUMERIC,
	horsepower INT,
	max_speed INT,
	purchase_date TIMESTAMP
	);
  ```
</details>

| vehicle_id | customer_id | brand_id | model        | body_type | production_date | price  | mileage | color  | powertrain | transmission | fuel_type | engine_capacity | horsepower | max_speed | purchase_date |
|----|-------------|----------|--------------|-----------|-----------------|--------|---------|--------|------------|--------------|-----------|-----------------|------------|-----------|----------------|

### 2️⃣ Вставляем значения в таблицы

