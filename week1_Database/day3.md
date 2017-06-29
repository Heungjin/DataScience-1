# 3일차 


-----------------------


#### **1. 기본 실습**


>demo_madang_init 열기 한 후에

>>코드 ctrl + a -> ctrl + enter


>>데이터베이스 접속 명령어 : conn

```sql
select *
from Book;
-- Book의 모든 것을 보여줌

select phone
FROM Customer
WHERE name='김연아'
-- Customer중 name을 검색하여 phone을 보여줌 (name, phone을 다 보여주고 싶으면 select phone, name)

select DISTINCT name 
-- 중복 제거 셀렉트문

select *
from book
where bookname like '_구%' 
-- 책의 이름에서 두번째 문자가 '구'인 책들 찾음.
```

> 여러 가지 예제들
```sql
select *
from book
order by price DESC, publisher ASC;

select *
from book
where price between 10000 and 20000;

select *
from book
where publisher not in ('굿스포츠', '대한미디어')

select *
from book
where publisher LIKE '굿스포츠' or publisher LIKE '대한미디어'

select bookname, publisher
from book
where bookname LIKE '축구의 역사'

select bookname, publisher
from book
where bookname LIKE '%축구%'

select *
from book
where price >= 20000 and bookname like '%축구%'

select *
from book
where publisher in ('굿스포츠', '대한미디어')

SELECT * 
FROM Book
WHERE Bookname LIKE '%억'
SELECT * 
FROM Book
WHERE Bookname LIKE '%억'

select name
from orders, customer
where saleprice between 15000 and 20000

select *
from book
order by price DESC, publisher ASC;
```

-----------------------


#### **2. 함수 사용등 응용 실습**

```sql
select saleprice, custid
from orders

select sum(saleprice)
from orders

select sum(saleprice) as 총매출
from orders
where custid=2;

select sum(saleprice) as Total,
        avg(saleprice) as Average,
        min(saleprice) as Minimum,
        max(saleprice) as Maximum
from orders

select count(*)
from orders

select sum(saleprice) as "총 매출" -- 쌍따옴표로 해야 가능. 속성의 string은 쌍따옴표로.
from orders

select custid, count(*) as 도서수량, sum(saleprice) as 총액
from orders
group by custid;

select custid, count(*) as 도서수량, sum(saleprice) as 총액
from orders
where saleprice >= 8000 -- saleprice가 8000 이상인것만 연산에 포함
group by custid
having count(*) >= 2; -- having 조건은 순서가 중요하다. 여기서는 뒤에 나오는게 중요.
-- having은 검색조건 문법.
```



연습

```sql

-- 가격이 10000원 이상인 도서를 구매한 고객에 대하여 총 도서 판매액을 구하시오.
select custid, sum(saleprice) as "총 도서 판매액"
from orders
where saleprice >= 10000
group by custid;

-- 고객별로 주문한 도서의 수량과 평균 판매액을 구하시오
select custid, count(*) as 도서수량, avg(saleprice)
from orders
group by custid

-- 가격이 10000원 이상인 도서를 구매한 고객에 대하여 고객별 주문 도서의 총 수량을 구하시오. 단, 고객ID를 기준으로 정렬하시오.
select custid, count(*) 총수량
from orders
where saleprice >= 10000
group by custid
order by custid;

-- 총 만원이상 구매한 사람의 목록을 구하시오
select custid, sum(saleprice)
from orders
where saleprice >= 10000
group by custid

-- 1번 박지성 고객이 주문한 도서의 총 판매액을 구하세용
select custid, sum(saleprice) as 판매액
from orders
where custid=1
group by custid;

-- 축구 관련 도서를 구매한 고객에 대하여 고객별 주문 도서의 총 수량을 구하시오. 단, 두 권 이상 구매한 고객만 구하시오
select custid, count(*) as 수량
from orders
where bookid in (1,2,3)
group by custid
having count(*) >= 2;

-- 도서번호가 1인 도서의 이름
select bookname
from book
where bookid=1

-- 가격이 20000원 이상인 도서의 이름
select bookname, price
from book
where price >= 20000

-- 서점 도서의 총 개수
select count(*) as "총 개수"
from book

-- 서점에 도서를 출고하는 출판사의 총 개수
select count(DISTINCT publisher) as "출판사 개수"
from book

-- 모든 고객의 이름, 주소
select name, address
from customer

-- 2014.7.4 ~ 7.7 사이에 주문받은 도서의 주문번호
select orderid
from orders
where orderdate between '14/07/04' and '14/07/07'

-- 2014.7.4 ~ 7.7 사이에 주문받지 않은 도서의 주문번호
select orderid
from orders
where orderdate not between '14/07/04' and '14/07/07'

-- 성이 김씨인 고객의 이름과 주소
select name, address
from customer
where name like '김%'

-- 성이 김씨이고 아로 끝나는 고객의 이름과 주소
select name, address
from customer
where name like '김%' and name like '%아'

```

-----------------------

#### **3. k-ict**
>https://kbig.kr/ -> 인프라 -> 분석실습 관리

-----------------------