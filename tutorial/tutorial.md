# XML Tutorial


For this tutorial we will once again return to the same domain.
Previously we have used a relational model, for which we have identified
the following relations:

```
  Teachers(_name, room)
      room -> Rooms.name

  TeacherTitles(_teacher, _title)
      teacher -> Teachers.name

  Rooms(_name, nrSeats)

  Courses(_name, teacher, nrStudents)
      teacher -> Teachers.name

  Classes(_course, _day, _hour)
      course -> courses.name
```

Now we will switch to a semi-structured data model.

## DTDs


Your first task is to come up with a schema for a semi-structured model
of the same domain, in other words to create a DTD for the domain. Note
that there are several ways of creating a DTD that would make perfect
sense for this domain.

-  Create a schema that directly mirrors the relational model. Remember
   that a "relational" DTD consists of exactly three levels below the
   root, with values only at the outermost level (in the leaves).
-  Create a schema that makes use of the flexibility of the
   semi-structured model. In particular your schema should allow values
   on other levels than the outermost, and have a varying number of
   levels in various parts of the schema.

## XML


Once you have your second schema, construct a small sample XML document
that conforms to it.

Note that XML is a fairly verbose language, and this task could take
quite some time if you don't restrict yourself. The point is to practise
the relationship between XML and DTDs, not to practise your skill at
writing < and > symbols…

## XPath

Use the second schema you constructed. For each of the following, write
an XPath expression that:

-  finds all courses that have at least 20 students.
-  lists all professors at the school.
-  finds all courses that have classes on Mondays.
-  finds all rooms that are used on Mondays.

Use [XPath Checker](https://addons.mozilla.org/firefox/addon/xpath-checker/)
or any other tool for checking your XPath expressions.


# Solutions


## DTDs


First, a schema that directly mirrors the relational model:


```
    <!DOCTYPE Hogwarts [

     <!ELEMENT Hogwarts (Teachers, TeacherTitles, Rooms, Courses, Classes)>

     <!ELEMENT Teachers (Teacher*)>
      <!ELEMENT Teacher EMPTY>
       <!ATTLIST Teacher
         name ID    #REQUIRED
         room IDREF #REQUIRED>


     <!ELEMENT TeacherTitles (TeacherTitle*) >
      <!ELEMENT TeacherTitle EMPTY >
       <!ATTLIST TeacherTitle
         teacher IDREF #REQUIRED
         title   CDATA #REQUIRED>

     <!ELEMENT Rooms (Room*)>
      <!ELEMENT Room EMPTY>
       <!ATTLIST Room
         name    ID    #REQUIRED
         nrSeats CDATA #IMPLIED>


     <!ELEMENT Courses (Course*)>
      <!ELEMENT Course EMPTY>
       <!ATTLIST Course
         name       ID    #REQUIRED
         teacher    IDREF #REQUIRED
         nrStudents CDATA #IMPLIED>

     <!ELEMENT Classes (Class*)>
      <!ELEMENT Class EMPTY>
       <!ATTLIST Class
         course IDREF #REQUIRED
         day    CDATA #REQUIRED
         hour   CDATA #REQUIRED>

     ]>
```

Three levels everywhere, for tables, rows, and attributes respectively.
Note that we cannot declare composite keys, so Classes and TeacherTitles
don't have any ID attributes.

Then a more natural approach:


```
     <!DOCTYPE Hogwarts [

     <!ELEMENT Hogwarts (Rooms, Teachers, Courses) >

     <!ELEMENT Rooms (Room*) >
      <!ELEMENT Room EMPTY >
       <!ATTLIST Room
         name    ID    #REQUIRED
         nrSeats CDATA #IMPLIED >

     <!ELEMENT Teachers (Teacher*) >
      <!ELEMENT Teacher (Title*) >
       <!ELEMENT Title (#PCDATA) >
       <!ATTLIST Teacher
         name ID    #REQUIRED
         room IDREF #REQUIRED >

     <!ELEMENT Courses (Course*) >
      <!ELEMENT Course (Class*) >

       <!ATTLIST Course
         name       ID    #REQUIRED
         teacher    IDREF #REQUIRED
         nrStudents CDATA #IMPLIED >
       <!ELEMENT Class EMPTY >
        <!ATTLIST Class
          day    CDATA #REQUIRED
          hour   CDATA #REQUIRED >

     ]>
```

There are room for differences of course. We might choose to make
Classes children of Rooms instead, and include an IDREF course, to get a
model similar in spirit to the one we got when doing the 3NF
decomposition in (the solutions of) exercise 3. Similarly we could add
an IDREF room to the Class element in the model above, to get a model
similar inspirit to the one that we got from the E-R diagram in exercise
2. There are other (endless) variations as well, but these are (in my
opinion at least) the most natural.

Files containing both the DTDs and XML data are available on-line:

- [Relational approach](relational.xml)
- [More natural approach](natural.xml)
- [More natural approach with more data added](natural_extra.xml)
  (for testing the XPath solutions)

These XML files have been validated using the
[W3C validation service](http://validator.w3.org/).

## XML


An XML document conforming to the DTD above:

```xml
<?xml version="1.0" standalone="yes" ?>

<!-- put the DTD here -->

<Hogwarts>
 <Rooms>
  <Room name="The_Dungeon" nrSeats="34" />
  <Room name="The_Cabin" nrSeats="163" />
 </Rooms>

 <Teachers>
  <Teacher name="Snape" room="The_Dungeon" >
   <Title>Professor</Title>
  </Teacher>
  <Teacher name="Hagrid" room="The_Cabin" />
 </Teachers>

 <Courses>
  <Course name="Potioncraft" teacher="Snape" nrStudents="28">
   <Class day="Monday" hour="10" />
  </Course>
  <Course name="Handling_of_Wild_Creatures" teacher="Hagrid">
   <Class day="Saturday" hour="13" />
   <Class day="Thursday" hour="7" />
  </Course>
 </Courses>
</Hogwarts>
```

## XPath

(These solutions have been tested using an on-line XPath
tester and also the XPath progam on the Linux system at Chalmers.)

-  Find all courses that have at least 20 students:

   ```
   //Course[@nrStudents >= 20]
   ```

-  List all professors at the school:

   ```
   //Teacher[Title = "Professor"]
   ```

-  Find all courses that have classes on Mondays:

   ```
   //Course[Class/@day = "Monday"]
   ```

-  Find all rooms that are used on Mondays:

   ```
   //Room[@name = ancestor::Hogwarts//Teacher[@name = ancestor::Hogwarts//Course[Class/@day = "Monday"]/@teacher]/@room]
   ```
