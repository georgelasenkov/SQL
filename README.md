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
#### <h3 align="center">brands</h3>
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
Результат:

| id | brand_name      | country  |
|----|-----------------|----------|

<h3 align="center">customers</h3>
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
Результат:

| customer_id | first_name | last_name | age | sex |
|--------------|------------|-----------|-----|-----|

<h3 align="center">vehicles</h3>
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
Результат:

| vehicle_id | customer_id | brand_id | model        | body_type | production_date | price  | mileage | color  | powertrain | transmission | fuel_type | engine_capacity | horsepower | max_speed | purchase_date |
|----|-------------|----------|--------------|-----------|-----------------|--------|---------|--------|------------|--------------|-----------|-----------------|------------|-----------|----------------|

### 2️⃣ Вставляем значения в таблицы
#### <h3 align="center">brands</h3>
<details>
  <summary>Запрос</summary>

  ```
INSERT INTO brands (brand_name, country)
	VALUES
		('Toyota', 'Japan'),
		('Lamborghini', 'Italy'),
		('Chevrolet', 'USA'),
		('Aston Martin', 'GB'),
		('Porsche', 'Germany'),
		('Geely', 'China'),
		('Renault', 'France'),
		('Lada', 'Russia'),
		('Cupra', 'Spain'),
		('Ford', 'Usa'),
		('Nissan', 'Japan'),
		('Audi', 'Germany'),
		('Ferrari', 'Italy'),
		('BMW', 'Germany'),
		('Land Rover', 'GB'),
		('Dodge', 'USA'),
		('Mercedes', 'Germany'),
		('Volkswagen', 'Germany'),
		('Mazda', 'Japan'),
		('Alfa Romeo', 'Italy'),
		('Fiat', 'Italy'),
		('Peugeot', 'France');
  ```
</details>

<details>
  <summary>Результат</summary>

| id | name            | country  |
|----|-----------------|----------|
| 1  | Toyota          | Japan    |
| 2  | Lamborghini     | Italy    |
| 3  | Chevrolet       | USA      |
| 4  | Aston Martin    | GB       |
| 5  | Porsche         | Germany  |
| 6  | Geely           | China    |
| 7  | Renault         | France   |
| 8  | Lada            | Russia   |
| 9  | Cupra           | Spain    |
| 10 | Ford            | USA      |
| 11 | Nissan          | Japan    |
| 12 | Audi            | Germany  |
| 13 | Ferrari         | Italy    |
| 14 | BMW             | Germany  |
| 15 | Land Rover      | GB       |
| 16 | Dodge           | USA      |
| 17 | Mercedes        | Germany  |
| 18 | Volkswagen      | Germany  |
| 19 | Mazda           | Japan    |
| 20 | Alfa Romeo      | Italy    |
| 21 | Fiat            | Italy    |
| 22 | Peugeot         | France   |
</details>

<h3 align="center">customers</h3>
<details>
  <summary>Запрос</summary>

  ```
INSERT INTO customers (first_name, last_name, age, sex)
	VALUES
		('Emma', 'Smith', 18, 'female'),
		('Liam', 'Johnson', 22, 'male'),
		('John', 'Williams', 35, 'male'),
		('Noah', 'Jones', 27, 'male'),
		('Ava', 'Brown', 42, 'female'),
		('Oliver', 'Davis', 30,	'male'),
		('Isabella', 'Miller', 55, 'female'),
		('Elijah', 'Wilson', 60, 'male'),
		('Brad', 'Moore', 75, 'male'),
		('James', 'Taylor', 40,	'male'),
		('Amelia', 'Anderson', 29, 'female'),
		('Alexander', 'Thomas', 34,	'male'),
		('Mia', 'Jackson', 50, 'female'),
		('William', 'White', 52, 'male'),
		('Harper', 'Harris', 65, 'female'),
		('Benjamin', 'Martin', 19, 'male'),
		('Evelyn', 'Thompson', 24, 'female'),
		('Lucas', 'Garcia', 48, 'male'),
		('Abigail', 'Martinez', 33,	'female'),
		('Henry', 'Robinson', 70, 'male'),
		('Ella', 'Clark', 38, 'female'),
		('Jackson', 'Rodriguez', 46, 'male'),
		('Dylan', 'Lewis', 58, 'male'),
		('Aiden', 'Lee', 63, 'male'),
		('Grace', 'Walker', 80,	'female'),
		('Samuel', 'Hall', 25, 'male'),
		('Chloe', 'Allen', 31, 'female'),
		('David', 'Young', 45, 'male'),
		('Joseph', 'Hernandez', 39,	'male'),
		('Joseph', 'King', 67, 'male'),
		('Nathan', 'Wright', 28, 'male'),
		('Matthew', 'Lopez', 23, 'male'),
		('Charlotte', 'Hill', 36, 'female'),
		('Daniel', 'Scott', 54,	'male'),
		('Zoey', 'Green', 20, 'female'),
		('Jack', 'Adams', 71, 'male'),
		('John', 'Baker', 49, 'male'),
		('Anthony', 'Gonzalez', 78,	'male'),
		('Aurora', 'Nelson', 72, 'female'),
		('Wyatt', 'Carter', 41,	'male'),
		('Natalie', 'Mitchell', 37,	'female'),
		('Dylan', 'Perez', 66, 'male'),
		('Hannah', 'Roberts', 77, 'female'),
		('Isaac', 'Turner', 82,	'male'),
		('Hazel', 'Phillips', 53, 'female'),
		('Levi', 'Campbell', 20, 'male'),
		('Addison', 'Parker', 18, 'female'),
		('Sebastian', 'Evans', 26, 'male'),
		('Stella', 'Edwards', 44, 'female'),
		('Nathan', 'Collins', 61, 'male'
);
  ```
