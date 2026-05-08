# 스마트 가계부 프로젝트 문서

## 1. Introduction
성인이 된 후에 고정지출뿐만 아니라 예상치 못한 지출이나 과소비를 하는 경향이 있다는 것을 인지하였다. 그래서 고치기 위해 편한 가계부라는 가계부 앱을 사용하고 있는데 직관적이고 깔끔한 디자인이며 간편하긴 하지만 카테고리 분류가 수동으로만 가능하다는 점, 외부 데이터 자동 입력이 없다는 점이 아쉬웠고, 추천/피드백 기능이 추가적으로 있었으면 좋겠다는 생각이 들었다.

## 2. Use case analysis

### 2-1. Use case diagram

시스템의 주 사용자로 가계부의 모든 입력 권한을 가지는 클라이언트 입장에서 시스템이 제공하는 주요 기능들을 정의하였다. 그리고 통계 시각화, 지출 패턴 분석, 예산 알림 등 데이터들을 관리하는 시스템 및 문의사항에 직접 답변하는 관리자와의 상호작용을 도식화하였다.

### 2-2. Use case description 

**Use case # 1 : 회원가입 및 로그인**

Summary - 클라이언트가 서비스를 사용하기 위해 본인 인증을 통해 계정을 생성하고, 시스템에 접속할 때 사용한다.

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - client

Precondition - 클라이언트가 앱을 실행한 상태여야 하며, 로그아웃 상태여야 한다.

Trigger - 클라이언트가 앱을 최초로 실행하거나 로그아웃 후 시스템에 다시 접속을 시도할 때

Success post condition - 인증의 완료되어 메인 화면으로 전환되며, 개인별 데이터 환경이 제공된다.

Failed post condition - 로그인에 실패하고 로그인 화면에 머무르며, 오류 메시지가 표시된다.

Main success scenario
S - 클라이언트가 로그인 버튼을 클릭한 후 아이디/비밀번호를 입력하거나 소셜 로그인 버튼을 클릭하면 시작된다.
1 - 시스템은 입력된 정보가 데이터 베이스에 저장된 암호화 데이터와 일치하는지 확인한다.
2 - 시스템은 클라이언트 개인의 데이터 환경을 불러온다.
3 - 접속이 완료되며 메인 화면으로 전환된다.

Extension scenarios
아이디 또는 비밀번호가 틀렸거나 일치하는 계정이 없는 경우
시스템은 “아이디 또는 비밀번호가 일치하지 않습니다.” 또는 “일치하는 계정이 없습니다.” 라는 경고 메시지를 띄운다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other

**Use case # 2 :  지출 데이터 입력 및 수동/자동 분류**
Summary - 사용자가 소비 내역을 입력하거나 외부 파일(CSV)을 업로드해 데이터 등록, 자동으로 분류할 때 사용

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - client, system

Precondition - 클라이언트가 서비스에 접속한 상태여야 한다.

Trigger - 클라이언트가 ‘지출 추가’ 버튼을 누른 후 자동 분류와 수동 분류 중 선택한다.

Success post condition - 지출 데이터를 입력하고 수동 분류나 자동 분류를 이용시 원하는 카테고리로 분류가 되며, 오류가 발생하지 않는다.

Failed post condition - 자동 분류를 이용 시 원하는 카테고리로 분류가 되지 않거나 지출 데이터를 입력하고 수동 분류를 할 때 오류가 발생한다.

Main success scenario
S - 클라이언트가 지출을 입력하기 위해 앱을 이용하는 경우 시작된다.
1 - 직접 지출을 입력하는 경우 오른쪽 하단의 + 버튼을 누르고 ‘지출 추가’ 버튼을 클릭한다.
1-1 - 은행 앱을 연결하는 경우 오른쪽 하단의 + 버튼을 누르고 ‘은행 연동’ 버튼을 클릭한 뒤 원하는 은행을 클릭한다.
2 - 당일이 아니면 날짜를 수정하고, 수동 분류를 이용하는 경우 카테고리를 선택하고 금액을 입력한 뒤 추가한다.
자동 분류를 이용하는 경우 금액을 입력하고. 메모를 작성한 뒤 추가한다.

Extension scenarios
은행 연동 및 자동 분류가 애매하거나 틀린 경우
시스템은 ‘기타’ 카테고리로 임시 분류한다.
사용자가 수동으로 카테고리를 변경할 수 있는 선택창을 제공한다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other - 모든 금액은 양의 정수여야 한다.

**Use case # 3 : 지출 패턴 피드백**
Summary - 저장된 지출 데이터를 바탕으로 피드백을 제공한다.

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - system

Precondition - 최소 1건 이상의 지출 데이터가 시스템에 저장되어 있어야 한다.

Trigger - 클라이언트가 ‘추천/피드백’ 버튼을 클릭할 때

Success post condition - ‘추천/피드백’ 버튼을 클릭하면 클라이언트가 확인하고 싶을 때 맞춤형 소비 개선 조언을 
확인할 수 있다.

Failed post condition - 데이터 분석에 실패하고, “데이터를 불러올 수 없습니다.” 라는 메시지를 띄운다.

