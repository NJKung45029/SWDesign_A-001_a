```mermaid
classDiagram
    class User {
        - id: String
        - pw: String
        - name: String
        - phone: String
        - address: String
        + registerUser(id: String, pw: String, name: String, phone: String, address: String) void
        + updateUser(name: String, phone: String, address: String) void
        + deleteUser(id: String) void
        + searchUser(id: String) User
    }

    class Account {
        - number: String
        - balance: long
        - owner: User
        + deposit(id: String, amount: long) void
        + withdraw(id: String, amount: long) boolean
        + transfer(id: String, targetAccountNumber: String, amount: long) boolean
        + computeBalance(): long
    }

    class BankUI {
        + displayMenu() void
        + inputTransactionData() void
    }

    %% 관계 설정
    %% User 1명당 Account는 1개 이상 (1..*)
    %% Account에서 User로의 조회를 위한 연관 관계
    User "1" <-- "1..*" Account : references

    %% BankUI가 Account를 사용하는 의존 관계
    BankUI ..> Account : uses
