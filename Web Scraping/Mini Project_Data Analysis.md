# Melon Chart Analysis Project

## 데이터 분석

작성한 테이블에 삽입된 데이터 분석하기

### 데이터를 통해 분석하고자 하는 것

- 2012~2022 top100 중 가장 많이 순위권 든 노래 top15, 가수 top15
- top3 기획사 중, 가장 많이 이름을 올린 가수 top15
- 플랫폼별 2012~2022 1위곡 비교(melon, circle chart)
- 가장 많이 차트 인한 가수 top5 중, 연도별로 가장 많이 차트에 올라간 가수
- 질문 4에 속하면서 현재 가장 인기있는 아티스트 top5에도 속하는 가수의 팬 남녀, 연령대 비율
- 아티스트 랭킹 1~50위에 속하며 top100에도 속하는 가수들의 차트 인한 곡수와 종합 세부점수

---
#### 데이터 분석 시작

use melon;

select * from top100;<br>
select * from circle_digital_chart_top100;<br>
select * from artist_rank_top50;<br>
select * from artist_rank_top5;<br>

#### top100 중 2012~2022 가장 많이 순위권에 든 노래 top15

select singer_name 가수명, song_name 곡명, count(song_name) 횟수, likes 좋아요<br>
  from top100<br>
  group by song_name<br>
  order by 3 desc<br>
  limit 15;<br>
  
#### top100 중 2012~2022 가장 많이 순위권에 든 가수 top15

select singer_name 가수명, count(singer_name) 횟수<br>
  from top100<br>
  group by singer_name<br>
  order by 2 desc<br>
  limit 15;<br>
  
#### circle_digital_chart_top100 중 기획사 많은 순 top15

select production 기획사, count(production) 횟수<br>
  from circle_digital_chart_top100<br>
  group by production<br>
  order by count(production) desc<br>
  limit 15;<br>

#### 기획사 많은 top3에 속하는 가수들 top15

select production 기획사, count(production) 횟수, singer_name 가수명<br>
  from circle_digital_chart_top100<br>
  where production = 'YG Entertainment' <br>
        or production = 'Stone Music Entertainment' 
        or production = 'SM Entertainment'<br>
  group by singer_name<br>
  order by count(production) desc<br>
  limit 15;<br>
  
#### circle_digital_chart_top100 중 기획사 적은 순 top30

select song_name, singer_name, production, count(production) 횟수<br>
  from circle_digital_chart_top100<br>
  group by production<br>
  order by count(production) asc<br>
  limit 30;<br>
  
#### 연도별 top3 노래 (melon)

select years, ranks, song_name, singer_name<br>
  from top100<br>
  where ranks <= 3<br>
  order by 1;<br>
  
#### 연도별 top3 노래 (circle chart)

select year, ranks, song_name, singer_name<br>
  from circle_digital_chart_top100<br>
  where ranks <= 3<br>
  order by 1;<br>

#### 연도별 top 노래 (melon + circle chart)

select a.years, a.ranks, a.song_name, a.singer_name, b.song_name, b.singer_name<br>
  from top100 a<br>
  left join circle_digital_chart_top100 b<br>
    on a.years = b.year<br>
  where a.ranks <= 1 and b.ranks <= 1<br>
  group by a.years<br>
  order by 1;<br>
  
#### 가장 많이 차트 인한 가수 top5

select singer_name, count(singer_name)<br>
  from top100<br>
  group by singer_name<br>
  order by count(singer_name) desc<br>
  limit 5;
  
#### 역대 가장 많이 차트 인 한 가수 중에 현재 top5인 아티스트의 팬 남녀, 연령대 비율

select a.singer_name, count(a.singer_name) 차트인횟수, b.man_share, b.woman_share, b.teenager, b.twenty, b.thirty, b.forty, b.fifty, b.others<br>
  from top100 a<br>
  left join artist_rank_top5 b<br>
    on a.singer_name = b.singer_name<br>
  group by singer_name<br>
  order by count(singer_name) desc<br>
  limit 2;
  
#### 현재 가장 인기있는 아티스트 top5의 팬 남녀 비율, 연령대 비율

select * from artist_rank_top5;

#### 아티스트 랭킹 1~50위에 속하며 top100에도 속하는 가수들의 차트 인 곡수와 종합 세부점수

