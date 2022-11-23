# SQL

```sql
CREATE TABLE branch
(
branch_name CHAR(20) NOT NULL,
adress      VARCHAR(30) NOT NULL,
assets      BIGINT NOT NULL,
PRIMARY KEY(branch_name),
CHECK(assets>=0)
);

CREATE TABLE employee
(
employee_num  INT NOT NULL auto_increment,
workplace     CHAR(20) NOT NULL,
employee_name CHAR(10) NOT NULL,
position      CHAR(20) NOT NULL,
phone_num     CHAR(15) NOT NULL,
PRIMARY KEY(employee_num),
FOREIGN KEY(workplace) REFERENCES branch(branch_name) ON UPDATE CASCADE
);

CREATE TABLE stm
(
s_device_num           INT NOT NULL auto_increment,
management_branch_name CHAR(20) NOT NULL,
address                 VARCHAR(30) NOT NULL,
installation_date      DATE,
PRIMARY KEY(s_device_num),
FOREIGN KEY(management_branch_name) REFERENCES branch(branch_name) ON
UPDATE CASCADE
);

CREATE TABLE atm
(
a_device_num           INT NOT NULL auto_increment,
management_branch_name CHAR(20) NOT NULL,
address                 VARCHAR(30) NOT NULL,
installation_date      DATE,
PRIMARY KEY(a_device_num),
FOREIGN KEY(management_branch_name) REFERENCES branch(branch_name) ON
UPDATE CASCADE
);

#ALTER TABLE atm CHANGE adress address VARCHAR(30) NOT NULL;

CREATE TABLE client
(
client_num          INT NOT NULL auto_increment,
client_name         VARCHAR(10) NOT NULL,
client_address      VARCHAR(30) NOT NULL,
client_rank         CHAR(10) NOT NULL DEFAULT "프리미엄 스타",
security_rank       CHAR(10) NOT NULL DEFAULT "보안카드",
client_age          SMALLINT NOT NULL,
account_possibility BOOL NOT NULL,
job                 VARCHAR(10),
PRIMARY KEY(client_num)
);

CREATE TABLE account
(
account_num            VARCHAR(20) NOT NULL,
client_num             INT NOT NULL,
employee_num_in_charge INT,
balance                BIGINT NOT NULL DEFAULT 0,
ic_date                DATE NOT NULL,
PRIMARY KEY(account_num),
FOREIGN KEY (client_num) REFERENCES client(client_num) ON UPDATE CASCADE,
FOREIGN KEY (employee_num_in_charge) REFERENCES employee(employee_num) ON
UPDATE CASCADE,
CHECK(balance >= 0)
);

CREATE TABLE card_product_type
(
product_num  INT NOT NULL auto_increment,
product_name VARCHAR(20) NOT NULL,
PRIMARY KEY(product_num)
);

CREATE TABLE card
(
card_num    VARCHAR(20) NOT NULL,
account_num VARCHAR(20) NOT NULL,
client_num  INT NOT NULL,
product_num INT NOT NULL,
validation_date DATE NOT NULL,
is_validate BOOLEAN NOT NULL DEFAULT FALSE,
PRIMARY KEY(card_num),
FOREIGN KEY(account_num) REFERENCES account(account_num) ON DELETE no
action ON UPDATE CASCADE,
FOREIGN KEY(client_num) REFERENCES client(client_num) ON DELETE no action
ON UPDATE CASCADE,
FOREIGN KEY(product_num) REFERENCES card_product_type(product_num) ON
DELETE no action ON UPDATE CASCADE
);

CREATE TABLE franchise
(
franchise_num     INT NOT NULL auto_increment,
franchise_name    VARCHAR(20) NOT NULL,
franchise_address VARCHAR(40) NOT NULL,
PRIMARY KEY(franchise_num)
);

CREATE TABLE card_discount_benefit
(
product_num   INT NOT NULL,
franchise_num INT NOT NULL,
discount_rate DECIMAL(6, 3) NOT NULL,
PRIMARY KEY(product_num, franchise_num),
FOREIGN KEY(product_num) REFERENCES card(product_num) ON DELETE no action
ON UPDATE CASCADE,
FOREIGN KEY(franchise_num) REFERENCES franchise(franchise_num) ON UPDATE
CASCADE
);

CREATE TABLE app_list
(
app_num  INT NOT NULL auto_increment,
app_name VARCHAR(10) NOT NULL,
PRIMARY KEY(app_num)
);

CREATE TABLE service_list
(
service_num  INT NOT NULL auto_increment,
service_name VARCHAR(10) NOT NULL,
PRIMARY KEY(service_num)
);

CREATE TABLE app_signup_list
(
client_num  INT NOT NULL,
app_num     INT NOT NULL,
signup_date DATE,
PRIMARY KEY(app_num, client_num),
FOREIGN KEY(client_num) REFERENCES client(client_num)ON DELETE no action ON
UPDATE CASCADE,
FOREIGN KEY(app_num) REFERENCES app_list(app_num)ON DELETE no action ON
UPDATE CASCADE
);

CREATE TABLE service_signup_list
(
client_num  INT NOT NULL,
service_num INT NOT NULL,
signup_date DATE,
PRIMARY KEY(service_num, client_num),
FOREIGN KEY(client_num) REFERENCES client(client_num) ON DELETE no action
ON UPDATE CASCADE,
FOREIGN KEY(service_num) REFERENCES service_list(service_num) ON DELETE no
action ON UPDATE CASCADE
);

CREATE TABLE loan_product_type
(
product_num  INT NOT NULL AUTO_INCREMENT,
product_name VARCHAR(20) NOT NULL,
product_interest_rate DECIMAL(6,3) NOT NULL,
PRIMARY KEY(product_num)
);

CREATE TABLE loan_product
(
loan_num        INT NOT NULL AUTO_INCREMENT,
product_num     INT NOT NULL,
loan_amount     BIGINT NOT NULL,
loan_period     TINYINT NOT NULL DEFAULT 1,
loan_start_date DATE NOT NULL,
PRIMARY KEY(loan_num),
FOREIGN KEY(product_num) REFERENCES loan_product_type(product_num) ON
DELETE no action ON UPDATE CASCADE,
CHECK(loan_amount > 0)
);

CREATE TABLE loan_product_info
(
product_num     INT NOT NULL,
product_interest_rate DECIMAL(6,3) NOT NULL,
product_loan_period TINYINT NOT NULL,
PRIMARY KEY(product_num),
FOREIGN KEY(product_num) REFERENCES loan_product_type(product_num) ON
DELETE NO ACTION ON UPDATE CASCADE,
CHECK (product_interest_rate > 0 and product_loan_period > 0)
);

CREATE TABLE repayment
(
repayment_num    INT NOT NULL auto_increment,
loan_num         INT NOT NULL,
repayment_type   VARCHAR(10) NOT NULL,
repayment_date   DATE NOT NULL,
repayment_amount BIGINT NOT NULL,
PRIMARY KEY(repayment_num),
FOREIGN KEY(loan_num) REFERENCES loan_product(loan_num) ON DELETE no action
ON UPDATE CASCADE,
CHECK (repayment_amount > 0),
CHECK (repayment_type = '전액' or repayment_type ='분할')
);

CREATE TABLE loan_state
(
account_num VARCHAR(20) NOT NULL,
loan_num    INT NOT NULL,
PRIMARY KEY(account_num, loan_num),
FOREIGN KEY(account_num) REFERENCES account(account_num) ON DELETE no
action ON UPDATE CASCADE,
FOREIGN KEY(loan_num) REFERENCES loan_product(loan_num) ON DELETE no action
ON UPDATE CASCADE
);

CREATE TABLE saving_product_type
(
product_num  INT NOT NULL auto_increment,
product_name VARCHAR(20) NOT NULL,
PRIMARY KEY(product_num)
);

CREATE TABLE saving_product_info
(
product_num           INT NOT NULL,
product_interest_rate DECIMAL(6, 3) NOT NULL,
product_saving_period TINYINT NOT NULL,
PRIMARY KEY(product_num),
FOREIGN KEY(product_num) REFERENCES saving_product_type(product_num) ON
DELETE no action ON UPDATE CASCADE
);

CREATE TABLE saving_account
(
account_num VARCHAR(20) NOT NULL,
product_num INT NOT NULL,
PRIMARY KEY(account_num),
FOREIGN KEY(account_num) REFERENCES account(account_num) ON DELETE no
action ON UPDATE CASCADE,
FOREIGN KEY(product_num) REFERENCES saving_product_type(product_num) ON
DELETE no action ON UPDATE CASCADE
);

CREATE TABLE daw_product_type
(
product_num  INT NOT NULL auto_increment,
product_name VARCHAR(20) NOT NULL,
PRIMARY KEY(product_num)
);

CREATE TABLE daw_account
(
account_num                    VARCHAR(20) NOT NULL,
product_num                    INT NOT NULL,
transfer_limit_once            INT DEFAULT 10000000,
transfer_limit_day             INT DEFAULT 50000000,
machine_withdrawl_registration BOOL DEFAULT false,
PRIMARY KEY(account_num),
FOREIGN KEY(account_num) REFERENCES account(account_num) ON DELETE no
action ON UPDATE CASCADE,
FOREIGN KEY(product_num) REFERENCES daw_product_type(product_num) ON DELETE
no action ON UPDATE CASCADE
);

CREATE TABLE remittance_record
(
remittance_num        INT NOT NULL auto_increment,
receiving_account_num VARCHAR(20) NOT NULL,
sending_account_num   VARCHAR(20),
remittance_type       VARCHAR(20) NOT NULL,
remittance_amount     INT NOT NULL,
remittance_time       DATETIME NOT NULL,
PRIMARY KEY(remittance_num),
FOREIGN KEY(receiving_account_num) REFERENCES daw_account(account_num) ON
DELETE NO ACTION ON UPDATE CASCADE,
FOREIGN KEY(sending_account_num) REFERENCES daw_account(account_num) ON
DELETE NO ACTION ON UPDATE CASCADE,
CHECK(remittance_amount >= 0)
);

CREATE TABLE daw_record
(
daw_num         INT NOT NULL auto_increment,
a_device_num    INT,
s_device_num    INT,
account_num     VARCHAR(20) NOT NULL,
deal_type       VARCHAR(20) NOT NULL,
amount_of_money INT NOT NULL,
PRIMARY KEY(daw_num),
FOREIGN KEY(a_device_num) REFERENCES atm(a_device_num) ON UPDATE CASCADE,
FOREIGN KEY(s_device_num) REFERENCES stm(s_device_num) ON UPDATE CASCADE,
FOREIGN KEY(account_num) REFERENCES daw_account(account_num) ON UPDATE CASCADE,
CHECK ((deal_type = '입금' AND amount_of_money > 0 AND amount_of_money <= 7500000) OR
(deal_type = '출금' AND amount_of_money > 0 AND amount_of_money <= 1000000) OR
(deal_type = '무통장 입금' AND amount_of_money > 0 AND amount_of_money <= 1000000) OR
(deal_type = '무통장 출금' AND amount_of_money > 0 AND amount_of_money <= 1000000))
);

# 은행 지점 생성
INSERT INTO branch VALUES ('아주대점', '경기도 수원시 영통구 월드컵로 206','5000000');

#3. 아주대점에 설치된 STM 생성
INSERT INTO STM(management_branch_name, address, installation_date)
VALUES ('아주대점', '아주대학교 구학생회관 1층', '2022-01-01');
INSERT INTO STM(management_branch_name, address, installation_date)
VALUES ('아주대점', '아주대학교 중앙도서관 1층', '2022-05-05');

#4. 아주대점에 설치된 ATM 생성
INSERT INTO ATM(management_branch_name, address, installation_date)
VALUES ('아주대점', '아주대학교 구학생회관 1층', '2022-01-01');
INSERT INTO ATM(management_branch_name, address, installation_date)
VALUES ('아주대점', '아주대학교 팔달관 2층', '2022-05-05');

# 아주대점에서 근무하는 직원 생성
INSERT INTO employee(workplace, employee_name, position, phone_num)
VALUES ('아주대점','김미영','팀장','010-1234-5678');
INSERT INTO employee(workplace, employee_name, position, phone_num)
VALUES ('아주대점','오상식','차장','010-5678-1234');

#5. 고객 리스트 생성
INSERT INTO client(client_name, client_address, client_rank, security_rank, client_age, account_possibility, job)
VALUES ('아이유', '서울시', 'MVP스타', '보안카드', 30, 1, '가수');

INSERT INTO client(client_name, client_address, client_rank, security_rank, client_age, account_possibility, job)
VALUES ('이지은', '고양시', '로얄스타', '모바일 인증서', 30, 1, '배우');

#9. 계좌 생성
INSERT INTO account(account_num, client_num, employee_num_in_charge, balance, ic_date)
VALUES ('943202-00-123456', '1', '2', 300000, '2022-01-03');

INSERT INTO account(account_num, client_num, employee_num_in_charge, balance, ic_date)
VALUES ('372076-90-401234', '2', '1', 250000, '2022-02-04');

#8. 입출금 상품 종류 생성
INSERT INTO daw_product_type VALUES(1, 'KB 마이핏통장');
INSERT INTO daw_product_type VALUES(2, '직장인우대 종합통장');`
INSERT INTO daw_product_type VALUES(3, 'KB Young Youth 청소년통장');
INSERT INTO daw_product_type VALUES(4, 'KB able plus 통장');
INSERT INTO daw_product_type VALUES(5, 'KB 내맘대로 프리랜서 통장');

