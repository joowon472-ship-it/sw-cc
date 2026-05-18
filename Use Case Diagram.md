```mermaid

graph LR
    %% Actor Definitions
    User[/"👤 일반 사용자"\]
    Admin[/"👤 관리자"\]

    %% Use Cases (General User)
    UC01(["UC-01: 회원가입"])
    UC01_1(["UC-01-1: 이메일 형식 검증"])
    UC01_2(["UC-01-2: 비밀번호 길이 검증"])
    
    UC02(["UC-02: 강의자료 업로드"])
    UC03(["UC-03: 시험 날짜 입력"])
    UC03_1(["UC-03-1: 과거 날짜 입력 검증"])
    
    UC04(["UC-04: 맞춤형 학습 계획 생성"])
    UC05(["UC-05: 강의자료 핵심 요약 제공"])

    %% Relationships for UC-01
    User --> UC01
    UC01 -.->|&lt;&lt;include&gt;&gt;| UC01_1
    UC01 -.->|&lt;&lt;include&gt;&gt;| UC01_2

    %% Relationships for UC-02 & UC-03
    User --> UC02
    User --> UC03
    UC03 -.->|&lt;&lt;include&gt;&gt;| UC03_1

    %% Relationships for UC-04 & UC-05 (System-driven but triggered by User/Data)
    User --> UC04
    User --> UC05
    
    UC04 -.->|&lt;&lt;include&gt;&gt;| UC02
    UC04 -.->|&lt;&lt;include&gt;&gt;| UC03
    UC05 -.->|&lt;&lt;include&gt;&gt;| UC02

    %% Admin Relationships
    Admin --> UC02
    Admin --> UC03
    %% 관리자는 일반 사용자의 모든 기능을 기본적으로 포함하거나 모니터링할 수 있다고 가정하여 상속 표현 가능
    Admin -.->|&lt;&lt;extends&gt;&gt;| User

    %% Style Settings
    style User fill:#e1f5fe,stroke:#039be5,stroke-width:2px
    style Admin fill:#ffe0b2,stroke:#fb8c00,stroke-width:2px
    style UC01 fill:#f5f5f5,stroke:#333,stroke-width:2px
    style UC02 fill:#f5f5f5,stroke:#333,stroke-width:2px
    style UC03 fill:#f5f5f5,stroke:#333,stroke-width:2px
    style UC04 fill:#f5f5f5,stroke:#333,stroke-width:2px
    style UC05 fill:#f5f5f5,stroke:#333,stroke-width:2px



## 클래스 다이어그램
```mermaid
classDiagram

class User {
    -String userId
    -String email
    -String password
    +signUp()
    +login()
    +uploadLectureMaterial()
    +setExamDate()
}

class Admin {
    -String adminId
    -String password
    +manageUsers()
    +manageMaterials()
}

class LectureMaterial {
    -String fileName
    -Date uploadDate
    +uploadMaterial()
    +summarizeMaterial()
}

class Exam {
    -Date examDate
    -String subject
    +setExamDate()
    +validateDate()
}

class StudyPlan {
    -String planContent
    -Date createdDate
    +generatePlan()
}

class Summary {
    -String summaryContent
    +generateSummary()
}

User --> LectureMaterial : uploads
User --> Exam : sets
User --> StudyPlan : generates
User --> Summary : requests

Admin --> User : manages
Admin --> LectureMaterial : manages

LectureMaterial --> Summary : creates
Exam --> StudyPlan : used for
```
