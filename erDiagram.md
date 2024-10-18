```mermaid
erDiagram
    %% Entity: CUSTOMUSER
    %% Represents a user of the system, whether a teacher or a student
    CUSTOMUSER {
        int id PK
        string full_name
        string email
        string password
        string profile_picture
        string bio
        boolean is_teacher
        boolean is_student
        datetime date_joined
    }

    %% Entity: SKILL
    %% Represents the various skills that can be taught or learned
    SKILL {
        int id PK
        string skill_name
        string category
    }

    %% Entity: USERSKILL 
    %% Junction table that maps users and their associated skills
    USERSKILL {
        int id PK
        int user_id FK
        int skill_id FK
        string skill_type
        string proficiency_level
    }

    %% Entity: AVAILABILITY 
    %% Lists the available days and times for a user to teach/learn
    AVAILABILITY {
        int id PK
        int user_id FK
        string days
        string time_slots
    }

    %% Relationships
    %% CUSTOMUSER to USERSKILL (One-to-Many)
    %% A user can be linked to multiple skills (teaching or learning)
    CUSTOMUSER ||--o{ USERSKILL : "has"

    %% SKILL to USERSKILL (One-to-Many)
    %% One skill can be associated with many users (teaching/learning)
    SKILL ||--o{ USERSKILL : "containing"

    %% CUSTOMUSER to AVAILABILITY (One-to-One)
    %% Each user has one availability schedule
    CUSTOMUSER ||--|{ AVAILABILITY : "has"