#10. 입출금 계좌 생성 및 고객의 계좌와 연동
INSERT INTO daw_account(account_num,product_num, transfer_limit_once, transfer_limit_day, machine_withdrawl_registration)
VALUES ('943202-00-123456', 2, '10000000', '50000000', true);
INSERT INTO daw_account(account_num,product_num, transfer_limit_once, transfer_limit_day, machine_withdrawl_registration)
VALUES ('372076-90-401234', 5, '30000000', '400000000', false);
------------------------------------------------
# ATM에서 입출금 계좌에 50000원 입금, 입출금 기록 생성
INSERT INTO daw_record
VALUES      (1,NULL,1,'943202-00-123456','무통장 입금',50000);

UPDATE account
SET    balance = balance + 50000
WHERE  account_num = '943202-00-123456';

# STM에서 입출금 계좌에서 100000원 출금, 입출금 기록 생성
INSERT INTO daw_record
VALUES      (2,1,NULL,'372076-90-401234','출금',100000);

UPDATE account
SET    balance = balance - 100000
WHERE  account_num = '372076-90-401234';

# 송금 기록 생성
INSERT INTO remittance_record(receiving_account_num, sending_account_num, remittance_type, remittance_amount, remittance_time)
VALUES ('943202-00-123456', '372076-90-401234', '단순 송금', 50000, '2022-05-15');
INSERT INTO remittance_record(receiving_account_num, sending_account_num, remittance_type, remittance_amount, remittance_time)
VALUES ('943202-00-123456', '372076-90-401234', '결제', 50000, '2022-05-21');

