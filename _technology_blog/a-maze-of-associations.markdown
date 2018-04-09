---
layout: post
title: A maze of Associations
date:  2017-08-25 13:00:00
categories: main
banner_image: "maze.jpg"
summary: I find Associations extremely fascinating. They make a programmer's life easy, but understanding the is no joke!
---

When I started learning Rails, I was extremely confused in associations. They are like a maze in which getting lost is easy.

**Associations** serve as link between models. They make performing operations on the records easier.

So, let's take plunge into the details of Associations!

There are four types of associations.
1. One-to-Many
2. One-to-one
3. Many-to-Many
4. Polymorphic One-to-Many

<br/>
1. **One-to-Many** : [One-to-Many](http://guides.rubyonrails.org/association_basics.html#the-has-many-association) is one of
  the most commonly used association. It states that an instance of model has many instances of another model.
  For example, A student is enrolled in a University but a University has many students.<br/>
  We can say : <br/>
     _A Student `belongs_to` a University._<br/>
   _A University `has_many` Students._ <br/>
<br/>
     ```ruby
     class Student < ApplicationRecord
       belongs_to :university
     end

     class University < ApplicationRecord
        has_many :students
     end
     ```
     <br/>
    `belongs_to` is usually on the other side of has_many or has_one relationship.

     Once we establish _One-to-Many_ association, we get some very useful methods at our disposal:
     * `university.students` : gives us all the students, enrolled in a university.
     * `student.university` : gives us the name of university student is enrolled in.
     * `university.students << student1` : adds student1 to the collection and returns the collection.
     * `university.students.delete(@student1)` : deletes student1 from the collection. Sets foreign key to null.
     * `university.students.destroy(@student1)` : removes @student1 from collection by running destroy on each object.
     * `university.students.build({ })` : instantiates a new student but does not save it.
     * `university.students.create({ })` : validates and creates a new student and saves it in the database.
     * `university.students.create!({})` : validates, creates and saves student in database, but returns the exception in case of failure.
     * `university.build_student` : instantiates a new student but does not save it.
     * `university.create_student` : creates a new student and saves it in the database.<br/>
<br/>
<br/>
2. **One-to-One** : [One-to-One](http://guides.rubyonrails.org/association_basics.html#the-has-one-association)
  association states that one instance of model contains exactly one instance of other model.
 What that means is, for example:  A student has one University Account. One University Account belongs to one Student<br/>
  We can say:<br/>
 _A student `has_one` Account_<br/>
 _An Account `belongs_to` a Student_<br/>
    <br/>
    ```ruby
    class Student < ApplicationRecord
      has_one :account
    end

    class Account < ApplicationRecord
      belongs_to :student
    end
    ```
    <br/>
    After the relation is established, in _One-to-One_ as well we get few useful methods:
    * `student.account` : gets the account details for the student.
    * `student.build_account` : instantiates the new account but does not save it.
    * `student.create_adress` : validates, creates and saves new address to the database.<br/>
    <br/>
<br/>

3. **Many-to-Many** : This association says that many instances of model has many instances of another model. It needs
a join table which stores the relation between the two models.

   It can be set up in two ways :<br/>
    a) _Has_And_Belongs_To_Many (HABTM)_: In case of [Has And Belongs To Many](http://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association)
      , lets take an example and say, Teachers teach many Students and Students are taught by many Teachers.
   We can say it as :<br/>
     _Teacher `has_and_belongs_to_many` Students_<br/>
     _Student `has_and_belongs_to_many` Teachers_<br/>

   In this case the join table name by default will be `students_teachers`, but can be customized by the programmer.
   <br/>
   <br/>

    ```ruby
    class Teacher < ApplicationRecord
      has_and_belongs_to_many :students
    end

    class Student < ApplicationRecord
      has_and_belongs_to_many :teachers
    end
    ```
    <br/>

    Now, with the establishment of _HABTM_ relation, we get another set of methods to play around with:
    * `student.teachers`: all teachers teaching a particular student
    * `student.teacher_ids`: returns ids from the colection
    * `student.teacher_ids = [1, 2, 3]` : creates collection with objects corresponding to PK values supplied.
    * `student.teachers.delete(teacher_1)` or `student.teachers.destroy(teacher_1)`: deletes or destroys the relations for teacher_1
    * `teachers.empty?` : checks if teachers contains data
    * `teachers.size` : checks the size of teachers collection
    * `student.teachers.create(attributes = {})`: creates and adds objects to the collection.

    <br/>
    _HABTM_ is an approach which looks easy, but it is very rigid in the sense that we gain almost no flexibility
     of working with the relationship model. This problem is solved using _Has Many Through_ relation.
<br/>
<br/>
   b) _Has Many Through_ :
   [Has Many Through](http://guides.rubyonrails.org/association_basics.html#the-has-many-through-association) is a more flexible approach under _many_to_many_ relation.
   Let's say that Students in a university are to be sent many reminders for events and each event has many students attending it.<br/>
   We can say: <br/>
       _Students `has_many` Reminders `through` StudentsReminder_<br/>
       _Reminders `has_many` Students `through` StudentsReminder_<br/>
       _StudentsReminder `belongs_to` Students and Reminders_<br/>
    <br/>

    ```ruby
       class Student < ApplicationRecord
         has_many :students_reminders
         has_many :reminders, through: :students_reminders
       end

       class StudentsReminder < ApplicationRecord
         belongs_to :students
         belongs_to :reminders
       end

       class Reminder < ApplicationRecord
         has_many :students_reminders
         has_many :students, through: :students_reminders
       end
     ```
    <br/>

     _Has Many Through_ is a more flexible approach because now we can work with
     StudentsReminder model as well.
     <br/>
     <br/>

4. **Polymorphic One-to-Many**: In [Polymorphic association](http://guides.rubyonrails.org/association_basics.html#polymorphic-associations), the model belongs to more than one other models,
   on a single association. For example, a photo model can belong to either Student or Teacher.
    <br/>
     <br/>
    ```ruby
    class Photo < ApplicationRecord
      belongs_to :identification, polymorphic: true
    end

    class Student < ApplicationRecord
      has_many :photos, as: :identification
    end

    class Teacher < ApplicationRecord
      has_many :photos, as: :identification
    end
    ```
    <br/>
   While setting up _Polymorphic Association_ we must declare _Foregin Key_ column and a _Type_ column in the Photos model.

   Now, that we are done with setting up , we can go ahead and access the photos belonging to students and teachers.<br/>
   From an instance of Student we can say, `@student.photos`.<br/>
   And, from an instance of Teacher model, `@teacher.photos`.

   How amazing is that!
