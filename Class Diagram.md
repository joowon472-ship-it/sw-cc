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
