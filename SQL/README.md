# StudyForJober
Joberになるために必要な勉強

## SQL
- インプット
  - ER図作成
  - テーブル操作
- アウトプット
  - [SQL練習問題 – 一覧まとめ](https://tech.pjin.jp/blog/2016/12/05/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E4%B8%80%E8%A6%A7%E3%81%BE%E3%81%A8%E3%82%81/)
  - [SQL練習問題 回答・解答・メモ](https://zenn.dev/itoo/articles/sql-practice)
  - チーム開発
  - tech-app
  - 学習サイト


## 解答
  - Q1
  各グループの中でFIFAランクが最も高い国と低い国のランキング番号を表示してください。
  ```
SELECT 
min(ranking) as "最上位", 
max(ranking) as "雑魚", 
group_name
FROM countries 
GROUP BY group_name LIMIT 0,100
  ```

  - Q2
  全ゴールキーパーの平均身長、平均体重を表示してください

  ```
SELECT
avg(height) as "平均身長",
avg(weight) as "平均体重"
FROM players
where position = "GK" LIMIT 0,100
  ```

  - Q3
  各国の平均身長を高い方から順に表示してください。ただし、FROM句はcountriesテーブルとしてください。
  ```
SELECT 
countries.name as "国名", 
avg(height)
FROM countries
join players
on country_id = countries.id 
group by countries.name 
order by avg(height) DESC LIMIT 0,100
  ```

  - Q4
  各国の平均身長を高い方から順に表示してください。ただし、FROM句はplayersテーブルとして、テーブル結合を使わず副問合せを用いてください。

  ```
  SELECT (SELECT c.name FROM countries c WHERE p.country_id = c.id) AS 国名, AVG(p.height) AS 平均身長
FROM players p
GROUP BY p.country_id
ORDER BY AVG(p.height) DESC
  ```

  - Q5
  キックオフ日時と対戦国の国名をキックオフ日時の早いものから順に表示してください。
  ```
  SELECT * FROM pairings_tmp 
ORDER BY kickoff ASC LIMIT 0,100
  ```