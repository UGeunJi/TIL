### 데이터베이스 생성
```
CREATE DATABASE mywork;
create database if not exists mywork;
```

### 데이터베이스 삭제
```
DROP database mywork;
drop database if exists mywork;
```

### 데이터베이스 진입
```
USE mywork;
```
### 테이블 생성
```
create table if not exists highschool_students(
  student_no varchar(20) not null primary key,
  student_name varchar(100) not null,
  grade tinyint,
  class varchar(20),
  gender varchar(20),
  age smallint,
  enter_date date
);
```

### 생성된 테이블 정보 확인
```
desc highschool_students;
```
```
drop table if exists highschool_students;
```
### 기본키 설정 방법 (method 1)
```
create table if not exists highschool_students(
  student_no varchar(20) not null primary key,
  student_name varchar(100) not null,
  grade tinyint,
  class varchar(20),
  gender varchar(20),
  age smallint,
  enter_date date
);
```
### 기본키 설정 방법 (method 2)
```
create table if not exists highschool_students(
  student_no varchar(20) not null,
  student_name varchar(100) not null,
  grade tinyint,
  class varchar(20),
  gender varchar(20),
  age smallint,
  enter_date date,
  constraint primary key (student_no)
);
```
```
drop table if exists highschool_students;
```
### 기본키 설정 방법 (method 3)
```
create table if not exists highschool_students(
  student_no varchar(20) not null,
  student_name varchar(100) not null,
  grade tinyint,
  class varchar(20),
  gender varchar(20),
  age smallint,
  enter_date date
);
```
```
desc highschool_students;
```
```
alter table highschool_students
add primary key (student_no);
```
```
desc highschool_students;
```
### (실습)
- my_first_table이라는 테이블을 만드려고 합니다.
--(1) 각 컬럼의 내용을 보고 어떤 데이터 타입을 사용하면 될지 데이터 타입 항목을 채우세요.

-- 항목		컬럼명			컬럼설명				데이터 타입 <br>
-- 사번		employee_id		숫자 1에서 300까지 할당	smallint <br>
-- 이름		employee_name	문자					varchar(20)  -- varchar()과 char()의 차이: char은 무조건 할당된 수만큼 출력하고 varchar은 유동적이다. <br>
-- 급여		salary			사원의 급여			int <br>
-- 입사일자	hire_date		날짜					date

- (2) 위 데이터 타입을 기준으로 my_first_table이라는 SQL문을 작성하세요.
```
create table if not exists my_first_table(
  employee_id smallint,
  employee_name varchar(20),
  salary int,
  hire_date date
);
```
```
desc my_first_table;
```
- (3) 위에서 생성한 테이블을 삭제하는 SQL문을 작성하세요.
```
drop table if exists my_first_table;
```
- (4) (2)에서 작성한 테이블 생성 문장을 참고해 사전 컬럼(employee_id)을 기본 키로 하는 테이블을 다시 만드세요.

### method 1
```
create table if not exists my_first_table(
  employee_id smallint not null primary key,   -- primary를 지정하는 순간 not null인 것으로 설정된다.
  employee_name varchar(20)not null,
  salary int,
  hire_date date
);
```
```
desc my_first_table;
```
### method 2
```
create table if not exists my_first_table(
  employee_id smallint not null,
  employee_name varchar(20)not null,
  salary int,
  hire_date date
);
```
```
alter table my_first_table
add primary key (employee_id);
```
```
desc my_first_table;
```
### method 3
```
create table if not exists my_first_table(
  employee_id smallint not null,
  employee_name varchar(20)not null,
  salary int,
  hire_date date,
  constraint primary key (employee_id)
);
```
```
desc my_first_table;
```
```
desc box_office;
```

### box_office 테이블의 모든 컬럼 조회하기
```
desc box_office;
```
```
select *   -- 모든 컬럼
  from box_office;
```
```
select count(*)   -- 해당 테이블의 행의 수가 몇 개인지를 집계
  from box_office;
```
### 다른 데이터베이스의 테이블 조회하기
```
select *
  from world.city;
```
```
select count(*)
  from world.city;
```
### where절로 조회 조건 지정하기
```
select *
 from world.city
 where CountryCode = 'KOR';
```
### like로 같은 문자열 조회하기 
```
use world;
```
```
select *
  from city
  where district like 'k%';  -- district 컬럼에 해당하는 값 중에 k로 시작하는 문자열이 있으면 True
```
```
select *
  from city
  where district like '%k';  -- district 컬럼에 해당하는 값 중에 k로 끝나는 문자열이 있으면 True
```
```
select *
  from city
  where district like '%k%';  -- district 컬럼에 해당하는 값 중에 k가 중간에 포함된 문자열이 있으면 True
```
```
select district, Name, population
  from city
  where district like '%k';
```  
### 논리 연산자
```
select *
  from city
  where countrycode = 'kor' and population > 300000 ;
```  
### in 연산자
```
select *
  from city
  where district in('seoul', 'kyonggi');
  -- where district = 'seoul' or district = 'kyonggi';
```
### country 테이블 조회하기
```
select * from country;
```
### 인구가 4500만명 이상, 5500만명 이하인 name, continent, population, region
```
select name, population, Region, continent
  from country
  where population >= 45000000 and population <= 55000000;
```  
### between ~ and ~로 위와 같은 결과
```
select name, population, Region, continent
  from country
  where population between 45000000 and 55000000;
```
```
use mywork;
select * from box_office;
```

### 내가 여기서 어떤 코멘트를 달아도 코드로 간주하지 않음
```
/*
여러 문장을 넣어도
모두 주석으로
처리됨
*/
```
```
/*
(테이블) box_office table : 2004~2019년까지 개봉된 영화 정보
-- seq_no : 일련번호, 기본키
-- years : 제작연도
-- ranks : 순위
-- movie_name : 영화명
-- release_date : 개봉일
-- sale_amt : 매출액
-- share_rate : 점유율(매출액 기준)
-- audience_num : 관객수
-- screen_num : 스크린수
-- showing_count : 상영횟수
-- rep_country : 대표국적
-- countries : 국적
-- distributor : 배급사
-- movie_type : 유형(장편, 단편, ...)
-- genre : 장르(스릴러, 액션..)
-- director : 감독
*/
```
```
desc box_office;
```
### (실습)
- 2018년에 개봉한 한국 영화 조회하기
```
select *
  from box_office
  where release_date between '2018-01-01' and '2018-12-31' and rep_country = '한국';
```
```
select *
  from box_office
  where release_date like '2018%' and rep_country = '한국';
```  
- 2019년 개봉 영화 중 관객수가 500만명 이상인 영화 조회하기
```
select *
  from box_office
  where release_date like '2019%' and audience_num >= 5000000;
```
- 2019년 개봉 영화 중 관객수가 500만명 이상이거나 매출액이 400억원 이상인 영화 조회하기
```
select *
  from box_office
  where release_date like '2019%' and  (audience_num >= 5000000 or sale_amt >= 40000000000);
```  
```  
use world;
select id, name, population / 10000 as 'population(만명단위)'
 from city;
```

### 데이터 정렬하기
- country 테이블에서 population이 1억명 이상인 나라에 대해 내림차순 정렬하되,
- code, name, continent, region, population 가져오기

```
select code, name, continent, population, region
 from country
 where population >= 100000000
 order by population desc;
```  
- 컬럼명 대신 순번(4)으로 대체해서 위의 코드와 동일한 결과 출력
```
select name, code, continent, population, region
 from country
 where population >= 100000000
 order by 4 desc;
```

### (실습) 
- country 테이블에서 population이 5천만명 이상인 나라에 대해
- continent 오름차순 정렬한 뒤,
- name, continent, region 가져오기
```
desc country;
```
```
select name, continent, region
  from country
  where population >= 50000000
  order by continent asc, region desc;
```  
### (실습)
- city 테이블에서 우리나라에 속한 도시에 대해
- 도시명은 오름차순, 인구는 내림차순으로 조회하기
```
desc city;
```
```
select *
  from city
  where countrycode = 'KOR'
  order by name asc, population desc;
```
```
use mywork;
select * from box_office
  limit 10;
```  
### (실습)
- 2019년 개봉 영화 중에 관객이 500만명 이상인 데이터에 대해
- 매출액 기준 내림차순으로 정렬한 뒤, 상위 5건만 가져오기
```
desc box_office;
```  
### (실습)
- 2019년 개봉영화중에 관객이 500만명 이상인 데이터에 대해
- 매출액 기준 내림차순 정렬한 뒤, 상위 5건만 가져오기

```
select * from box_office
  where release_date like '2019%' and audience_num >= 5000000
  order by sale_amt asc
  limit 5;
```

### (실습)
- world database의 countrylanguage table에 국가별 사용 언어가 있고,
- 이 테이블 percentage 컬럼에는 해당 언어가 사용되는 비율값이 들어 있음
- 이 비율이 99% 이상인 것을 국가코드 순으로 조회하기

```
use world;
select * from countrylanguage
  where percentage >= 99
  order by countrycode;
```
### (실습)
- world database에 접속된 상태에서 mywork database에 있는 box_office 테이블에서
- 2019년 제작된 영화중 순위(ranks)가 1위에서 10위까지인 영화를 순위(ranks)로 조회하기

```
select * from mywork.box_office
  where years like '2019%'
  order by ranks
  limit 10;
```

### (실습)
- mywork database로 이동해 box_office 테이블에서
- 2019년 제작된 영화중 영화유형(movie_type)이 장편이 아닌 영화를 순위(ranks)대로 조회하기

```
use mywork;
desc box_office;
```
```
select * from box_office
  where years like '2019%' and movie_type != '장편'
  order by ranks;
```  
### (실습)
- box_office 테이블에서 2019년 제작된 영화 중 스크린수 기준 상위 10개 영화 조회하기
```
select * from box_office
  where years like '2019%'
  order by screen_num desc
  limit 10;
```
## SQL 함수 사용하기

### 수식 연산자
```
select 7+2;
select 7-2;
select 7/2, 7%3, 7 div 2;
```
### 숫자형 함수
```
select ceil(6.5);
select floor(6.5);
select mod(7, 2), 7%2;  -- 나머지 연산
select power(4, 3);  -- 제곱 연산
select sqrt(25);
select round(1153.456, 1), round(1153.456, 2);
select round(1153.456, 1), round(1153.456, -2);
select rand(9);  -- 0~1 사이의 무작위 수
```
### 문자형 함수
```
select char_length('sql');
select char_length('한글');
```
```
select length('sql');
select length('한글');
```
```
select concat('this', 'is', 'mysql');
select concat('this', null, 'mysql');
select concat_ws('__','this', 'is', 'mysql');
```
```
select format(550000000000000, 0);
```
```
select lower('ASD'), upper('ajwnd');
```
```
select lpad('sql', 7, '#');   -- left padding
select rpad('sql', 7, '#');   -- right padding
```
```
select left('thisismysql', 6);   -- 왼쪽부터 글자 떼어내기
select right('thisismysql', 6);   -- 오른쪽부터 글자 떼어내기
```
```
select reverse('sql');
```
```
select replace('생일 축하해 우근아', '우근', '재근');
```
```
select instr('abc', 'c');
select locate('c', 'abcabcabc', 7);   -- 어디서부터 찾을지도 설정 가능
select position('c' in 'abc');
```
```
select substring('this is mysql', 6, 2);
select substr('this is mysql', -8, 2);
select mid('this is mysql', 6);           -- substr, substring, mid 모두 같다.
```
```
select mid('this is mysql', 6) as mid_함수결과;
```
```
select trim('    mysql     ');    -- 공백제거
select trim(both ' ' from '    mysql     ');
select trim(both '*' from '*****mysql*****');
select trim(leading '*' from '*****mysql*****');
select trim(trailing '*' from '*****mysql*****');
```
```
select strcmp('mysql', 'mysql');
select strcmp('mysql1', 'mysql2');
select strcmp('mysql2', 'mysql1');
```

### (실습) 문자형 함수 사용
- world 데이터베이스에 접속해서 country table에서 인구가 4,500만명에서 5,500만명 사이에 있는 국가를 조회하되,
- 국가명(Name)과 대륙명(continent)을 연결해서 'Name (continent)' 형태로 조회하기
- (예: South Korea (Asia)) 
- 표시될 컬럼명: code, name, continent, name (continent)
```
use world;
desc country;
```
```
select code, name, continent;
select code, name, continent, concat(name, continent) as 'name (continent)'
from country
  where population between 45000000 and 55000000;
```
### (실습) 숫자형 함수 사용
- mywork 데이터베이스에 접속해 box_office 테이블에서 2019년 개봉한 한국 영화 중 관객수가 500만 명 이상인 영화를 조회
- 이 때 매출액은 1억으로 나눈 후 소수점 없이 반올림 한 결과를 표시하기
- 표시될 컬럼명(4개) : years, ranks, movie_name, release_date, audience_num, sales_amt(1억단위)
```
use mywork;
desc box_office;
```
```
select years, ranks, movie_name, release_date, audience_num, round(sale_amt / 100000000, 0) as 'sales_amt(1억단위)'
  from box_office
  where release_date like '2019%' and audience_num >= 5000000;
```  
### (실습) 문자형 함수 사용
- 현재 box_office 테이블에 영화감독(director)이 두명 이상이면 ','로 연결되어 있음
- 감독이 1명이면 그대로 두고, 두명 이상이면 ',' 대신 '/' 값으로 대체해 조회