Main success scenario
S - 클라이언트가 ‘추천/피드백’ 버튼을 클릭하면 시작된다.
1 - 데이터 분석 결과를 바탕으로 맞춤형 피드백을 제공한다.

Extension scenarios
매달 마지막 날에 추천/피드백 화면이 자동으로 뜨지 않는 경우
클라이언트가 “추천/피드백” 버튼을 눌러 확인할 수 있도록 한다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other

**Use case # 4 : 예산 설정 및 초과 알림**
Summary - 계획된 소비를 위해 사용자가 한 달 지출 한도를 설정하고, 총 지출액이 임계치에 도달하면 알림을 제공한다.

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - client, system

Precondition - 클라이언트가 로그인 상태이며, 예산 금액이 입력되어 있어야 한다.

Trigger - 새로운 지출 데이터가 추가되어, 총 지출액이 입력된 예산에 도달할 때

Success post condition - 클라이언트에게 초과 알림이 발송된다.

Failed post condition - 알림 발송이 실패한다.

Main success scenario
S - 클라이언트가 새로운 지출을 입력해 총액이 변동되면 시작한다.
1 - 시스템은 총 지출액, 설정 예산을 실시간으로 비교한다.
2 - 총 지출액이 설정 예산을 초과하는지 검사한다.
3 - 초과 시 시스템은 “이번 달 지출 비용이 예산 금액을 초과했습니다.” 라는 경고 알림을 생성해 화면에 띄운다.

Extension scenarios
예산을 이미 초과한 상태에서 추가 지출이 발생한 경우
최종 경고 알림을 1회 재발송한다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other

**Use case # 5 : 데이터 내보내기**
Summary - 시스템에 저장된 데이터를 외부 파일(CSV)로 다운로드하여 다른 환경에 활용하거나 백업할 수 있도록 한다.

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - client

Precondition - 클라이언트가 로그인 상태이며, 시스템에 저장된 데이터가 존재해야 한다.

Trigger - 클라이언트가 ‘다운로드’ 버튼을 클릭할 때

Success post condition - 클라이언트가 지정한 데이터가 CSV 형태로 변환되어 다운로드 된다.

Failed post condition - CSV 형태로 변환에 실패하고, “파일을 만들 수 없습니다.” 라는 오류 메시지를 띄운다.

Main success scenario
S - 클라이언트가 데이터 기간을 설정하고 다운로드 버튼을 누르면 시작한다.
1 - 시스템은 해당 기간의 저장된 지출 내역을 추출한다.
2 - 추출된 데이터를 CSV 규격에 맞게 변환한다.
3 - 파일 다운로드를 시작하고 완료 메시지를 띄운다.

Extension scenarios
파일 다운로드에 실패한 경우
“다운로드에 실패했습니다.” 라는 창을 띄운 즉시 원인을 찾아 해결한다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other

**Use case # 6 : 통계 시각화**
Summary - 사용자의 지금까지 입력한 재정 상태를 막대 그래프와 원그래프를 이용하여 직관적으로 제공하고, 통계 요약도 제공한다.

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - system

Precondition - 최소 1건 이상의 지출 데이터가 시스템에 저장되어 있어야 한다.

Trigger - 클라이언트가 ‘분석’ 버튼을 클릭할 때

Success post condition - ‘분석’ 버튼을 클릭하면 카테고리별 지출 통계 막대 그래프와 원 그래프 두 가지 버전을 제공하며, 통계 요약을 제공한다.

Failed post condition - 데이터 분석에 실패하고, “데이터를 불러올 수 없습니다.” 라는 메시지를 띄운다.

Main success scenario
S - 클라이언트가 ‘분석’ 버튼을 클릭하면 시작된다.
1 - 시스템이 클라이언트가 지금까지 입력한 지출 총액과 카테고리별 비중을 계산한다.
2 - 클라이언트가 ‘분석’ 버튼 클릭 시 시스템은 결과를 시각화한 막대 그래프와 원그래프, 결과를 바탕으로 한 통계 요약을 제공한다.

Extension scenarios
지금까지의 데이터가 반영이 안 된 상태로 통계를 낸 경우
클라이언트가 새로고침을 클릭하면 시스템은 데이터가 다 반영되었는지 확인하고 안 되었으면 수정한다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other

**Use case # 7 : 문의 및 피드백**
Summary - 사용자가 분석 결과에 대한 궁금증이나 시스템 개선 사항을 “Q&A” 버튼을 클릭해 등록하고, 답변을 확인할 때 사용한다.

Scope /Level - 스마트 가계부 / User level

Author

Last update

Status - analysis 

Primary actor - manager, client

Precondition - 사용자가 로그인 상태여야 한다.

Trigger - 클라이언트가 ‘Q&A’ 버튼을 클릭 후 문의글을 등록할 때

Success post condition - 문의글이 시스템에 등록되고, 관리자에게 알림이 가고, 관리자가 답변 시 클라이언트에게 알림이 제공된다.

Failed post condition - 문의글 등록에 실패한다.

