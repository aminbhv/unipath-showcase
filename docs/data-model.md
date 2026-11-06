# Data model: selected relationships

The diagram below summarizes a subset of the relational model. It is a conceptual view, not an export of the private database schema.

```mermaid
erDiagram
    ORGANIZATION ||--o{ ACCOUNT : contains
    ACCOUNT ||--o| STUDENT_PROFILE : has
    ACCOUNT ||--o| STAFF_PROFILE : has
    ACCOUNT ||--o{ MENTOR_ASSIGNMENT : participates_in
    ACCOUNT ||--o{ CLASS : teaches
    CLASS ||--o{ CLASS_ENROLLMENT : contains
    ACCOUNT ||--o{ CLASS_ENROLLMENT : enrolls
    ACCOUNT ||--o{ APPLICATION : owns
    ACCOUNT ||--o{ TEST_SCORE : records_for_student
```

## Why separate these entities?

- **Accounts and profiles:** authentication identity and role are distinct from student- or staff-specific information.
- **Mentor assignments:** a relationship has a start and optional end. Ending an assignment changes access without deleting its history.
- **Classes and enrollments:** a class can contain many students, and a student can join multiple classes. Enrollment is a separate relationship.
- **Applications:** multiple applications can belong to a student, each with its own status and deadline.
- **Test scores:** exam type, test date, official/practice status and scale-specific values are stored explicitly rather than treating unrelated exams as interchangeable numbers.

## Integrity rules

- Foreign keys preserve valid references between records.
- Organization-scoped relationships prevent a record in one organization from referencing a participant in another.
- Uniqueness rules prevent conflicting active mentor assignments.
- Validation triggers enforce role and relationship rules alongside application validation.
- Row Level Security determines which records a signed-in account may read.

The full platform also includes tasks, document workflows, roadmaps, homework, assessments, meetings, notifications, messaging and internal payment records.