```
select * , replace(director, ',', '/' ) from box_office;
```
```
select movie_name, replace(director, ',', '/' ) as 'director(/로 구분)' from box_office
  where instr(director, ',') > 0;
```  
### 날짜형 함수
```
select current_date();
select current_time();
select now();
select current_timestamp();
select dayname('2023-11-02');
select dayofmonth('2022-11-02');
select dayofweek('2022-11-02');   -- 일요일 기준으로 몇 번째 날인지
select dayofyear('2022-11-02');
select last_day('2028-2-02');
select year('2022-11-02');
select month('2022-11-02');
select quarter('2022-11-02');
select weekofyear('2022-11-02');
```
```
select adddate('2022-11-02', 100);
select date_add('2022-11-02', interval 100 month);   -- date_add는 날뿐만 아니라 달, 년 모두 가능하다.
-- interval expr unit
-- https://dev.mysql.com/doc/refman/8.0/en/expressions.html#temporal-intervals
select date_add('2022-11-02', interval '1-3' year_month);
```
```
select subdate('2022-11-02', 20);
select date_sub('2022-11-02', interval 10 day);
select date_sub('2022-11-02', interval '1 3' day_hour);
```
```
select extract(year_month from '2022-11-02');
select extract(year_month from '2022-11-02 12:08:00');
select extract(minute_second from '2022-11-02 12:08:00');
```
```
select datediff('2022-11-02', '2021-11-02');
select datediff('2022-11-02', '2023-11-02');
```
- date_format에서 사용하는 식별자
- https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format
```
select date_format('2022-11-02', '%y-%b-%d');
```
```
select makedate(2022, 100);
select makedate(2022, 365);
```
```
select sysdate(), sleep(2), sysdate();  -- 함수가 호출된 시간을 기준으로
select now(), sleep(2), now();    -- 문장 단위 시간 기준
```
### week 함수에서 사용할 수 있는 mode
```
select week('2022-11-02');
select yearweek('2022-11-02');
```
### (실습) 날짜형 함수
- 현재 날짜를 기준으로 현재 Day가 속한 월의 마지막 날짜에 해당하는 요일 구하기
```
select last_day('2022-11-02'), dayname('2022-11-02');
select dayname(last_day(now()));
```
### (실습) 날짜형 함수
- 연인과 처음 만난 날이 2021년 5월 12일인데, 100일, 500일, 1000일이 되는 날을 조회하기
```
select adddate('2021-05-12', 99), adddate('2021-05-12', 499), adddate('2021-05-12', 999);
select adddate('2021-05-12', 100) as '100일', adddate('2021-05-12', 500) as '500일', adddate('2021-05-12', 1000) as '1000일';
```
### (실습) 날짜형, 문자형 함수
- mywork 데이터베이스에 접속해 box_office 테이블에서 2019년에 개봉된 영화 중, 영화 제목에 ':'이 들어간 영화 조회
```
use mywork;
desc box_office;
select * from box_office
  where instr(movie_name, ':') and year(release_date) = 2019;
```
```
select movie_name, release_date
  from box_office
  where year(release_date) = 2019 and instr(movie_name, ':') > 0;
```  
### 기타 함수들
```
select cast(10 as char);  -- 숫자가 문자형으로
select convert(10, char);
```
```
select cast('2022-11-02' as datetime);
select convert('2022-11-02', datetime);
```
### 흐름제어 함수
```
select if(2 > 1, '참', '거짓');
select if(2 < 1, '참', '거짓');
```
```
select ifnull(null, 'null입니다');
select ifnull(1, 'null입니다');
```
```
select nullif(1, 1);
select nullif(1, 2);
```
```
select case 1 when 1 then '1입니다.'
			  when 2 then '2입니다.'
			  when 3 then '3입니다.'
			  when 4 then '4입니다.'
			  else 'None'
       end case1,
       case 2 when 1 then '1입니다.'
			  when 2 then '2입니다.'
			  when 3 then '3입니다.'
			  when 4 then '4입니다.'
			  else 'None'
       end case2;
```
```
select case when 1=1 then '1입니다.'
			when 1=2 then '2입니다.'
			when 1=3 then '3입니다.'
			when 1=4 then '4입니다.'
			else 'None'
       end case1,
       case when 2=1 then '1입니다.'
		    when 3=2 then '2입니다.'
			when 2=3 then '3입니다.'
			when 4=4 then '4입니다.'
			else 'None'
       end case2;
```       
### (실습) 날짜형 함수
- box_office 테이블에서 2019년 개봉한 영화 중 순위(ranks) 기준으로 상위 10위까지의 영화를 조회하되,
- 이때 개봉일이 무슨 요일인지와 개봉일이 어떤 분기에 속해있는지에 대한 컬럼을 추가하시오.
- 표시할 컬럼: 영화 이름, 개봉일, 개봉 요일, 분기
```
desc box_office;
select movie_name, release_date, dayname(release_date), quarter(release_date) from box_office
  where release_date like '2019%'
  order by ranks
  limit 10;
```
```
select movie_name as '영화 이름', release_date as '개봉일', dayname(release_date) as '개봉요일', quarter(release_date) as '분기' from box_office
  where year(release_date) = 2019
  and ranks <= 10
  order by ranks;
``` 
### (실습) 흐름제어 함수
- 위의 결과를 활용하여 분기를 상반기, 하반기로 바꾸어 표현해보자.
- (예: 1,2분기이면 상반기, 3,4분기이면 하반기

### option 1
```
select movie_name, release_date, dayname(release_date), quarter(release_date), 
case when quarter(release_date) = 1 then '상반기'
     when quarter(release_date) = 2 then '상반기'
	 when quarter(release_date) = 3 then '하반기'
	 when quarter(release_date) = 4 then '하반기'
     else ''
     end quarter
  from box_office
  where release_date like '2019%'
  order by ranks
  limit 10;
```  
### option 2
```
select movie_name as '영화 이름', release_date as '개봉일', dayname(release_date) as '개봉요일', quarter(release_date) as '분기',
if (quarter(release_date) = 1 or quarter(release_date) = 2, '상반기', '하반기') as '상/하반기' 
from box_office
  where year(release_date) = 2019
  and ranks <= 10
  order by ranks;
```  
### option 3
```
select movie_name as '영화 이름', release_date as '개봉일', dayname(release_date) as '개봉요일', quarter(release_date) as '분기',
	   case quarter(release_date) when 1 then '상반기' 
								  when 2 then '상반기' 
                                  when 3 then '하반기' 
                                  when 4 then '하반기' 
	   end '상/하반기'
  from box_office
  where year(release_date) = 2019
  and ranks <= 10
  order by ranks;
```  
### option 4
```
select movie_name as '영화 이름', release_date as '개봉일', dayname(release_date) as '개봉요일', quarter(release_date) as '분기',
	   case when quarter(release_date) = 1 or quarter(release_date) = 2 then '상반기'
	        when quarter(release_date) = 3 or quarter(release_date) = 4 then '하반기'
	   end '상/하반기'
  from box_office
  where year(release_date) = 2019
  and ranks <= 10
  order by ranks;
```
### option 5
```
select movie_name as '영화 이름', release_date as '개봉일', dayname(release_date) as '개봉요일', quarter(release_date) as '분기',
	   case when quarter(release_date) in (1, 2) then '상반기'
	        when quarter(release_date) in (3, 4) then '하반기'
	   end '상/하반기'
  from box_office
  where year(release_date) = 2019
  and ranks <= 10
  order by ranks;
```  
### (실습) 흐름제어 함수
- world 데이터베이스에 있는 country 테이블에는 indepyear라는 컬럼에는 해당국가의 독립연도가 저장되어 있음
- 이때 각 국가명과 독립연도를 조회(출력)해 독립연도의 값이 없으면 '없음', 있으면 해당 독립연도가 출력
```
use world;
desc country;
```
```
select name as 국가명, ifnull(indepyear, '없음') as '독립연도' from country;
```
### (실습) 
- mywork 데이터베이스의 box_office 테이블에서 2019년 개봉한 영화 중 
- 순위(ranks)가 1~10위인 경우 "상위10" 그 외(11위 이상)는 "나머지" 라고 표시하기
```
use mywork;
desc box_office;
```
```
select ranks, movie_name as '영화이름', release_date as 개봉년도, if(ranks <= 10, '상위10', '나머지') as '상위권' from box_office
 where year(release_date) = 2019
 order by ranks;
```  
## 데이터 집계하기
### (1) 그룹화하기 (2) 집계함수 사용 (3) 집계쿼리((1)+(2))

### (1) 그룹화하기
```
use world;
select continent from country
 group by 1
 order by 1;
```
```
select continent, region from country
 group by continent, region
 order by continent, region;
```
```
select name, district, substr(district, 1, 3) as dist
  from city
  where countrycode = 'kor'
  group by district;
```
```
select name, district, substr(district, 1, 3) as dist
  from city
  where countrycode = 'kor'
  group by substr(district, 1, 3);
```
```
select name, district, substr(district, 1, 3) as dist
  from city
  where countrycode = 'kor'
  group by 3;
```
```
select name, district, substr(district, 1, 3) as dist
  from city
  where countrycode = 'kor'
  group by dist;
```  
- Note. group by한 대상(컬럼, 표현식, 순번)이 select에 나와야 의미가 있음
- (아래와 같이 하면 안됨)
```
select continent
  from country
  group by region;
```
```
select continent
  from country
  group by continent;
```
```
select distinct continent   -- 중복되지 않은 유일한 값만 출력해주세요.  group by와 내부적으로 다름
  from country;
```  
### (2) 집계 함수
```
select *
  from country;
```
```
select count(*) from country;
```
```
select count(name), count(continent), count(distinct continent)
  from country;
```
```
select name, min(population), max(population), avg(population)
  from country
  where continent = 'europe';
```
- (1단계) 유럽인구의 최솟값을 구한다.
```
select min(population)
  from country
  where continent = 'europe';
```
- (2단계) 인구가 1000명인 나라를 조회한다.
```
select name, population
  from country
  where continent = 'europe' and population = 1000;
```  
- (sub query 방식: 1, 2단계를 한 번에)
```
select b.name, b.population
from (
select min(population) as min_population
  from country
  where continent = 'europe'
) a, country b
where b.population = a.min_population;
```

## 데이터 집계하기

### (3) 집계 쿼리
- "연도"별 개봉 영화 수의 합 집계하기
```
use mywork;
```
```
select year(release_date), count(*)
  from box_office
  group by year(release_date)
  order by year(release_date);
```
### (실습) 2019년 개봉 영화의 "유형"별 매출액의 최댓값, 최솟값, 전체합 집계하기
```
select movie_type, max(sale_amt), min(sale_amt), sum(sale_amt)
  from box_office
  where year(release_date) = 2019
  group by movie_type
  order by 1;
```
### (실습) 2019년 개봉 영화 중 매출액이 1억원 이상인 영화의 "분기"별, "배급사"별 개봉 영화수와 매출액(합계) 집계하기
```
select quarter(release_date) '분기', distributor 배급사, count(*) 영화수, sum(sale_amt) 매출액합
  from box_office
  where year(release_date) = 2019 and sale_amt >= 100000000
  group by quarter(release_date), distributor
  order by 1;
```  
### (실습) world 데이터베이스에서의 city 테이블에서 "국가코드"별로 도시의 수 집계하기
```
use world;
desc city;
select countrycode, count(*)
  from city
  group by countrycode
  order by 2 desc;
```  
### (실습) world 데이터베이스의 country 테이블에서 "대륙"별 면적(surfacearea)이 가장 큰 순으로 정렬하기
```
select continent 대륙, sum(surfacearea) 총면적, count(*) 나라수, sum(population) 총인구
  from country
  group by continent
  order by 2 desc;
```  
### (실습) mywork 데이터베이스의 box_office 테이블에서 2019년 개봉 영화 중 1~10위 영화와 나머지 영화를 구분하되, 각 그룹의 매출액 합 집계하기
```
use mywork;
desc box_office;
```
```
select release_date 개봉년도, if(ranks <= 10, '상위10', '나머지') '상위권', sum(sale_amt) 총매출액, count(*) 영화수
 from box_office
 where year(release_date) = 2019
 group by 2
 order by 2 desc;
```
```
select case when ranks between 1 and 10 then '상위10'
			else '나머지'
		end top_ranks, count(*) 영화수, round(sum(sale_amt)/100000000, 0) '총매출액(unit:억원)'
	from box_office
where year(release_date) = 2019
group by top_ranks
order by 3 asc;
```
- 2019년에 개봉한 영화 중 매출액이 1000만원 이상인 영화를 유형별로 매출액 합을 집계(+ 총합 with rollup)
- with rollup으로 합계(소계, 총계) 구하기
```
select movie_type, count(*), sum(sale_amt)   -- 1870105386118
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by movie_type with rollup;
```
- 아래 쿼리문으로 위의 rollup 총합값이 같음을 확인할 수 있음
```
select sum(sale_amt)   -- 1870105386118
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000;
```
- 2019년에 개봉한 영화 중 매출액이 1000만원 이상인 영화를 
- "월"별, "영화유형"별  매출액 집계하기
```
select movie_type 영화유형, count(*) 영화수, sum(sale_amt) 총매출액, month(release_date) 월
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by month(release_date), movie_type with rollup
  order by 4;
```  
- grouping 함수 사용하기: grouping의 결과가 1일 때 with rollup의 결과인 총합임을 알 수 있음
- grouping을 응용하여 총합에 해당하는 null값을 적당한 단어("합계")로 대체
```
select if(grouping(movie_type) = 0, movie_type, "합계") 유형, count(*) 영화수, sum(sale_amt) 총매출액
  from box_office
  where year(release_date) = 2019
  group by movie_type with rollup;
```  
### Having 절 사용하기
- box_office 테이블에서 순위가 1~10위에 있는 영화를 조회하되,
- "개봉연월별"로 개봉영화 편수 집계하기
```
select ranks, extract(year_month from release_date) 개봉연월, count(*) 영화수, if(count(*) >= 2, count(*), null) 2편이상
  from box_office
  where ranks <= 10
  group by 2
  order by ranks;
```
```
select release_date, extract(year_month from release_date) 개봉연월, count(*) 개봉편수
  from box_office
  where ranks between 1 and 10
  group by 개봉연월;
```

- 이때 영화가 2편 이상 개봉한 항목만 조회하기
```
select ranks, extract(year_month from release_date) 개봉연월, count(*) 영화수
  from box_office
  where ranks <= 10 and '영화수' >= 2
  group by 2
  order by ranks;
```  
- 이때 아래와 같이 하면 오류가 뜸
```
select release_date, extract(year_month from release_date) 개봉연월, count(*) 개봉편수
  from box_office
  where ranks between 1 and 10 and count(*) >= 2
  group by 개봉연월;
```  
- having 절을 사용했을 때 (오류 안뜸)
```
select extract(year_month from release_date) 개봉연월, count(*) 개봉편수
  from box_office
  where ranks between 1 and 10
  group by 개봉연월
  having count(*) >= 2
  order by 2 desc;
```  
### (실습) "개봉년월"별로 순위가 1~10위에 있는 영화 편수와 매출액 구하기
```
select ranks, extract(year_month from release_date) 개봉연월, count(*) 영화수, sum(sale_amt)
  from box_office
  where ranks <= 10
  group by 2
  order by ranks;
```
```
select extract(year_month from release_date)개봉년월, count(*) 영화편수, sum(sale_amt) 매출액함
 from box_office
 where ranks between 1 and 10
 group by 1;
```
- 이때 "개봉년월"별 매출액 합이 1500억원 이상인 경우만 조회하기 (having 절 사용)
```
select ranks, extract(year_month from release_date) 개봉연월, count(*) 영화수, sum(sale_amt)
  from box_office
  where ranks <= 10
  group by 2
  having sum(sale_amt) >= 150000000000
  order by ranks;
```
```
select extract(year_month from release_date)개봉년월, count(*) 영화편수, round(sum(sale_amt)/100000000,0) '매출액합(unit:억원)'
 from box_office
 where ranks between 1 and 10
 group by 1
 having sum(sale_amt) >= 150000000000;
```
### (실습) 2019년 개봉영화 중 매출액이 1000만원 이상인 것을 골라 "영화유형"별로 매출액 합 구하기 (with rollup)
```
select movie_type, sum(sale_amt)
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by movie_type with rollup;
```
```
select movie_type 영화유형, count(*) 영화편수, round(sum(sale_amt)/1000000) '총매출액(unit: 백만)'
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by movie_type with rollup;
```  
- 이때 "영화유형"별로 매출액 합계로 나온 결과 행만 조회하기 (having)
```
select movie_type, sum(sale_amt)
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by movie_type with rollup
  having grouping(movie_type) = 1;
```
```
select movie_type 영화유형, count(*) 영화편수, round(sum(sale_amt)/1000000) '총매출액(unit: 백만)'
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by movie_type with rollup
  having grouping(movie_type) = 1;
```  
### if절 사용
```
select if(grouping(movie_type) = 0, movie_type, "합계") 영화유형, count(*) 영화편수, round(sum(sale_amt)/1000000) '총매출액(unit: 백만)'
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by movie_type with rollup;
```  
### (실습) 2019년 개봉 영화 중 매출액이 1000만원 이상인것을 골라 "월"별, "영화유형"별로 매출액합 집계하기 (with rollup)
```
select movie_type 영화유형, count(*) 영화편수, round(sum(sale_amt)/1000000) '총매출액(unit: 백만)', month(release_date) 월
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by month(release_date), movie_type with rollup;
```
- 이 때 "월"별, "영화유형"별 매출액 합계(유형별소계, 월별총계)로 나온 결과 행만 조회하기 (having 절)
 ```
 select count(*) 영화편수, round(sum(sale_amt)/1000000) '총매출액(unit: 백만)', if(grouping(month(release_date)) = 0, month(release_date), "총계") 월, if(grouping(movie_type) = 1, movie_type, "소계") 영화유형
  from box_office
  where year(release_date) = 2019 and sale_amt >= 10000000
  group by month(release_date), movie_type with rollup
  having grouping(movie_type) = 1
  order by month(release_date);
``` 
### (실습) box_office 테이블에서 2019년 개봉영화 중 "국가(rep_country)"별 관객수(audience_num)의 합이 50만명 이상인 것을 조회하기 
```
desc box_office;
select rep_country, sum(audience_num)
  from box_office
  where year(release_date) = 2019
  group by rep_country
  having sum(audience_num) >= 500000;
```
- 이때 "국가"별 합계까지 구하는 쿼리 작성하기 (with rollup)
```
select rep_country, sum(audience_num)
  from box_office
  where year(release_date) = 2019
  group by rep_country with rollup
  having sum(audience_num) >= 500000;
```  
### (실습) box_office 테이블에서 2015년 이후 개봉한 영화 중
- 관객수가 100만을 넘긴 영화의 감독과 관객수, 개봉편수를 "연도"별, "감독"별로 집계하기
```
desc box_office;
select director 감독, year(release_date) 개봉년도, audience_num 관객수, count(*) 개봉편수
  from box_office
  where year(release_date) >= 2015 and audience_num >= 1000000
  group by year(release_date), director;
```  
- 이 때 개봉 편수가 2번 이상되는 건수만 조회하기(having 절)
```
 select director 감독, year(release_date) 개봉년도, audience_num 관객수, count(*) 개봉편수
  from box_office
  where year(release_date) >= 2015 and audience_num >= 1000000
  group by year(release_date), director
  having count(*) >= 2;
``` 
## 테이블간 관계 맺기
### (1) 내부 조인 
```
use world;
select count(*) from city;     -- 4097
select count(*) from country;  -- 239
```
### city 테이블과 country 테이블을 조인해서 country 테이블에 있는 국가명, 대륙명, 인구까지 조회하기
```
select count(*)   -- 4079건 조회 (1:m의 관계에서 join시 m의 개수로 맞춰짐)
  from city a
  inner join country b
    on a.countrycode = b.code;
```
```
select a.*, b.name, b.continent, b.population
  from city a
  inner join country b
    on a.countrycode = b.code;
```
### join된 결과에 대해 추가적으로 where 문을 통해 필터링
```
select a.*, b.name, b.continent, b.population
  from city a
  inner join country b
    on a.countrycode = b.code
  where a.countrycode = 'kor';
```    
### 내부 조인에서는 테이블의 위치를 바꿔도 결과는 동일
```
select a.*, b.name, b.population
  from country a
  inner join city b
    on b.countrycode = a.code
  where b.countrycode = 'kor';
```
### (실습) country 테이블과 countrylanguage 테이블 내부조인
- 조인결과가 어떤 테이블의 개수에 맞춰졌는지 확인
```
select count(*) from countrylanguage;    -- countrycode, 984, 자식
select count(*) from country;            -- code, 239, 부모
```
```
desc country;            
select count(*)             -- 984개로 countrylanguage 테이블의 개수로 맞춰졌다. 1:m의 관계에서 m으로 맞춰짐.
  from country a
  inner join countrylanguage b
	on b.countrycode = a.code;
```
### 한국인 경우로 추가 필터링 해보기
```
select count(*)
  from country a
  inner join countrylanguage b
	on b.countrycode = a.code
  where b.countrycode = 'kor';
```

## 테이블간 관계 맺기
### (1) 내부 조인 

- (실습) world 데이터베이스에서 country와 city 테이블을 내부 조인해 국가별 도시 수를 구하되
- 국가 코드가 아닌 국가명이 표시되도록 조회하고,
- 마지막에는 전체 도시수의 합을 구하는 쿼리 작성하기 (with rollup)
```py
use world;
desc city;
desc country;
select a.name, b.name, count(*)
  from country a
  inner join city b
    on b.countrycode = a.code
  group by a.name with rollup;
```
```py
select count(*) from country;  -- 239
select count(*) from city;  -- 4079
```
### 1:m(country:code)의 관계에서 내부조인을 하면 m개의 집합체로 맞춰짐
```py
select count(*)  -- 4079
  from country a
  inner join city b
    on a.code = b.countrycode;
```
### 국가별 도시수를 구함
```py
select a.name, count(b.name)
  from country a
  inner join city b
    on a.code = b.countrycode
  group by a.name with rollup;
```
### 전체 도시수의 합 구하기 (with rollup)
```py
select if(grouping(a.name), "도시수의 합", a.name) 국가명, count(b.name) '도시수의 합'
  from country a
  inner join city b
    on a.code = b.countrycode
  group by a.name with rollup;
```

- (실습) world 데이터베이스에서 country, city, countrylanguage 테이블을 조인해서
- countryode가 'kor'인 경우로 한정해
- 국가코드, 국가명, 대륙명, 인구수, 국가언어, 도시명, 도시인구가 출력되게 쿼리 작성하기
```py
desc country;
desc city;
desc countrylanguage;
select a.code, a.name, a.continent, a.population, c.language, b.population
  from country a
  inner join city b
    on a.code = b.countrycode
  inner join countrylanguage c
    on b.countrycode = c.countrycode
where a.code = 'kor';
```
```py
select count(*) from country;  -- 239
select count(*) from city;  -- 4079
select count(*) from countrylanguage; -- 984
```
### 전체 국가에 대해 3개의 테이블을 내부조인 했을 때의 건수
```py
select count(*)
  from country a
  inner join city b
    on a.code = b.countrycode   -- 4079
  inner join countrylanguage c
    on b.countrycode = c.countrycode   -- 30670
  where a.code = 'kor';
```
```py
select count(*) from country where code = 'kor';   -- 1
select count(*) from city where countrycode = 'kor';   -- 70
select count(*) from countrylanguage where countrycode = 'kor';   -- 2
```
- 한 국가(kor)에 대해 3개의 테이블을 내부조인 했을 때의 건수
```py
select count(*)
  from country a
  inner join city b
    on a.code = b.countrycode   -- 70
  inner join countrylanguage c
    on b.countrycode = c.countrycode  -- 140
  where a.code = 'kor';
```
### 조회해야 하는 정보 표시하기
```py
select a.code, a.name, a.continent, a.population, c.language, b.name, b.population
  from country a
  inner join city b
    on a.code = b.countrycode   -- 70
  inner join countrylanguage c
    on b.countrycode = c.countrycode  -- 140
  where a.code = 'kor';
```  
  
```
inner join 한 번에 하는 방법
select
  from 테이블1 a
  join 테이블2 b join 테이블3 c
    on a.col1 = b.col1 and b.col1 = c.col1;

-- from where절로 바꾸면
select
  from 테이블1 a, 테이블2 b, 테이블 cache index
  where a.col1 = b.col1 and b.col1 = c.col1;
```

### (2) 외부 조인 
### 아래 쿼리문으로부터 country 테이블에 존재하는 대륙이 7개임을 알 수 있음
```py
select continent from country
 group by continent;
```
### 그러나 country 테이블과 city 테이블의 결과를 조회했을 때 antarctica가 누락되어 6개가 나왔음
```py
select a.continent, count(*) 도시수
  from country a
  inner join city b
    on a.code = b.countrycode
  group by a.continent;
```
### 누락된 대륙인 antarctica의 국가명을 조회해보니 총 5개의 나라가 표시되었음
```py
select *
  from country
  where continent = 'antarctica';
```
### antarctica에 속한 5개의 국가를 city 테이블에서는 조회가 안됨
```py
select *
  from city
  where countrycode in ('ATA', 'ATF', 'BVT', 'HMD', 'SGS');
```
### 외부조인으로 누락된 대륙까지 조회되도록 할 수 있음
```py
select a.continent, count(b.name) 도시수
  from country a
  left join city b
    on a.code = b.countrycode
  group by a.continent;
```
### 위의 left join은 테이블 위치만 바꾼 뒤 right join으로 대체할 수 있음
```py
select b.continent, count(a.name) 도시수
  from city a
  right join country b
    on b.code = a.countrycode
  group by b.continent;
```

- (실습) 아프리카(africa) 대륙에 속한 국가 중 사용 언어가 없는 국가가 있음
- country 테이블과 countrylanguage 테이블을 조인해서
- 이 국가의 이름이 무엇인지 찾는 쿼리 작성하기
```py
desc country;
desc countrylanguage;
select a.name, b.language, a.region, count(b.language) 언어수
  from country a
  left join countrylanguage b
    on a.code = b.countrycode
group by b.language
order by 3;
```
### (1) 외부조인을 통해 country에서 빠지는 나라가 없도록 함
```py
select a.name, b.language
  from country a
  left join countrylanguage b
    on a.code = b.countrycode
  where a.continent = 'africa';
```  
### (2) 위에서 조인한 테이블에서 나라의 언어가 없는 값 조회하기
```py
select a.name, b.language
  from country a
  left join countrylanguage b
    on a.code = b.countrycode
  where a.continent = 'africa'
    and b.language is null;
```
```py
select a.name, count(b.language) 언어수
  from country a
  left join countrylanguage b
    on a.code = b.countrycode
  where a.continent = 'africa'    
  group by a.name
  having count(b.language) = 0;
```

### (3) 기타 조인 
### (3-1) 자연조인
```py
select count(*)
  from country a
  inner join city b
    on a.code = b.countrycode;
```
### 위의 내부 조인을 자연조인으로 바꾸기
- 두 테이블의 조인 조건에 사용되는 컬럼명이 같지 않기 때문에 자연조인이 안됨
```py
select count(*)
  from country a
  natural join city b;
```
```py
select count(*)
  from city a
  inner join countrylanguage b
    on a.countrycode = b.countrycode;
```    
### 위의 내부조인을 자연조인으로 바꿔보기
- 두 테이블의 조인 조건에 사용되는 컬럼명이 같으므로 자연조인에 성공!!
```py
select count(*)
  from city a
  natural inner join countrylanguage b;
```
- (3-2) 카티전곱(크로스 조인)
```py
select count(*) from country; -- 239
select count(*) from city; -- 4079
```
- 조인 조건을 기술하지 않으면 됨
```py
select count(*)   -- 239 X 4079 = 974881
  from country a
  inner join city b;
```  
- cross join이란 문법을 사용
```py
select count(*)   -- 239 X 4079 = 974881
  from country a
  cross join city b;
```  
  
### (4) Union (물리적으로 연결)
```py
use mywork;
```
```py
create table tbl1
(
  col1 int,
  col2 varchar(20)
);

create table tbl2
(
  col1 int,
  col2 varchar(20)
);
```
```py
select * from tbl1;
insert into tbl1 values (1, '가');
insert into tbl1 values (2, '나');
insert into tbl1 values (3, '다');
```
```py
select * from tbl2;
insert into tbl2 values (1, 'A');
insert into tbl2 values (2, 'B');
insert into tbl2 values (3, 'C');
```
```py
select col1, col2
  from tbl1
union  -- default option: distinct
select col1, col2
  from tbl2;
```
```py
select col1, col2
  from tbl1
union all -- all 옵션은 모두 다 가져옴
select col1, col2
  from tbl2;
```
```py
select *
  from tbl1
union all -- all 옵션은 모두 다 가져옴
select *
  from tbl2;
```
### union된 집합체의 정렬
```py
select col1, col2
  from tbl1
union all -- all 옵션은 모두 다 가져옴
select col1, col2
  from tbl2
order by col1 desc;  -- 이때의 order by 정렬은 전체 결과물에 대한 정렬
```
### 개별 테이블만 정렬하고 싶을 때
- 아래와 같이 소괄호를 이용해서 개별테이블을 정렬하게 했으나
```py
(select col1, col2
  from tbl1
order by 1 desc
)
union
select col1, col2
  from tbl2;
```
- limit 옵션을 줘서 개별 테이블 정렬 가능
```py
(select col1, col2
  from tbl1
order by 1 desc
limit 3
)
union
select col1, col2
  from tbl2;
```  
- (실습) tbl1과 tbl2에서 tbl1은 전체, tbl2는 col1 값이 1인 건만 조회하기
```py
select *
  from tbl1
union all
select *
  from tbl2
  where col1 = 1;
```
```
   /* 사원 기존 정보를 이용한 테이블 조인 실습 */
-- employees : 사원정보
-- dept_emp : 사원의 부서 할당정보
-- departments : 부서정보
-- dept_manager : 부서의 관리자 정보
-- titles : 사원의 직급 정보
-- salaries : 사원의 급여 정보
```
```py
desc employees;
desc dept_emp;
desc departments;
desc dept_manager;
desc titles;
desc salaries;
```
```py
select * from employees;
select * from dept_emp;
select * from departments;
select * from dept_manager;
select * from titles;
select * from salaries;
```
```py
select count(*) from employees;    -- 30023
select count(*) from dept_emp;     -- 33188
select count(*) from departments;  -- 10
select count(*) from dept_manager; -- 24
select count(*) from titles;       -- 44423
select count(*) from salaries;     -- 285271
```
### (실습) 사원의 사번, 이름, 부서명 조회하기
```py
select a.emp_no, a.first_name, a.last_name, dept_name
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no       -- 33188
  left join departments c
    on b.dept_no = c.dept_no;     -- 33188
```
```py
desc employees;
desc dept_emp;
desc departments;
```
- 1:m (employees:dept_emp)
- 한 직원이 여러부서에 속한 이력이 있음 (33188 > 30023)
```py
select a.emp_no, b.dept_no
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no; -- 33188
```    
### 위 결과에서는 부서명까지는 알 수 없으므로 departments를 추가로 조인
- 1:m(departments:dept_emp(+emploees))
```py
select count(*)
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no -- 33188
  inner join departments c
    on b.dept_no = c.dept_no; -- 33188
``` 
### 마지막으로 조회할 정보를 명시
```py
select a.emp_no 사번, concat(a.first_name, ' ', a.last_name) 이름, c.dept_name 부서명
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no -- 33188
  inner join departments c
    on b.dept_no = c.dept_no; -- 33188    
```   
### (실습) Marketing과 Finance 부서의 현재 관리자 (직원)정보 조회하기
```py
select *
  from dept_manager a
  inner join departments b
    on a.dept_no = b.dept_no       -- 24
  where b.dept_name = 'marketing' or b.dept_name = 'Finance';
```
```py
select count(*) from departments; -- 10
select count(*) from dept_manager; -- 24
```
- 1:m(departmenst:dept_manger)
```py
select *
  from departments a
  inner join dept_manager b
    on a.dept_no = b.dept_no -- 24
 where sysdate() between b.from_date and b.to_date; -- 9
```
- 1:m(employees:위에서 얻은 테이블)
```py
select *
  from departments a
  inner join dept_manager b
    on a.dept_no = b.dept_no -- 24
  inner join employees c
    on b.emp_no = c.emp_no 
 where sysdate() between b.from_date and b.to_date; -- 9
``` 
### 마지막으로 해당 부서로 필터링
```py
select a.dept_name 부서명, concat(c.first_name, ' ', c.last_name) 이름
  from departments a
  inner join dept_manager b
    on a.dept_no = b.dept_no -- 24
  inner join employees c
    on b.emp_no = c.emp_no 
 where sysdate() between b.from_date and b.to_date -- 9
   and a.dept_name in('Marketing' , 'Finance');
```   
### (실습) 모든 부서의 이름과 현재 관리자의 사번 조회하기
```py
select dept_name, emp_no
  from departments a
  inner join dept_manager b
    on a.dept_no = b.dept_no;
```    
- 1:m(departments:dept_manager)
- 현재 관리자로 필터링해서 건수를 조회해보면 총 9건
```py
select count(*)
  from departments a
  inner join dept_manager b 
    on a.dept_no = b.dept_no -- 24
  where sysdate() between b.from_date and b.to_date; -- 9
```
### 하지만 departments에서 부서 이름으로 유일한 이름을 구해보면 10건
```py
select distinct dept_name -- 10
  from departments;
```
- 따라서 외부조인을 통해서 누락된 부서정보까지 조회를 해야 함
- 외부 조인 결과를 보면 IT 부서에는 할당된 매니저가 없음을 확인
```py
select a.dept_name, b.emp_no
  from departments a
  left join dept_manager b
    on a.dept_no = b.dept_no
 where sysdate() between b.from_date and b.to_date
   or b.from_date is null; -- 10
```
### (실습) 부서별 사원 수와 전체 부서의 총 사원 수 구하기 
```py
select *, count(*)
  from departments a
  inner join dept_emp b
    on a.dept_no = b.dept_no
  inner join employees c
    on b.emp_no = c.emp_no
  group by a.dept_name with rollup;
```
### 우선 dept_emp 테이블로부터 dept_no로 group by
```py
select dept_no, count(*)
  from dept_emp
 where sysdate() between from_date and to_date -- 24135
 group by dept_no;
```
- 부서명까지 조회하기 위해 departments 테이블과 조인
- option 1 (with rolllup 사용)
```py
select if(grouping(a.dept_name), "총사원수", a.dept_name) 부서명, count(*) 사원수
  from departments a
  inner join dept_emp b
    on a.dept_no = b.dept_no -- 33188
 where sysdate() between b.from_date and b.to_date -- 24135
 group by a.dept_name with rollup;
```
- option 2 (union 사용)
- (1) 부서별 사원수
```py
select a.dept_name 부서명, count(*) 사원수
  from departments a
  inner join dept_emp b
    on a.dept_no = b.dept_no -- 33188
 where sysdate() between b.from_date and b.to_date
 group by a.dept_name;
``` 
- (2) 총사원수
```py
select "총사원수", count(*) -- 24135
  from dept_emp
 where sysdate() between from_date and to_date;
```
- (3) (1) + (2)
```py
select a.dept_name 부서명, count(*) 사원수
  from departments a
  inner join dept_emp b
    on a.dept_no = b.dept_no -- 33188
 where sysdate() between b.from_date and b.to_date
 group by a.dept_name
union
select "총사원수", count(*) -- 24135
  from dept_emp
 where sysdate() between from_date and to_date;
```
### (실습) 모든 부서의 이름과 현재 관리자의 사번 조회하기 + 관리자 이름까지
```py
desc employees;
desc dept_emp;
desc departments;
desc dept_manager;
desc titles;
desc salaries;
```
```py
select * from employees;
select * from dept_emp;
select * from departments;
select * from dept_manager;
select * from titles;
select * from salaries;
```
### (실습) 모든 부서의 이름과 현재 관리자의 사번 조회하기 + 관리자 이름까지
```py
select a.dept_name, b.emp_no, concat(c.first_name, ' ', c.last_name) fullname
  from departments a
  left join dept_manager b
    on a.dept_no = b.dept_no
  inner join employees c
    on b.emp_no = c.emp_no
 where sysdate() between b.from_date and b.to_date
   or b.from_date is null; -- 10
```
- (실습) employees 테이블에서 1965년 2월 이후 출생자의 사번, 이름, 생일, 부서명을 조회하는 쿼리를
- Natural 조인으로 작성하기
```py
select a.emp_no, concat(a.first_name, ' ', a.last_name) fullname, a.birth_date, c.dept_name
  from employees a
  natural join dept_emp b
  natural join departments c
  where extract(year_month from a.birth_date) >= '196502';
```
- (실습) departments 테이블에서 Sales 부서의 코드(dept_no) 값은 'd007'임
- 이 부서에 속한 "관리자의 사번과 급여", 이 부서에 속한 "사원의 사번과 급여"를 구하는 쿼리 작성하기
```py
select d.emp_no, c.salary, e.emp_no, c.salary
  from departments a
  natural join dept_emp b
  natural join salaries c
  inner join dept_manager d
    on b.dept_no = d.dept_no
  inner join employees e
    on b.emp_no = e.emp_no
  where b.dept_no = 'd007'
  group by d.dept_no, e.emp_no;
```
### (실습) 모든 부서의 이름과 현재 관리자의 사번 조회하기 + 관리자 이름까지
```py
select a.dept_name, b.emp_no, concat(c.first_name, ' ', c.last_name) fullname
  from departments a
  left join dept_manager b
    on a.dept_no = b.dept_no
  inner join employees c
    on b.emp_no = c.emp_no
 where sysdate() between b.from_date and b.to_date
   or b.from_date is null; -- 10
```
```py
select a.dept_name, b.emp_no, concat(c.first_name, ' ', c.last_name)
  from departments a
  left join dept_manager b
    on a.dept_no = b.dept_no
  left join employees c       -- b에서 IT부서의 누락된 None값의 영향을 받지 않기 위해 left join
    on b.emp_no = c.emp_no
  where sysdate() between b.from_date and b.to_date;
```
- (실습) employees 테이블에서 1965년 2월 이후 출생자의 사번, 이름, 생일, 부서명을 조회하는 쿼리를
- Natural 조인으로 작성하기
```py
select a.emp_no, concat(a.first_name, ' ', a.last_name) fullname, a.birth_date, c.dept_name
  from employees a
  natural join dept_emp b
  natural join departments c
  where extract(year_month from a.birth_date) >= '196502';
```
- inner join
```py
select b.dept_no, concat(a.first_name, ' ', a.last_name), a.birth_date, c.dept_name
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no  -- 33188
  inner join departments c
    on b.dept_no = c.dept_no  -- 33188
  where extract(year_month from a.birth_date) >= '196502';  
```
- natural join
```py
select b.dept_no, concat(a.first_name, ' ', a.last_name), a.birth_date, c.dept_name
  from employees a
  natural join dept_emp b
  natural join departments c
  where extract(year_month from a.birth_date) >= '196502';  
```
- (실습) departments 테이블에서 Sales 부서의 코드(dept_no) 값은 'd007'임
- 이 부서에 속한 "관리자의 사번과 급여", 이 부서에 속한 "사원의 사번과 급여"를 구하는 쿼리 작성하기
```py
select d.emp_no, c.salary, e.emp_no, c.salary
  from departments a
  natural join dept_emp b
  natural join salaries c
  inner join dept_manager d
    on b.dept_no = d.dept_no
  inner join employees e
    on b.emp_no = e.emp_no
  where b.dept_no = 'd007'
  group by d.dept_no, e.emp_no;
```  
```py  
select * from dept_manager;
select * from salaries;
```
### (1) 관리자의 사번과 급여
- 현재 부서의 매니저, 현재의 급여가 반영되도록 하려면 where절 조건 추가
```py
select a.emp_no, b.salary
  from dept_manager a
  inner join salaries b
    on a.emp_no = b.emp_no    -- 383
  where a.dept_no = 'd007'     -- 34
    and sysdate() between a.from_date and a.to_date -- 16 현재 부서의 매니저만
    and sysdate() between b.from_date and b.to_date;  -- 현재의 급여만
```    
### (2) 사원의 사번과 급여
```py
select count(*) from dept_emp;   -- 33188
select count(*) from salaries;   -- 285271
```
```py
select a.emp_no, b.salary
  from dept_emp a
  inner join salaries b
    on a.emp_no = b.emp_no   -- 315322
  where a.dept_no = 'd007'   -- 50110
    and sysdate() between a.from_date and a.to_date  -- 40092  현재 근무하는 사원만
    and sysdate() between b.from_date and b.to_date;  -- 3810  현재 급여만
```  
### (3) = (1) + (2)
```py
select '관리자' job_title, a.emp_no, b.salary
  from dept_manager a
  inner join salaries b
    on a.emp_no = b.emp_no    -- 383
  where a.dept_no = 'd007'     -- 34
    and sysdate() between a.from_date and a.to_date  -- 16 현재 부서의 매니저만
    and sysdate() between b.from_date and b.to_date  -- 현재의 급여만
union all
select '사원' job_title, a.emp_no, b.salary
  from dept_emp a
  inner join salaries b
    on a.emp_no = b.emp_no   -- 315322
  where a.dept_no = 'd007'   -- 50110
    and sysdate() between a.from_date and a.to_date  -- 40092  현재 근무하는 사원만
    and sysdate() between b.from_date and b.to_date;  -- 3810  현재 급여만
```    
## 서브 쿼리
### 1. 스칼라 서브쿼리
```py
select 컬럼, (서브커리)
  from 테이블
  where 조건식;
```
### 2. 파생 테이블
```py
select 컬럼
  from 테이블, (서브커리) 
  where 조건식;
```  
### 3. 조건 서브쿼리
```py
select 컬럼
  from 테이블
  where 값 > (서브커리);
```  
### 연도별 1위 영화들의 평균 매출액보다 큰 영화만 조회
```py
select year(release_date), count(*), movie_name, sale_amt, avg(sale_amt)
  from box_office
  where ranks = 1
  group by year(release_date), movie_name;
```
-- > avg(sale_amt) 컬럼값으로 조회된 평균 매출액은 16개 영화의 평균이 아님, 1위인 영화 각자의 평균

- 1단계: 16개 영화의 평균을 구한다.
```py
select avg(sale_amt)
  from box_office
  where ranks = 1;
```
- 2단계: 1단계에서 구한 평균보다 큰 영화를 조회
```py
select year(release_date), movie_name, sale_amt
  from box_office
  where ranks = 1 and sale_amt > 81906468809.6;
```  
- 앞에서 1위들의 영화 평균보다 큰 영화를 조회하는 쿼리를 한단계로 만들기
- 1. 스칼라 서브쿼리 사용
```py
select year(release_date), movie_name, sale_amt, 
(
select avg(sale_amt)
  from box_office
  where ranks = 1
) as average
  from box_office
  where ranks = 1
  having sale_amt > average;
```  
- 2. 파생 테이블 서브쿼리
```py
select year(release_date), movie_name, sale_amt
  from box_office, 
  (
  select avg(sale_amt) average
  from box_office a
  where ranks = 1
  ) as b
  where ranks = 1 and sale_amt > b.average;
```
- 3. 조건 서브쿼리
```py
select year(release_date), movie_name, sale_amt
  from box_office
  where ranks = 1 and sale_amt > (select avg(sale_amt)
                                  from box_office
                                  where ranks = 1);
```                                  
### 서로 다른 테이블 이용
```py
use world;
```
- 스칼라 서브쿼리 응용
- city 테이블과 country 테이블을 내부 조인해서 country에 있는 정보를 추가로 가져왔었음
```py
select a.*, b.name
  from city a
  inner join country b
    on a.countrycode = b.code;
```    
-- > 위의 코드를 스칼라 서브쿼리
```py
select a.*,
(
	select b.name
      from country b
      where a.countrycode = b.code
) country_name
  from city a;
```  
### 스칼라 서브쿼리 안에 두개의 컬럼을 넣어서 오류가 발생한 예
```py
select a.*,
(
	select b.name, b.continent
      from country b
      where a.countrycode = b.code
) country_name
  from city a;
```
### concat 함수를 사용해서 에러 없이 이와 같이 나타낼 수는 있음
```py
select a.*,
(
	select concat(b.name, '/',  b.continent)
      from country b
      where a.countrycode = b.code
) country_name
  from city a;
```  
### (2) 파생 테이블 응용
```py
use mywork;
```
- 1단계: 현재 관리자의 부서번호, 사번, 사원이름을 조회하는 쿼리
```py
select b.dept_no, b.emp_no, concat(c.first_name, ' ', c.last_name)
  from dept_manager b
  inner join employees c
   on b.emp_no = c.emp_no
  where sysdate() between b.from_date and b.to_date;
```
- 2단계: 부서명까지 추가하면  
```py
select b.emp_no, b.emp_no, concat(c.first_name, ' ', c.last_name), a.dept_name
  from dept_manager b
  inner join employees c
   on b.emp_no = c.emp_no
  inner join departments a
    on a.dept_no = b.dept_no
  where sysdate() between b.from_date and b.to_date;    -- 9건 조회
```  
- 위의 코드를 파생 테이블로 작성
```py
select *
  from departments a
  inner join ( 
		select b.dept_no, b.emp_no, concat(c.first_name, ' ', c.last_name) fullname
		  from dept_manager b
          inner join employees c
            on b.emp_no = c.emp_no
  ) manager
  on a.dept_no = manager.dept_no;
```  
```
-- (실습) box_office 테이블에서 2015년 이후 연도별 순위가 1~3위인 영화와 <br>
-- 해당 영화의 매출액이 "연도별 전체 매출액"에서 차지하는 비율을 구하는 쿼리 <br>
-- 1단계: "연도별 전체 매출액"을 구하는 부분 <br>
-- 2단계: 연도별 1~3위 영화와 매출액을 구한 뒤 <br>
--       각 영화의 매출액을 전체 매출액으로 나누는 부분
```
```py
use mywork;
```
- 1단계
```py
select years, sum(sale_amt)
  from box_office
  group by years;
```
- 2단계
```py
select years, sum(sale_amt)
  from box_office
  where ranks between 1 and 3
  group by years;
```  
- 3단계
```py
select years, sum(sale_amt), sale_amt
  from box_office,
  (
  select sum(sale_amt) s
    from box_office
    where ranks between 1 and 3 and year(release_date) = 2015
    group by ranks, years
  ) as top_3
  where ranks between 1 and 3 and year(release_date) = 2015 and top_3.s / s
  group by years;
```
```py
select year(release_date), ranks, movie_name, sale_amt, count(*), sum(sale_amt)
  from box_office
  where year(release_date) >= 2015 and ranks <= 3
  group by 1, 2;
```
-- > 위의 쿼리만으로는 연도별 전체 매출액을 알 수는 없음

- 1단계: "연도별 전체 매출액"을 구하는 부분
```py
select year(release_date), sum(sale_amt)
  from box_office
  where year(release_date) >= 2015
  group by year(release_date)
  order by 1;
```
```
-- 1657667127054
-- 1719186452482
-- 1808938584214
-- 1734872210331
-- 1870784163188
-- 316011700
```
- 2단계: 연도별 1~3위 영화의 정보와 매출액을 구한 뒤 각 영화의 매출액을 전체 매출액으로 나누는 부분
```py
select year(a.release_date), a.ranks, a.movie_name, a.sale_amt top_3_movies, b.total_amt , round(a.sale_amt / b.total_amt * 100, 2) 비율
  from box_office a,
  (
		select year(release_date) release_year, sum(sale_amt) total_amt
		  from box_office
		  where year(release_date) >= 2015
		  group by year(release_date)
		  order by 1
  ) b
  where year(a.release_date) = b.release_year and a.ranks <= 3
  group by 1, 2
  order by 1, 2;
```  
### 3. 조건 서브쿼리 응용
- 2019년도 개봉한 영화의 매출액이 2018년도 최대 매출액보다 큰 영화
```py
select movie_name, max(sale_amt)
  from box_office
  where year(release_date) = 2018;
```
```py
select movie_name, sale_amt
  from box_office
  where year(release_date) = 2019 and sale_amt > (select max(sale_amt)
									 from box_office
									 where year(release_date) = 2018
                                     );
```				     
- 2018년도 최대 매출을 올린 영화 조회
```py
select movie_name, sale_amt
  from box_office
  where year(release_date) = 2018
  order by 2 desc;
```  
### 2018년도 최대 매출을 올린 영화와 2019년도에 2018년도 최대 매출보다 큰 영화를 함께 표시
- option 1
```py
select movie_name, sale_amt
  from box_office
  where year(release_date) = 2019 and sale_amt > (select max(sale_amt)
									 from box_office
									 where year(release_date) = 2018
                                     )
union
select year(release_date), sale_amt
  from box_office
  where year(release_date) = 2018
  order by 2 desc
  limit 5;
```  
- option 2
```py
select movie_name, sale_amt
  from box_office
  where year(release_date) = 2019 and sale_amt > (select max(sale_amt)
									 from box_office
									 where year(release_date) = 2018
                                     )
union
select year(release_date), sale_amt
  from box_office
  where sale_amt = (select max(sale_amt)
					  from box_office
                      where year(release_date) = 2018
  );
```
```py
select year(release_date), movie_name, sale_amt
  from box_office
  where year(release_date) = 2019 and sale_amt >= ( select sale_amt   -- 1~3위인 3개의 행이 반환되어서 문제가 생김
                                                      from box_office
                                                      where year(release_date) =2018 and ranks between 1 and 3);
                                    
select sale_amt
  from box_office
  where year(release_date) = 2018 and ranks between 1 and 3;
```  
```
102666146909
99926399769
80010440345 
```

### All (서브쿼리의 결과로 나온 다수의 값 모두를 만족하는 결과를 조회)
```py
select year(release_date), movie_name, sale_amt
  from box_office
  where year(release_date) = 2019 and sale_amt >= All( select sale_amt
														 from box_office
                                                         where year(release_date) = 2018
                                                           and ranks between 1 and 3);
```  
### Any (서브쿼리의 결과로 나온 다수의 값 중에 하나라도 만족하는 결과를 조회)
```py
select year(release_date), movie_name, sale_amt
  from box_office
  where year(release_date) = 2019 and sale_amt >= Any( select sale_amt
														 from box_office
                                                         where year(release_date) = 2018
                                                           and ranks between 1 and 3);
```                                                           
### IN
- 2018년에 개봉한 영화 중 2019년까지 상영 중인 영화의 이름과 감독 조회
```py
select movie_name, director
  from box_office
  where year(release_date) = 2018;
```
```py
select movie_name, director
  from box_office
  where year(release_date) = 2019 and (movie_name, director) in ( select movie_name, director
  from box_office
  where year(release_date) = 2018);
```
### NOT IN
- 2019년도 1~100위 안에 든 영화의 대표국가(rep_country)가 2018년도 1~100위권에 없었던 나라
```py
select movie_name, ranks, rep_country
  from box_office
  where ranks <= 100 and year(release_date) = 2019 and rep_country not in (select rep_country
																	  from box_office
                                                                      where year(release_date) = 2018 and ranks <= 100);
```                                                                      
### Exists
- 2018년에 개봉한 영화 중 2019년에 상영 중인 영화의 이름과 감독 조회
```py
select movie_name, director
  from box_office a
  where year(release_date) = 2019 and exists (select *
											    from box_office b
                                                where year(release_date) = 2018
                                                and a.movie_name = b.movie_name
                                                and a.director = b.director);
```                                                
### Not exists
```py
select movie_name, ranks, rep_country
  from box_office a
  where ranks <= 100 and year(release_date) = 2019 and not exists (select *
																	  from box_office b
                                                                      where year(release_date) = 2018 and ranks <= 100
                                                                      and a.rep_country = b.rep_country);
```                                                                      
- (실습)
- 현재를 기준으로 각 부서에서 급여를 가장 많이 받는 사원이 누군지 찾는 쿼리
```py
select * from employees;
select * from dept_emp;
select * from departments;
select * from salaries;
```
```py
select *
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no
  where sysdate() between b.from_date and b.to_date and ( select max(salary)
															from departments c
															inner join dept_emp d
															  on c.dept_no = d.dept_no
															inner join salaries e
															  on d.emp_no = e.emp_no
														    group by dept_name);
```
```py
select dept_name, max(salary), d.emp_no
  from departments c
  inner join dept_emp d
    on c.dept_no = d.dept_no
  inner join salaries e
    on d.emp_no = e.emp_no
  where sysdate() between d.from_date and d.to_date
  group by c.dept_name;
```
```py
select *
  from dept_emp
  where sysdate() between from_date and to_date; 
```
```py
select a.dept_no, max(b.salary)
  from dept_emp a
  inner join salaries b
    on a.emp_no = b.emp_no
  where sysdate() between a.from_date and a.to_date
    and sysdate() between a.from_date and a.to_date
    group by a.dept_no;
```
-- > 위의 쿼리만으로는 부서별 최대 급여값은 알 수 있으나 해당 사원의 정보는 알 수 없음
```py
select k.dept_no, c.emp_no, c.salary
  from salaries c,
  (
		select a.dept_no, max(b.salary) max_salary
		  from dept_emp a
		  inner join salaries b
            on a.emp_no = b.emp_no
		  where sysdate() between a.from_date and a.to_date
			and sysdate() between a.from_date and a.to_date
		  group by a.dept_no
  ) k
where c.salary = k.max_salary
order by 1;
```

### (실습) 현재를 기준으로 어느 부서에도 속하지 않는 사원은 모두 몇 명인지 구하는 쿼리 작성하기   
```py
select count(*)
  from employees k
  where k.emp_no and not exists ( select c.dept_no
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no
  inner join departments c
    on b.dept_no = c.dept_no
  where sysdate() between b.from_date and b.to_date);
```  
```py
select dept_name
  from employees a
  inner join dept_emp b
    on a.emp_no = b.emp_no
  inner join departments c
    on b.dept_no = c.dept_no
  where sysdate() between b.from_date and b.to_date;
```
```py
select count(emp_no)
  from employees a
  where a.emp_no not in (select b.emp_no
						   from dept_emp b
						  where sysdate() between b.from_date and b.to_date);
```
```py
select *
  from dept_emp
  where sysdate() between from_date and to_date; 
```

-- (실습) box_office 테이블에서 2018년과 2019년에 개봉한 영화를 대상으로 연도별, 분기별 매출액을 구하되, <br>
-- 아래와 같은 형식으로 조회되도록 쿼리 작성하기 <br>
-- (힌트 : case~end 구문 이용, sum(sale_amt)를 활용할 수 있는 서브쿼리 이용가능) <br>
-- ---------------------------------------------- <br>
-- 연도  |    1분기  |   2분기  |   3분기  |  4분기  <br>
-- ---------------------------------------------- <br>
-- 2018 |          |         |         | <br>
-- ---------------------------------------------- <br>
-- 2019 |          |         |         | <br>
-- ---------------------------------------------- <br>
```py
select years, sum(sale_amt)
  from box_office
  where year(release_date) between 2018 and 2019
  group by 1
  order by 1;
```
```py
select years, sum(sale_amt), quarter(release_date),
case when quarter(release_date) = 1 then '1분기'
     when quarter(release_date) = 2 then '2분기'
	 when quarter(release_date) = 3 then '3분기'
	 when quarter(release_date) = 4 then '4분기'
     else ''
     end quarter
  from box_office
  where year(release_date) between 2018 and 2019 and (select sum(sale_amt)
  from box_office
  where year(release_date) between 2018 and 2019)
  group by years, quarter(release_date)
  order by years, quarter(release_date);
```  
- (1)
```py
select year(release_date), quarter(release_date), sum(sale_amt)
  from box_office
  where year(release_date) in (2018, 2019)
  group by 1, 2
  order by 1, 2;
```
- (2)
```py
select a.years,
	   case a.qtr when 1 then a.qt_sum_amt else 0 end "1분기",
       case a.qtr when 2 then a.qt_sum_amt else 0 end "2분기", 
       case a.qtr when 3 then a.qt_sum_amt else 0 end "3분기",
       case a.qtr when 4 then a.qt_sum_amt else 0 end "4분기" 
       
from (select year(release_date) years, quarter(release_date) qtr, sum(sale_amt) qt_sum_amt
  from box_office
  where year(release_date) in (2018, 2019)
  group by 1, 2
  order by 1, 2) a;
```  
```py  
select year(release_date), quarter(release_date), sum(sale_amt),
       case quarter(releaese_date) when 1 then sum(sale_amt) else 0 end "1분기",
       case quarter(releaese_date) when 2 then sum(sale_amt) else 0 end "2분기", 
       case quarter(releaese_date) when 3 then sum(sale_amt) else 0 end "3분기",
       case quarter(releaese_date) when 4 then sum(sale_amt) else 0 end "4분기" 
       
  from box_office
  where year(release_date) in (2018, 2019)
  group by 1, 2
  order by 1, 2;
```  
- (3)
```py
select a.years,
	   sum(case a.qtr when 1 then a.qt_sum_amt else 0 end) "1분기",
       sum(case a.qtr when 2 then a.qt_sum_amt else 0 end) "2분기", 
       sum(case a.qtr when 3 then a.qt_sum_amt else 0 end) "3분기",
       sum(case a.qtr when 4 then a.qt_sum_amt else 0 end) "4분기" 
       
from (select year(release_date) years, quarter(release_date) qtr, sum(sale_amt) qt_sum_amt
  from box_office
  where year(release_date) in (2018, 2019)
  group by 1, 2
  order by 1, 2) a
  group by 1;
```  
## 데이터 입력, 수정, 삭제, 트랜잭션
### Insert 문으로 데이터 입력하기

- 테이블 생성하기
```py
create table emp_test(
  emp_no int not null,
  emp_name varchar(30) not null,
  hire_date date null,
  salary int null,
  primary key (emp_no)
);
```
- 단일 로우 입력 insert문
```py
insert into emp_test(emp_no, emp_name, hire_date, salary)
	   values (1001, '아인슈타인', '2021-01-01', 1000);
```
```py
select * from emp_test;
```
```py
insert into emp_test(emp_no, emp_name, hire_date)  -- 데이터를 모두 넣지 않아도 됨
	   values (1002, '아이작뉴턴', '2021-02-01');
``````py       
select * from emp_test;
```
```py
insert into emp_test(hire_date, emp_no, emp_name)  -- 순서를 섞어서 넣어도 됨
	   values ('2021-03-01', 1003, '다빈치');
```
```py
select * from emp_test;
```
- (오류 예) not null 옵션이 있는 emp_name 컬럼은 필히 입력
```py
insert into emp_test(emp_no, hire_date)
	   values (1004, '2021-04-01');
```       
- (오류 예) primary key에 중복값 입력
```py
insert into emp_test(emp_no, emp_name, hire_date)
	    values (1003, '리어드파인만', '2021-01-10');
```
- 컬럼명을 생략
```py
insert into emp_test
	   values (1004, '리차드파인만', '2021-01-10', 3000);  -- 아무것도 안 넣어도 된다.
```
```py
select * from emp_test;
```
### 다중 로우 입력 insert문
```py
insert into emp_test values
row (1005, '퀴리부인', '2021-03-01', 4000),
row (1006, '스티븐호킹', '2021-03-05', 5000);
```
```py
select * from emp_test;
```
```py
insert into emp_test values
(1007, '마이클페러데이', '2021-04-01', 2200),
(1008, '맥스웰', '2021-04-05', 3300),
(1009, '막스클랑크', '2021-03-05', 4400);
```
```py
select * from emp_test;
```
### select 문이 결합된 insert문
- 테이블 생성
```py
create table emp_test2(
  emp_no int not null,
  emp_name varchar(30) not null,
  hire_date date null,
  salary int null,
  primary key (emp_no)
);
```
```py
select * from emp_test2;
```
```py
insert into emp_test2
select *
  from emp_test
  where emp_no in (1003, 1004);
```
```py
select * from emp_test2; -- 2행 추가
```
- (오류 예) 중복된 키값 (1004) 입력
```py
insert into emp_test2
select *
  from emp_test
  where emp_no >= 1004;
```
```py
select * from emp_test;
```
```py
insert into emp_test
select enp_no + 10m emp_name, hire_date, 100
  from emp_test
  where emp_no >= 1008;
```
```py
select * from emp_test;
```
-- (실습) emp_test 테이블에 insert 문을 사용하여 아래와 같이 입력하세요. <br>
-- -------------------------------------------------- <br>
-- 사번  |   이름   |      입사일     |   급여  <br>
-- -------------------------------------------------- <br>
-- 2001 |  장영실  |   2020-01-01   |   1500 <br>
-- -------------------------------------------------- <br>
-- 2002 |  최무선  |   2020-01-31   |   <br>
-- ---------------------------------------------------
```py
insert into emp_test values
(2001, '장영실', '2020-01-01', 1500),
(2002, '최무선', '2020-01-31', null);
```
```py
select * from emp_test;
```
```py
insert into emp_test2
select *
  from emp_test
  where emp_no in (1001, 1002);
```
```py
select * from emp_test2;
```
### update문으로 데이터 입력하기
- emp)update1 테이블을 생성 (emp_test로부터 복사)
- primary key 지정
```py
create table emp_update1
select * from emp_test;
```
```py
select * from emp_update1;
desc emp_update1;
desc emp_test;
```
```py
alter table emp_update1
  add constraint primary key (emp_no);    -- 제약사항
```
``` 
컬럼 추가 (Add)
ALTER TABLE table_name ADD COLUMN ex_column varchar(32) NOT NULL;

컬럼 변경 (Modify)
ALTER TABLE table_name MODIFY COLUMN ex_column varchar(16) NULL;

컬럼 이름까지 변경 (Change)
ALTER TABLE table_name CHANGE COLUMN ex_column ex_column2 varchar(16) NULL;

컬럼 삭제 (Drop)
ALTER TABLE table_name DROP COLUMN ex_column;

테이블 이름 변경 (RENAME)
ALTER TABLE table_name1 RENAME table_name2;

출처: https://extbrain.tistory.com/39
```
```py
create table emp_update2
select * from emp_test2;
```
```py
alter table emp_update2
  add constraint primary key (emp_no);
```
```py
desc emp_update2;
select * from emp_update2;
```
```py
select * from emp_update1;
```
### 단일 테이블 데이터 수정하기
```py
update emp_update1
  set emp_name = concat(emp_name, '2'),
	  salary = salary + 100;
```
```py
select * from emp_update1;
```
### (오류 예) primary key 중복 입력
```py
update emp_update1
  set emp_no  = emp_no + 1
  where emp_no >= 1018;
```  
- 뒤부터 입력(꼼수)
- 그러나 Primary key는 테이블의 근간이 되므로 수정하지 않아야 한다.
```py
update emp_update1
  set emp_no  = emp_no + 1
  where emp_no >= 1018
  order by emp_no desc;
```  
### 다중 테이블 데이터 수정하기
- 두 테이블 간 관계를 이용해서 업데이트
- 한 테이블(a)의 컬럼값을 참조해서 다른 테이블(b)의 컬럼값을 변경
```py
update emp_update1 a, emp_update2 b
  set a.salary = b.salary + 1000
  where a.emp_no = b.emp_no;
```
```py
  select * from emp_update1;
```  
- null 값 때문에 연산이 이루어지지 않을 때에는 0으로 바꾼 뒤에 다시 실행을 해주어야 한다.
```py
update emp_update1 a, emp_update2 b
  set a.salary = ifnull(a.salary, 0),
      b.salary = a.salary + 1000
  where a.emp_no = b.emp_no;
```
```py
select * from emp_update1;                                                                                                                                             ```
```py;
select * from emp_update2;
```
- null 값을 없애고 1000을 더해주는 것이 한 번에 되지 않아서 작업을 따로 분리해서 실행시켰다.
```py
update emp_update1 a, emp_update2 b
  set a.salary = ifnull(a.salary, 0)
  where a.emp_no = b.emp_no;
```
```
2000
0
0
4000
```
```py
update emp_update1 a, emp_update2 b
  set b.salary = a.salary + 1000
  where a.emp_no = b.emp_no;
```
```
3000
1000
1000
5000
```

