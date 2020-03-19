# 作成目的
最近趣味で動画編集を始めた際、専門的に編集技術をアウトプットできるかつトラブルシューティングできるサイトが存在しなかったため
動画編集者版Qiitaのような物を作ってみたかった

#### [Editmaster](http://www.editmasterhub.com/)

## 搭載機能
### 実装
Markdownによる投稿機能  
検索機能  
タグ機能  

### 実装予定
いいね機能
コミュニティ機能

## version
ruby 2.5.7  
Rails 5.2.3  
mysql 0.5.2  

## DB設計 

### usersテーブル

|Column|Type|Options|
|------|----|-------|
|image|string|
|nickname|string|null: false,index: true|
|mail|string|null: false, unipue: true|

#### Association
- has_many :articles
- has_many :comments
- has_many :groups, through: :group_users
- has_many :group_users

### groupsテーブル

|Column|Type|Options|
|------|----|-------|
|group_name|string|null: false, unipue: true|

#### Association
- has_many :users, through: :group_users
- has_many :group_users
- has_many :articles


### groups_usersテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

#### Association
- belongs_to :group
- belongs_to :user

### articlesテーブル

|Column|Type|Options|
|------|----|-------|
|title|text|null: false,index: true|
|text|text|null: false,index: true|
|image|string|null: true|
|user_id|integer|foreign_key: true|


#### Association
- belongs_to :user
- has_many :comments


### commentsテーブル

|Column|Type|Options|
|------|----|-------|
|text|text|null: false|
|image|string|null: true|
|user_id|integer|null: false, foreign_key: true|
|article_id|integer|null: false, foreign_key: true|

#### Association
- belongs_to :article
- belongs_to :user# editgate