select b.singer_name,  a.fans, a.ranks 'artist rank', count(b.song_name) 차트인곡수,<br>
 round(detail_score_music + detail_score_ascending_fans + detail_score_likes + detail_score_photo + detail_score_video, 2) '세부점수 총점 50점'<br>
  from artist_rank_top50 a<br>
  inner join top100 b<br>
    on a.singer_name = b.singer_name<br>
    group by a.singer_name<br>
    order by a.ranks;
    
#### 종합 세부점수가 높은 가수순

select ranks, singer_name, round(detail_score_music + detail_score_ascending_fans + detail_score_likes + detail_score_photo + detail_score_video, 2) '세부점수 총점 50점',<br>
detail_score_music, detail_score_ascending_fans, detail_score_likes, detail_score_photo, detail_score_video, fans<br>
 from artist_rank_top50<br>
 order by 3 desc;

#### 각 연도별로 가장 많이 차트에 올라간 가수

select years, singer_name, count(singer_name) 곡수<br>
  from top100<br>
  where singer_name = '아이유' or singer_name = '방탄소년단' or singer_name = '볼빨간사춘기' or singer_name = 'TWICE (트와이스)' or singer_name = '다비치'<br>
  group by years<br>
  order by 1 asc;


select * from top100;<br>
select * from circle_digital_chart_top100;<br>
select * from artist_rank_top50;<br>
select * from artist_rank_top5;

#### 플랫폼별 각 연도의 top1 가수 (melon, circle chart)

create view melon_v as -- 멜론차트 뷰만들기<br>
with top_rank as<br>
(<br>
select years, ranks, song_name<br>
  from top100<br>
  where ranks = 1<br>
  group by 1, 2<br>
  order by 1, 2<br>
)<br>
select ranks,<br>
       case when years = 2012 then song_name else 0 end year_2012,<br>
       case when years = 2013 then song_name else 0 end year_2013,<br>
       case when years = 2014 then song_name else 0 end year_2014,<br>
	   case when years = 2015 then song_name else 0 end year_2015,<br>
       case when years = 2016 then song_name else 0 end year_2016,<br>
	   case when years = 2017 then song_name else 0 end year_2017,<br>
       case when years = 2018 then song_name else 0 end year_2018,<br>
       case when years = 2019 then song_name else 0 end year_2019,<br>
       case when years = 2020 then song_name else 0 end year_2020,<br>
       case when years = 2021 then song_name else 0 end year_2021,<br>
       case when years = 2022 then song_name else 0 end year_2022<br>
from top_rank;

create view circle_v as -- 써클차트 뷰 만들기<br>
with top_rank as<br>
(<br>
select years, ranks, song_name<br>
  from circle_digital_chart_top100<br>
  where ranks = 1<br>
  group by 1, 2<br>
  order by 1, 2<br>
)<br>
select ranks,<br>
       case when years = 2012 then song_name else 0 end year_2012,<br>
       case when years = 2013 then song_name else 0 end year_2013,<br>
       case when years = 2014 then song_name else 0 end year_2014,<br>
       case when years = 2015 then song_name else 0 end year_2015,<br>
       case when years = 2016 then song_name else 0 end year_2016,<br>
       case when years = 2017 then song_name else 0 end year_2017,<br>
       case when years = 2018 then song_name else 0 end year_2018,<br>
       case when years = 2019 then song_name else 0 end year_2019,<br>
       case when years = 2020 then song_name else 0 end year_2020,<br>
       case when years = 2021 then song_name else 0 end year_2021,<br>
       case when years = 2022 then song_name else 0 end year_2022<br>
   from top_rank<br>
   group by years;
   
select * from melon_v;<br>
select ranks 순위, '멜론차트' 차트종류, -- union으로 이어주기 , max로 값이 1인 값만 불러오기<br>
max(year_2012) '2012년', max(year_2013) '2013년', max(year_2014) '2014년', max(year_2015) '2015년',<br>
max(year_2016) '2016년', max(year_2017) '2017년', max(year_2018) '2018년',max(year_2019) '2019년',<br>
max(year_2020) '2020년', max(year_2021) '2021년', max(year_2022) '2022년' from melon_v<br>
union<br>
select ranks 순위, '서클차트' 차트종류,<br>
max(year_2012) '2012년', max(year_2013) '2013년', max(year_2014) '2014년', max(year_2015) '2015년',<br>
max(year_2016) '2016년', max(year_2017) '2017년',max(year_2018) '2018년',max(year_2019) '2019년',<br>
max(year_2020) '2020년', max(year_2021) '2021년',max(year_2022) '2022년' from circle_v;