</details>

<details>
	<summary>Результат</summary>
	
| customer_id | first_name | last_name  | age | sex    |
|--------------|------------|------------|-----|--------|
| 1            | Emma       | Smith      | 18  | female |
| 2            | Liam       | Johnson    | 22  | male   |
| 3            | John       | Williams   | 35  | male   |
| 4            | Noah       | Jones      | 27  | male   |
| 5            | Ava        | Brown      | 42  | female |
| 6            | Oliver     | Davis      | 30  | male   |
| 7            | Isabella   | Miller     | 55  | female |
| 8            | Elijah     | Wilson     | 60  | male   |
| 9            | Brad       | Moore      | 75  | male   |
| 10           | James      | Taylor     | 40  | male   |
| 11           | Amelia     | Anderson   | 29  | female |
| 12           | Alexander  | Thomas     | 34  | male   |
| 13           | Mia        | Jackson    | 50  | female |
| 14           | William    | White      | 52  | male   |
| 15           | Harper     | Harris     | 65  | female |
| 16           | Benjamin   | Martin     | 19  | male   |
| 17           | Evelyn     | Thompson   | 24  | female |
| 18           | Lucas      | Garcia     | 48  | male   |
| 19           | Abigail    | Martinez   | 33  | female |
| 20           | Henry      | Robinson   | 70  | male   |
| 21           | Ella       | Clark      | 38  | female |
| 22           | Jackson    | Rodriguez  | 46  | male   |
| 23           | Dylan      | Lewis      | 58  | male   |
| 24           | Aiden      | Lee        | 63  | male   |
| 25           | Grace      | Walker     | 80  | female |
| 26           | Samuel     | Hall       | 25  | male   |
| 27           | Chloe      | Allen      | 31  | female |
| 28           | David      | Young      | 45  | male   |
| 29           | Joseph     | Hernandez  | 39  | male   |
| 30           | Joseph     | King       | 67  | male   |
| 31           | Nathan     | Wright     | 28  | male   |
| 32           | Matthew    | Lopez      | 23  | male   |
| 33           | Charlotte   | Hill      | 36  | female |
| 34           | Daniel     | Scott      | 54  | male   |
| 35           | Zoey       | Green      | 20  | female |
| 36           | Jack       | Adams      | 71  | male   |
| 37           | John       | Baker      | 49  | male   |
| 38           | Anthony    | Gonzalez   | 78  | male   |
| 39           | Aurora     | Nelson     | 72  | female |
| 40           | Wyatt      | Carter     | 41  | male   |
| 41           | Natalie    | Mitchell   | 37  | female |
| 42           | Dylan      | Perez      | 66  | male   |
| 43           | Hannah     | Roberts    | 77  | female |
| 44           | Isaac      | Turner     | 82  | male   |
| 45           | Hazel      | Phillips   | 53  | female |
| 46           | Levi       | Campbell   | 20  | male   |
| 47           | Addison    | Parker     | 18  | female |
| 48           | Sebastian  | Evans      | 26  | male   |
| 49           | Stella     | Edwards    | 44  | female |
| 50           | Nathan     | Collins    | 61  | male   |
</details>

