# Oracle-SQL

#오라클 공부내용
#2022-10-20
#sqlplus /nolog << sqlplus 진입 명령어
#conn sys as sysdba << sys계정(데이터베이스 최상위 관리자 계정) 로그인
#show user << 현재 접속중인 계정 확인
#create user c##아이디 identified by 비밀번호; << 계정생성(sys계정으로 접속해서 생성해야함)
#conn c##아이디/비밀번호 << 생성한 아이디 로그인
#grant connect,resource,dba to c##아이디; << 생성한 계정에 권한을 부여(sys계정 접속한 상태에서 가능)
#alter user c#아이디 identified by 비밀번호; << 만든 계정 비밀번호 변경
#select * from tab;
#테이블 생성 : create table 테이블명 (컬럼명 자료형,
                                   컬럼명 자료형,
                                   컬럼명 자료형,
                                   );
#select * from tab; < 현재 데이터베이스에 있는 테이블 정보 출력
desc 테이블명; < **테이블 상세 내용 출력
테이블에 데이터 입력
insert into 테이블명(컬럼명,컬럼명,...) values(들어갈 값, 들어갈 값,...);
테이블에 전체 데이터를 넣는다면
insert into 테이블명 values (값, 값, ...); 으로 생략 가능
commit; < 모든 입력이 끝나면 반드시 commit;을 해줘야 완료
insert into 테이블명 values ('','',null,null);
테이블에서 null값 삭제하는 명령어 : delete from 테이블명 where name is null;

데이터 검색
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
update 테이블명 set 컬럼명=변경값, 컬럼명=변경값, .... where 조건;
human 테이블의 age를 100으로 변경하려면
update human set age=100; < human테이블의 모든 age 데이터가 100으로 변경됨
commit;을 사용하면 저장이 되고, rollback;을 하면 원래 age값으로 다시 돌아감
특정 데이터만 변경하고싶으면 where절을 사용해서
김민기의 나이와 키를 바꾸려면
update human set age=28, height=180 where name = '김민기';
작업을 완료하려면 commit; 되돌리려면 rollback;
데이터 삭제하기
delete from 테이블명 where 삭제조건;
나이가 30보다 큰 사람의 데이터를 삭제하려면
deletr from 테이블명 where age>30;
commit; or rollback;
테이블 삭제
drop table 테이블명;
