# 仕様書

機能仕様

[目的]
飲食業界に転職したい人が、その店でどういうことが学べるか、どんな人と働くことになるのかがもっと明確にわかるように。
無料では出せないレシピ、技、経営ノウハウ等を有料コンテンツとして販売。飲食業界の副業になれば。

[登場人物]
・様々な飲食店で働いている職人、シェフ、等を総じて「chef」とする。
・飲食店への転職を希望する人、飲食業界や料理についての情報を得たい人を総じて「user」とする。

[詳細機能]
・chef, user 共に自己紹介を登録する。「career」
・chefは自分のお店を登録する。「restaurant」
・chefのみ、有料コンテンツを作成できる。「note」
・とりあえずはuserのみ、noteの購入が可能。「order」（後々はchefも購入可能にする。)






# テーブル設計

## users テーブル
| Column             | Type   | Options     |
| ------------------ | ------ | ----------- |
| email              | string | null: false |
| encrypted_password | string | null: false |
| nickname           | string | null: false |
| last_name          | string | null: false |
| first_name         | string | null: false |
| last_name_kana     | string | null: false |
| first_name_kana    | string | null: false |

### Association

- has_one  :career
- has_many :orders



## chefs テーブル
| Column             | Type   | Options     |
| ------------------ | ------ | ----------- |
| email              | string | null: false |
| encrypted_password | string | null: false |
| last_name          | string | null: false |
| first_name         | string | null: false |
| last_name_kana     | string | null: false |
| first_name_kana    | string | null: false |

### Association

- has_one  :career
- has_many :orders
- has_many :chefs_restaurants
- has_many :restaurants, through: :chefs_restaurants
- has_many :notes



## restaurants テーブル
| Column        | Type    | Options     |
| ------------- | ------- | ----------- |
| image         |         |             |
| name          | string  | null: false |
| address       | string  | null: false |
| average_price | string  | null: false |
| info          | text    | null: false |
| employment_id | integer | null: false |
| occupation    | string  | null: false |
| shift         | string  | null: false |
| holiday       | string  | null: false |
| salary        | text    | null: false |
| genre_id      | integer | null: false |
| treatment     | text    | mull: false |
| statue        | text    | null: false |


### Association

- has_many :chefs_restaurants
- has_many :chefs, through: chefs_restaurants



## chefs_restaurants テーブル
| Column        | Type       | Options           |
| ------------- | ---------- | ----------------- |
| chef_id       | references | foreign_key: true |
| restaurant_id | references | foreign_key: true |

### Association

- belongs_to :chef
- belongs_to :restaurant



## notes テーブル
| Column | Type    | Options     |
| ------ | ------- | ----------- |
| title  | string  | null: false |
| info   | text    | null: false |
| price  | integer | null: false |

### Association

- belongs_to :chef
- has_one    :order



## orders テーブル
| Column  | Type       | Options           |
| ------- | ---------- | ----------------- |
| user_id | references | foreign_key: true |
| chef_id | references | foreign_key: true |
| note_id | references | foreign_key: true |

### Association

- belongs_to :user
- belongs_to :chef
- belongs_to :note


