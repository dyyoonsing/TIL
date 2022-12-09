## Control-M

### Control-M이란?
- 컨트롤엠은 BMC Software의 배치 자동화 솔루션. "Workload Automation"
- 은행/증권 등 금융긱관들은 배치성 업무 자동화의 도입을 통해 1)사용자 조작 실수의 최소화 2)배치 작업들 간의 연관관계 보장 3)현실성 있는 다양한 스케줄링 기능 4)통일된 모니터링 인터페이스 등 효과
- CA의 '워크로드 오토메이션', IBM, LG 히다찌 등도 관련 솔루션 보유

<br><br>

### Control-M의 구성요소
1. Control-M / EnterPrise Manager
    Enterprise Control Station은 작업을 통합관리하는 사용자 GUI
    - 서로 다른 기종의 작업을 동일한 gui로 처리하는 통합된 사용자 인터페이스
    - 이 기종간의 연계 작업처리
    - 전체의 작업 정보 현황 monitoring
    - 기종에 상관없이 모든 작업 환경 제어 가능
2. Control-M Server
    관리 대상 Agent에 대한 작업 정보 관리
    - 정의된 작업 관리, 작업의 대기 실행 종료 결과 전달 / 자체적인 스케줄링 기능 수행
    - 자체 인터페이스 기능 제공(enterprise control station의 사용 불능 상태 대비)
    - 작업의 정상, 비정상 종료에 따른 후속조치 수행
3. Control-M Agent
    Control-M Server의 제어를 받아 실제 작업을 실행
    - 작업의 실행상황 모니터링, 종료 시 작업의 결과 분석, 상태 전달

### Control-M 배치 스케줄 주요 개념
1. Order
    - DEF 안에 정의된 작업들 중 scheduling panel에 정의돈 parameter에 의해 당일 돌아갈 작업 ajf(active jobs file)에 저장
    - 정의된 작업들 중 오늘 수행할 작업들을 차출하여 복사해서 따로 관리
2. New Day Process
    - table 단위의 user daily가 SYSTEM으로 되어 있는 작업들이 자동 order, 전일 작업들이 formatting
    - 특정 시간에 new day processing이 start되면 ctm/em과 ctm/server 간의 gateway 연결을 끊고 전날 수행된 작업을 삭제, 보관
    - DEF에서 AJF로 copy, new day processing 작업이 끝나고, ctm/server에서 ctm/em으로 AJF, Quantitive Resource, Control Resources, Prerequisite Conditions, Runtime statistics를 다운로드함
    - CTM/Agent는 JOB의 실행만 맡고 있기 때문에 특별한 작업하지 않음
    