#받는 쪽 계좌의 잔고 증가
UPDATE account, remittance_record
SET account.balance = account.balance + 50000
WHERE remittance_record.sending_account_num=account.account_num AND account.account_num ='372076-90-401234';
#보낸 쪽 계좌의 잔고 감소
UPDATE account, remittance_record
SET account.balance = account.balance - 50000
WHERE remittance_record.receiving_account_num=account.account_num AND account.account_num ='943202-00-123456';

# 결제 타입별로 송금 기록 확인
SELECT *
FROM remittance_record
WHERE remittance_record.receiving_account_num='943202-00-123456' AND remittance_record.remittance_type='결제';
# 한달 동안 최고 지출액 확인
SELECT SUM(remittance_amount) AS '한달 지출액', remittance_type AS '결제 방법'
FROM remittance_record
WHERE remittance_time BETWEEN date('2022-05-01') and date('2022-05-31'));

------------------------------------------------------------------------------
#19. 예적금 상품 종류
INSERT INTO saving_product_type VALUES(1, '국민수퍼정기예금');
INSERT INTO saving_product_type VALUES(2, 'KB Star 정기예금');
INSERT INTO saving_product_type VALUES(3, 'KB 첫재테크예금');
INSERT INTO saving_product_type VALUES(4, 'KB 장병내일준비적금');
INSERT INTO saving_product_type VALUES(5, 'KB 청년희망적금');