Main success scenario
S - 클라이언트가 문의 내용을 입력하고 ‘전송’ 버튼을 누르면 시작된다.
1 - 시스템은 문의글을 데이터 베이스에 저장하고, 관리자에게 알림을 보낸다.
2 - 관리자가 시스템에 접속해 해당 문의를 확인 후 답변을 작성해 등록한다.
3 - 클라이언트는 작성한 문의글에 달린 관리자의 답변을 확인한다.

Extension scenarios
로그인을 하지 않은 경우
클라이언트가 로그인을 하지 않고 문의글을 등록할 경우 시스템은 “로그인을 해주세요.” 라는 메시지 창을 띄우고 로그인 화면으로 이동한다.

Related information
Performance - <= 3sec
Frequency - veriable
Concurrency - None
Other - 비밀글 설정 지원

## 3. Domain analysis

1) UserController
사용자의 계정 정보를 관리하는 클래스이다. 아이디, 비밀번호 등 개인 프로필 정보를 저장하는 클래스이다.

2) TransactionManager
개별 지출 내역을 생성, 수정, 삭제하는 기능을 관리하는 클래스이다. 금액, 날짜, 메모 등의 정보를 데이터베이스에 저장하는 클래스이다.

3) CategoryClassifier
입력된 지출 내역 키워드를 분석해 적절한 카테고리를 자동으로 할당하는 클래스이다. 클라이언트가 직접 카테고리를 변경할 경우 그 학습 데이터를 저장하는 클래스이다.

4) AnalysisEngine
저장된 데이터들을 불러와 기간별 통계를 계산하는 클래스이다.

5) BudgetController
클라이언트가 설정한 목표 예산 정보를 관리하는 클래스이다. 월별 지출 한도 수치를 저장하고, 현재 지출액과 비교한다.

6) AlertSystem
실시간으로 지출 상태를 확인하는 클래스이다. BudgetController와 연동하여 클라이언트의 지출이 설정한 예산 금액에 도달하면 알림을 보낸다.

7) VisualDataGenerator
분석된 결과값을 그래프로 변환하기 위한 데이터를 생성하는 클래스이다. 막대 그래프, 원그래프를 그리기 위한 좌표값이나 비율 데이터를 관리한다.

8) DataPorter (Import/Export)
외부 파일과의 상호작용을 담당하는 클래스이다. 은행에서 제공하는 CSV 파일을 읽어오거나(Import), 가계부 데이터를 파일 형태로 내보내는(Export) 기능을 수행한다.

9) FeedbackManager
AnalysisEngine의 분석 결과를 바탕으로 클라이언트에게 보여줄 피드백 문구를 생성하는 클래스이다. 

10) DatabaseManager (DBHandler)
모든 클래스에서 발생하는 데이터들을 실제 저장소에 안전하게 기록하고 가져오는 역할을 하는 클래스이다. 데이터의 무결성을 유지하며 보안을 위해 민감 정보 마스킹 처리를 수행한다.

## 4. User Interface prototype 

처음 시스템을 실행하면 로그인 및 회원가입 화면이 보인다. 
비회원인 경우 회원가입을 눌러 가입을 하고, 회원인 경우 소셜 로그인나 이메일을 입력하면 다음 화면으로 넘어간다.

+ 버튼을 누르면 지출 추가, 분석, 추천/피드백, 다운로드, 은행 연동, Q&A 버튼이 표시된다.
또한 지출 내역을 펜 모양 버튼을 클릭해 수정할 수 있고, 휴지통 모양 버튼을 클릭해 삭제할 수 있다.

지출 추가 버튼을 누르면 화면과 같이 나온다. 클라이언트가 날짜를 변경하고 싶다면 직접 변경이 가능하며 자동 분류 또는 수동 분류를 선택한다. 자동 분류를 선택했으면 금액을 입력하고 메모를 입력하고, 수동 분류를 선택했다면 카테고리와 금액을 입력한다.

분석 버튼을 클릭하면 화면과 같이 나온다. 막대 그래프, 원그래프를 보여주고, 통계 요약은 총 지출 건수, 평균 지출액, 가장 많이 쓴 카테고리 세 가지를 보여준다.

추천&피드백 버튼을 클릭하면 화면과 같이 나온다.

다운로드 버튼을 클릭하면 화면과 같이 나온다. csv 파일로 기기에 저장된다.

은행 연동 버튼을 클릭하면 화면과 같이 나온다. 연동하고 싶은 은행을 클릭하면 해당 은행의 지출 금액이 나타난다.

Q&A 버튼을 클릭하면 화면과 같이 나온다. 자주 묻는 질문 네 가지가 나오며, 그 외에 문의 사항이나 시스템에 관련된 피드백이 있다면 직접 질문하기 버튼을 클릭해 문의 내용을 입력 후 전송한다.

설정 버튼을 클릭하면 예산 설정이 가능하다.

## 5. Glossary
가계부 시스템 - 가계부를 사용하고 싶은 사람들 모두가 사용할 수 있는 앱
사용자 - 스마트 가계부를 사용하는 사용자
데이터 - 사용자가 입력한 데이터
통계 그래프 - 사용자가 입력한 데이터를 바탕으로 한 통계

## 6. References
편한가계부 앱

토스앱

Analysis with examples
