---
layout: post
title: A maze of associations
date:  2017-03-13 13:00:00
categories: main
banner_image: "rubygem.jpeg"
summary: I find associations extremely fascinating, so decided to publish a post regarding Rails Associations. This post talks about the connection created by associations between two models, how they can be used, what methods user gets at his or her disposal, etc.
---

When I started learning rails, I was extremely confused in associations. They are like a maze in which you can get lost easily,
if you have not understood it properly. But when I understood associations I realized that they make our life easy when we are
trying to code in Rails.

Associations serve as link between models. For example, a Post is created by an Author. Fine! But how will Rails know that these
two models, Post and Author are related to each other. This is where Associations come into play.

That sounds great but how do they work? Before getting into that, Let’s go ahead and see the types of associations.
There are four types of associations.
1. One-to-Many
2. One-to-one
3. Many-to-Many
4. Polymorphic one-to-many

Time to dive in and have a closer look at these associations:

1. **One-to-Many** : [One-to-Many](http://guides.rubyonrails.org/association_basics.html#the-has-many-association) is one of
  the most commonly used association. It states that an instance of model has many instances of another model.
  For example, A student is enrolled in a University but a University has many students. We can say :
  _A University has_many students._
  _A student belongs_to a University._

  ```ruby
  class University < ApplicationRecord
    has_many :students
  end

  class Student < ApplicationRecord
    belongs_to :university
  end
  ```
  belongs_to is usually on the other side of has_many or has_one relationship and must be specified as singular.

  Once we establish _One-to-Many_ association, we get some very useful methods at our disposal:
  ..* university.students : name of students, enrolled in a university.
  ..* student.university : name of university student is enrolled in.
  ..* university.students << student : adds student to the collection.
  ..* university.students.delete(@student1) : deletes student1 from the collection. Sets foreign key to null.
  ..* university.students.destroy(@student1) : removes @student1 from collection by running destroy on each object.
  ..* university.students.build({ }) : instantiates a new student but does not save it.
  ..* university.students.create({ }) : validates and creates a new student and saves it in the database.
  ..* university.students.create!({}) : validates, creates and saves student in database, but returns the exception in case of failure.
  ..* university.build_student : instantiates a new student but does not save it.
  ..* university.create_student : creates a new student and saves it in the database.


2. **One-to-One** : [One-to-One](http://guides.rubyonrails.org/association_basics.html#the-has-one-association)
  association states that one instance of model contains exactly one instance of other model.
 What that means is, for example A student enrolled in a university owns one University Account. We can say like this:
 _A student has_one Account_

 ```ruby
 class Student < ApplicationRecord
   has_one :account
 end

 class Account < ApplicationRecord
   belongs_to :student
 end
 ```
 After the relation is established, in _One-to-One_ as well we get few useful methods:
 ..* student.account - gets the account details for the student.
 ..* student.build_account - instantiates the new account but does not save it.
 ..* student.create_adress - validates, creates and saves new address to the database.

3. **Many-to-Many** : This association states that many instances of model has many instances of another model.
It can be set up in two ways :
..* _Has_And_Belongs_To_Many_ (HABTM) : This asociation does not require a join table. It is mor eor less a direct relation.
For example, Teachers teach many Students and Students are taught by many Teachers.
We can say it as :
  _Teachers has_many Students_
  _Students has_many Teachers_


