### 오라클 공부하고 정리하는 곳
  
오라클 기본 명령어
-  
sqlplus /nolog << sqlplus 진입 명령어  
conn sys as sysdba << sys계정(데이터베이스 최상위 관리자 계정) 로그인  
show user << 현재 접속중인 계정 확인  
create user c##아이디 identified by 비밀번호; << 계정생성(sys계정으로 접속해서 생성해야함)  
conn c##아이디/비밀번호 << 생성한 아이디 로그인  
grant connect,resource,dba to c##아이디; << 생성한 계정에 권한을 부여(sys계정 접속한 상태에서 가능)  
alter user c#아이디 identified by 비밀번호; << 만든 계정 비밀번호 변경  
select * from tab;  
  
테이블 생성  
-  
create table 테이블명 (컬럼명 자료형,  
                                   컬럼명 자료형,  
                                   컬럼명 자료형,  
                                   );  
  
 
  
테이블에 데이터 입력 
-
  
insert into 테이블명(컬럼명,컬럼명,...) values(들어갈 값, 들어갈 값,...);  
테이블에 전체 데이터를 넣는다면  
insert into 테이블명 values (값, 값, ...); 으로 생략 가능  
commit; < 모든 입력이 끝나면 반드시 commit;을 해줘야 완료  
insert into 테이블명 values ('','',null,null);  
  

데이터 검색 
-
select * from tab; 현재 데이터베이스에 있는 테이블 정보 출력  
desc 테이블명;  테이블 상세 내용 출력 
select 컬럼명, 컬럼명,... from 테이블명;   
select * from 컬럼명; < 테이블의 모든 컬럼이 출력된다. ( * 을 넣으면 모든 컬럼이 출력)  
select * from 테이블명; < 테이블의 모든 컬럼이 출력된다. ( * 을 넣으면 모든 컬럼이 출력)  
이름과 나이만 출력하고싶으면  
select name, age from 테이블명;  
원하는 데이터(row)만 출력하고싶으면 where절 사용  
select * from 테이블명 where name = '김민기';  
나이가 25보다 큰 사람만 출력하고싶으면  
select * from 테이블명 where age>25;  
  
데이터 변경하기  
-
update 테이블명 set 컬럼명=변경값, 컬럼명=변경값, .... where 조건;  
human 테이블의 age를 100으로 변경하려면  
update human set age=100; < human테이블의 모든 age 데이터가 100으로 변경됨  
commit;을 사용하면 저장이 되고, rollback;을 하면 원래 age값으로 다시 돌아감  
특정 데이터만 변경하고싶으면 where절을 사용해서  
김민기의 나이와 키를 바꾸려면  
update human set age=28, height=180 where name = '김민기';  
작업을 완료하려면 commit; 되돌리려면 rollback;  
  
데이터 삭제하기  
-
delete from 테이블명 where 삭제조건;  
나이가 30보다 큰 사람의 데이터를 삭제하려면  
deletr from 테이블명 where age>30;  
테이블에서 null값 삭제하는 명령어 : delete from 테이블명 where name is null;  
commit; or rollback;  
  
테이블 삭제  
-
drop table 테이블명;  
  
Null 처리  
=
  
NVL 함수 = NVL(대상, null인 경우 값)  
-
ex) select nvl(car, 0) from cars;  
cars테이블에 car가 null일 경우 0으로 치환  
  
NVL2 함수 = NVL2(대상, null 아닌경우에 값, null인 경우 값) 
-
ex) select nvl2(car, car, '차량미보유') from cars;  
cars 테이블에 car가 null이 아닌경우 car 로 치환  
cars 테이블에 car가 null일 경우 '차량미보유'로 치환  
  
Decode 문법
-
select decode(컬럼명, 값1, 변경값1,    
			           값2, 변경값2, ...   
			           '나머지 경우 변경값');  
			from 테이블명;  
  
ex) 사원 테이블에서 10, 20, 30 부서는 숫자 + '부서입니다.'  
나머지 부서는 '그밖에 부서입니다.' 가 출력되도록 쿼리 작성  
select decode(department_id, 10, '10번 부서',   
			 20, '20번 부서',  
			 30, '30번 부서',   
			 '나머지 부서')  
	    		 from 테이블명  
  
