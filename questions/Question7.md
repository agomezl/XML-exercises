# Question7

Consider the following piece of XML:

```xml
<Question7>
  <Applicants>
    <Applicant name="Andersson" appNum="a1" />
    <Applicant name="Jonsson" appNum="a2" />
    <Applicant name="Larsson" appNum="a3" />
  </Applicants>

<Choices>
  <Choice applicant="a1" code="MPSOF" choiceNum="1" meritScore="750" />
  <Choice applicant="a1" code="MPALG" choiceNum="2" meritScore="750" />
  <Choice applicant="a1" code="MPCSN" choiceNum="3" meritScore="800" />
  <Choice applicant="a2" code="MPALG" choiceNum="1" meritScore="700" />
  <Choice applicant="a3" code="MPCSN" choiceNum="1" meritScore="850" />
  <Choice applicant="a3" code="MPALG" choiceNum="2" meritScore="850" />
</Choices>
</Question7>
```


* (**A**) Write a Document Type Definition (DTD) for the XML that is given above.

* (**B**) Write an XPath expression that finds Choice elements where
   the choice number is 1 and the merit score is greater than 800.

* (**C**) The flexibility of XML enables us to nest elements in a
  more natural way than in the example shown at the top of this
  question. Write a piece of XML that contains the same information
  as in the example shown above, but which uses nesting, and avoids
  duplication of applicant identifiers.