#20. 예적금 상품 정보
INSERT INTO saving_product_info VALUES(1, 1.9, 3);
INSERT INTO saving_product_info VALUES(2, 2.35, 3);
INSERT INTO saving_product_info VALUES(3, 1.85, 1);
INSERT INTO saving_product_info VALUES(4, 5.5, 2);
INSERT INTO saving_product_info VALUES(5, 6, 2);

#21. 계좌 생성
INSERT INTO account(account_num,client_num, employee_num_in_charge, balance, ic_date)
VALUES ('111213-14-151617', 2, 1, 100000, '2022-03-05');

#22. 예적금 계좌 생성
INSERT INTO saving_account(account_num, product_num)
VALUES ('111213-14-151617', 4);

#고객의 모든 계좌 조회
SELECT client.client_name, account.account_num
FROM client, account
WHERE client.client_num = account.client_num;

#select에서 예적금 테이블들 보여주기

#15. 카드 상품 종류
INSERT INTO card_product_type VALUES(1, 'KB 청춘대로 톡톡카드');
INSERT INTO card_product_type VALUES(2, 'KB 탄탄대로 올쇼핑 티타늄카드');
INSERT INTO card_product_type VALUES(3, 'KB 굿데이카드');
INSERT INTO card_product_type VALUES(4, 'KB 나라사랑카드');
INSERT INTO card_product_type VALUES(5, 'KB 노리체크카드');