Case 문법
-
select 컬럼명(생략가능),  
		case when 조건식1 then 값1  
		case when 조건식2 then 값2  
		case when 조건식3 then 값3  
		else 값4 end as '별명'  
		from 테이블명;  
출력예  
  
컬럼명	별명  
값	     값1or2or3or4  
값	     값1or2or3or4  
값	     값1or2or3or4  
값	     값1or2or3or4  
  
case 문법 = select   
	case when 조건식1 then 값1  
	case when 조건식2 then 값2  
	case when 조건식3 then 값3  
	else 값4 end as '별명'  
	from 테이블명;  
  
출력예  
  
별명  
값1or2or3or4  
값1or2or3or4  
값1or2or3or4  
값1or2or3or4  
  
  
And or not 논리 연산자  
=
  
and연산  
-
select 컬럼명 from 테이블명 where 조건 and 조건;  
  
or연산  
-
select 컬럼명 from 테이블명 where 조건 or 조건;  
  
not연산  
-
select 컬럼명 from 테이블명 where 컬럼명!=조건;  
select 컬럼명 from 테이블명 where not 컬럼명1=조건;  
  
  
Between 연산자  
-
between은 특정 컬럼의 특정 범위에 해당하는 값을 출력하고 싶을 때 사용한다  
  
where 컬럼명 between a and b - a,b를 '포함'한 사이값을 찾음  
where 컬럼명 not between a and b - a,b를 '포함'한 사이값을 제외한 모든 데이터를 찾음  
  
between을 이용해서 문자열(ex 사원이름)을 검색할때  
첫번째 이름이 A~C인 사람을 검색하고싶으면  
select * from 테이블명 where first_name between 'A' and 'D(원하는 검색최대값+1인 D)' and first_name!='D';  
를 해주는게 좋다.  
이유는 사원이름이 ABC, BCA, CEE, CZZ가 있다면  
between 'A' and 'C' 를 하면  
앞에 한 글자만 C만 조회해서 CEE, CZZ는 C보다 큰 값이라 검색이 안된다.  
억지로 between 'A' and 'C'를 하고싶으면  
첫글자가 C인 이름중 최대값인 CZZ를 넣어서  
between 'A' and 'CZZ' 로 해줘야 정상적으로 출력가능해서  
이렇게 불편하게 하는거보단  
원하는 최대 검색값인 C의 다음인 D로 검색을 하고 뒤에 조건 and first_name!='D' 을 넣어서  
잘라주는게 깔끔하기 때문  
  
In 연산자  
-
  
컬럼 in (값1, 값2, 값3) 해당 컬럼의 값으로 값1, 값2, 값3중 하나를 가지고 있으면 출력  
컬럼 not in (값1, 값2, 값3) 해당 컬럼의 값으로 값1, 값2, 값3중 하나를 가지고 있으면 출력되지 않는다(값1,값2,값3이 없으면 출력된다)  
select * from 테이블명 where 컬럼명 in (값);  
select * from 테이블명 where 컬럼명 not in (값);  
null은 사용불가함( is null 이나 nvl등을 사용해서 null처리 가능)  
  
Like 연산자 
-
like연산자는 부분 문자열을 이용해서 원하는 문자열을 찾을 수 있다.  
where 컬럼명 like ‘부분 문자열’  
부분문자열에 %는 문자가 없거나 하나 이상의 어떤 문자가 와도 상관 없다는 의미로  
사용되고 밑줄 _ 은 반드시 하나의 어떤 문자가 와야 할때 사용된다.  
where 컬럼명 not like ‘부분 문자열’ 부분 문자열에 해당하지 않는 문자열을 출력한다.  
-‘hi’ 해당 컬럼 문자열이 hi인 데이터만 검색  
-‘hi%’ hi로 시작하는 모든 문자열  
-‘%hi’ hi로 끝나는 모든 문자열  
-‘%hi%’ hi가 들어간 모든 문자열  
-‘%%’ 모든 문자열   
-‘_ _’ 글자수가 2개인 모든 문자열 ‘a’ (x)  
-‘_hi’ 3글자인데 hi로 끝나는 모든 문자열    
-‘hi_’ 3글자인데 hi로 시작하는 모든 문자열  
-‘_hi_’ 4문자이고 두번째위치에 hi가 들어간 모든 문자열  
-‘_ _%’ 두글자 이상의 모든 데이터 (‘hi’)(0)  