-- 입력과 수정을 동시에 처리하기 <br>
-- on diplicate key <br>
-- emp_update2 테이블에 pk가 1003, 1004, 1005인 데이터를 입력 <br>
-- 수정 / 입력할 데이터는 emp_name 컬럼 <br>
-- 1003, 1004번은 수정, 1005번은 새롭게 입력

```
a 테이블
1003	다빈치2	2021-03-01	0
1004	리차드파인만2	2021-01-10	4000
1005	퀴리부인2	2021-03-01	4100
```
```
emp_update2 테이블
1001	아인슈타인	2021-01-01	3000
1002	아이작뉴턴	2021-02-01	1000
1003	다빈치	2021-03-01	1000
1004	리차드파인만	2021-01-10	5000
```
```py
insert into emp_update2
select * from emp_update1 a
  where emp_no between 1003 and 1005
  on duplicate key update emp_name = a.emp_name,
						  salary = a.salary;
```
```py
select * from emp_update2;
```
```
1001	아인슈타인	2021-01-01	3000
1002	아이작뉴턴	2021-02-01	1000
1003	다빈치2	2021-03-01	0
1004	리차드파인만2	2021-01-10	4000
1005	퀴리부인2	2021-03-01	4100
```

### (실습) emp_update2 테이블에서 사번이 1001과 1002인 사원명을
- emp_update1 테이블의 동일 사번을 가진 사원명으로 emp_update2에 변경하는 쿼리 작성하기
```pyupdate emp_update1 a, emp_update2 b
  set b.emp_name = a.emp_name
  where a.emp_no = b.emp_no
    and b.emp_no between 1001 and 1005;
```
```py
select * from emp_update1;
select * from emp_update2;
```

