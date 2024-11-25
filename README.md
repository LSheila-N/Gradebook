# Gradebook
#Section A-Program starting
# Get the number of students

num_students = int(input("Enter the number of students in the class: ")) 

# Initialize total grade

total_grade = 0

# Loop through each student

for _ in range(num_students):

    name = input("Enter the student's name: ")  # Asking for the student's name

    # Get the grade and validate

    grade = float(input(f"Enter the grade for {name} (0-100): "))

    while grade < 0 or grade > 100:

        print("Grade must be between 0 and 100. Try again.")

        grade = float(input(f"Enter the grade for {name} (0-100): "))

    # Add the grade to the total and display the student's grade

    total_grade += grade

    print(f"{name}: {grade}")

# Calculate and display the class average

average_grade = total_grade / num_students

print(f"\nClass Average: {average_grade:.2f}")
 
 #Section B Program starting
 # Initialize an empty list to store subjects

subjects = []

# Prompt the user to enter the number of subjects

while True:

    try:

        num_subjects = int(input("Enter the number of subjects: "))

        break

    except ValueError:

        print("Invalid input. Please enter a number.")

# Loop to input subjects

for _ in range(num_subjects):

    while True:

        subject = input("Enter the subject name: ")

        if subject.isalpha():

            subjects.append(subject)

            break

        else:

            print("Invalid input. Please enter a valid subject name.")

# Initialize an empty list to store student data

students = []

# Prompt the user to enter the number of students

while True:

    try:

        num_students = int(input("Enter the number of students in the class: "))

        break

    except ValueError:

        print("Invalid input. Please enter a number.")

# Loop to process the input for multiple students

for _ in range(num_students):

    while True:

        name = input("Enter the student's name: ")

        if name.isalpha():

            break

        else:

            print("Invalid input. Please enter a valid name.")

    grades = []

    for subject in subjects:

        while True:

            try:

                grade = float(input(f"Enter {name}'s grade for {subject} (0-100): "))

                if 0 <= grade <= 100:

                    break

                else:

                    print("Grade must be between 0 and 100. Please try again.")

            except ValueError:

                print("Invalid input. Please enter a number.")

        grades.append(grade)

    # Convert grades list to a tuple

    grades_tuple = tuple(grades)

    # Add the student's data to the list

    students.append((name, grades_tuple))

# Calculate the average grade for each student across all subjects

print("\n--- Student Grades and Averages ---")

for name, grades in students:

    average_grade = sum(grades) / len(subjects)

    grades_str = ", ".join(f"{subject}: {grade:.2f}" for subject, grade in zip(subjects, grades))

    print(f"Student: {name}\nGrades: {grades_str}\nAverage: {average_grade:.2f}\n")

# Determine and print the highest and lowest grade for each subject

print("\n--- Highest and Lowest Grades for Each Subject ---")

for i, subject in enumerate(subjects):

    subject_grades = [grades[i] for name, grades in students]

    highest_grade = max(subject_grades)

    lowest_grade = min(subject_grades)

    print(f"{subject}\nHighest Grade: {highest_grade}\nLowest Grade: {lowest_grade}\n")

# Summary display of each student's name, grades, and average grade

print("\n--- Class Summary ---")

for name, grades in students:

    average_grade = sum(grades) / len(subjects)

    grades_str = ", ".join(f"{subject}: {grade:.2f}" for subject, grade in zip(subjects, grades))

    print(f"Student: {name}\nGrades: {grades_str}\nAverage: {average_grade:.2f}\n")
 
 #Section C Program starting
def add_student(student_data, subjects):
   while True:
       name = input("Enter student's name: ")
       if name.isalpha() and name not in student_data:
           break
       else:
           print("Invalid name or name already exists! Please enter a unique name with letters only.")
   grades = {}
   for subject in subjects:
       while True:
           grade = input(f"Enter {name}'s grade in {subject} (0-100): ")
           if grade.isdigit() and 0 <= int(grade) <= 100:
               grade = int(grade)
               break
           else:
               print("Invalid grade! Please enter a number between 0 and 100.")
       grades[subject] = grade
   student_data[name] = grades
def update_grades(student_data):
   name = input("Enter the student's name to update grades: ")
   if name in student_data:
       subject = input("Enter the subject to update: ")
       if subject in student_data[name]:
           while True:
               grade = input(f"Enter the new grade for {subject} (0-100): ")
               if grade.isdigit() and 0 <= int(grade) <= 100:
                   student_data[name][subject] = int(grade)
                   break
               else:
                   print("Invalid grade! Please enter a number between 0 and 100.")
       else:
           print(f"{subject} is not a valid subject for {name}.")
   else:
       print("Student not found!")
