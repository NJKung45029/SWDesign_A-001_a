graph LR
    User((온라인 뱅킹 사용자))
    BankSystem[[외부 은행 시스템]]

    subgraph "온라인 뱅킹 시스템"
        %% 사용자 관리
        UC1(사용자 등록)
        UC2(사용자 정보 수정)
        UC3(사용자 삭제)
        UC4(사용자 조회)

        %% 계좌 관리
        UC5(입금)
        UC6(출금)
        UC7(이체)
        UC8(잔액 조회)

        %% Include 관계 설정 (조회 포함)
        UC1 -. "&lt;&lt;include&gt;&gt;" .-> UC4
        UC2 -. "&lt;&lt;include&gt;&gt;" .-> UC4
        UC3 -. "&lt;&lt;include&gt;&gt;" .-> UC4

        %% 금융 업무 Include 관계 (조회 및 잔액조회 포함)
        UC5 -. "&lt;&lt;include&gt;&gt;" .-> UC4
        UC5 -. "&lt;&lt;include&gt;&gt;" .-> UC8
        
        UC6 -. "&lt;&lt;include&gt;&gt;" .-> UC4
        UC6 -. "&lt;&lt;include&gt;&gt;" .-> UC8
        
        UC7 -. "&lt;&lt;include&gt;&gt;" .-> UC4
        UC7 -. "&lt;&lt;include&gt;&gt;" .-> UC8
    end

    %% 액터 연결
    User --> UC1
    User --> UC2
    User --> UC3
    User --> UC4
    User --> UC5
    User --> UC6
    User --> UC7
    User --> UC8

    %% 외부 시스템 연결
    UC5 --- BankSystem
    UC6 --- BankSystem
    UC7 --- BankSystem
    UC8 --- BankSystem