#16. 카드 생성
INSERT INTO card VALUES ('1234-5678-9101-1121', '943202-00-123456', 1, 2, '2027-04-24', true);
INSERT INTO card VALUES ('1121-2342-3563-4784', '943202-00-123456', 1, 5, '2027-05-05', true);
INSERT INTO card VALUES ('4784-3563-2342-1121', '372076-90-401234', 1, 5, '2027-06-12', true);

#17. 가맹점 생성
INSERT INTO franchise VALUES (1, '파리바게트 아주대점', '경기도 수원시 영통구 월드컵로 205');
INSERT INTO franchise VALUES (2, 'GS25 아주대점', '경기도 수원시 영통구 아주로 46');
INSERT INTO franchise VALUES (3, '도담도담 아주대점', '경기도 수원시 팔달구 월드컵로 211');

#18. 카드 할인
INSERT INTO card_discount_benefit VALUES (5, 3, 0.05);
INSERT INTO card_discount_benefit VALUES (5, 2, 0.10);
INSERT INTO card_discount_benefit VALUES (2, 1, 0.08);

# 카드로 결제 시 해당 카드를 사용한 고객이름, 사용매장, 카드번호, 할인율 출력
SELECT c.client_name "고객이름", f.franchise_name "사용 매장", ca.card_num "카드번호", cdb.discount_rate "할인율"
FROM franchise as f, card_discount_benefit as cdb, card as ca, card_product_type as cp, client as c
WHERE ((ca.card_num = "1234-5678-9101-1121") AND (f.franchise_num = cdb.franchise_num) AND (cdb.product_num = ca.product_num)
	AND (ca.product_num = cp.product_num) AND (ca.client_num = c.client_num));

# 사용한 카드번호에 해당하는 계좌의 잔고에서 할인율*사용금액 만큼의 금액을 뺌 
UPDATE account as a SET balance = balance - 0.080*50000
WHERE a.account_num = ( SELECT ca.account_num
												FROM card as ca
												WHERE (ca.card_num = "1234-5678-9101-1121"));
                                                
#23. 대출 상품 종류
INSERT INTO loan_product_type VALUES(1, 'KB 직장인든든 신용대출', 3.48);
INSERT INTO loan_product_type VALUES(2, 'KB 플러스 전세자금대출', 3.18);
INSERT INTO loan_product_type VALUES(3, 'KB 일반부동산 담도대출', 3.8);
INSERT INTO loan_product_type VALUES(4, 'KB 주택담보대출', 3.55);
INSERT INTO loan_product_type VALUES(5, 'KB 매직카대출', 5.2);

#24. 대출 상품 정보
INSERT INTO loan_product_info VALUES(1, 3.48, 5);
INSERT INTO loan_product_info VALUES(2, 3.18, 3);
INSERT INTO loan_product_info VALUES(3, 3.8, 35);
INSERT INTO loan_product_info VALUES(4, 3.55, 40);
INSERT INTO loan_product_info VALUES(5, 5.2, 5);