def remove_student(student_data):
   name = input("Enter the student's name to remove: ")
   if name in student_data:
       del student_data[name]
       print(f"Record for {name} has been deleted.")
   else:
       print("Student not found!")
def view_subject_grades(student_data):
   subject = input("Enter the subject to view grades: ")
   subject_grades = {name: grades[subject] for name, grades in student_data.items() if subject in grades}
   if subject_grades:
       print(f"\n{subject} Grades Across All Students:")
       print(f"{'Name':<20} {'Grade':<5}")
       print("-" * 25)
       for name, grade in subject_grades.items():
           print(f"{name:<20} {grade:<5}")
   else:
       print(f"No grades found for the subject {subject}.")
def search_student(student_data):
   name = input("Enter the student's name to search: ")
   if name in student_data:
       grades = student_data[name]
       average_grade = sum(grades.values()) / len(grades)
       print(f"\n{name}'s Grades:")
       print(f"{'Subject':<10} {'Grade':<5}")
       print("-" * 15)
       for subject, grade in grades.items():
           print(f"{subject:<10} {grade:<5}")
       print(f"\n{name}'s Average Grade: {average_grade:.2f}")
   else:
       print("Student not found!")
def display_class_results(student_data):
   print("\nClass Student Results:")
   for name, grades in student_data.items():
       average_grade = sum(grades.values()) / len(grades)
       print(f"{name}: {grades}, Average: {average_grade:.2f}")
def main():
   student_data = {}
   subjects = []
   while True:
       print("\n----- GRADEBOOK SYSTEM MENU -----")
       print("1. Enter Subjects")
       print("2. Enter Students and Grades")
       print("3. Search for a student")
       print("4. Update student grades")
       print("5. Delete student record")
       print("6. Display class student results")
       print("7. Exit system")
       choice = input("Enter Your Option (1-7): ")
       if choice == '1':
           subjects_input = input("Enter the subjects (comma-separated): ").split(",")
           subjects = [subject.strip() for subject in subjects_input if subject.strip() and subject.strip() not in subjects]
           for name in student_data:
               student_data[name] = {subject: student_data[name].get(subject, 0) for subject in subjects}
       elif choice == '2':
           if subjects:
               add_student(student_data, subjects)
           else:
               print("Please enter subjects first.")
       elif choice == '3':
           search_student(student_data)
       elif choice == '4':
           update_grades(student_data)
       elif choice == '5':
           remove_student(student_data)
       elif choice == '6':
           display_class_results(student_data)
       elif choice == '7':
           print("Exiting system...")
           break
       else:
           print("Invalid option! Please select a number between 1 and 7.")
if __name__ == "__main__":
   main()
   
   #Section D Program starting
   def add_student(student_data, subjects):

    while True:

        name = input("Enter student's name: ")

        if name.isalpha() and name not in student_data:

            break

        else:

            print("Invalid name or name already exists! Please enter a unique name with letters only.")

    grades = {}

    for subject in subjects:

        while True:

            grade = input(f"Enter {name}'s grade in {subject} (0-100): ")

            if grade.isdigit() and 0 <= int(grade) <= 100:

                grade = int(grade)

                break

            else:

                print("Invalid grade! Please enter a number between 0 and 100.")

        grades[subject] = grade

    student_data[name] = grades

def update_grades(student_data):

    name = input("Enter the student's name to update grades: ")

    if name in student_data:

        subject = input("Enter the subject to update: ")

        if subject.isalpha() and subject in student_data[name]:

            while True:

                grade = input(f"Enter the new grade for {subject} (0-100): ")

                if grade.isdigit() and 0 <= int(grade) <= 100:

                    student_data[name][subject] = int(grade)

                    break

                else:

                    print("Invalid grade! Please enter a number between 0 and 100.")

        else:

            print(f"{subject} is not a valid subject for {name}.")

    else:

        print("Student not found!")

def remove_student(student_data):

    name = input("Enter the student's name to remove: ")

    if name in student_data:

        del student_data[name]

        print(f"Record for {name} has been deleted.")

    else:

        print("Student not found!")