### Delete문으로 데이터 삭제하기
```py
create table emp_delete
select * from emp_test;
```
```py
alter table emp_delete
  add constraint primary key (emp_no);
```
```py
desc emp_delete;  
select * from emp_delete;
```
```py
create table emp_delete2
select * from emp_test2;
```
```py
alter table emp_delete2
  add constraint primary key (emp_no);
```
```py
desc emp_delete2;  
select * from emp_delete2;
```
### 단일 테이블 삭제
- (1) 조건(where)을 넣어서 삭제
```py
select * from emp_delete;
```
```py
delete from emp_delete
  where salary is null;
```
- (2) 모두 삭제
```py
delete from emp_delete;
```
- 데이터 복구
```py
insert into emp_delete
select * from emp_test;
```
- (3) order by, limit의 조합 추가
- 두 명의 맥스월 중 한 명(뒷번호 1018)만 삭제하기
```py
select * from emp_delete;
```
```py
delete from emp_delete
  where emp_name = '맥스웰'
  order by emp_no desc
  limit 1;
```

- 원하는 것인지 확인
```py
select * from emp_delete
  where emp_name = '맥스웰'
  order by emp_no desc
  limit 1;
```  
### 다중 테이블 삭제
- (1) 조건으로 삭제
```py
delete a, b
  from emp_delete a, emp_delete2 b
  where a.emp_no = b.emp_no;
```
```py
select * from emp_delete;    -- a table
select * from emp_delete2;   -- b table
```
- (2) 모두 삭제
```py
delete a, b
  from emp_delete a, emp_delete b;
```
```py
delete from emp_delete;
delete from emp_delete2;
```

