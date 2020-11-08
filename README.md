## users

|Column          |Type    |Options                      |
|----------------|--------|-----------------------------|
|nickname        |string  |null:false                   |
|email           |string  |null:false,uniqueness:true   |
|password        |string  |null:false,uniqueness:true   |
|family_name     |string  |null:false                   |
|first_name      |string  |null:false                   |
|family_name_kana|string  |null:false                   |
|first_name_kana |string  |null:false                   |
|birth_day       |date    |null:false                   |

### Association

- has_many :items
_ has_many :purchases

## items

|Column            |Type            |Options                      |
|------------------|-----------------|----------------------------|
|name              |string          |null:false                   |
|price             |integer         |null:false                   |
|user              |references      |null:false, foreign_key:true |
|category_id       |integer         |null:false                   |
|condition_id      |integer         |null:false                   |
|shipping_charge_id|integer         |null:false                   |
|shipping_date_id  |integer         |null:false                   |
|prefecture_id     |integer         |null:false                   |
|images_id         |integer         |null:false                   |
|description       |text            |null:false                   |

### Association

- belongs_to :users
- has_one :purchase
- has_many :images
- belongs_to :category
- belongs_to :condition
- belongs_to :shipping_charge
- belongs_to :shipping_date
- belongs_to :prefecture


## purchases

|Column  |Type             |Options                         |
|--------|-----------------|--------------------------------|
|item    |references       |null:false, foreign_key:true    |
|user    |references       |null:false, foreign_key:true    |

### Association

- belongs_to :users
- belongs_to :items
- has_one :shipping_addressees

## shipping_addressees

|Column            |Type             |Options                      |
|------------------|-----------------|-----------------------------|
|postal_cord       |string           |null:false                   |
|prefectures_id    |integer          |null:false, foreign_key:true |
|municipality      |string           |null:false                   |
|building_name     |string           |                             |
|phone_number      |string           |null:false, uniqueness:true  |
|purchases         |references       |null:false, foreign_key:true |

 ### Association

 - belongs_to :purchases
 - belongs_to :prefecture

## images

|Column   |Type             |Options                            |
|---------|-----------------|-----------------------------------|
|image    |string           |null:false                         |
|item     |references       |null:false, foreign_key:true       |

### Association

- belongs_to :items

## category

|Column   |Type     |Options         |
|---------|---------|----------------|
|category |string   |null:false      |

### Association

- has_many :items

## condition

|Column     |Type    |Options      |
|-----------|--------|-------------|
|condition  |string  |null:false   |

### Association

- has_many :items

# shipping_charge

|Column          |Type    |Options     |
|----------------|--------|------------|
|shipping_charge |string  |null:false  |

### Association

- has_many :items

## shipping_date

|column         |Type    |Options    |
|---------------|--------|-----------|
|shipping_date  |string  |null:false |

### Association

- has_many :items

## prefecture

|column     |Type   |Options    |
|-----------|-------|-----------|
|prefecture |string |null:false |

### Association

- has_many :items
- has_many :shipping_addressees