#대출 상품 생성
INSERT 
INTO loan_product 
VALUES (1, 1, 10000000, 3, '2022-06-01');

INSERT 
INTO loan_product 
VALUES (2, 4, 50000000, 20, '2022-07-01');

#대출 현황
INSERT 
INTO loan_state 
VALUES ('943202-00-123456',1);

INSERT
INTO loan_state 
VALUES ('372076-90-401234',2);

UPDATE account
SET balance = balance + 10000000
WHERE account.account_num = '943202-00-123456';

UPDATE account
SET balance = balance + 50000000
WHERE account.account_num = '372076-90-401234';
---------------------------------------------------------------
# 고객마다 대출한 잔액 조회
SELECT c.client_name "고객이름", a.account_num "계좌번호", lp.loan_num "대출번호", lt.product_name "대출상품", lp.loan_amount "대출금액"
FROM loan_product as lp, loan_state as ls, loan_product_type as lt, client as c, account as a
WHERE (c.client_num = a.client_num) and ( a.account_num = ls.account_num) and ( ls.loan_num = lp.loan_num) and (lp.product_num = lt.product_num)
ORDER BY lp.loan_num;

INSERT INTO repayment 
VALUES (1, 2, '분할', '2023-01-01', 3500000);

INSERT INTO repayment 
VALUES (2, 1, '전액', '2023-05-27', 50000000);

UPDATE account
SET balance = balance - 3500000
WHERE account_num = '943202-00-123456';

UPDATE account
SET balance = balance - 50000000
WHERE account_num = '372076-90-401234';

#한 고객의 모든 상환 기록 조회
# 상환 하나 더 추가
INSERT INTO repayment
            (loan_num,
             repayment_type,
             repayment_date,
             repayment_amount)
VALUES      (1,
             '분할',
             '2022-10-05',
             '1000000');

SELECT client.client_name,
       repayment.*
FROM   repayment,
       client,
       account,
       loan_state,
       loan_product
WHERE  client.client_num = '1'
       AND client.client_num = account.client_num
       AND account.account_num = loan_state.account_num
       AND loan_state.loan_num = loan_product.loan_num
       AND loan_product.loan_num = repayment.loan_num ;
       
#6. 앱 리스트 생성
INSERT INTO app_list VALUES (1, 'KB스타뱅킹');
INSERT INTO app_list VALUES (2, 'KB스타알림');
INSERT INTO app_list VALUES (3, 'KB Pay');
INSERT INTO app_list VALUES (4, '리브');
INSERT INTO app_list VALUES (5, '리브똑똑');

#7. 서비스리스트 생성
INSERT INTO service_list VALUES (1, '손으로 출금');
INSERT INTO service_list VALUES (2, 'KB모바일인증서');
INSERT INTO service_list VALUES (3, '마이데이터');
INSERT INTO service_list VALUES (4, '오픈뱅킹');
INSERT INTO service_list VALUES (5, '입출금알림');

#13. 앱가입
INSERT INTO app_signup_list VALUES (1,1,'2022-03-15');
INSERT INTO app_signup_list VALUES (1,3,'2022-04-05');
INSERT INTO app_signup_list VALUES (2,5,'2022-05-15');

#14. 서비스 가입
INSERT INTO service_signup_list VALUES (1,3,'2022-03-15');
INSERT INTO service_signup_list VALUES (2,4,'2022-04-25');
INSERT INTO service_signup_list VALUES (2,2,'2022-05-27');

# 고객이 가입 할 수 있는 앱 정보
SELECT app_num AS '앱 번호',app_name AS '앱 이름'
  FROM app_list;
# 고객이 가입 할 수 있는 서비스 정보
SELECT service_num AS "서비스 번호", service_name AS "서비스 이름"
  FROM service_list;
# 고객이 가입 한 앱 종류 확인
SELECT app_signup_list.app_num AS '앱 번호',client.client_num AS '고객 번호'
  FROM app_signup_list,client
  WHERE app_signup_list.client_num=client.client_num AND client.client_num=1;
# 고객이 가입한 서비스 종류 확인
SELECT service_signup_list.service_num AS '서비스 번호',client.client_num AS '고객 번호'
  FROM service_signup_list,client
  WHERe service_signup_list.client_num=client.client_num AND client.client_num=1;
```