- 데이터 복구
```py
select * from emp_test;
```
```py
insert into emp_delete
select * from emp_test
where emp_no <> 1018;   -- 1018번만 빼고 복사
```
```py
select * from emp_delete;
```
```py
insert into emp_delete2
select * from emp_test;
```
```py
select * from emp_delete2;
```
```py
insert into emp_delete values
(1019, '막스클랑크', '2021-04-05', 100);
```
```py
insert into emp_delete2 values
(1018, '맥스웰', '2021-04-05', 100),
(1019, '막스클랑크', '2021-04-05', 100);
```

### using 문법으로 테이블 삭제

```py
delete from b
using emp_delete a, emp_delete2 b
  where a.emp_no = b.emp_no;
```
```py
select * from emp_delete;  -- a table
select * from emp_delete2;  -- b table
```
### (실습) emp_delete 테이블에서 사원명이 막스클랑크인 데이터를 삭제하는데,
- 이번에는 사번이 빠른 1건만 삭제하는 쿼리 작성하기
```py
delete from emp_delete
  where emp_name = '막스클랑크'
  order by emp_no asc
  limit 1;
```
```py
select * from emp_delete;
```
```py
select * from emp_delete
  where emp_name = '막스클랑크'
  order by emp_no asc
  limit 1;
```
### (실습) box_office 테이블을 참조해 box_office_copy 테이블을 만들기 (create ~ select ~
- 이때 box_office 테이블에서 2019년도 개봉 영화 중 관객수가 800만명 이상인 데이터만 들어가야 함
```py
create table box_office_copy
select * from box_office
  where year(release_date) = 2019 and audience_num >= 8000000;
```
```py
select * from box_office_copy;
```
### (실습) box_office_copy 테이블 last_year_audi_num 이라는 int 컬럼을 추가한 뒤,
- box_office 테이블에서 2018년도 개봉영화와 box_office_copy(2019) 테이블의 순위가 같은 건에 대해
- last_year_audi_num에 2018년도의 관객수를 설정
```py
select years, movie_name, ranks, audience_num, last_year_audi_num from box_office_copy;
```
```py
ALTER TABLE box_office_copy ADD COLUMN last_year_audi_num int NOT NULL;
```
```py
update box_office_copy a, box_office b
  set a.audience_num = b.audience_num
  where year(b.release_date) = 2019
    and b.ranks = a.ranks;
```
```py
select * from box_office_copy;
```
```
12274996	16265618
11212710	13934592
9224582	13369064
6584915	12552283
none    none
5661128	9426011
5448134	8021145
```

