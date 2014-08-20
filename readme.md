## Console Lab

For this lab, we'd like you to strengthen your Rails console skills. This lab is going to be very familiar to the SQL lab, where we'll ask you to create a model and then write out the console commands you would use to execute these queries

### To Start

1. Create a model called Student, that has a first_name, last_name and age
2. Don't forget to run your migrations

### Tasks to create

1. Using the new/save syntax, create a student, first and last name and an age
elie = Student.create(:first_name=>"Elie", :last_name=>"Schoppik", :age=>30)

2. Save the student to the database
elie = Student.create(:first_name=>"Elie", :last_name=>"Schoppik", :age=>30)

3. Using the find/set/save syntax update the student's first name to taco
elie = Student.find(1)
elie.first_name="taco"

4. Delete the student (where first_name is taco)
elie=Student.find(1).destroy

5. Validate that every Student's last name is unique
validates :last_name, :uniqueness => true

6. Validate that every Student has a first and last name that is longer than 4 characters
validates :last_name, :length => {:minimum => 4}
validates :first_name,:length => {:minimum => 4}

7. Validate that every first and last name cannot be empty
validates :last_name,  	:presence => true
validates :first_name, :presence => true

7. Combine all of these individual validations into one validation (using validate and a hash) 
validates :last_name, 
				:uniqueness => true, 
				:presence => true,
				:length => {:minimum => 4}
				
	validates :first_name, 
				:presence => true,
				:length => {:minimum => 4}

8. Using the create syntax create a student named John Doe who is 33 years old
john=Student.create(:first_name=>"John", :last_name=>"Doe", :age=>30)

9. Show if this new student entry is valid
 SELECT  1 AS one FROM "students"  WHERE "students"."last_name" = 'Doe' LIMIT 1
   (0.2ms)  ROLLBACK

10. Show the number of errors for this student instance
@messages={:last_name=>["has already been taken", "is too short (minimum is 4 characters)"]}>

11. In one command, Change John Doe's name to Jonathan Doesmith 
jane.update_attributes(:first_name=>"Jonathan", :last_name=>"Doesmith")

12. Clear the errors array
jane.errors.clear

13. Save Jonathan Doesmith
jane.save

15. Find all of the Students
Student.all

16. Find the student with an ID of 128 and if it does not exist, make sure it returns nil and not an error
Student.find_by_id(128)

17. Find the first student in the table
Student.first

18. Find the last student in the table
Student.last
19. Find the student with the last name of Doesmith
Student.find_by_last_name("Doesmith")

20. Find all of the students and limit the search to 5 students, starting with the 2nd student and finally, order the students in alphabetical order
Student.offset(2).limit(5).order(:last_name)

21. Delete Jonathan Doesmith
Student.where(:last_name=>"Doesmith").first.destroy

### Bonus
1. Use the validates_format_of and regex to only validate names that consist of letters (no numbers or symbols) and start with a capital letter
validates_format_of :first_name => /[A-Z][a-z]+/

2. Write a custom validation to ensure that no one named Delmer Reed, Tim Licata, Anil Bridgpal or Elie Schoppik is included in the students table


