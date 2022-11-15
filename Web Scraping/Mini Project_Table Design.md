# Melon Chart Analysis Project
> 2012~2022년도 가수와 곡들에 대한 분석



- 데이터 분석을 위한 테이블 설계

## 데이터베이스 생성

create database melon;

use melon;

## top100 테이블 생성

create table top100 (  <br>
    years int,      <br>
    ranks int,    <br>
    song_name varchar(300),   <br>
    singer_name varchar(300), <br>
    likes VARCHAR(300)<br>
);

## artist_rank_top5 테이블 생성

create table artist_rank_top5 (<br>
    ranks int,<br>
    singer_name varchar(200),<br>
    Top10_Share VARCHAR(200),<br>
    man_share varchar(200),<br>
    woman_share varchar(200),<br>
    teenager VARCHAR(200),<br>
    twenty VARCHAR(200),<br>
    thirty VARCHAR(200),<br>
    forty VARCHAR(200),<br>
    fifty VARCHAR(200),<br>
    others VARCHAR(200)<br>
);

## artist_rank_top50 테이블 생성

create table artist_rank_top50 (<br>
    ranks int,<br>
    singer_name varchar(200),<br>
    fans VARCHAR(300),<br>
    detail_score_music float,<br>
    detail_score_ascending_fans float,<br>
    detail_score_likes float,<br>
    detail_score_photo float,<br>
    detail_score_video float<br>
);

## circle_digital_chart_top100 테이블 생성

create table circle_digital_chart_top100 (<br>
    ranks int,<br>
    song_name varchar(100),<br>
    singer_name varchar(200),<br>
    production varchar(100),<br>
    year int<br>
);