### (실습) 사원의 부서 할당 정보가 들어있는 dept_emp 테이블에서
- 현재 일하고 있는 않은 사람 삭제하는 쿼리 작성하기
```py
create table dept_emp_test
select * from dept_emp;
```
```py
select count(*) from dept_emp_test;     -- 33188에서 24135로
```
```py
delete from dept_emp_test
where sysdate() <= from_date or sysdate() >= to_date;   -- not between도 사용가능
```
### 트랜잭션 처리하기
```py
select @@autocommit;
```
```py
set autocommit = 0;
set autocommit = 1;
```
### 트랜잭션용 테이블 생성
```py
create table emp_tran1
select * from emp_test;
```
```py
alter table emp_tran1
  add constraint primary key (emp_no);
```
```py
create table emp_tran2
select * from emp_test;
```
```py
alter table emp_tran2
  add constraint primary key (emp_no);
```
### DDL(Data Definition Language)
- 트랜잭션에 영향을 받지 않으므로 commit이나 rollback을 사용할 필요가 없음

### DML(Data Manipulation Language)
- 트랜잭션에 영향 받기에 commit이나 rollback 사용 가능

### 자동커밋 모두 비활성화 상태에서 트랜잭션 처리하기
```py
set autocommit = 0;
select @@autocommit;
```
### 데이터 삭제
```py
delete from emp_tran1;
delete from emp_tran2;
```
### 데이터 확인(데이터 없음)
```py
select * from emp_tran1;
select * from emp_tran2;
```
### 삭제 취소
```py
rollback;
```
### 데이터 확인(데이터 있음)
```py
select * from emp_tran1;
select * from emp_tran2;
```
### 데이터 삭제
```py
delete from emp_tran1;
```
### 삭제 반영
```py
commit;
```
### 데이터 확인(emp_tran1 데이터 없음)
```py
select * from emp_tran1;
select * from emp_tran2;
```

