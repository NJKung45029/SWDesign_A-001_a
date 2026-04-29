```mermaid
classDiagram
    %% 클래스 정의
    class 고객정보 {
        -주민번호: String
        -성명: String
        +고객등록(주민번호: String, 성명: String): boolean
        +고객수정(주민번호: String, 성명: String): boolean
        +고객삭제(주민번호: String): boolean
        +고객조회(주민번호: String): boolean
    }

    class 차량정보 {
        -차량번호: String
        -차량명: String
        -렌트비용: double
        -렌트여부: boolean
        +차량등록(차량번호: String, 차량명: String, 렌트비용: double): boolean
        +차량수정(차량번호: String, 차량명: String, 렌트비용: double): boolean
        +차량삭제(차량번호: String): boolean
        +차량조회(차량번호: String): boolean
        +렌트여부확인(차량번호: String): boolean
        +렌트비용조회(차량번호: String): double
    }

    class 렌트정보 {
        -렌트id: String
        -주민번호: String
        -차량번호: String
        -렌트총액: double
        -렌트일: int
        -반납예정일: int
        -반납일: int
        +렌트(주민번호: String, 차량번호: String, 렌트일: int, 반납예정일: int): double
        +반납(주민번호: String, 차량번호: String, 반납일: int): double
        +지연확인(반납일: int): boolean
    }

    class 렌트UI {
        <<Boundary>>
        +렌트요청(): boolean
        +반납요청(): boolean
    }

    %% 관계 설정
    %% 렌트정보 -> 고객정보 (연관관계, 목적: 고객정보, 다중성 0..* : 1)
    렌트정보 "0..*" --> "1" 고객정보 : 고객정보

    %% 렌트정보 -> 차량정보 (연관관계, 목적: 차량정보조회, 다중성 1 : 1)
    렌트정보 "1" --> "1" 차량정보 : 차량정보조회

    %% 렌트UI -> 렌트정보 (의존관계)
    렌트UI ..> 렌트정보 : 의존

