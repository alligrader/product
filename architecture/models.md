# User Models

---

## User

Peeps.

---

github_ID
email
courses: [Course]
roles: ['student', 'teacher', 'ta']
student: Student || null
teacher: Student || null
ta: Student || null

---

## Student

Special user attributes for student users.

---

courses: [Course]

---

## TA

Special user attributes for TA users.

---

courses: [Course]

---

## Teacher

Special user attirbutes for teacher users.

---

courses: [Course]

---

## Course

Collection of assignments.

---

assignments: [Assignment]
weight: int

---

## Assignment

Template for repositories, synonymous with projects. Contains all metadata for running generating student instances and running tests.

---

name: String
tests: [Test]
weight: int
repository: (GHRepository, contains the gradeshaman.yaml)

---

## Test

Template for tests to be run, separate from the results on a per-repository basis.

---

weight: int

---

## StudentRepository

Assignment instances on a per-student basis.

---

student: Student
assignment: Assignment
run_results: [RunResults]
repository: (GHRepository)

---

## RunResults

Aggregate result of unit tests on an assignment.

---

test_results: [TestResult]
comilation_message: String (or null on success)

---

## TestResult

Atomic unit test.

---

test: Test
passed: Bool
error_message: String
