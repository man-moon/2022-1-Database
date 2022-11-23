# 2022 데이터베이스 팀 프로젝트

## 프로젝트 개요
---
소비자들의 상품 구매 형태가 변화하고 있다. 기존의 모든 상품구매가 오프라인 매장에
국한되어 있었다면 이제는 온라인 매장에서의 구매가 기하급수적으로 늘어나고 있다. 
 소비자의 요구 사항과 온라인 매장의 제공 사항이 정확하게 들어맞으면서 서로에게
만족을 주는 소비행태를 변모하고 있는 것이다.

 온라인 매장이용의 장점을 살펴보면 온라인 구매가 급격히 증가하는 이유를 찾아볼수 있다.

1.  온라인 매장은 상품에 대한 정보를 쉽게 얻을 수 있다. 소비자가 구매하고자
하는 상품이 있을 경우 원하는 상품에 대한 정보는 온라인 매장속에 다 담겨져 있다. 
같은 종류의 상품을 모델별로 제조회사별로 확인 할수 있으며 소비자가 예상한 예상구매가에 맞는 상품을 찾을수 있으며 상품 가격 비교 또한 쉽다. 그리고 이미 상품을 구매하여 사용해본 다른 소비자들의 사용기와 상품평을 보고 상품에 대한 판단을 할 수가 있다.

1. 둘째, 온라인 매장은 오프라인 매장보다 비교적 가격이 저렴하다. 같은 물건이면 좀더 싼곳을 찾게 되는 건 당연한 소비자의 욕구이다. 온라인 매장은 오프라인 매장을 운영시에 드는 매장 관리비, 유지비의 비용이 들지 않고 오프라인보다 더 많은 고객이 접근할 수 있어 소비자 가격을 낮출 수 있다. 하여 조금 더 싼 가격에 같은 상품을 제공해 줄 수 있다.

1. 셋째, 온라인 매장은 소비자에게 보다 적극적이고 가깝게 다가갈수 있다. 온라인 매장은 고객이 사이트를 찾아 들러주어야만 한다는 점에서 오프라인과 같이 수동적인 판매형태로 보일수 있지만 문의 사항이나 불만 사항등 소비자의 요구 사항을 즉각적으로 응답이 가능하다. 구매 상품의 전달 또한 택배에 의해 모든 것이 이루어지므로 요구사항에 즉각적인 대응이 가능하다. 구매 상품의 전달 또한 택배에 의해 모든 것이 이루어지므로 소비자는 편히 상품을 받아볼수 있다. 또한 온라인 매장은 24시간 휴일없이 구매 주문을
할 수 있어 언제 어디서든 원하는 물건을 주문이 가능하다.

이 밖에도 반품, 환불등이 비교적 쉬우며 여러가지 쇠자를 위한 각종 이벤트를 운영하는등 오프라인 매장으로 향하는 소비자들의 발길을 온라인 매장으로 되돌리고 있다.


## 업무 기능도
---
<img width="60%" src="https://user-images.githubusercontent.com/88218891/203600150-c539ebaa-acc4-4ac6-9715-1f8271871dc3.png"/>


## 요구사항 분석
---
### 계좌개설 및 고객관리
1. 국민은행을 이용하는 고객은 1개 이상의 계좌를 만들 수 있다.  
1. 국민은행 계좌를 만들기 위해서 고객은 이름, 휴대폰 번호, 자택주소, 직업에 대한 정보를 제공해야한다.  
1. 고객은 고객번호로 구분된다.  
1. 각 계좌는 계좌번호로 식별되며 공동명의로 만들 수 없다.  
1. 계좌 종류에 상관없이 계좌 발급 후 20일동안 새로운 계좌를 만들지 못한다.  
1. 고객은 고객이 원할 때 언제든지 계좌를 해지할 수 있다.  
1. 미성년자의 경우 법적보호자를 통해서만 개설할 수 있으며 청소년 및 성인은 청소년증 및 주민등록번호가 표기된 공인문서를 통해 개설할 수 있다.  
1. 계좌를 개설해주는 직원이 해당 계좌의 담당직원이 된다.  
1. 특정 계좌에서 월 단위로 지출되는 금액에 따라 고객 등급을 높일 수 있다.  
1. 계좌는 거래가 자유로운 입출금, 출금이 불가하지만 은행으로부터 이자를 받을 수 있는 정기예금/자유적금을 포함하는 예적금으로 구분된다.  

### 입출금 계좌 개설
1. 입출금 계좌는 고객이 언제든 자유롭게 돈을 입/출금 할 수 있는 통장을 말한다.  
1. 고객은 보안등급에 따라 입출금 계좌의 하루/한번 이체한도를 최대 5억/1억까지 
    조정할 수 있다.  
1. 입출금 계좌를 신규 개설하면 최대 3개월동안 하루 30만원 이상 이체할 수 없는 한
도제한계좌가 되며, 법으로 지정된 증빙서류를 통해 해지할 수 있다.  
1. ATM 출금 가능 서비스를 등록하지 않으면 STM/ATM에서 돈을 출금할 수 없다.  
1. 고객은 하나 이상의 계좌로 돈을 단순 이체할 수 있다.  
1. 고객은 하나 이상의 계좌에, 원하는 날짜와 금액을 설정해 돈을 자동으로 이체시킬 수 있다.  
1. 고객은 동일한 상품 종류의 입출금 계좌를 가질 수 없다.  
1. 고객은 원할 때마다 입출금 계좌 상품 종류를 전환할 수 있다.