def view_subject_grades(student_data):

    subject = input("Enter the subject to view grades: ")

    if not subject.isalpha():

        print("Invalid subject! Please enter letters only.")

        return

    subject_grades = {name: grades.get(subject) for name, grades in student_data.items() if subject in grades}

    if subject_grades:

        print(f"\n{subject} Grades Across All Students:")

        print(f"{'Name':<20} {'Grade':<5}")

        print("-" * 25)

        for name, grade in subject_grades.items():

            print(f"{name:<20} {grade:<5}")

    else:

        print(f"No grades found for the subject {subject}.")

def search_student(student_data):

    name = input("Enter the student's name to search: ")

    if name in student_data:

        grades = student_data[name]

        average_grade = sum(grades.values()) / len(grades)

        print(f"\n{name}'s Grades:")

        print(f"{'Subject':<10} {'Grade':<5}")

        print("-" * 15)

        for subject, grade in grades.items():

            print(f"{subject:<10} {grade:<5}")

        print(f"\n{name}'s Average Grade: {average_grade:.2f}")

    else:

        print("Student not found!")

def display_class_results(student_data):

    print("\nClass Student Results:")

    for name, grades in student_data.items():

        average_grade = sum(grades.values()) / len(grades)

        print(f"{name}: {grades}, Average: {average_grade:.2f}")

def input_subjects():

    subjects_input = input("Enter the subjects (comma-separated): ").split(",")

    return [subject.strip() for subject in subjects_input if subject.strip().isalpha()]

def main():

    student_data = {}

    subjects = []

    while True:

        print("\n----- GRADEBOOK SYSTEM MENU -----")

        print("1. Enter Subjects")

        print("2. Enter Students and Grades")

        print("3. Search for a student")

        print("4. Update student grades")

        print("5. Delete student record")

        print("6. Display class student results")

        print("7. Exit system")

        choice = input("Enter Your Option (1-7): ")

        if choice == '1':

            subjects = input_subjects()

            for name in student_data:

                student_data[name] = {subject: student_data[name].get(subject, 0) for subject in subjects}

        elif choice == '2':

            if subjects:

                add_student(student_data, subjects)

            else:

                print("Please enter subjects first.")

        elif choice == '3':

            search_student(student_data)

        elif choice == '4':

            update_grades(student_data)

        elif choice == '5':

            remove_student(student_data)

        elif choice == '6':

            display_class_results(student_data)

        elif choice == '7':

            print("Exiting system...")

            break

        else:

            print("Invalid option! Please select a number between 1 and 7.")

if __name__ == "__main__":

    main() 
    
#Section E Program starting 
class Student:
   def __init__(self, name):
       self.name = name
       self.grades = {}
   def add_grade(self, subject, grade):
       if subject not in self.grades:
           self.grades[subject] = []
       self.grades[subject].append(grade)
   def calculate_average(self):
       total_grades = sum(sum(grades) for grades in self.grades.values())
       total_count = sum(len(grades) for grades in self.grades.values())
       return total_grades / total_count if total_count else 0
   def print_details(self):
       print(f"Student Name: {self.name}")
       for subject, grades in self.grades.items():
           print(f"{subject}: {grades}")
       print(f"Overall Average: {self.calculate_average():.2f}")

class Gradebook:
   def __init__(self):
       self.students = {}
   def add_student(self, name):
       self.students[name] = Student(name)
   def remove_student(self, name):
       if name in self.students:
           del self.students[name]
       else:
           print(f"Student {name} not found.")
   def search_student(self, name):
       return self.students.get(name)
   def sort_students_by_average(self):
       return sorted(self.students.values(), key=lambda student: student.calculate_average(), reverse=True)
   def sort_students_by_subject(self, subject):
       return sorted(
           self.students.values(),
           key=lambda student: sum(student.grades.get(subject, [])) / len(student.grades.get(subject, [])) if subject in student.grades else 0,
           reverse=True
       )
   def print_all_students(self):
       for student in self.students.values():
           student.print_details()
           print('---')

def test_gradebook():
   # Create a Gradebook instance
   gradebook = Gradebook()
   # Add students
   gradebook.add_student("Sheila")
   gradebook.add_student("Amber")
   # Add grades for Sheila
   sheila = gradebook.search_student("Sheila")
   if sheila:
       sheila.add_grade("Math", 85)
       sheila.add_grade("English", 90)
       sheila.add_grade("Science", 78)
   # Add grades for Amber
   amber = gradebook.search_student("Amber")
   if amber:
       amber.add_grade("Math", 92)
       amber.add_grade("English", 88)
       amber.add_grade("Science", 95)
   # Print all students
   print("All students:")
   gradebook.print_all_students()
   # Search for a student
   print("\nSearching for student Sheila:")
   found_student = gradebook.search_student("Sheila")
   if found_student:
       found_student.print_details()
   # Sort students by average grade
   print("\nStudents sorted by average grade:")
   sorted_by_average = gradebook.sort_students_by_average()
   for student in sorted_by_average:
       student.print_details()
   # Sort students by Math grades
   print("\nStudents sorted by Math grades:")
   sorted_by_math = gradebook.sort_students_by_subject("Math")
   for student in sorted_by_math:
       student.print_details()
   # Remove a student
   print("\nRemoving student Amber.")
   gradebook.remove_student("Amber")
   print("All students after removal:")
   gradebook.print_all_students()

