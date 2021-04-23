# アプリ名
 booster

# 概要
 NBA（バスケ）ファンの交流・チャットアプリ

# 制作背景
 日本ではあまりフィーチャーされていないNBAを盛り上げたい。
 NBAファンが気軽に情報共有などができるアプリが欲しかった。

# 実装予定の内容
 ・ユーザー管理機能
 ・タイムライン機能
 ・チャット機能
 ・チャットルーム作成機能
 ・画像投稿機能
 ・評価機能
 ・コメント機能

# DB設計

## users テーブル

| Column    | Type       | Options     |
| --------- | ---------- | ----------- |
| nickname  | string     | null: false |
| email     | string     | null: false |
| password  | string     | null: false |

### Association

- has_one :team
- has_many :locker_room_users
- has_many :locker_rooms, through: locker_room_users
- has_many :comment

## teams テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |

belongs_to :user

## locker_rooms テーブル

| Column    | Type    | Options     |
| --------- | ------- | ----------- |
| name      | string  | null: false |

### Association

- has_many :locker_room_users
- has_many :users, through: locker_room_users
- has_many :comment

## locker_room_users テーブル

| Column    | Type       | Options                        |
| --------- | -------    | ------------------------------ |
| user      | references | null: false, foreign_key: true |
| team      | references | null: false, foreign_key: true |

### Association

- belongs_to :locker_room
- belongs_to :user

## comments テーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| content          | string     |                                |
| user             | references | null: false, foreign_key: true |
| locker_room      | references | null: false, foreign_key: true |

### Association

- belongs_to :locker_room
- belongs_to :user


## trash_talks テーブル

| Column  |   Type     | Options                        |
| ------- | ---------- | ------------------------------ |
| content | string     |                                |
| user    | references | null: false, foreign_key: true |

### Association

- belongs_to :user