### 예적금 계좌 개설
1. 적금은 매월 정해놓은 금액을 특정일에 넣는 정기적금과 매월 은행이 지정한 금액 내
     에서 자유롭게 넣을 수 있는 자유적금이 있다.
1. 정기예금/적금 상품은 은행이 지정한 서로 다른 금리, 저축 기간을 가진다.
1. 정기예금/적금 중도 해지 시 은행에서 지정한 이자 약관에 따른 이자를 지급한다.
1. 예금/적금 계좌에선 돈을 인출할 수 없다.
1. 고객은 동일한 상품 종류의 예/적금 계좌를 가질 수 없다. 

### 대출
1. 한 고객이 여러 번 대출을 받을 수 있다.
1. 고객이 지정한 계좌에 대출받은 돈이 들어온다.
1. 대출 업무를 진행한 직원이 해당 대출 건을 담당한다.
1. 고객은 지정한 날짜까지 대출금을 모두 상환해야 한다.
1. 상환금은 전액 납부 및 분할 납부가 가능하다.
1. 은행 내규로 지정된 조건이 만족되면 고객은 대출연장을 시킬 수 있다.

### 카드발급 및 해지
1. 계좌를 가진 고객은 카드 발급을 요청할 수 있다.
1. 고객은 카드와 연동할 입출금 계좌를 선택할 수 있다.
1. 카드 발급 시, 고객은 원하는 카드 상품 종류를 고를 수 있다.
1. 카드는 16자리의 고유번호로 만들어지며, 유효 기간은 발급 받은 날로부터 5년이다.
1. 고객이 카드 해지신청을 하거나 분실 신고시, 카드는 사용이 불가능한 상태로 바뀐다.

### 카드사용
1. 카드 결제 시, 카드와 연동되어 있는 계좌의 잔액에서 돈이 출금된다.
1. 카드와 연동되어 있는 계좌의 잔액이 부족하면 거래 요청이 거부된다.
1. 고객은 카드를 발급받을 때 가입한 상품 종류에 따라 혜택을 받을 수 있다.
1. 협약을 맺은 가맹점에서 카드 결제시, 카드 상품 종류에 따라 할인을 받을 수 있다.

### 카드 상품 등록
1. 관리자는 카드 상품을 등록할 수 있다.
1. 카드 상품 등록 시, 카드 상품 이름만 입력하면 카드 상품 번호는 자동으로 생성되고 등록이 완료된다.

### 가맹점 등록
1. 관리자는 협약을 맺은 가맹점을 등록할 수 있다.
1. 가맹점 등록 시, 가맹점 이름, 주소만 입력하면 가맹점 번호는 자동으로 생성되고 등록이 완료된다.

### 앱, 서비스 관리
1. 고객은 국민은행이 제공하는 여러 앱 리스트에 있는 앱들을 이용한다.
1. 앱 리스트에는 KB스타뱅킹, KB국민알림, KBPAY, 리브, 리브톡톡이 있다.
1. 앱 리스트에 있는 앱들은 앱 번호, 이름, 가입일자를 통해 유지한다.
1. 앱 리스트에 있는 앱들은 앱 번호로 식별한다.
1. 고객은 국민은행이 제공하는 여러 서비스리스트에 있는 서비스를 가입 할 수 있다.
1. 서비스 리스트에 있는 서비스들에 대한 서비스 번호, 이름, 가입일자를 유지한다.
서비스 리스트에는 손으로 출금, KB 모바일 인증서, 마이데이터, 오픈뱅킹,입출금 알림들이 있다.
1. 서비스 리스트에 있는 서비스들은 서비스 번호로 식별한다.
1. 고객의 개인정보 사용 기간은 1년으로 제한하고 고객의 요청에 의해 1년 단위로 갱신 될 수 있다.

### 지점 운영
1. 직원은 특정 계좌들을 관리한다.
1. 직원은 특정 지점에서 근무한다.
1. 고객은 STM을 통해 제신고 업무를 하거나 입출금을 할 수 있다.
1. 지점은 특정 STM들을 관리한다.
1. 고객은 ATM을 통해 입출금을 할 수 있다.
1. 지점은 특정 ATM들을 관리한다.
1. ATM과 STM에서 카드를 이용해 입출금 시 카드에 연동된 계좌가 출금 불가능할 경우 출금을 제한할 수 있다.

## ER-Diagram
---
<img src="https://user-images.githubusercontent.com/88218891/203602298-e3537c59-cd09-4772-96da-7f44e621d225.png"/>

## 논리적 데이터 모델
---
<img src="https://user-images.githubusercontent.com/88218891/203602432-c433a017-b056-4fab-bc77-122c0a18df9c.png"/>

## 물리적 데이터 모델
---
<img src="https://user-images.githubusercontent.com/88218891/203602486-9b515ac3-f6a9-44d3-8036-2d9756a4dbcf.png"/>