# Run the test function
test_gradebook()

#Section F Program starting
class StudentNotFoundError(Exception):

    """Exception raised when a student is not found."""

    pass

class InvalidGradeError(Exception):

    """Exception raised when an invalid grade is entered."""

    pass

class Student:

    def __init__(self, name):

        self.name = name

        self.grades = {}

    def add_grade(self, subject, grade):

        if not (0 <= grade <= 100):

            raise InvalidGradeError(f"Invalid grade: {grade}. Grade must be between 0 and 100.")

        if subject not in self.grades:

            self.grades[subject] = []

        self.grades[subject].append(grade)

    def calculate_average(self):

        total_grades = sum(sum(grades) for grades in self.grades.values())

        total_count = sum(len(grades) for grades in self.grades.values())

        return total_grades / total_count if total_count > 0 else 0

class Gradebook:

    def __init__(self):

        self.students = {}

    def add_student(self, name):

        if name in self.students:

            raise ValueError(f"Student {name} already exists.")

        self.students[name] = Student(name)

    def remove_student(self, name):

        if name not in self.students:

            raise StudentNotFoundError(f"Student {name} not found.")

        del self.students[name]

    def find_student(self, name):

        if name not in self.students:

            raise StudentNotFoundError(f"Student {name} not found.")

        return self.students[name]

    def sort_students_by_average(self):

        sorted_students = list(self.students.values())

        n = len(sorted_students)

        for i in range(n):

            for j in range(0, n - i - 1):

                if sorted_students[j].calculate_average() < sorted_students[j + 1].calculate_average():

                    sorted_students[j], sorted_students[j + 1] = sorted_students[j + 1], sorted_students[j]

        return sorted_students

def display_menu():

    print("\nMenu:")

    print("1 = Subject Details")

    print("2 = Add Student")

    print("3 = Display Student Data")

    print("4 = Update Grade")

    print("5 = Search Student")

    print("6 = Remove Student")

    print("7 = Exit")

def subject_details():

    print("This function should provide details about subjects. (Not implemented)")

def add_student(gradebook):

    name = input("Enter the student's name: ")

    try:

        gradebook.add_student(name)

        print(f"Student {name} added successfully.")

    except ValueError as e:

        print(e)

def display_student_data(gradebook):

    for name, student in gradebook.students.items():

        print(f"Name: {name}, Grades: {student.grades}, Average: {student.calculate_average():.2f}")

def update_grade(gradebook):

    name = input("Enter the student's name to update grades: ")

    try:

        student = gradebook.find_student(name)

        subject = input("Enter the subject: ")

        grade = float(input("Enter the new grade: "))

        student.add_grade(subject, grade)

        print(f"Grade updated for {name} in {subject}.")

    except (StudentNotFoundError, InvalidGradeError) as e:

        print(e)

def search_student(gradebook):

    name = input("Enter the student's name to search: ")

    try:

        student = gradebook.find_student(name)

        print(f"Student found: {student.name}, Average grade: {student.calculate_average():.2f}")

    except StudentNotFoundError as e:

        print(e)

def remove_student(gradebook):

    name = input("Enter the student's name to remove: ")

    try:

        gradebook.remove_student(name)

        print(f"Student {name} removed successfully.")

    except StudentNotFoundError as e:

        print(e)

def main():

    gradebook = Gradebook()

    while True:

        display_menu()

        choice = input("Enter your choice: ")

        if choice == '1':

            subject_details()

        elif choice == '2':

            add_student(gradebook)

        elif choice == '3':

            display_student_data(gradebook)

        elif choice == '4':

            update_grade(gradebook)

        elif choice == '5':

            search_student(gradebook)

        elif choice == '6':

            remove_student(gradebook)

        elif choice == '7':

            print("Exiting the program.")

            break

        else:

            print("Invalid choice. Please try again.")

if __name__ == "__main__":

    main() 
#END OF Program