### 삭제 최소
```py
rollback;
```
### 데이터 확인(삭제 취소가 되지는 않음)
```py
select * from emp_tran1;
select * from emp_tran2;
```
-- > commit이나 rollback문을 만나게 되면 이 지점까지가 한 트랜잭션 (종료)
```py
select @@autocommit;
set autocommit = 1;
```
### 데이터 입력
```py
insert into emp_tran1
select * from emp_test;
```
```py
select * from emp_tran1;
```
### 입력 취소
```py
rollback;
```
### 데이터 확인(자동커밋이 활성화(@@autocommit = 1)된 상태라 입력(insert)이 실행됨과 동시에 commit이 이루어져 트랜잭션이 완료
```py
select * from emp_tran1;
```
- 자동커밋이 활성화된 상태에서 수동으로 트랜잭션을 처리하고 싶을 때
- start transaction문 사용 (일시적으로 자동커밋이 비활성화됨)
- commit이나 rollback을 만났을 때 트랜잭션이 종료, 자동커밋이 활성화됨
```py
select @@autocommit;  -- 1로 조회
```
```py
start transaction;  -- 일시적으로 자동커밋이 비활성화된 상태
```
### 데이터 삭제
```py
delete from emp_tran1
  where emp_no >= 1006;
```  
### 데이터 수정
```py
update emp_tran1
  set salary = 0
  where salary is null;
```
```py
select * from emp_tran1;
```
### start transaction 이후에 했던 작업들(삭제, 수정) 취소
```py
rollback;
```
### 데이터 확인
```py
select * from emp_tran1;
```
### savepoint문 사용방법
```py
start transaction;
```
### savepoint A 설정
```py
savepoint A;
```
### 데이터 삭제
```py
delete from emp_tran1
  where salary is null;
```  
### savepoint B 설정
```py
savepoint B;
```
### 데이터 삭제
```py
delete from emp_tran1
  where emp_name = '맥스웰'
  order by emp_no
  limit 1;
```
### savepoint B 이후 작업 취소
```py
rollback to savepoint B;
```
```py
select * from emp_tran1;
```
### 최종 반영
```py
commit;
```
```py
select * from emp_tran1;
```
- (실습) 수동으로 트랜잭션 처리하던 중 emp_tran2 테이블에서 salary 컬럼 값이 1000인 건을 삭제하려고 했는데,
- 실수로 1000이 아닌 100인 건을 삭제
- 삭제 전으로 되돌리는 과정을 쿼리문으로 작성하기
```py
select @@autocommit;  -- 1로 조회
```
```py
start transaction;
```
```py
savepoint C;
```
```py
delete from emp_tran2
  where salary = 100;
```
```py
rollback to savepoint C;
```
```py
commit;
```
## 데이터 분석에 유용한 분석 쿼
-- 개선된 서브쿼리 CTE 사용하기 <br>
-- 부서 관리자 테이블(dept_manager)과 사원 테이블(employees)을 조인해 <br>
-- 현재 관리자의 부서번호, 사번, 사원, 이름을 조회하는 쿼리 작성 후 <br>
-- 부서 테이블(departments)과 최종 조인해서 부서명까지 조회하는 쿼리
### (1) 서브쿼리 방식
```py
select a.dept_no, a.dept_name, manager.emp_no, manager.first_name, manager.last_name
  from departments a,
(select b.dept_no, b.emp_no, c.first_name, c.last_name
  from dept_manager b, employees c
  where b.emp_no = c.emp_no
  and sysdate() between b.from_date and b.to_date
) manager
where a.dept_no = manager.dept_no;
```

### (2) CTE 방식
```py
with manager as (select b.dept_no, b.emp_no, c.first_name, c.last_name
  from dept_manager b, employees c
  where b.emp_no = c.emp_no
  and sysdate() between b.from_date and b.to_date
)
select a.dept_no, a.dept_name, b.emp_no, b.first_name, b.last_name
  from departments a, manager b
  where a.dept_no = b.dept_no;
```  
- 현재 시점을 기준으로 각 부서에 속한 사원들의 총 급여에 대한 부서별 평균을 구하는 쿼리 작성하기
### (1) 서브쿼리 방식
```py
select avg(f.dept_salary_sum)  -- 9개 부서에 지출되는 총급여 자체의 평균 193044765.5556
from
(
select a.dept_no, a.dept_name, sum(c.salary) dept_salary_sum, avg(c.salary) dept_salary_avg
  from departments a, dept_emp b, salaries c
  where a.dept_no = b.dept_no
    and b.emp_no = c.emp_no
    and sysdate() between b.from_date and b.to_date
    and sysdate() between c.from_date and c.to_date
  group by a.dept_no
  ) f;
```

### (2) CTE
- 서브쿼리만 만들 수 있으면 굉장히 변환시켜줄 수 있다.
```py
with dept_info as (select a.dept_no, a.dept_name, sum(c.salary) dept_salary_sum, avg(c.salary) dept_salary_avg
  from departments a, dept_emp b, salaries c
  where a.dept_no = b.dept_no
    and b.emp_no = c.emp_no
    and sysdate() between b.from_date and b.to_date
    and sysdate() between c.from_date and c.to_date
  group by a.dept_no
)
select avg(f.dept_salary_sum) -- 9개 부서에 지출되는 총급여 자체의 평균 193044765.5556
from dept_info f;
```
```py
with dept_info as (select a.dept_no, a.dept_name, sum(c.salary) dept_salary_sum, avg(c.salary) dept_salary_avg
  from departments a, dept_emp b, salaries c
  where a.dept_no = b.dept_no
    and b.emp_no = c.emp_no
    and sysdate() between b.from_date and b.to_date
    and sysdate() between c.from_date and c.to_date
  group by a.dept_no
),
dept_avg as
(
select avg(f.dept_salary_sum) dept_avg_salary -- 9개 부서에 지출되는 총급여 자체의 평균 193044765.5556
from dept_info f
)
select a.dept_no, a.dept_salary_sum, b.dept_avg_salary
  from dept_info a, dept_avg b;
```  
### window function