<h3 align="center">vehicles</h3>
<details>
  <summary>Запрос</summary>

  ```
INSERT INTO vehicles (customer_id, brand_id, model, body_type, production_date, price, mileage, color, powertrain, transmission, fuel_type, engine_capacity, horsepower, max_speed, purchase_date)
	VALUES
		(14, 3, 'Chevelle SS', 'coupe', '1970-12-08', 65990, 93576, 'black', 'RWD', 'manual', 'petrol', 7.4, 450, 209, '2024-03-12 11:45:12'),
		(37, 19, 'MX-5 Miata', 'roadster', '2022-08-04', 20580, 15603, 'red', 'RWD', 'manual', 'petrol', 2.0, 181, 217, '2024-07-11 13:33:53'),
		(22, 4, 'DB9', 'cabriolet', '2015-03-10', 118990, 55609, 'blue', 'RWD', 'automatic', 'petrol', 5.9, 510, 295, '2024-06-12 19:19:19'),
		(19, 8, 'Vesta Sport', 'sedan', '2020-03-04', 13299, 84438, 'white', 'FWD', 'manual', 'petrol', 1.8, 145, 200, '2024-01-03 14:22:35'),
		(45, 2, 'Huracan', 'roadster', '2020-03-10', 180600, 12107, 'yellow', 'AWD', 'automatic', 'petrol', 5.2, 602, 323, '2024-09-20 14:14:14'),
		(31, 21, '500', 'hatchback', '2024-01-01', 26990, 284, 'black', 'FWD', 'manual', 'petrol', 1.4, 85, 155, '2024-05-28 17:17:17'),
		(8, 6, 'Coolray', 'CUV', '2020-08-13', 14390, 94380, 'blue', 'FWD', 'automatic', 'petrol', 1.5, 177, 210, '2024-04-20 19:20:00'),
		(49, 7, 'Sport Spider', 'roadster', '1996-09-13', 66990, 35821, 'yellow', 'RWD', 'manual', 'petrol', 2.0, 150, 220, '2024-03-18 18:18:18'),
		(26, 10, 'Bronco Raptor', 'SUV', '2022-04-19', 75990, 14589, 'orange', 'AWD', 'automatic', 'petrol', 3.0, 400, 209, '2024-01-25 08:18:40'),
		(5, 3, 'Corvette C2', 'coupe', '1963-10-09', 105890, 66238, 'orange', 'RWD', 'manual', 'petrol', 5.4, 360, 233, '2024-10-10 11:17:07'),
		(44, 9, 'Tavascan', 'CUV', '2023-09-17', 48995, 2380, 'silver', 'AWD', 'automatic', 'electric', 0.0, 306, 180, '2024-06-20 21:21:21'),
		(10, 21, '124 Sport Spider', 'roadster', '1973-10-29', 35790, 63902, 'red', 'RWD', 'manual', 'petrol', 1.8, 110, 193, '2024-08-10 12:12:12'),
		(24, 1, 'GR86', 'coupe', '2014-01-12', 17650, 46595, 'white', 'RWD', 'manual', 'petrol', 2.4, 228, 225, '2024-02-10 13:15:42'),
		(33, 11, 'Note e-Power Nismo', 'hatchback', '2022-05-16', 34990, 29856, 'yellow', 'FWD', 'automatic', 'hybrid', 1.2, 134, 185, '2024-05-02 18:28:38'),
		(17, 19, 'RX-7', 'coupe', '1992-08-20', 27000, 36573, 'black', 'RWD', 'manual', 'petrol', 1.3, 255, 250, '2024-02-02 17:35:53'),
		(29, 10, 'Fiesta ST', 'hatchback', '2020-02-20', 27990, 23543, 'yellow', 'FWD', 'manual', 'petrol', 1.5, 197, 225, '2024-04-15 16:45:07'),
		(42, 5, '944 Turbo', 'coupe', '1989-10-03', 37990, 167551, 'black', 'RWD', 'manual', 'petrol', 2.5, 250, 241, '2024-07-30 11:00:00'),
		(1, 14, '2002', 'sedan', '1973-08-10', 39990, 145830, 'white', 'RWD', 'manual', 'petrol', 2.0, 120, 193, '2024-03-25 14:33:33'),
		(38, 4, 'One-77', 'coupe', '2012-03-27', 2290600, 8657, 'silver', 'RWD', 'automatic', 'petrol', 7.3, 750, 354, '2024-09-12 19:19:19'),
		(47, 12, 'R8', 'cabriolet', '2012-01-29', 85990, 67006, 'black', 'AWD', 'manual', 'petrol', 4.2, 420, 300, '2024-11-07 12:12:12'),
		(12, 17, '190E', 'sedan', '1989-08-03', 8990, 212345, 'black', 'RWD', 'manual', 'petrol', 2.6, 158, 210, '2024-09-01 11:09:09'),
		(40, 13, '458 Italia', 'cabriolet', '2011-10-06', 198990, 29034, 'silver', 'RWD', 'automatic', 'petrol', 4.5, 570, 325, '2024-01-15 11:30:07'),
		(23, 1, 'Land Cruiser', 'SUV', '2009-03-05', 36990, 131055, 'black', 'AWD', 'automatic', 'petrol', 5.7, 381, 209, '2024-10-05 18:18:18'),
		(6, 19, '3 Turbo', 'hatchback', '2021-11-10', 21300, 16903, 'blue', 'AWD', 'automatic', 'petrol', 2.5, 250, 250, '2024-08-25 22:25:25'),
		(21, 8, 'Niva', 'SUV', '2020-07-12', 9890, 44693, 'green', 'AWD', 'manual', 'petrol', 1.7, 80, 140, '2024-04-06 19:22:22'),
		(35, 14, 'M4 F82', 'coupe', '2017-09-07', 60990, 54382, 'red', 'RWD', 'automatic', 'petrol', 3.0, 425, 250, '2024-10-21 14:44:44'),
		(11, 7, 'Alpine A110', 'coupe', '2020-03-05', 73950, 13394, 'blue', 'RWD', 'automatic', 'petrol', 1.8, 252, 251, '2024-05-20 15:07:47'),
		(48, 17, 'AMG GT', 'roadster', '2022-06-30', 205990, 18343, 'white', 'RWD', 'automatic', 'petrol', 4.0, 720, 312, '2024-10-15 16:25:33'),
		(15, 16, 'Ram 1500', 'pickup', '2019-07-22', 46990, 28304, 'black', 'RWD', 'automatic', 'petrol', 5.7, 395, 193, '2024-06-28 11:11:11'),
		(34, 10, 'Mustang GT', 'cabriolet', '2021-12-25', 55990, 21060, 'white', 'RWD', 'automatic', 'petrol', 5.0, 450, 250, '2024-08-07 19:15:00'),
		(2, 2, 'Aventador', 'roadster', '2017-09-15', 335200, 19580, 'red', 'AWD', 'automatic', 'petrol', 6.5, 730, 349, '2024-01-20 16:05:25'),
		(25, 5, 'Cayman', 'coupe', '2019-02-24', 98990, 24309, 'blue', 'RWD', 'manual', 'petrol', 2.0, 300, 265, '2024-02-18 20:50:11'),
		(39, 11, 'Juke', 'CUV', '2012-04-22', 21590, 84906, 'black', 'FWD', 'automatic', 'petrol', 1.6, 134, 186, '2024-06-06 14:14:14'),
		(9, 13, 'F355', 'coupe', '1998-04-13', 74890, 69057, 'red', 'RWD', 'manual', 'petrol', 3.5, 375, 295, '2024-02-15 09:48:29'),
		(30, 17, '280 SL', 'roadster', '1971-12-03', 163990, 30500, 'red', 'RWD', 'automatic', 'petrol', 2.8, 170, 210, '2024-07-04 16:04:04'),
		(20, 16, 'Charger', 'coupe', '1973-06-09', 55990, 61043, 'black', 'RWD', 'manual', 'petrol', 7.0, 425, 210, '2024-03-01 10:05:55'),
		(41, 18, 'Beetle', 'coupe', '1972-09-10', 4390, 143502, 'white', 'RWD', 'manual', 'petrol', 1.6, 60, 112, '2024-07-15 09:45:00'),
		(4, 20, '156', 'sedan', '2004-06-09', 8990, 123860, 'silver', 'FWD', 'manual', 'diesel', 2.0, 180, 205, '2024-11-01 21:01:01'),
		(13, 15, 'Defender', 'SUV', '2022-01-03', 85990, 20003, 'green', 'AWD', 'automatic', 'diesel', 3.0, 350, 193, '2024-09-07 13:07:07'),
		(32, 4, 'Vantage V8', 'roadster', '2021-03-14', 167990, 12305, 'red', 'RWD', 'automatic', 'petrol', 4.0, 503, 314, '2024-05-12 11:01:01'),
		(46, 9, 'Born', 'hatchback', '2021-01-19', 37990, 4650, 'green', 'RWD', 'automatic', 'electric', 0.0, 231, 160, '2024-01-10 09:45:12'),
		(3, 14, 'Z3 M Coupe', 'coupe', '2000-11-24', 42950, 76920, 'blue', 'RWD', 'automatic', 'petrol', 3.2, 316, 258, '2024-01-30 12:55:10'),
		(16, 3, 'Corvette C7', 'coupe', '2017-04-01', 86599, 33578, 'red', 'RWD', 'manual', 'petrol', 6.2, 650, 290, '2024-06-01 10:10:10'),
		(36, 16, 'Challenger', 'coupe', '1971-11-09', 73590, 80490, 'orange', 'RWD', 'manual', 'petrol', 7.2, 425, 217, '2024-08-15 16:16:16'),
		(28, 18, 'Golf', 'hatchback', '1982-10-15', 5690, 254903, 'silver', 'FWD', 'manual', 'petrol', 1.6, 90, 160, '2024-02-05 14:33:33'),
		(50, 12, 'TT', 'coupe', '2006-11-26', 15990, 125694, 'red', 'FWD', 'manual', 'petrol', 2.0, 211, 250, '2024-04-27 12:00:00'),
		(18, 11, '370Z', 'coupe', '2020-02-18', 44590, 18544, 'green', 'RWD', 'manual', 'petrol', 3.0, 400, 250, '2024-08-01 15:15:15'),
		(27, 10, 'GT', 'coupe', '2020-07-02', 690000, 3409, 'silver', 'RWD', 'automatic', 'petrol', 3.5, 660, 348, '2024-01-28 12:00:00'),
		(7, 20, 'Stelvio', 'CUV', '2024-02-16', 94590, 894, 'white', 'AWD', 'automatic', 'petrol', 2.9, 505, 232, '2024-08-05 15:27:39'),
		(43, 6, 'Atlas Pro', 'CUV', '2021-12-19', 23550, 46933, 'silver', 'FWD', 'automatic', 'petrol', 2.0, 190, 210, '2024-04-11 22:11:11'),
		(14, 18, 'Passat', 'wagon', '2019-04-12', 30990, 34504, 'blue', 'AWD', 'manual', 'diesel', 2.0, 240, 209, '2024-06-02 20:20:20'),
		(39, 11, 'GT-R', 'coupe', '2021-05-01', 145990, 40012, 'silver', 'AWD', 'automatic', 'petrol', 3.8, 565, 315, '2024-04-01 17:05:05'),
		(22, 3, 'Silverado 1500', 'pickup', '2021-09-01', 61390, 18305, 'green', 'AWD', 'automatic', 'petrol', 6.2, 420, 193, '2024-05-09 13:13:13'),
		(5, 7, 'Megane RS', 'hatchback', '2021-06-12', 45990, 13510, 'red', 'FWD', 'manual', 'petrol', 1.8, 300, 250, '2024-10-28 10:10:10'),
		(24, 12, 'A5 3.0 TDI Quattro', 'coupe', '2015-02-28', 4390, 67324, 'black', 'AWD', 'automatic', 'diesel', 3.0, 245, 250, '2024-07-21 18:22:22'),
		(33, 12, 'e-tron', 'CUV', '2021-10-16', 85290, 29843, 'white', 'AWD', 'automatic', 'electric', 0.0, 402, 200, '2024-04-02 12:33:22'),
		(12, 22, '205 GTI', 'hatchback', '1984-12-22', 13390, 232960, 'white', 'FWD', 'manual', 'petrol', 1.6, 105, 190, '2024-08-06 16:16:16'),
		(30, 16, 'Viper', 'roadster', '2006-05-30', 100590, 26505, 'white', 'RWD', 'manual', 'petrol', 8.4, 505, 322, '2024-02-25 17:25:00'),
		(20, 15, 'Range Rover Sport', 'SUV', '2018-01-25', 109990, 25088, 'black', 'AWD', 'automatic', 'diesel', 3.0, 355, 225, '2024-05-17 10:17:17'),
		(46, 14, 'i3', 'hatchback', '2020-05-14', 37490, 13554, 'black', 'RWD', 'automatic', 'electric', 0.0, 170, 150, '2024-06-15 15:15:15'),
		(1, 14, 'M550d xDrive', 'sedan', '2013-03-19', 64990, 87643, 'black', 'AWD', 'automatic', 'diesel', 3.0, 381, 250, '2024-03-22 12:12:12'),
		(19, 10, 'Mustang Mach-E', 'CUV', '2022-07-11', 55990, 6433, 'blue', 'AWD', 'automatic', 'electric', 0.0, 480, 180, '2024-01-16 13:30:45'),
		(29, 14, '335d', 'sedan', '2010-01-30', 24690, 136890, 'green', 'RWD', 'automatic', 'diesel', 3.0, 286, 250, '2024-02-08 16:40:55'),
		(10, 20, 'Giulia', 'sedan', '2018-08-13', 42190, 56732, 'red', 'RWD', 'automatic', 'diesel', 2.2, 180, 230, '2024-03-30 09:09:09'),
		(38, 13, 'SF90 Stradale', 'coupe', '2020-05-19', 945990, 10803, 'red', 'AWD', 'automatic', 'hybrid', 4.0, 986, 340, '2024-04-13 14:14:14'),
		(45, 18, 'ID.4', 'CUV', '2022-11-03', 67990, 5404, 'white', 'AWD', 'automatic', 'electric', 0.0, 300, 161, '2024-05-14 09:30:30'),
		(8, 22, '306 GTI-6', 'hatchback', '1996-04-13', 9990, 143569, 'yellow', 'FWD', 'manual', 'petrol', 2.0, 167, 220, '2024-06-05 17:55:11'),
		(41, 2, 'Urus', 'SUV', '2021-03-06', 200500, 21532, 'silver', 'AWD', 'automatic', 'petrol', 4.0, 641, 305, '2024-07-29 19:22:22'),
		(3, 11, 'Leaf', 'hatchback', '2021-12-19', 38490, 26433, 'silver', 'FWD', 'automatic', 'electric', 0.0, 147, 157, '2024-08-24 13:15:15'),
		(11, 10, 'Focus RS TDCi', 'hatchback', '2016-04-05', 44290, 76544, 'blue', 'AWD', 'manual', 'diesel', 2.0, 250, 250, '2024-09-15 10:10:10'),
		(36, 12, 'RS4 Avant', 'wagon', '2007-06-08', 40990, 120405, 'black', 'AWD', 'automatic', 'petrol', 4.2, 420, 250, '2024-10-12 20:20:20'),
		(26, 18, 'Golf R TDI', 'hatchback', '2021-11-24', 41990, 17643, 'red', 'AWD', 'automatic', 'diesel', 2.0, 200, 250, '2024-10-30 22:22:22'),
		(4, 22, '407 Coupe', 'coupe', '2006-07-07', 14590, 165987, 'silver', 'FWD', 'automatic', 'petrol', 3.0, 211, 240, '2024-11-02 11:11:11'),
		(50, 5, '911 Carrera S', 'cabriolet', '2021-07-15', 183990, 19570, 'silver', 'RWD', 'automatic', 'petrol', 3.0, 443, 307, '2024-11-03 15:15:15'),
		(27, 5, 'Taycan', 'sedan', '2022-04-04', 143990, 8542, 'green', 'AWD', 'automatic', 'electric', 0.0, 616, 250, '2024-11-06 09:30:00'),
		(13, 1, 'Supra', 'coupe', '2022-07-09', 40900, 25697, 'blue', 'RWD', 'automatic', 'petrol', 3.0, 382, 250, '2024-04-22 18:00:00');
  ```
