# フリマアプリ_DB設計 (76期/チームB) 


## ①usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false|
|password|string|null: false|
|last_name|string|null: false|
|first_name|string|null: false|
|last_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birthday|date|null: false|

### Association
- has_many :products
- has_one :address
- has_one :credit

### index
- add_index :users, :email,unique: true

## ②productsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|name|string|null: false|
|content|string|null: false|
|bland_name|string||
|price|integer|null: false|
|product_status_id|integer|null: false|
|delively_cost_id|integer|null: false|
|prefecture_id|integer|null: false|
|delively_days_id|integer|null: false|

### Association
- belongs_to :user
- belongs_to_active_hash :product_status
- belongs_to_active_hash :delively_cost
- belongs_to_active_hash :prefecture
- belongs_to_active_hash :delively_days
- has_many :product_categories
- has_many :categories, through: :product_categories
- has_many :images

## ③product_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|category_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :product
- belongs_to :category

## ④categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### Association
- has_many :product_categories
- has_many :products, through: :product_categories

## ⑤imagesテーブル
|Column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|name|string|null: false|

### Association
- belongs_to :product

## ⑥addressesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|delively_last_name|string|null: false|
|delively_first_name|string|null: false|
|delively_last_name_kana|string|null: false|
|delively_first_name_kana|string|null: false|
|postcode|string|null: false|
|prefecture_id|integer|null: false|
|city|string|null: false|
|block|string|null: false|
|building|string||
|phone_number|string||

### Association
- belongs_to :user
- belongs_to_active_hash :prefecture

## ⑦creditsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|code|string|null: false|

### Association
- belongs_to :user