- box_office 테이블에서 2018년 이후 개봉된 영화 중에서 랭킹 10위 안에 든 영화들의
- "연도별" 총 매출액과 평균 매출액을 구하되,
- 집계되기 전의 개별 영화이름, 랭킹, 매출액도 함께 표시하기
### (CTE 사용)
```py
select years, sum(sale_amt), avg(sale_amt)
  from box_office
  where year(release_date) >= 2018 and ranks <= 10
  group by year(release_date);
```
```py
select movie_name, ranks, sale_amt
  from box_office
  where year(release_date) >= 2018 and ranks <= 10;
```  
### 서브쿼리
```py
select a.movie_name 이름, a.ranks 순위, a.sale_amt 매출액, f.sale_sum 합계, f.sale_avg 평균
  from box_office a,
  (
  select years, sum(sale_amt) sale_sum, avg(sale_amt) sale_avg
  from box_office
  where year(release_date) >= 2018 and ranks <= 10
  group by year(release_date)
  ) f
  where year(release_date) >= 2018 and ranks <= 10
  group by year(release_date), ranks;
```
### CTE
```py
with box_office_sale as (
 select years, sum(sale_amt) sale_sum, avg(sale_amt) sale_avg
  from box_office
  where year(release_date) >= 2018 and ranks <= 10
  group by year(release_date)
)
select a.years 연도, a.movie_name 이름, a.ranks 순위, a.sale_amt 매출액, b.sale_sum 합계, b.sale_avg 평균
  from box_office a, box_office_sale b
  where year(release_date) >= 2018 and ranks <= 10
  group by year(release_date), ranks
  order by a.ranks;
```
### 윈도우 함수 사용
```py
select year(release_date), movie_name, ranks, sale_amt,
  sum(sale_amt) over (partition by year(release_date)) 합계,
  avg(sale_amt) over (partition by year(release_date)) 평균
  from box_office
  where year(release_date) >= 2018
    and ranks <= 10;
```    
- 1위인 영화들의 평균 매출액보다 큰 매출액이 큰 영화만 조회
### (CTE 방식)
```py
with avg_top_movie as (
select avg(sale_amt) avg_sale_amt
  from box_office
  where ranks = 1
  ) 
select a.movie_name, a.years, a.sale_amt, b.avg_sale_amt
  from box_office a, avg_top_movie b
  where a.ranks = 1
  order by years;
```  
### 윈도우 함수
```py
select movie_name, years, sale_amt,
avg(sale_amt) over (partition by ranks) 합계
  from box_office
  where ranks = 1;
```  
- 1위인 영화들의 평균 매출액과 개별 영화이름, 랭킹, 매출액 조회하기
### (CTE 방식)
```py
with avg_first as
(
select avg(sale_amt) avg_amt
  from box_office
 where ranks = 1
)
select year(a.release_date), a.ranks, a.movie_name, a.sale_amt, b.avg_amt
  from box_office a, avg_first b
 where a.ranks = 1
   -- and a.sale_amt > b.avg_amt
 order by 1;
``` 
### (2) 윈도우 함수  
```py
select year(release_date), ranks, movie_name, sale_amt,
  avg(sale_amt) over(partition by ranks) avg_amt
  from box_office
 where ranks = 1;
``` 
 - 참고 window 함수에는 평균 매출보다 큰 조건이 안들어가서 아래와같이 cte 사용하여 해결
 ```py
 with avg_info as
 (
 select year(release_date), ranks, movie_name, sale_amt,
  avg(sale_amt) over(partition by ranks) avg_amt
  from box_office
 where ranks = 1
 )
 select year(a.release_date), a.ranks, a.movie_name, a.sale_amt, b.avg_amt
  from box_office a, avg_info b
   where a.ranks = b.ranks	
     and a.sale_amt = b.sale_amt
     and a.sale_amt > b.avg_amt;
```
### (2) 윈도우 함수
- 테이블 생성
```py
create table emp_hierarchy (
  employee_id int,
  emp_name varchar(80),
  manager_id int,
  salary int,
  dept_name varchar(80)
);
```
```py
 insert into emp_hierarchy values
(200,'Jennifer Whalen',101,4400,'Administration'),
(203,'Susan Mavris',101,6500,'Human Resources'),
(103,'Alexander Hunold',102,9000,'IT'),
(104,'Bruce Ernst',103,6000,'IT'),
(105,'David Austin',103,4800,'IT'),
(107,'Diana Lorentz',103,4200,'IT'),
(106,'Valli Pataballa',103,4800,'IT'),
(204,'Hermann Baer',101,10000,'Public Relations'),
(100,'Steven King',null,24000,'Executive'),
(101,'Neena Kochhar',100,17000,'Executive'),
(102,'Lex De Haan',100,17000,'Executive'),
(113,'Luis Popp',108,6900,'Finance'),
(112,'Jose Manuel Urman',108,7800,'Finance'),
(111,'Ismael Sciarra',108,7700,'Finance'),
(110,'John Chen',108,8200,'Finance'),
(108,'Nancy Greenberg',101,12008,'Finance'),
(109,'Daniel Faviet',108,9000,'Finance'),
(205,'Shelley Higgins',101,12008,'Accounting'),
(206,'William Gietz',205,8300,'Accounting');
```
```py
select * from emp_hierarchy;
```
- 부서별 salary 합계
```py
select *,
sum(salary) over (partition by dept_name
				  order by dept_name) sum_salary
  from emp_hierarchy;
```  
- 그러나 order by 뒤에 기본값으로 프레임의 범위가 지정되어 있는다.
- order by가 지정되어 있을 떄와 order by가 지정되지 않았을 때 차이가 있음

-- order by가 지정되어 있을 경우에는 <br>
-- range between unbounded preceding and current row이며 <br>
-- 그런 이유로 sum_salary가 위에 order by를 지정하지 않았을 때와 다른 값으로 표시가 됨 <br>
-- unbounded following (월급이 처음부터 합계로 나옴) <br>
-- 해당 파티션 안에서 sum 값이 동일하게 지정되게 하고자 한다면 <br>
-- rows between unbounded preceding and unbounded following과 같이 기본값을 변경해 주면 됨
```py
select *,
sum(salary) over (partition by dept_name
				  order by salary rows between unbounded preceding and unbounded following) sum_salary
  from emp_hierarchy;
```  
- current row (월급이 누적합 형태로 나옴)
```py
select *,
sum(salary) over (partition by dept_name
				  order by salary rows between unbounded preceding and current row) sum_salary
  from emp_hierarchy;
```  
- row_number(): 로우의 순번
```py
select *,
row_number() over (partition by dept_name
				  order by salary) sequence
  from emp_hierarchy;
```  
-- rank(): 순위
-- dense_rank(): 누적 순위
-- percent_rank(): 비율 순위(rank()-1)/(row-1), 상위 몇 % ~ 
```py
select *,
rank() over (partition by dept_name order by salary ) ranks,
percent_rank() over (partition by dept_name order by salary ) percent_ranks
  from emp_hierarchy;
```  
-- lag(컬럼명): 현재 로우를 기준으로 바로 앞 로우의 컬럼 가져오기, lag(컬럼명, 1, null)와 같음 <br>
-- lead(컬럼명): 현재 로우를 기준으로 바로 뒤 로우의 컬럼 가져오기, lead(컬럼명, 1, null)와 같음
```py
select employee_id, emp_name, manager_id, salary, dept_name,
  lag(salary) over (partition by dept_name order by salary desc) lag_,
  lead(salary) over (partition by dept_name order by salary desc) lead_
  from emp_hierarchy;
```  
-- lag(컬럼명, n, null) <br>
-- lag(컬럼명, n, '값'): 현재 로우를 기준으로 n행 앞의 로우의 컬럼값을 가져오기 <br>
-- lead(컬럼명, n, null) <br>
-- lead(컬럼명, n, '값'): 현재 로우를 기준으로 n행 뒤의 로우의 컬럼값을 가져오기 <br>
```py
select employee_id, emp_name, manager_id, salary, dept_name,
  lag(salary, 2, 0) over (partition by dept_name order by salary desc) lag_,
  lead(salary, 2, 0) over (partition by dept_name order by salary desc) lead_
  from emp_hierarchy;
```  
### (실습) box_office 테이블에서 해마다 1위였던 영화들에 대해 전년도 기준으로 다음연도 매출의 증감율 구하기
```py
select years, ranks, movie_name, format(sale_amt, 0),
format(lag(sale_amt) over (partition by ranks), 0) last_year_sale_amt,
format((sale_amt - lag(sale_amt) over (partition by ranks))/ lag(sale_amt) over (partition by ranks) * 100, 0) 증감율
  from box_office
  where ranks = 1
  order by 1;
```  
- 매출 증감율 : (올해 매출 - 전년 매출)/전년 매출 * 100
```py
select year(release_date) release_year, ranks, movie_name, sale_amt curr_year_sale_amt,
  lag(sale_amt) over (order by year(release_date)) last_year_sale_amt
  from box_office
 where ranks = 1
 order by 1;
```
```py
with sale_amt_summary as
(select year(release_date) release_year, ranks, movie_name, sale_amt curr_year_sale_amt,
  lag(sale_amt) over (order by year(release_date)) last_year_sale_amt
  from box_office
 where ranks = 1
 order by 1
 )
 select release_year, ranks, movie_name, curr_year_sale_amt, last_year_sale_amt, 
        (curr_year_sale_amt - last_year_sale_amt)/last_year_sale_amt*100 as rates
 from sale_amt_summary;
 ```
 ### (실습) box_office 테이블에서 2019년 개봉 영화의 월별 총 매출액과 전월 대비 증감율을 구하는 쿼리 작성하기
 - (1) 월별 매출 합
 ```py
 select year(release_date), month(release_date), sum(sale_amt)
   from box_office
   where year(release_date) = 2019
   group by month(release_date)
   order by 2;
 ```
 - (2) (1)의 쿼리에 추가하여 전월 매출까지 표시
 ```py
 select year(release_date) 연도, month(release_date) 월, sum(sale_amt) 매출합,
  lag(sum(sale_amt)) over (order by month(release_date)) 전월매출합
   from box_office
   where year(release_date) = 2019
   group by month(release_date)
   order by 2;
```   
 - (3) 최종적으로 매출 증감율 구하기
```py
 with month_sale_amt as
 (
 select year(release_date) 연도, month(release_date) 월, sum(sale_amt) 매출합,
  lag(sum(sale_amt)) over (order by month(release_date)) 전월매출합
   from box_office
   where year(release_date) = 2019
   group by month(release_date)
   order by 2
 )
select 연도, 월, 매출합, 전월매출합, round((매출합 - 전월매출합) / 전월매출합 * 100, 2) as 매출증감율
  from month_sale_amt;
```  
-- 프레임절로 집계 범위 조정하기 <br>
-- https://dev.mysql.com/doc/refman/8.0/en/window-functions-frames.html <br>
-- with order by: RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW <br>
-- without order by: RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING <br>

-- 부서별 salary 합계: sum() over ~ 
-- without order by
```py
select *,
  sum(salary) over (partition by dept_name) sum_salary
  from emp_hierarchy;
```  
- with order by
```py
select *,
  sum(salary) over (partition by dept_name order by salary) sum_salary
  from emp_hierarchy;
```  
-- ROWS와 RANGE의 차이
-- ROWS: 현재 로우를 기준으로 로우 단위로 대상 프레임 지정
-- RANGE: 현재 로우를 기준으로 값의 범위 단위로 대상 프레임 지정
```py
select *,
  sum(salary) over (partition by dept_name order by salary rows between unbounded preceding and current row) row_sum_salary,
  sum(salary) over (partition by dept_name order by salary range between unbounded preceding and current row) range_sum_salary
  from emp_hierarchy;
```
```py
select *,
  sum(salary) over (partition by dept_name order by salary rows between 1 preceding and 1 following) row_sum_salary,
  sum(salary) over (partition by dept_name order by salary range between 1000 preceding and 1000 following) range_sum_salary
  from emp_hierarchy;
```  
### 뷰 생성하기
```py
select *
  from dept_emp
  where sysdate() between from_date and to_date;
```
```py
create or replace view dept_emp_v as 
select *
  from dept_emp
  where sysdate() between from_date and to_date;
```
```py
select *
  from dept_emp_v;
```  
### 뷰 수정하기
- option 1
```py
create or replace view dept_emp_v as 
select emp_no, dept_no
  from dept_emp
  where sysdate() between from_date and to_date;
```
```py
select *
  from dept_emp_v;
```  
- option 2
```py
alter view dept_emp_v as
select *
  from dept_emp
  where sysdate() between from_date and to_date;
```
```py
select *
  from dept_emp_v;
```  
### 뷰 삭제하기
```py
drop view dept_emp_v;
```
-- 복잡한 쿼리를 뷰로 만들기
-- 1위인 영화들의 평균 매출보다 큰 영화
```py
create or replace view sale_amt_v as
with avg_info as
 (
 select year(release_date), ranks, movie_name, sale_amt,
  avg(sale_amt) over(partition by ranks) avg_amt
  from box_office
 where ranks = 1
 )
 select year(a.release_date), a.ranks, a.movie_name, a.sale_amt, b.avg_amt
  from box_office a, avg_info b
   where a.ranks = b.ranks	
     and a.sale_amt = b.sale_amt
     and a.sale_amt > b.avg_amt;
```
```py
select *
  from sale_amt_v;
```
```py
select *
  from sale_amt_v
  order by sale_amt;
```
```py
select *
  from sale_amt_v
  order by 1;
```