</details>

<details>
	<summary>Результат</summary>
	
| id | customer_id | brand_id | model                | body_type | production_date | price  | mileage | color   | powertrain | transmission | fuel_type | engine_capacity | horsepower | max_speed | purchase_date         |
|----|-------------|----------|---------------------|-----------|-----------------|--------|---------|---------|------------|--------------|-----------|-----------------|------------|-----------|---------------------|
| 1  | 14          | 3        | Chevelle SS         | coupe     | 1970-12-08      | 65990  | 93576   | black   | RWD        | manual       | petrol    | 7.4             | 450        | 209       | 2024-03-12 11:45:12 |
| 2  | 37          | 19       | MX-5 Miata          | roadster  | 2022-08-04      | 20580  | 15603   | red     | RWD        | manual       | petrol    | 2.0             | 181        | 217       | 2024-07-11 13:33:53 |
| 3  | 22          | 4        | DB9                  | cabriolet | 2015-03-10      | 118990 | 55609   | blue    | RWD        | automatic    | petrol    | 5.9             | 510        | 295       | 2024-06-12 19:19:19 |
| 4  | 19          | 8        | Vesta Sport          | sedan     | 2020-03-04      | 13299  | 84438   | white   | FWD        | manual       | petrol    | 1.8             | 145        | 200       | 2024-01-03 14:22:35 |
| 5  | 45          | 2        | Huracan              | roadster  | 2020-03-10      | 180600 | 12107   | yellow  | AWD        | automatic    | petrol    | 5.2             | 602        | 323       | 2024-09-20 14:14:14 |
| 6  | 31          | 21       | 500                  | hatchback | 2024-01-01      | 26990  | 284     | black   | FWD        | manual       | petrol    | 1.4             | 85         | 155       | 2024-05-28 17:17:17 |
| 7  | 8           | 6        | Coolray              | CUV       | 2020-08-13      | 14390  | 94380   | blue    | FWD        | automatic    | petrol    | 1.5             | 177        | 210       | 2024-04-20 19:20:00 |
| 8  | 49          | 7        | Sport Spider         | roadster  | 1996-09-13      | 66990  | 35821   | yellow  | RWD        | manual       | petrol    | 2.0             | 150        | 220       | 2024-03-18 18:18:18 |
| 9  | 26          | 10       | Bronco Raptor        | SUV       | 2022-04-19      | 75990  | 14589   | orange  | AWD        | automatic    | petrol    | 3.0             | 400        | 209       | 2024-01-25 08:18:40 |
| 10 | 5           | 3        | Corvette C2         | coupe     | 1963-10-09      | 105890 | 66238   | orange  | RWD        | manual       | petrol    | 5.4             | 360        | 233       | 2024-10-10 11:17:07 |
| 11 | 44          | 9        | Tavascan             | CUV       | 2023-09-17      | 48995  | 2380    | silver  | AWD        | automatic    | electric   | 0.0             | 306        | 180       | 2024-06-20 21:21:21 |
| 12 | 10          | 21       | 124 Sport Spider     | roadster  | 1973-10-29      | 35790  | 63902   | red     | RWD        | manual       | petrol    | 1.8             | 110        | 193       | 2024-08-10 12:12:12 |
| 13 | 24          | 1        | GR86                 | coupe     | 2014-01-12      | 17650  | 46595   | white   | RWD        | manual       | petrol    | 2.4             | 228        | 225       | 2024-02-10 13:15:42 |
| 14 | 33          | 11       | Note e-Power Nismo   | hatchback | 2022-05-16      | 34990  | 29856   | yellow  | FWD        | automatic    | hybrid     | 1.2             | 134        | 185       | 2024-05-02 18:28:38 |
| 15 | 17          | 19       | RX-7                 | coupe     | 1992-08-20      | 27000  | 36573   | black   | RWD        | manual       | petrol    | 1.3             | 255        | 250       | 2024-02-02 17:35:53 |
| 16 | 29          | 10       | Fiesta ST            | hatchback | 2020-02-20      | 27990  | 23543   | yellow  | FWD        | manual       | petrol    | 1.5             | 197        | 225       | 2024-04-15 16:45:07 |
| 17 | 42          | 5        | 944 Turbo            | coupe     | 1989-10-03      | 37990  | 167551  | black   | RWD        | manual       | petrol    | 2.5             | 250        | 241       | 2024-07-30 11:00:00 |
| 18 | 1           | 14       | 2002                 | sedan     | 1973-08-10      | 39990  | 145830  | white   | RWD        | manual       | petrol    | 2.0             | 120        | 193       | 2024-03-25 14:33:33 |
| 19 | 38          | 4        | One-77               | coupe     | 2012-03-27      | 2290600| 8657    | silver  | RWD        | automatic    | petrol    | 7.3             | 750        | 354       | 2024-09-12 19:19:19 |
| 20 | 47          | 12       | R8                   | cabriolet | 2012-01-29      | 85990  | 67006   | black   | AWD        | manual       | petrol    | 4.2             | 420        | 300       | 2024-11-07 12:12:12 |
| 21 | 12          | 17       | 190E                 | sedan     | 1989-08-03      | 8990   | 212345  | black   | RWD        | manual       | petrol    | 2.6             | 158        | 210       | 2024-09-01 11:09:09 |
| 22 | 40          | 13       | 458 Italia           | cabriolet | 2011-10-06      | 198990 | 29034   | silver  | RWD        | automatic    | petrol    | 4.5             | 570        | 325       | 2024-01-15 11:30:07 |
| 23 | 23          | 1        | Land Cruiser         | SUV       | 2009-03-05      | 36990  | 131055  | black   | AWD        | automatic    | petrol    | 5.7             | 381        | 209       | 2024-10-05 18:18:18 |
| 24 | 6           | 19       | 3 Turbo              | hatchback | 2021-11-10      | 21300  | 16903   | blue    | AWD        | automatic    | petrol    | 2.5             | 250        | 250       | 2024-08-25 22:25:25 |
| 25 | 21          | 8        | Niva                 | SUV       | 2020-07-12      | 9890   | 44693   | green   | AWD        | manual       | petrol    | 1.7             | 80         | 140       | 2024-04-06 19:22:22 |
| 26 | 35          | 14       | M4 F82               | coupe     | 2017-09-07      | 60990  | 54382   | red     | RWD        | automatic    | petrol    | 3.0             | 425        | 250       | 2024-10-21 14:44:44 |
| 27 | 11          | 7        | Alpine A110          | coupe     | 2020-03-05      | 73950  | 13394   | blue    | RWD        | automatic    | petrol    | 1.8             | 252        | 251       | 2024-05-20 15:07:47 |
| 28 | 48          | 17       | AMG GT               | roadster  | 2022-06-30      | 205990 | 18343   | white   | RWD        | automatic    | petrol    | 4.0             | 720        | 312       | 2024-10-15 16:25:33 |
| 29 | 15          | 16       | Ram 1500             | pickup    | 2019-07-22      | 46990  | 28304   | black   | RWD        | automatic    | petrol    | 5.7             | 395        | 193       | 2024-06-28 11:11:11 |
| 30 | 34          | 10       | Mustang GT           | cabriolet | 2021-12-25      | 55990  | 21060   | white   | RWD        | automatic    | petrol    | 5.0             | 450        | 250       | 2024-08-07 19:15:00 |
| 31 | 2           | 2        | Aventador            | roadster  | 2017-09-15      | 335200 | 19580   | red     | AWD        | automatic    | petrol    | 6.5             | 730        | 349       | 2024-01-20 16:05:25 |
| 32 | 25          | 5        | Cayman               | coupe     | 2019-02-24      | 98990  | 24309   | blue    | RWD        | manual       | petrol    | 2.0             | 300        | 265       | 2024-02-18 20:50:11 |
| 33 | 39          | 11       | Juke                 | CUV       | 2012-04-22      | 21590  | 84906   | black   | FWD        | automatic    | petrol    | 1.6             | 134        | 186       | 2024-06-06 14:14:14 |
| 34 | 9           | 13       | F355                 | coupe     | 1998-04-13      | 74890  | 69057   | red     | RWD        | manual       | petrol    | 3.5             | 375        | 295       | 2024-02-15 09:48:29 |
| 35 | 30          | 17       | 280 SL               | roadster  | 1971-12-03      | 163990 | 30500   | red     | RWD        | automatic    | petrol    | 2.8             | 170        | 210       | 2024-07-04 16:04:04 |
| 36 | 20          | 16       | Charger              | coupe     | 1973-06-09      | 55990  | 61043   | black   | RWD        | manual       | petrol    | 7.0             | 425        | 210       | 2024-03-01 10:05:55 |
| 37 | 41          | 18       | Beetle               | coupe     | 1972-09-10      | 4390   | 143502  | white   | RWD        | manual       | petrol    | 1.6             | 60         | 112       | 2024-07-15 09:45:00 |
| 38 | 4           | 20       | 156                  | sedan     | 2004-06-09      | 8990   | 123860  | silver  | FWD        | manual       | diesel    | 2.0             | 180        | 205       | 2024-11-01 21:01:01 |
| 39 | 13          | 15       | Defender             | SUV       | 2022-01-03      | 85990   | 20003   | green   | AWD        | automatic    | diesel    | 3.0             | 350        | 193       | 2024-09-07 13:07:07 |
| 40 | 32          | 4        | Vantage V8           | roadster  | 2021-03-14      | 167990  | 12305   | red     | RWD        | automatic    | petrol    | 4.0             | 503        | 314       | 2024-05-12 11:01:01 |
| 41 | 46          | 9        | Born                 | hatchback | 2021-01-19      | 37990   | 4650    | green   | RWD        | automatic    | electric   | 0.0             | 231        | 160       | 2024-01-10 09:45:12 |
| 42 | 3           | 14       | Z3 M Coupe           | coupe     | 2000-11-24      | 42950   | 76920   | blue    | RWD        | automatic    | petrol    | 3.2             | 316        | 258       | 2024-01-30 12:55:10 |
| 43 | 16          | 3        | Corvette C7          | coupe     | 2017-04-01      | 86599   | 33578   | red     | RWD        | manual       | petrol    | 6.2             | 650        | 290       | 2024-06-01 10:10:10 |
| 44 | 36          | 16       | Challenger           | coupe     | 1971-11-09      | 73590   | 80490   | orange  | RWD        | manual       | petrol    | 7.2             | 425        | 217       | 2024-08-15 16:16:16 |
| 45 | 28          | 18       | Golf                 | hatchback | 1982-10-15      | 5690    | 254903  | silver  | FWD        | manual       | petrol    | 1.6             | 90         | 160       | 2024-02-05 14:33:33 |
| 46 | 50          | 12       | TT                   | coupe     | 2006-11-26      | 15990   | 125694  | red     | FWD        | manual       | petrol    | 2.0             | 211        | 250       | 2024-04-27 12:00:00 |
| 47 | 18          | 11       | 370Z                 | coupe     | 2020-02-18      | 44590   | 18544   | green   | RWD        | manual       | petrol    | 3.0             | 400        | 250       | 2024-08-01 15:15:15 |
| 48 | 27          | 10       | GT                   | coupe     | 2020-07-02      | 690000  | 3409    | silver  | RWD        | automatic    | petrol    | 3.5             | 660        | 348       | 2024-01-28 12:00:00 |
| 49 | 7           | 20       | Stelvio              | CUV       | 2024-02-16      | 94590   | 894     | white   | AWD        | automatic    | petrol    | 2.9             | 505        | 232       | 2024-08-05 15:27:39 |
| 50 | 43          | 6        | Atlas Pro            | CUV       | 2021-12-19      | 23550   | 46933   | silver  | FWD        | automatic    | petrol    | 2.0             | 190        | 210       | 2024-04-11 22:11:11 |
| 51 | 14          | 18       | Passat               | wagon     | 2019-04-12      | 30990   | 34504   | blue    | AWD        | manual       | diesel    | 2.0             | 240        | 209       | 2024-06-02 20:20:20 |
| 52 | 39          | 11       | GT-R                 | coupe     | 2021-05-01      | 145990  | 40012   | silver  | AWD        | automatic    | petrol    | 3.8             | 565        | 315       | 2024-04-01 17:05:05 |
| 53 | 22          | 3        | Silverado 1500       | pickup    | 2021-09-01      | 61390   | 18305   | green   | AWD        | automatic    | petrol    | 6.2             | 420        | 193       | 2024-05-09 13:13:13 |
| 54 | 5           | 7        | Megane RS            | hatchback | 2021-06-12      | 45990   | 13510   | red     | FWD        | manual       | petrol    | 1.8             | 300        | 250       | 2024-10-28 10:10:10 |
| 55 | 24          | 12       | A5 3.0 TDI Quattro   | coupe     | 2015-02-28      | 4390    | 67324   | black   | AWD        | automatic    | diesel    | 3.0             | 245        | 250       | 2024-07-21 18:22:22 |
| 56 | 33          | 12       | e-tron               | CUV       | 2021-10-16      | 85290   | 29843   | white   | AWD        | automatic    | electric   | 0.0             | 402        | 200       | 2024-04-02 12:33:22 |
| 57 | 12          | 22       | 205 GTI              | hatchback | 1984-12-22      | 13390   | 232960  | white   | FWD        | manual       | petrol    | 1.6             | 105        | 190       | 2024-08-06 16:16:16 |
| 58 | 30          | 16       | Viper                | roadster  | 2006-05-30      | 100590  | 26505   | white   | RWD        | manual       | petrol    | 8.4             | 505        | 322       | 2024-02-25 17:25:00 |
| 59 | 20          | 15       | Range Rover Sport    | SUV       | 2018-01-25      | 109990  | 25088   | black   | AWD        | automatic    | diesel    | 3.0             | 355        | 225       | 2024-05-17 10:17:17 |
| 60 | 46          | 14       | i3                   | hatchback | 2020-05-14      | 37490   | 13554   | black   | RWD        | automatic    | electric   | 0.0             | 170        | 150       | 2024-06-15 15:15:15 |
| 61 | 1           | 14       | M550d xDrive         | sedan     | 2013-03-19      | 64990   | 87643   | black   | AWD        | automatic    | diesel    | 3.0             | 381        | 250       | 2024-03-22 12:12:12 |
| 62 | 19          | 10       | Mustang Mach-E       | CUV       | 2022-07-11      | 55990   | 6433    | blue    | AWD        | automatic    | electric   | 0.0             | 480        | 180       | 2024-01-16 13:30:45 |
| 63 | 29          | 14       | 335d                 | sedan     | 2010-01-30      | 24690   | 136890  | green   | RWD        | automatic    | diesel    | 3.0             | 286        | 250       | 2024-02-08 16:40:55 |
| 64 | 10          | 20       | Giulia               | sedan     | 2018-08-13      | 42190   | 56732   | red     | RWD        | automatic    | diesel    | 2.2             | 180        | 230       | 2024-03-30 09:09:09 |
| 65 | 38          | 13       | SF90 Stradale        | coupe     | 2020-05-19      | 945990  | 10803   | red     | AWD        | automatic    | hybrid     | 4.0             | 986        | 340       | 2024-04-13 14:14:14 |
| 66 | 45          | 18       | ID.4                 | CUV       | 2022-11-03      | 67990   | 5404    | white   | AWD        | automatic    | electric   | 0.0             | 300        | 161       | 2024-05-14 09:30:30 |
| 67 | 8           | 22       | 306 GTI-6            | hatchback | 1996-04-13      | 9990    | 143569  | yellow  | FWD        | manual       | petrol    | 2.0             | 167        | 220       | 2024-06-05 17:55:11 |
| 68 | 41          | 2        | Urus                 | SUV       | 2021-03-06      | 200500  | 21532   | silver  | AWD        | automatic    | petrol    | 4.0             | 641        | 305       | 2024-07-29 19:22:22 |
| 69 | 3           | 11       | Leaf                 | hatchback | 2021-12-19      | 38490   | 26433   | silver  | FWD        | automatic    | electric   | 0.0             | 147        | 157       | 2024-08-24 13:15:15 |
| 70 | 11          | 10       | Focus RS TDCi        | hatchback | 2016-04-05      | 44290   | 76544   | blue    | AWD        | manual       | diesel    | 2.0             | 250        | 250       | 2024-09-15 10:10:10 |
| 71 | 36          | 12       | RS4 Avant            | wagon     | 2007-06-08      | 40990   | 120405  | black   | AWD        | automatic    | petrol    | 4.2             | 420        | 250       | 2024-10-12 20:20:20 |
| 72 | 26          | 18       | Golf R TDI           | hatchback | 2021-11-24      | 41990   | 17643   | red     | AWD        | automatic    | diesel    | 2.0             | 200        | 250       | 2024-10-30 22:22:22 |
| 73 | 4           | 22       | 407 Coupe            | coupe     | 2006-07-07      | 14590   | 165987  | silver  | FWD        | automatic    | petrol    | 3.0             | 211        | 240       | 2024-11-02 11:11:11 |
| 74 | 50          | 5        | 911 Carrera S        | cabriolet | 2021-07-15      | 183990  | 19570   | silver  | RWD        | automatic    | petrol    | 3.0             | 443        | 307       | 2024-11-03 15:15:15 |
| 75 | 27          | 5        | Taycan               | sedan     | 2022-04-04      | 143990  | 8542    | green   | AWD        | automatic    | electric   | 0.0             | 616        | 250       | 2024-11-06 09:30:00 |
| 76 | 13          | 1        | Supra                | coupe     | 2022-07-09      | 40900   | 25697   | blue    | RWD        | automatic    | petrol    | 3.0             | 382        | 250       | 2024-04-22 18:00:00 |
</details>
