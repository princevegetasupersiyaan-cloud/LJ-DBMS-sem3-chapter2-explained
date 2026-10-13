# DBMS Chapter 2 — Database Architecture

Source: Uploaded PPT — DBMS CH-2, Database Architecture · 31 slides

We’ll follow your requested workflow in order, using your uploaded PPT as the primary source. I’ve identified the chapter’s topics and will preserve the PPT’s terminology and sequence. Where a slide contains only a diagram or heading, I’ll distinguish what the PPT shows from any additional explanation used to make it easier to understand.

## STEP 1 — Deep Explanation

## 1. Introduction to Database Architecture

Database architecture describes how a database system is organized, how its different levels interact, and how users and applications access stored data.

The chapter covers:

1. Schemas, sub-schemas, and instances

2. Three-level ANSI/SPARC database architecture

3. Advantages and disadvantages of three-tier architecture

4. Data independence

5. Mappings

6. Data models

7. Types of database systems

The central idea is to understand how data is viewed by users, logically organized, and physically stored.

## 2. Schemas, Sub-schemas, and Instances

These are three important DBMS concepts introduced in slide 3.

### 2.1 Schema

Definition: A schema represents the logical configuration of all or part of a relational database.

In simple words, a schema describes the database's structure. It specifies how data is organized, such as tables, columns, and relationships.

Example: Consider a college database.

```
STUDENT
------------------------
Student_ID
Student_Name
Department
Semester
```

The structure of the `STUDENT` table is part of the database schema.

The schema describes the arrangement of the data, not the actual values stored in every row.

### 2.2 Sub-schema

Definition: A sub-schema is the logical description of the section of a database that is relevant and available to a particular application.

In simple words, it describes the part of the database that a specific user or application needs.

Example: A college database contains student details, fee details, attendance, and examination results.

* The examination department needs student details and marks.

* The accounts department needs student details and fee records.

* A student may need their own marks and attendance.

Each application can have a different view of the same overall database.

```
             COLLEGE DATABASE
                    |
          ┌─────────┼─────────┐
          |         |         |
       Exams      Accounts  Student Portal
       View         View       View
```

These application-specific views illustrate the idea of sub-schemas.

### 2.3 Instance

Definition: An instance of a database is the data stored in the database at a particular moment in time.

In simple words, the schema describes the structure, while the instance represents the actual data present at a specific time.

Suppose the `STUDENT` table has these records:

| Student_ID | Student_Name | Semester |
| ---------- | ------------ | -------- |
| 101        | Amit         | 3        |
| 102        | Neha         | 3        |

These records form part of the current database instance. If another student is added, the instance changes, even if the schema remains the same.

### Schema vs. sub-schema vs. instance

| Basis        | Schema                            | Sub-schema                                    | Instance                              |
| ------------ | --------------------------------- | --------------------------------------------- | ------------------------------------- |
| Meaning      | Overall logical structure         | Relevant portion of the database              | Actual data at a particular time      |
| Focus        | Database organization             | Application-specific view                     | Current stored values                 |
| Example      | Structure of the college database | Examination department's view                 | Current student records               |
| Changes when | Database structure is modified    | The application's view or requirements change | Data is inserted, updated, or deleted |

Exam point: Schema = structure; sub-schema = relevant portion or view; instance = data at a particular moment.

## 3. Three-Level ANSI/SPARC Database Architecture

Slides 4–9 introduce the three-schema architecture.

### 3.1 Meaning and purpose

Definition: The three-schema architecture, also called the ANSI/SPARC architecture or three-level architecture, is a framework used to describe the structure of a database system.

According to the PPT, it helps separate user applications from the physical database.

It divides the database system into three levels:

1. Internal level

2. Conceptual level

3. External level

Each level describes the database from a different perspective.

### 3.2 Overall architecture

### External Level

Different user views of the database

### Conceptual Level

Overall logical structure of the database

### Internal Level

Physical storage of data

The diagram summarizes the three levels. Mapping mechanisms connect the levels, allowing requests and results to be translated between them.

### 3.3 Internal Level

Definition: The internal level describes the physical storage structure of the database.

The PPT also calls the internal schema the physical schema.

Important points:

* It uses the physical data model.

* It defines how data is stored.

* It describes how data is organized in storage blocks.

* It focuses on the physical representation of data rather than the views presented to users.

Example: A college database might store records in disk blocks and use indexes to locate student records efficiently.

A user generally does not need to know the precise physical arrangement of those records.

Remember: Internal level = How is the data physically stored?

### 3.4 Conceptual Level

Definition: The conceptual level describes the design and logical structure of the entire database.

The PPT also calls it the logical level.

Important points:

* It describes the structure of the whole database.

* It specifies what data is stored.

* It describes the logical organization of the database.

* Programmers and database administrators (DBAs) work at this level.

Example: The college database contains `STUDENT`, `COURSE`, `FACULTY`, and `RESULT` tables, with relationships between them.

The conceptual level describes these logical structures without focusing on exactly how the records are placed on disk.

Remember: Conceptual level = What data is stored, and how is it logically organized?

### 3.5 External Level

Definition: The external level describes the different views of the database.

The PPT calls an external schema a view schema.

Important points:

* Different users can see different views of the same database.

* It describes how end users interact with the database system.

* Each view shows information relevant to a particular user or application.

Example: In a college system:

* A student sees their marks and attendance.

* A faculty member sees the students in their classes.

* An accounts employee sees fee-related information.

These are different views of the underlying database.

Remember: External level = What does a particular user see?

### 3.6 Comparison of the three levels

| Basis           | External               | Conceptual              | Internal            |
| --------------- | ---------------------- | ----------------------- | ------------------- |
| Also called     | View level             | Logical level           | Physical level      |
| Describes       | User-specific views    | Entire logical database | Physical storage    |
| Main question   | What can the user see? | What data is stored?    | How is data stored? |
| Main focus      | User interaction       | Database design         | Storage structure   |
| PPT terminology | View schema            | Conceptual schema       | Physical schema     |

Important exam question: Explain the three levels of ANSI/SPARC architecture with a diagram.

For this answer, draw the three boxes in order — External, Conceptual, Internal — and explain the purpose of each.

## 4. Advantages of Three-Tier Architecture

Slide 10 lists five advantages.

### 4.1 Scalability

Meaning: The system can be expanded to handle more users, applications, or data.

Example: A college database can be expanded to support additional departments and students.

### 4.2 Performance

Meaning: Separating responsibilities across tiers can help improve performance when the system is designed appropriately.

Example: An application tier can process requests while the database tier manages data storage and retrieval.

### 4.3 Easy to maintain and modify

Meaning: Separating system responsibilities makes it easier to maintain or modify individual parts without redesigning everything.

Example: The user interface can be redesigned without necessarily changing the underlying database structure.

### 4.4 Improved data integrity

Meaning: Data integrity means maintaining the accuracy and consistency of data. A well-designed architecture can help enforce validation rules and constraints.

Example: A database can enforce that a student ID must be unique.

### 4.5 Improved security

Meaning: Different tiers can apply access controls to restrict access to data and operations.

Example: Students may view their results, while authorized examination staff can update marks.

## 5. Disadvantages of Three-Tier Architecture

Slide 11 lists four disadvantages.

| Disadvantage                     | Explanation                                                                                          |
| -------------------------------- | ---------------------------------------------------------------------------------------------------- |
| More complex                     | Multiple tiers and their interactions increase system complexity.                                    |
| Requires a separate proxy server | The PPT lists this as a disadvantage. The need for a proxy depends on the particular implementation. |
| Increased complexity or effort   | Designing, configuring, and coordinating the tiers can require additional work.                      |
| Increased network traffic        | Communication between separate tiers can generate additional network requests and responses.         |

Exam tip: Learn all four disadvantages as listed in the PPT. The proxy-server requirement is not universal to every three-tier implementation.

## 6. Data Independence

Slides 12–15 cover data independence and its two types.

### 6.1 Definition

Data independence is the ability to modify the schema at one level of a database system without requiring changes to the schema at the next higher level.

In simple words, a change in one layer should not unnecessarily affect the layer above it.

The three-level architecture helps achieve this separation.

### 6.2 Types of data independence

The PPT identifies two types:

1. Logical data independence

2. Physical data independence

Data Independence

Logical Data Independence

Conceptual schema changes without requiring changes to external schemas.

Physical Data Independence

Internal schema changes without requiring changes to the conceptual schema.

### 6.3 Logical Data Independence

Definition: Logical data independence is the ability to change the conceptual schema without having to change the external schema.

The PPT explains that it separates the external level from the conceptual view.

Example: Suppose a college database adds a new column called `Email` to its student table. Existing student-facing views that do not use this column can remain unchanged.

The logical structure has changed, but the unaffected user views do not necessarily need to change.

Important points from the PPT:

* It concerns changes to the conceptual schema.

* The external schema should not need to change.

* It separates the external level from the conceptual level.

* The PPT associates it with the user interface level.

### 6.4 Physical Data Independence

Definition: Physical data independence is the ability to change the internal schema without having to change the conceptual schema.

The PPT explains that it separates the conceptual level from the internal level.

Example: Suppose a database administrator changes the way records are stored or increases the storage capacity of the database server. The logical tables and relationships can remain unchanged.

Important points from the PPT:

* It concerns changes to the internal schema.

* The conceptual schema should not need to change.

* It separates the conceptual level from the internal level.

* The PPT associates it with the logical interface level.

### 6.5 Logical vs. physical data independence

| Basis                        | Logical data independence                                 | Physical data independence                                    |
| ---------------------------- | --------------------------------------------------------- | ------------------------------------------------------------- |
| Schema that changes          | Conceptual schema                                         | Internal schema                                               |
| Schema protected from change | External schema                                           | Conceptual schema                                             |
| Separation                   | External and conceptual levels                            | Conceptual and internal levels                                |
| Example                      | Adding a database field without changing unaffected views | Changing storage organization without changing logical tables |

Memory trick:

* Logical: Conceptual changes should not force external changes.

* Physical: Internal changes should not force conceptual changes.

Important exam question: Differentiate between logical and physical data independence with examples.

## 7. Mappings

Slides 16–19 explain mappings between database levels.

### 7.1 Definition

Mapping is the process of converting a request and its result from one level of the database architecture to another.

A mapping defines the correspondence between the three levels.

According to the PPT:

* Mapping descriptions are stored in the data dictionary.

* The DBMS is responsible for performing mappings between the relevant schemas.

* There are two types of mapping.

The two types are:

1. External–Conceptual Mapping

2. Conceptual–Internal Mapping

### 7.2 External–Conceptual Mapping

Definition: External–conceptual mapping defines the correspondence between a particular external view and the conceptual view.

In simple words, it tells the DBMS which parts of the overall logical database correspond to the information requested through a particular user view.

Example: A student portal requests a student's name and marks. The mapping connects the student portal's view to the relevant data structures in the conceptual schema.

The student does not need to see every table in the database.

The PPT states that if the external view or conceptual view changes, the mapping must be changed accordingly.

### 7.3 Conceptual–Internal Mapping

Definition: Conceptual–internal mapping defines the correspondence between the conceptual view and the internal view, where the database is physically stored.

In simple words, it tells the DBMS how logical database records are represented in physical storage.

Example: A logical `STUDENT` table may be stored using particular files, pages, blocks, and indexes. The mapping connects the logical representation to the physical representation.

The PPT explains that:

* If the stored database structure changes, the mapping must be updated.

* The updated mapping must be saved accordingly.

* The DBA is responsible for managing such changes and helping protect the data from damage.

### 7.4 Comparison of mappings

| Basis        | External–Conceptual                                     | Conceptual–Internal                                           |
| ------------ | ------------------------------------------------------- | ------------------------------------------------------------- |
| Connects     | External and conceptual levels                          | Conceptual and internal levels                                |
| Main purpose | Relates a user view to the logical database             | Relates the logical database to physical storage              |
| Example      | Student portal view mapped to student records           | Logical records mapped to disk storage                        |
| When updated | When relevant external or conceptual definitions change | When the physical representation or related structure changes |

### 7.5 Complete mapping flow

```
        USER REQUEST
             |
             v
      EXTERNAL LEVEL
        User's view
             |
             | External–Conceptual Mapping
             v
     CONCEPTUAL LEVEL
      Logical database
             |
             | Conceptual–Internal Mapping
             v
       INTERNAL LEVEL
      Physical storage
```





## 8. Data Models

Slides 20–26 cover data models and the main data-model types.

### 8.1 Definition of a Data Model

According to slide 20, a data model is a collection of conceptual tools for describing:

1. Data

2. Data relationships

3. Data semantics

4. Consistency constraints

Let's understand each component.

* Data: The facts stored in a database, such as student IDs, names, and marks.

* Data relationships: The connections between different data items. For example, a student enrolls in a course.

* Data semantics: The meaning of the data. For example, `Marks = 85` represents a student's marks, not their age.

* Consistency constraints: Rules that keep data valid and consistent. For example, a student ID may be required to be unique.

### 8.2 Types of Data Models

Slide 21 states that data models can be logical data models or physical data models. It lists the following model names:

* Hierarchical Model

* Object-based Logical Data Model

* Entity-Relationship Data Model

* Object-Oriented Data Model

* Relational Model

* Network Model

* Physical Data Model

The slide lists Hierarchical Model twice. I'll preserve that observation rather than treating the duplicate as a separate model type.

The following explanations use the model names listed in the PPT, with standard DBMS examples to make the diagrams easier to understand.

## 9. Hierarchical Model

![Database Models: Different Types and Structures Explained](https://images.openai.com/static-rsc-4/GDSUilpxiUOYHISPehI9jCJrcVP_MZBO8NPWGzKTu4MgM7YD-cDLfzqrKJ0OsIrPGJdnfK2VJoL6DArVVIeq06nbM_pq0yhsG-Lq5-CEsUL4ZRtxlTO3m-gAEPGIPbYi55FkKiU1wNH4C_75Oxzf9UdF4JDtGJDuklhn6Qs2fe0?purpose=inline)

Add to Favorites

Definition: The hierarchical model organizes data in a tree-like structure using parent–child relationships.

### Main characteristics

* Data is arranged in a hierarchy.

* A parent record can have multiple child records.

* Each child record generally has one parent in the classic hierarchical model.

* The structure begins with a root record.

### Example

A college has several departments, and each department has several students.

```
             COLLEGE
                |
       ┌────────┴────────┐
       |                 |
   Computer            Civil
   Department         Department
       |                 |
    Students           Students
```

The college is the root, departments are children of the college, and students are children of departments.

### Advantages

* Simple to understand for naturally hierarchical data.

* Parent–child relationships are easy to represent.

* Data can be accessed efficiently when the required path is known.

### Limitations

* Many-to-many relationships are difficult to represent naturally.

* Structural changes can require changes to how data is accessed.

* The hierarchy can become restrictive when relationships are complex.

Exam point: The hierarchical model is associated with a tree structure and parent–child relationships.

## 10. Network Model

![Database Models: Different Types and Structures Explained](https://images.openai.com/static-rsc-4/j5JTVHePZNb9ElIlruV0KDi5HpYesZXJWxf47KA1Tm2I45kYvO8h9yAme1JYzAlvxnT3tg5IMugpLml4EFHlSbCh_maRoE_n1udXfLcKmlWoJDhvqhwQAdkXykUJS8CgCOOxPQftv7QjoOkGbFrfTz4_M3hN8QujqHBmsdtwVYY?purpose=inline)

Add to Favorites

Definition: The network model organizes records into a network of interconnected relationships, allowing a record to be connected to multiple other records.

### Main characteristics

* Data is represented as records connected through links.

* A record can have multiple parent records.

* It can represent more complex relationships than a simple hierarchy.

* The structure resembles a graph rather than a single tree.

### Example

A student can enroll in multiple courses, and each course can have multiple students.

```
       STUDENT A ───── COURSE X
           |               |
           |               |
       COURSE Y ───── STUDENT B
```

The diagram illustrates multiple connections between students and courses. It is conceptual rather than a formal network-schema notation.

### Advantages

* Supports complex relationships.

* Represents many-to-many relationships more naturally than a simple hierarchy.

* Can provide efficient navigation through predefined links.

### Limitations

* The structure can be complex to design and maintain.

* Applications may depend heavily on the paths used to access records.

Exam point: The network model supports interconnected records and allows a record to have multiple parents.

## 11. Entity–Relationship (ER) Model

![Entity Relationship Diagram ( ERD ) | Explained ER Model In DBMS](https://images.openai.com/static-rsc-4/RrWhXm-M63Y5v5TzdYlE_fjugPkLccCVpyMIKu6Lb_cituB4UFWIKW3s_a1PDx4Vtw4YF6XfduRwwS6nKZ6sPAC9nCeR-IBvhpI6eMXM5fBq43AOM1vNBRlbdB9rq7pdYbK7p4pfrJ4Fvr1Q3y4VZJlTut2sok0cf26CefhPuY8?purpose=inline)

Add to Favorites

Definition: The Entity–Relationship model represents data using entities, attributes, and relationships.

It is commonly used during conceptual database design.

### Main components

1. Entity: A distinguishable real-world object or concept.

Examples: `STUDENT`, `COURSE`, `FACULTY`.

2. Attribute: A property describing an entity.

For a student, attributes may include Student_ID, Name, and Semester.

3. Relationship: An association between entities.

Example: A student enrolls in a course.

### Example diagram

```
┌──────────────┐       ENROLLS       ┌──────────────┐
│   STUDENT    │─────────────────────│    COURSE    │
├──────────────┤                     ├──────────────┤
│ Student_ID   │                     │ Course_ID    │
│ Name         │                     │ Course_Name  │
└──────────────┘                     └──────────────┘
```

Here, `STUDENT` and `COURSE` are entities, their listed properties are attributes, and `ENROLLS` is the relationship.

### Uses

* Planning a database before creating tables.

* Identifying entities and their attributes.

* Understanding relationships among entities.

* Communicating database requirements clearly.

Exam point: Remember Entity + Attribute + Relationship. The ER model is primarily a conceptual design tool.

## 12. Relational Model

![Unleashing the Power of Document-based Databases: Flexibility, Scalability, and Beyond](https://images.openai.com/static-rsc-4/x1DwHbscU7p9VzQSpQxVigZBpwkiGKNJqeYxeGMqQ-1hC2u9SD8K4K469kS84RX06py0t4-vmjD_0eAlsN0uRcjj0sFIoK8K-Ju-pnNxe-E8yiwufGk-hAVvlzA4GTyzKOS-qsjxGfaKPRYUMKrYEpHra6fMAntrvs3A-uH_jUA?purpose=inline)

Add to Favorites

Definition: The relational model represents data in the form of relations, commonly displayed as tables consisting of rows and columns.

### Main characteristics

* A relation is represented as a table.

* A row represents a record or tuple.

* A column represents an attribute.

* A primary key uniquely identifies a row.

* A foreign key can establish a relationship between tables.

### Example

STUDENT table

| Student_ID | Name | Department_ID |
| ---------- | ---- | ------------- |
| 101        | Amit | 10            |
| 102        | Neha | 20            |
| 103        | Ravi | 10            |

DEPARTMENT table

| Department_ID | Department_Name |
| ------------- | --------------- |
| 10            | Computer        |
| 20            | Civil           |

Here, `Student_ID` can be the primary key of `STUDENT`, while `Department_ID` connects student records to the relevant department.

### Advantages

* Tables are easy to understand.

* Relationships can be represented using keys.

* Data can be queried and combined using relational operations.

* Integrity constraints can help maintain valid data.

### Limitations

* Complex relationships may require several related tables and joins.

* Poor database design can introduce redundancy or update anomalies.

Exam point: The relational model represents data using tables, rows, columns, and keys.

## 13. Object-Oriented Data Model

![What is Object Oriented Model in DBMS? - Scaler Topics](https://images.openai.com/static-rsc-4/qhC-PBXmkFWZOx7X3XTLX6tx6wTk_VmWUZ-Q9_WfCyMl5Y5NFcFIPG_svDS5e2p4DJuO4Yz4EME9M9cSy9FvfHvcx2gMPkp1H5Dj4YaKufPRsAyon8Tf-GyZ53vYuKsRKG-XRKPpP9VprQxo0pls0i843r9CA-PfulEl45FWnxw?purpose=inline)

Add to Favorites

Definition: The object-oriented data model represents data as objects that combine data and associated operations.

It draws concepts from object-oriented programming.

### Main characteristics

* Objects: Represent individual entities.

* Attributes: Describe an object's properties.

* Methods: Define operations associated with an object.

* Classes: Define the common structure and behavior of objects.

* Inheritance: Allows a class to derive characteristics from another class.

### Example

A `STUDENT` class might have the attributes `Student_ID` and `Name`, along with methods such as `displayDetails()`.

```
          STUDENT CLASS
       ┌──────────────────┐
       │ Attributes       │
       │ Student_ID       │
       │ Name             │
       ├──────────────────┤
       │ Methods          │
       │ displayDetails() │
       └──────────────────┘
                 |
                 v
        Student object
        ID: 101
        Name: Amit
```

The class defines the common structure; an object represents a particular student.

### Advantages

* Can represent complex objects.

* Supports object-oriented concepts such as inheritance.

* Useful for applications involving complex data, such as multimedia or engineering objects.

### Limitations

* Can require specialized database concepts and tools.

* May be less straightforward for users accustomed only to relational tables.

Exam point: The object-oriented model represents data as objects combining attributes and behavior.

## 14. Physical Data Model

Slide 21 includes the Physical Data Model in its list of model categories.

Definition: A physical data model describes how data is implemented and stored in a particular database system.

It focuses on the implementation details of data storage.

### What it describes

* Storage structures.

* Files and storage organization.

* Indexes and access paths.

* Physical implementation details of database objects.

### Example

A logical design may specify a `STUDENT` table with a `Student_ID` field. A physical design may specify the database-specific data type, index on `Student_ID`, and storage configuration.

```
Logical design                 Physical design
---------------                ----------------
STUDENT table                  Actual table definition
Student_ID                     Data type and constraints
Name                           Indexes and storage details
```

Important distinction: The PPT lists the physical data model, but it does not provide a separate detailed explanation of it. The explanation above is standard DBMS context to clarify the listed term.

## 15. Logical Data Model vs. Physical Data Model

| Basis                | Logical data model                          | Physical data model                        |
| -------------------- | ------------------------------------------- | ------------------------------------------ |
| Focus                | What data exists and how it relates         | How data is implemented and stored         |
| Main elements        | Entities, attributes, relationships, tables | Data types, indexes, storage structures    |
| DBMS-specific detail | Generally lower                             | Generally higher                           |
| Example              | A student has a Student_ID and Name         | Defining their database types and an index |

The PPT establishes that data models can be logical or physical. This comparison elaborates on that distinction using standard DBMS terminology.

## 16. Understanding the Data-Model Diagrams in the PPT

The diagrams on slides 22–26 illustrate the models visually. These are important for diagram-identification questions.

### 16.1 Hierarchical Model — Slide 22

The PPT uses a shoe-category example.

```
                 Shoes
                /     \
       Women's Shoes  Men's Shoes
          /     \       /      \
     High Heels Bellies Sports  Sneakers
                       Shoes
```

Explanation: The top-level category is the parent, and the lower-level categories are its children. The data follows a tree structure.

### 16.2 Network Model — Slide 23

The PPT shows a college connected to the CSE Department and Library, with a Student connected to both.

```
                College
                /     \
       CSE Department  Library
                \     /
                 Student
```

Explanation: The diagram illustrates interconnected relationships. Unlike a simple tree, a student can be connected to multiple higher-level entities.

### 16.3 Entity–Relationship Model — Slide 24

The PPT shows a `Teacher` entity connected to a `Department` entity through the relationship `Works for`.

The diagram also shows attributes such as:

* Teacher: `Teacher_name`, `Teacher_id`, `Mobile_no`, `Salary`, `Age`

* Department: `Dept_id`, `Dept_name`

* Relationship: `Works for`

Simplified diagram:

```
Teacher ───── Works for ───── Department
   |                              |
Teacher_name                   Dept_id
Teacher_id                     Dept_name
Mobile_no
Salary
Age
```

Explanation: The diagram represents entities, their attributes, and the relationship between them.

### 16.4 Relational Model — Slide 25

The PPT displays an `EMPLOYEE TABLE` with columns including:

* Emp_id

* Emp_name

* Job_name

* Salary

* Mobile_no

* Dep_id

* Project_id

Each row represents an employee record.

Explanation: The table stores related data in a structured format of rows and columns.

### 16.5 Object-Oriented Data Model — Slide 26

The PPT shows `Employee` and `Department` structures, each containing attributes and methods.

The Employee structure includes attributes such as name, date of birth, phone number, salary, and department ID, along with methods such as `Get_Hired` and `Change Number`.

The Department structure includes department ID and department name, with a `Change Department` method.

Explanation: Unlike a simple table representation, this diagram groups an object's data and its associated operations.

## 17. Types of Database Systems

Slides 27–30 present four database-system types:

1. Centralized Database

2. Parallel Database System

3. Client/Server Database System

4. Distributed Database System

These slides primarily use diagrams, so the following explanations interpret the structures shown.

## 17.1 Centralized Database

![แบบฝึกหัดที่ 4 เรื่องข้อมูลและสารสนเทศ | yuwadee333](https://images.openai.com/static-rsc-4/NL9wGgMb2kphgdzz1rrklElRo-kOj5UosZ8HmTg-cvb33PhbnnuR0JdTpUuZlTCri51kAr1-fk1J0ARCcxa3MoB_JDmllOzuJb3dpZZ3lCUT8SKhLst290I1X4rGTU2aRqPqYOYQPDNIaqn7b2mKgG_HbZ2-v70I7czCNbg4N2Y?purpose=inline)

Add to Favorites

Definition: A centralized database system stores and manages the database at a central location.

### Diagram explanation — Slide 27

The PPT shows:

* A central site in Chicago.

* Remote sites in San Francisco, New York, Los Angeles, and Atlanta.

* A communication network connecting these sites to the central location.

  San Francisco ──┐
  New York ───────┤
  Los Angeles ────┼── Communication Network ── Central Site
  Atlanta ────────┘                              (Database)

The central site is responsible for the main database storage and management.

### Characteristics

* Database management is concentrated at a central location.

* Other locations communicate with the central system.

* Administration and control can be coordinated centrally.

### Advantages

* Centralized administration.

* Easier enforcement of consistent rules.

* Reduced duplication of the main database.

### Limitations

* A central failure can interrupt access for connected sites.

* Remote access depends on communication links.

* The central server may become a performance bottleneck.

Exam point: Identify the central database location and the remote sites connected through the communication network.

## 17.2 Parallel Database System

![PPT - CGS 2545: Database Concepts Spring 2012 Distributed Database Management Systems PowerPoint Presentation - ID:5622175](https://images.openai.com/static-rsc-4/qqxRJ27SCnZmS6LVl1LXif0VAdenL5b-GffdGIBfolLsAMQl8fWfgDgnPRJzcCMowwz4NsVnkqdMHQSsnZRTaIqnpdXlapUBLxBECBm8VOXRT1vDN3V5Y4QbO12uOFgRgwa_GT-cef8_Kmh9vvThvbcPUe8yB29bKCE7mbyiAWM?purpose=inline)

Add to Favorites

Definition: A parallel database system uses multiple processors or processing units to execute database operations in parallel.

### Diagram explanation — Slide 28

The PPT shows multiple processors connected through a data bus to memory and several storage devices.

```
 Processor 1 ──┐
 Processor 2 ──┼── Data Bus ── Memory
 Processor 3 ──┘       |
                       ├── Storage Disk
                       └── Storage Disk
```

This is a simplified representation of the diagram; exact sharing arrangements depend on the system architecture.

### Characteristics

* Multiple processors can work on database tasks.

* Work can be divided into smaller operations.

* Processing and data access may occur concurrently.

### Advantages

* Can improve query-processing speed.

* Can handle large workloads efficiently.

* Can increase processing capacity.

### Limitations

* Coordination between processors adds complexity.

* Resource contention may affect performance.

* Parallel execution requires suitable database and hardware design.

Exam point: The key idea is multiple processors working together.

## 17.3 Client/Server Database System

![PPT - IS 4420 Database Fundamentals Chapter 9: The Client/Server Database Environment Leon Chen PowerPoint Presentation - ID:6775011](https://images.openai.com/static-rsc-4/QW4vCviLIrl5ysWspyffciK3QDmRtCfwC6xFj43xKfI-oO249yRx_TFEoLLgj65hhEZhnhxCeXCTblJHLWf9PJsfWwShMKFuNwR738TgYcesBnvh_9WgmsNW8Xtmj9IEME9M9cSy9FvfHvcx2gMPkp1H5Dj4YaKufPRsAyon8Tf?purpose=inline)

Add to Favorites

Definition: A client/server database system separates client applications, which request services, from a server that provides database services.

### Diagram explanation — Slide 29

The PPT shows several clients connected through a network to a server.

```
 Client 1 ──┐
 Client 2 ──┤
 Client 3 ──┼──── Network ──── Database Server
 Client 4 ──┘
```

### Main components

Client: Sends database requests and presents results to the user.

Server: Processes database requests, manages stored data, and returns results.

Network: Carries requests and responses between clients and the server.

### Example

A college management application runs on multiple computers. Each computer sends requests to a common database server to retrieve student information.

### Advantages

* Multiple clients can access shared database services.

* Database administration can be centralized on the server.

* Client applications can have different user interfaces.

### Limitations

* Server failure can affect connected clients.

* Network problems can prevent access.

* Heavy request loads can overload the server.

Exam point: Remember the basic request–response relationship: Client → Network → Server → Result to client.

## 17.4 Distributed Database System

![12.3 Components of a Distributed Database System - Databases Illuminated, 4th Edition \[Book\]](https://images.openai.com/static-rsc-4/4ZtGQsq4IOgcEx1ZkKPWiZPp5Hq7HMmHx5jhFegN6hLRtxi7NrzCt4o4lbD5Oj4Achb2Nvfvdj_UQDvDUxFShoWWbHougyHjr0tFz3E38fX8e0bnTUpya-P0mXW-nI5ZIVfcNArVjSszB-4ZdtK_Bt1JBiJDQ-cKCc-wLvrCESw?purpose=inline)

Add to Favorites

Definition: A distributed database system consists of a logically related database whose data is stored across multiple interconnected sites.

### Diagram explanation — Slide 30

The PPT shows three sites — A, B, and C — connected through a network.

* Site A contains local data.

* Site B contains local data.

* Site C contains local data.

* The network supports communication between sites.

  ```
     ┌───────────┐
     │  Site A   │
     └─────┬─────┘
           |
      ┌────┴────┐
      │ Network │
      └───┬───┬─┘
          |   |
    ┌─────┘   └─────┐
    |               |
  ```

  ┌────▼─────┐    ┌────▼─────┐
  │  Site B  │    │  Site C  │
  └──────────┘    └──────────┘

### Characteristics

* Data is stored at multiple sites.

* Sites communicate through a network.

* Users or applications may access data located at different sites.

* The system coordinates operations across the participating locations.

### Advantages

* Data can be located closer to the users or applications that need it.

* Workload can be spread across multiple sites.

* A well-designed system may continue some operations when an individual site is unavailable.

### Limitations

* Coordination across sites is more complex.

* Network failures can affect remote access.

* Maintaining consistency and security across sites requires care.

Exam point: A distributed database has multiple network-connected sites containing parts of a logically related database. It is not simply a collection of unrelated databases.

## 18. Comparison of the Four Database Systems

| Basis         | Centralized                           | Parallel                             | Client/Server                                  | Distributed                                         |
| ------------- | ------------------------------------- | ------------------------------------ | ---------------------------------------------- | --------------------------------------------------- |
| Main idea     | Central database location             | Multiple processors work in parallel | Clients request server services                | Database data exists across multiple sites          |
| Primary focus | Centralized storage and control       | Processing performance               | Service architecture                           | Data distribution                                   |
| Key component | Central site                          | Multiple processors                  | Clients and server                             | Multiple networked sites                            |
| Network role  | Connects remote sites to central site | Depends on implementation            | Connects clients to server                     | Connects database sites                             |
| Example       | Central college database              | Parallel query processing            | Multiple college computers using one DB server | Regional branches maintaining data at several sites |

Important difference: Parallel and distributed systems are not synonymous. Parallel databases emphasize concurrent processing, while distributed databases emphasize data and database services across multiple sites.

## 19. Structure Components and Functions of DBMS — PPT Coverage Check

The syllabus on slide 2 includes “Structure Components, and Functions of DBMS.” However, the extracted text from the remaining slides does not provide a dedicated section with component names, a component diagram, or a detailed list of DBMS functions.

To avoid inventing PPT content, I am marking this syllabus item as requiring verification against the original slide visuals or a more detailed copy of that section.

For general understanding only, standard DBMS components often include the query processor, storage manager, transaction manager, and database storage. These are additional standard DBMS knowledge, not a verified list from this PPT.

# Chapter Summary

* A schema describes database structure; a sub-schema describes the portion relevant to an application; an instance represents the data at a particular time.

* ANSI/SPARC architecture contains the external, conceptual, and internal levels.

* Three-tier architecture has advantages such as scalability and security, as well as potential complexity and network overhead.

* Data independence is classified into logical and physical data independence.

* Mappings connect the external, conceptual, and internal schemas.

* A data model describes data, relationships, semantics, and consistency constraints.

* The PPT covers hierarchical, network, ER, relational, object-oriented, and physical data models.

* The four database-system types shown are centralized, parallel, client/server, and distributed.

# Important Definitions

| Term                    | Definition                                                                                    |
| ----------------------- | --------------------------------------------------------------------------------------------- |
| Schema                  | Logical configuration of all or part of a relational database                                 |
| Sub-schema              | Logical description of the database section relevant to an application                        |
| Instance                | Data stored in a database at a particular moment                                              |
| ANSI/SPARC architecture | Three-level framework for describing database structure                                       |
| Internal level          | Level describing physical storage                                                             |
| Conceptual level        | Level describing the logical structure of the entire database                                 |
| External level          | Level describing user-specific views                                                          |
| Data independence       | Ability to change a schema at one level without requiring a change at the next higher level   |
| Mapping                 | Correspondence between schemas at different levels                                            |
| Data model              | Collection of conceptual tools for describing data, relationships, semantics, and constraints |
| Hierarchical model      | Data model organized as a tree                                                                |
| Network model           | Data model using interconnected records                                                       |
| ER model                | Model using entities, attributes, and relationships                                           |
| Relational model        | Model representing data using tables                                                          |
| Object-oriented model   | Model representing data using objects and their associated behavior                           |
| Centralized database    | Database managed at a central location                                                        |
| Parallel database       | Database system using parallel processing                                                     |
| Client/server database  | System separating client requests from server services                                        |
| Distributed database    | Logically related database distributed across multiple sites                                  |

# Important Differences

## Logical vs. Physical Data Independence

* Logical: Changes to the conceptual schema should not require changes to external schemas.

* Physical: Changes to the internal schema should not require changes to the conceptual schema.

## Hierarchical vs. Network Model

* Hierarchical: Tree structure, with a parent–child organization.

* Network: Interconnected records that can have multiple parents.

## ER vs. Relational Model

* ER: Conceptual representation through entities, attributes, and relationships.

* Relational: Table-based representation through rows, columns, and keys.

## Centralized vs. Distributed Database

* Centralized: Main database storage is at a central location.

* Distributed: Database data is maintained across multiple sites.

## Parallel vs. Distributed Database

* Parallel: Focuses on executing database tasks using multiple processors.

* Distributed: Focuses on storing and managing related data across networked sites.

# Important Exam Points

1. Learn the three ANSI/SPARC levels and their alternative names.

2. Remember the exact definitions of schema, sub-schema, and instance.

3. Understand both types of data independence and the schemas involved.

4. Learn the names and purposes of both mappings.

5. Remember the four elements described by a data model.

6. Practise identifying the hierarchical, network, ER, relational, and object-oriented diagrams.

7. Revise the five advantages and four disadvantages listed for three-tier architecture.

8. Distinguish centralized, parallel, client/server, and distributed database systems.

9. Note that the syllabus mentions DBMS structure, components, and functions, but the extracted slide text does not establish a detailed treatment of them.





# STEP 2 — Complete DBMS Chapter 2 Mind Map

Chapter: Database Architecture

This text-based mind map covers the topics explained so far, including the schema levels, mappings, data models, database-system types, and the syllabus item on DBMS structure and functions.

```
DBMS CHAPTER 2 — DATABASE ARCHITECTURE
│
├── 1. SCHEMAS, SUB-SCHEMAS AND INSTANCES
│   │
│   ├── Schema
│   │   ├── Logical database structure
│   │   └── Tables, columns and relationships
│   │
│   ├── Sub-schema
│   │   ├── Relevant portion of database
│   │   ├── Application-specific view
│   │   └── Different views for different users
│   │
│   └── Instance
│       ├── Actual stored data at a particular time
│       └── Changes when data is inserted, updated or deleted
│
├── 2. THREE-LEVEL ANSI/SPARC ARCHITECTURE
│   │
│   ├── External Level
│   │   ├── View level
│   │   ├── External schema / view schema
│   │   ├── User-specific views
│   │   └── User interaction
│   │
│   ├── Conceptual Level
│   │   ├── Logical level
│   │   ├── Conceptual schema
│   │   ├── Overall logical database structure
│   │   └── Data and relationships
│   │
│   └── Internal Level
│       ├── Physical level
│       ├── Internal schema / physical schema
│       ├── Physical data model
│       └── Storage organization
│
├── 3. THREE-TIER ARCHITECTURE
│   │
│   ├── Advantages
│   │   ├── Scalability
│   │   ├── Performance
│   │   ├── Easy maintenance and modification
│   │   ├── Improved data integrity
│   │   └── Improved security
│   │
│   └── Disadvantages
│       ├── More complexity
│       ├── Separate proxy server requirement (as listed in PPT)
│       ├── Increased complexity / effort
│       └── Increased network traffic
│
├── 4. DATA INDEPENDENCE
│   │
│   ├── Logical Data Independence
│   │   ├── Change conceptual schema
│   │   ├── External schema remains unaffected
│   │   └── External–conceptual separation
│   │
│   └── Physical Data Independence
│       ├── Change internal schema
│       ├── Conceptual schema remains unaffected
│       └── Conceptual–internal separation
│
├── 5. MAPPINGS
│   │
│   ├── Purpose
│   │   ├── Correspondence between schemas
│   │   ├── Request and result translation
│   │   ├── Descriptions stored in data dictionary
│   │   └── DBMS performs mappings
│   │
│   ├── External–Conceptual Mapping
│   │   ├── External view ↔ conceptual view
│   │   └── Connects user view to logical database
│   │
│   └── Conceptual–Internal Mapping
│       ├── Conceptual view ↔ internal view
│       └── Connects logical data to physical storage
│
├── 6. DATA MODELS
│   │
│   ├── Definition / Purpose
│   │   ├── Data
│   │   ├── Data relationships
│   │   ├── Data semantics
│   │   └── Consistency constraints
│   │
│   ├── Hierarchical Model
│   │   ├── Tree structure
│   │   ├── Root
│   │   ├── Parent–child relationships
│   │   └── PPT example: shoe categories
│   │
│   ├── Network Model
│   │   ├── Interconnected records
│   │   ├── Multiple parents possible
│   │   └── PPT example: college, CSE,
│   │       library and student
│   │
│   ├── Entity–Relationship Model
│   │   ├── Entities
│   │   ├── Attributes
│   │   ├── Relationships
│   │   └── PPT example: Teacher and Department
│   │       └── Works for
│   │
│   ├── Relational Model
│   │   ├── Tables / relations
│   │   ├── Rows / tuples
│   │   ├── Columns / attributes
│   │   ├── Primary key
│   │   └── Foreign key
│   │       └── PPT example: Employee table
│   │
│   ├── Object-Oriented Data Model
│   │   ├── Objects
│   │   ├── Classes
│   │   ├── Attributes
│   │   ├── Methods
│   │   ├── Inheritance
│   │   └── PPT example: Employee and Department
│   │
│   └── Physical Data Model
│       ├── Physical implementation
│       ├── Storage structures
│       ├── Data types
│       └── Indexes and access paths
│
├── 7. TYPES OF DATABASE SYSTEMS
│   │
│   ├── Centralized Database
│   │   ├── Central site
│   │   ├── Remote sites
│   │   └── Communication network
│   │       └── PPT example: Chicago and remote sites
│   │
│   ├── Parallel Database System
│   │   ├── Multiple processors
│   │   ├── Data bus
│   │   ├── Memory
│   │   └── Storage devices
│   │
│   ├── Client/Server Database System
│   │   ├── Clients
│   │   ├── Database server
│   │   ├── Network
│   │   └── Requests and responses
│   │
│   └── Distributed Database System
│       ├── Multiple sites
│       ├── Network connections
│       ├── Local data
│       └── Coordination between sites
│
└── 8. STRUCTURE, COMPONENTS AND FUNCTIONS OF DBMS
    │
    ├── Listed in the chapter syllabus
    └── Detailed component list / explanation
        └── Requires verification from the PPT
```

## Quick revision: the most important connections

3 Levels

External → Conceptual → Internal

User view → Logical structure → Physical storage

2 Types

Logical vs. Physical Data Independence

Conceptual changes should not force external changes; internal changes should not force conceptual changes.

2 Mappings

External–Conceptual and Conceptual–Internal

These connect the three schema levels.

4 Systems

Centralized, Parallel, Client/Server, Distributed

Remember the primary distinction between storage location, processing, service architecture, and distribution.

STEP 2 completed — Complete Text-Based Mind Map.

Next is STEP 3 — Mind Map Image, followed by STEP 4, the comprehensive MCQ bank. The DBMS component/function section will remain flagged for verification rather than being presented as though it were fully explained in the PPT.






<img src="Database Architecture Study Mind Map.png"></img>




# DBMS Chapter 2 — MCQ Question Bank

## MCQs 26–50

Continuing with the next batch, covering mappings, data models, and types of database systems.

### Topic E — Mappings (continued)

26. Which mapping connects the conceptual level with the internal level?

A. External–conceptual mapping B. Conceptual–internal mapping C. External–internal mapping D. Client–server mapping

Answer: B. Conceptual–internal mapping

27. Where are descriptions of mappings stored, according to the chapter explanation?

A. Data dictionary B. Recycle bin C. Operating system desktop D. Network cable

Answer: A. Data dictionary

28. External–conceptual mapping establishes a correspondence between:

A. The external view and the conceptual view B. The conceptual view and physical storage C. Two different processors D. A client and its keyboard

Answer: A. The external view and the conceptual view

29. Conceptual–internal mapping connects:

A. User screens to application colors B. The conceptual view to internal physical storage C. Two external user views only D. A database to a printer

Answer: B. The conceptual view to internal physical storage

### Topic F — Data Models

30. What is a data model used to describe?

A. Data, data relationships, data semantics, and consistency constraints B. Only the computer’s appearance C. Only the database administrator’s duties D. Only network cables

Answer: A. Data, data relationships, data semantics, and consistency constraints

31. Which data model organizes data in a tree-like structure?

A. Relational model B. Network model C. Hierarchical model D. Object-oriented model

Answer: C. Hierarchical model

32. In a hierarchical data model, records are organized using:

A. Parent–child relationships B. Only flat tables C. Independent objects without relationships D. A single network bus

Answer: A. Parent–child relationships

33. Which example was used to illustrate the hierarchical model?

A. Employee salary table B. Shoe categories C. Teacher–Department relationship D. CPU and memory connections

Answer: B. Shoe categories

34. Which data model allows records to be interconnected, with multiple parents possible?

A. Hierarchical model B. Network model C. Relational model D. Physical model

Answer: B. Network model

35. Which example illustrates the network model in the chapter?

A. College, CSE, library, and student B. Shoe categories only C. A single employee table only D. Presentation, application, and data tiers

Answer: A. College, CSE, library, and student

36. What does ER stand for in the ER data model?

A. External Record B. Entity–Relationship C. Electronic Register D. Entity Retrieval

Answer: B. Entity–Relationship

37. Which of the following is a key concept in the ER model?

A. Entities, attributes, and relationships B. CPUs, buses, and memory only C. Clients, cables, and keyboards D. Files, folders, and desktop icons

Answer: A. Entities, attributes, and relationships

38. In the chapter’s ER example, what relationship connects Teacher and Department?

A. Manages memory B. Works for C. Stores data in D. Connects through a bus

Answer: B. Works for

39. Which data model represents data using tables or relations?

A. Hierarchical model B. Network model C. Relational model D. Object-oriented model

Answer: C. Relational model

40. In a relational table, a row is commonly called a:

A. Tuple B. Column C. Schema D. Method

Answer: A. Tuple

41. In the relational model, columns represent:

A. Tuples B. Attributes C. Database servers D. Relationships between tiers only

Answer: B. Attributes

42. Which of the following was included in the chapter’s relational-model discussion?

A. Primary keys and foreign keys B. Only parent–child tree branches C. Only processor buses D. Only object methods

Answer: A. Primary keys and foreign keys

43. Which data model represents data using objects and classes?

A. Physical model B. Hierarchical model C. Object-oriented data model D. Network model

Answer: C. Object-oriented data model

44. Which concept is associated with the object-oriented data model?

A. Inheritance B. Parent–child records only C. Data bus D. Remote-site networking only

Answer: A. Inheritance

45. Which data model focuses on physical implementation and storage structures?

A. ER model B. Physical data model C. Relational model D. Hierarchical model

Answer: B. Physical data model

### Topic G — Types of Database Systems

46. In a centralized database system, the database is maintained primarily at:

A. A central site B. Every user's keyboard C. Each application screen D. An unrelated remote device

Answer: A. A central site

47. Which of the following is associated with a parallel database system?

A. Multiple processors and a data bus B. Only one remote user view C. Only a shoe-category tree D. Only a Teacher–Department relationship

Answer: A. Multiple processors and a data bus

48. In a client/server database system, clients typically communicate with:

A. A database server over a network B. A hierarchical tree root only C. A data dictionary without a server D. A physical model diagram only

Answer: A. A database server over a network

49. Which type of database system involves multiple sites connected through a network?

A. Centralized database system B. Distributed database system C. Hierarchical data model D. Object-oriented data model

Answer: B. Distributed database system

50. Which option correctly matches the database system type with its main characteristic?

A. Centralized — data managed at a central site B. Parallel — only one processor is used C. Client/server — no network communication D. Distributed — only one site exists

Answer: A. Centralized — data managed at a central site


# DBMS Chapter 2 — MCQ Question Bank

## MCQs 51–75

This batch focuses on diagram-based concepts, comparisons, and key definitions from Database Architecture.

### Topic H — Schemas and Three-Level Architecture

51. Which of the following is an example of a database schema element?

A. Table structure B. Current CPU temperature C. Monitor brightness D. Keyboard layout

Answer: A. Table structure

52. A university student sees only their own marks through an application. Which concept best represents this user-specific view?

A. Internal level B. External level C. Physical data model D. Parallel database system

Answer: B. External level

53. Which level provides the overall logical view of the entire database?

A. External level B. Conceptual level C. Internal level D. Presentation tier

Answer: B. Conceptual level

54. Which level deals most directly with how data is organized for storage?

A. External level B. Conceptual level C. Internal level D. Application tier

Answer: C. Internal level

55. Which statement about the three-level architecture is correct?

A. All users must see the same external view. B. It separates user views, logical structure, and physical storage. C. It eliminates the need for database storage. D. It is a type of network cable.

Answer: B. It separates user views, logical structure, and physical storage.

### Topic I — Data Independence and Mappings

56. A database administrator changes the internal storage organization without changing the conceptual schema. Which concept applies?

A. Logical data independence B. Physical data independence C. Data duplication D. External schema creation

Answer: B. Physical data independence

57. A change to the conceptual schema is made without requiring changes to external schemas. This illustrates:

A. Logical data independence B. Physical data independence C. Client/server communication D. Parallel processing

Answer: A. Logical data independence

58. Which mapping links an external view to the conceptual view?

A. Conceptual–internal mapping B. External–conceptual mapping C. Client–server mapping D. Network–storage mapping

Answer: B. External–conceptual mapping

59. Which mapping relates the logical database structure to physical storage?

A. External–conceptual mapping B. Conceptual–internal mapping C. Presentation–application mapping D. User–view mapping

Answer: B. Conceptual–internal mapping

60. According to the chapter explanation, which resource stores descriptions of mappings?

A. Data dictionary B. CPU register C. Network cable D. Presentation screen

Answer: A. Data dictionary

### Topic J — Three-Tier Architecture

61. Which tier is responsible for presenting information to the user?

A. Presentation tier B. Application tier C. Data tier D. Internal level

Answer: A. Presentation tier

62. Which tier contains the database in the three-tier diagram?

A. Presentation tier B. Application tier C. Data tier D. External tier

Answer: C. Data tier

63. Which of the following is a disadvantage of three-tier architecture according to the chapter?

A. Improved security B. Increased complexity and effort C. Easier maintenance D. Improved scalability

Answer: B. Increased complexity and effort

64. Which option is listed as an advantage of three-tier architecture?

A. More complex implementation B. Increased network traffic C. Improved data integrity D. Separate proxy server requirement

Answer: C. Improved data integrity

65. Which statement best describes the relationship between tiers in the chapter’s diagram?

A. The presentation tier communicates with the application tier, which communicates with the data tier. B. The data tier must always communicate directly with the user. C. The presentation tier replaces the database. D. The three tiers are unrelated.

Answer: A. The presentation tier communicates with the application tier, which communicates with the data tier.

### Topic K — Data Models and Their Diagrams

66. Which data model is best represented by a tree with a root and parent–child branches?

A. Relational model B. Hierarchical model C. Object-oriented model D. Physical model

Answer: B. Hierarchical model

67. In the chapter’s hierarchical-model example, what appears at the top of the shoe-category diagram?

A. Student B. Shoes C. Department D. Employee

Answer: B. Shoes

68. Which model is represented by interconnected records where multiple parents may be possible?

A. Network model B. Hierarchical model C. Relational model D. Physical model

Answer: A. Network model

69. Which model uses entities, attributes, and relationships to represent data?

A. Physical model B. Entity–Relationship model C. Hierarchical model D. Parallel database system

Answer: B. Entity–Relationship model

70. In the chapter’s ER diagram, “Works for” connects which entities?

A. Employee and Student B. Teacher and Department C. College and Library D. CPU and Memory

Answer: B. Teacher and Department

71. Which of the following is associated with the relational model?

A. Tables, rows, and columns B. Only tree branches C. Multiple processors connected by a data bus D. Network sites without tables

Answer: A. Tables, rows, and columns

72. Which concept is specifically associated with an object-oriented data model?

A. Inheritance B. Central site C. Data bus D. External–conceptual mapping

Answer: A. Inheritance

73. Which data model focuses on physical implementation, storage structures, and access paths?

A. ER model B. Physical data model C. Hierarchical model D. Network model

Answer: B. Physical data model

### Topic L — Types of Database Systems

74. A database has a central site and remote sites connected to it. Which type does this represent?

A. Distributed database system B. Centralized database system C. Object-oriented data model D. Three-level architecture

Answer: B. Centralized database system

75. A database system diagram shows several processors connected through a data bus, with memory and storage devices. Which type is it?

A. Centralized database system B. Parallel database system C. Client/server database system D. Hierarchical data model

Answer: B. Parallel database system


# DBMS Chapter 2 — MCQ Question Bank

## MCQs 76–100

This batch continues with database system types, relational and object-oriented models, and mixed revision questions.

### Topic L — Types of Database Systems (continued)

76. Which type of database system uses clients that send requests to a database server over a network?

A. Hierarchical database system B. Client/server database system C. Centralized database system only D. Physical data model

Answer: B. Client/server database system

77. In a client/server database system, which component receives and processes database requests from clients?

A. Database server B. Data dictionary only C. External schema D. Presentation screen

Answer: A. Database server

78. Which of the following best describes a distributed database system?

A. A database maintained at only one central site B. A system involving multiple sites connected through a network C. A database represented only by a tree D. A system without network connections

Answer: B. A system involving multiple sites connected through a network

79. Which feature distinguishes a parallel database system in the chapter’s diagram?

A. Multiple processors connected through a data bus B. Only user-specific views C. A Teacher–Department relationship D. A single presentation tier

Answer: A. Multiple processors connected through a data bus

80. Which database system type is represented by a central site and remote sites, such as Chicago and other cities in the chapter diagram?

A. Centralized database system B. Object-oriented database model C. Hierarchical database model D. Three-level architecture

Answer: A. Centralized database system

81. Which option correctly matches a database system with its diagram?

A. Parallel — processors, data bus, memory, and storage B. Client/server — shoe-category tree C. Centralized — Teacher–Department ER diagram D. Distributed — Employee table only

Answer: A. Parallel — processors, data bus, memory, and storage

82. Which of the following is a common feature of both centralized and distributed database systems?

A. Both must use a hierarchical data model. B. Both involve database data and its management. C. Both must contain only one site. D. Both eliminate communication requirements.

Answer: B. Both involve database data and its management.

### Topic M — Relational Data Model

83. In a relational database table, what does a row represent?

A. An attribute B. A tuple or record C. A data bus D. A database tier

Answer: B. A tuple or record

84. In a relational table, what does a column represent?

A. An attribute B. A tuple C. A remote site D. An application tier

Answer: A. An attribute

85. What is the primary purpose of a primary key?

A. To identify a row uniquely B. To connect processors C. To display user-specific screens D. To define physical storage devices only

Answer: A. To identify a row uniquely

86. What is the purpose of a foreign key in the relational model?

A. To establish a reference to a key in another or related table B. To define the database’s physical location C. To represent a class method D. To create a network connection between sites

Answer: A. To establish a reference to a key in another or related table

87. Which of the following is an example of a relational data structure?

A. An Employee table containing EmpID, Name, and DeptID B. A tree containing shoe categories C. A data bus connecting processors D. A network of remote database sites

Answer: A. An Employee table containing EmpID, Name, and DeptID

### Topic N — Object-Oriented Data Model

88. Which of the following is a concept associated with an object-oriented data model?

A. Classes B. Data buses only C. Central sites only D. External–conceptual mapping only

Answer: A. Classes

89. Which option lists concepts associated with the object-oriented data model in the chapter?

A. Objects, classes, attributes, methods, and inheritance B. Rows, columns, and tuples only C. Root nodes and child nodes only D. Processors, memory, and data buses only

Answer: A. Objects, classes, attributes, methods, and inheritance

90. In the object-oriented model, what is a method?

A. An operation or behavior associated with an object or class B. A physical storage device C. A database site D. A table column only

Answer: A. An operation or behavior associated with an object or class

91. Which model was illustrated using Employee and Department, with attributes and methods?

A. Hierarchical model B. Object-oriented data model C. Network model D. Physical data model

Answer: B. Object-oriented data model

### Topic O — Mixed Chapter Revision

92. Which pair is correctly matched?

A. Schema — actual data at a particular time B. Instance — logical database structure C. Schema — logical database structure D. Sub-schema — physical processor layout

Answer: C. Schema — logical database structure

93. Which pair is correctly matched?

A. External level — user-specific views B. Conceptual level — physical storage devices only C. Internal level — user interface only D. Presentation tier — physical data model

Answer: A. External level — user-specific views

94. Which pair is incorrectly matched?

A. Hierarchical model — tree structure B. Relational model — tables C. ER model — entities and relationships D. Parallel database system — only a parent–child tree

Answer: D. Parallel database system — only a parent–child tree

95. Which concept helps separate changes in physical storage from the logical database structure?

A. Physical data independence B. Database instance C. Sub-schema D. Entity attribute

Answer: A. Physical data independence

96. Which of the following is listed as a disadvantage of three-tier architecture?

A. Improved scalability B. Improved security C. Separate proxy server requirement D. Easier maintenance

Answer: C. Separate proxy server requirement

97. Which database model uses a network-like arrangement of interconnected records?

A. Network model B. Hierarchical model C. Relational model D. Physical data model

Answer: A. Network model

98. Which database model focuses on the physical implementation of data?

A. Object-oriented model B. Physical data model C. ER model D. Relational model

Answer: B. Physical data model

99. Which statement about mappings is correct?

A. They establish correspondence between database levels. B. They are the same as database instances. C. They eliminate the need for schemas. D. They represent only database tables.

Answer: A. They establish correspondence between database levels.

100. Which option correctly lists the four database system types covered in the chapter?

A. Hierarchical, network, relational, and ER B. Centralized, parallel, client/server, and distributed C. External, conceptual, internal, and physical D. Presentation, application, data, and external

Answer: B. Centralized, parallel, client/server, and distributed


# DBMS Chapter 2 — MCQ Question Bank

## MCQs 101–125

This batch revises important definitions, architecture levels, data models, mappings, and database system types.

### Topic A — Core Definitions

101. Which term describes the logical structure of a database?

A. Instance B. Schema C. Tuple D. Method

Answer: B. Schema

102. Which term refers to a relevant portion of a database designed for a particular view or application?

A. Sub-schema B. Data bus C. Internal storage D. Tuple

Answer: A. Sub-schema

103. Which of the following can change as database records are modified?

A. Database instance B. The meaning of the term schema C. The number of ANSI/SPARC levels D. The name of the relational model

Answer: A. Database instance

104. Which of the following is NOT one of the three ANSI/SPARC levels?

A. External B. Conceptual C. Internal D. Application

Answer: D. Application

105. Which level is also known as the logical level?

A. External level B. Conceptual level C. Internal level D. Presentation tier

Answer: B. Conceptual level

### Topic B — Architecture and Data Independence

106. Which level primarily describes how data is physically organized?

A. External B. Conceptual C. Internal D. Presentation

Answer: C. Internal

107. Which concept allows a database to have different user-specific views?

A. External-level architecture B. Physical data independence only C. Parallel processing D. Centralized storage only

Answer: A. External-level architecture

108. Which type of data independence separates changes in the conceptual schema from external schemas?

A. Physical data independence B. Logical data independence C. Network independence D. Instance independence

Answer: B. Logical data independence

109. Which type of data independence separates changes in internal storage from the conceptual schema?

A. Logical data independence B. Physical data independence C. External data independence D. Application-tier independence

Answer: B. Physical data independence

110. Which of the following is a benefit of data independence?

A. Certain changes can be made at one level without requiring corresponding changes at another. B. All data must be stored in one table. C. Every user must see the same view. D. All database mappings are removed.

Answer: A. Certain changes can be made at one level without requiring corresponding changes at another.

### Topic C — Three-Tier Architecture

111. Which tier is associated with user interaction?

A. Presentation tier B. Data tier C. Internal tier D. Storage tier

Answer: A. Presentation tier

112. Which tier acts between the presentation and data tiers?

A. External tier B. Application tier C. Internal tier D. Conceptual tier

Answer: B. Application tier

113. Which tier stores or manages the database in the chapter’s three-tier diagram?

A. Presentation tier B. Application tier C. Data tier D. External level

Answer: C. Data tier

114. Which option contains only disadvantages of three-tier architecture listed in the chapter?

A. Scalability and performance B. Improved security and integrity C. More complexity, additional effort, and increased network traffic D. Easy maintenance and modification

Answer: C. More complexity, additional effort, and increased network traffic

115. Which option contains only advantages of three-tier architecture listed in the chapter?

A. Scalability, performance, easier maintenance, and improved security B. Increased network traffic and greater complexity C. Extra effort and a separate proxy server requirement D. More complexity and more network traffic

Answer: A. Scalability, performance, easier maintenance, and improved security

### Topic D — Data Models

116. Which data model represents information using a tree structure?

A. Network B. Hierarchical C. Relational D. Object-oriented

Answer: B. Hierarchical

117. Which model permits interconnected records and multiple parents?

A. Hierarchical B. Network C. Relational D. Physical

Answer: B. Network

118. Which model represents data using entities, attributes, and relationships?

A. ER model B. Physical model C. Hierarchical model D. Parallel database system

Answer: A. ER model

119. Which model represents data as relations or tables?

A. Network B. Hierarchical C. Relational D. Object-oriented

Answer: C. Relational

120. Which model includes objects, classes, methods, and inheritance?

A. Physical B. Object-oriented C. Hierarchical D. ER

Answer: B. Object-oriented

### Topic E — Database System Types

121. A database is maintained at one central site, with remote sites communicating with it. Which type is illustrated?

A. Distributed database system B. Centralized database system C. Parallel database system D. Object-oriented model

Answer: B. Centralized database system

122. Which database system diagram contains multiple processors, a data bus, memory, and storage?

A. Client/server B. Centralized C. Parallel D. Distributed

Answer: C. Parallel

123. Which database system uses a client–server arrangement?

A. Client/server database system B. Hierarchical data model C. ER model D. Physical data model

Answer: A. Client/server database system

124. Which database system involves multiple sites and network connections between them?

A. Centralized database system B. Distributed database system C. Hierarchical model D. Relational model

Answer: B. Distributed database system

125. Which of the following is a data model rather than a database system architecture type?

A. Centralized B. Parallel C. Client/server D. Relational

Answer: D. Relational

# DBMS Chapter 2 — MCQ Question Bank

## MCQs 126–150

This batch provides another revision round covering the verified topics from Database Architecture. Answers appear immediately after each question.

### Topic A — Schemas and Instances

126. Which of the following describes the structure of a database rather than its current contents?

A. Instance B. Schema C. Tuple D. Record value

Answer: B. Schema

127. If a student record is updated, which database concept normally changes?

A. Database instance B. ANSI/SPARC architecture C. Data model classification D. Number of architecture levels

Answer: A. Database instance

128. Which concept allows different users to see different portions of the same database?

A. External views B. Physical storage C. Parallel processors D. Data bus

Answer: A. External views

### Topic B — Three-Level Architecture

129. Which sequence correctly represents the three ANSI/SPARC levels from external to internal?

A. Internal → Conceptual → External B. External → Conceptual → Internal C. Conceptual → External → Internal D. External → Internal → Conceptual

Answer: B. External → Conceptual → Internal

130. Which level represents the complete logical structure of the database?

A. External B. Conceptual C. Internal D. Presentation

Answer: B. Conceptual

131. Which level is most closely related to physical storage details?

A. External B. Conceptual C. Internal D. Application

Answer: C. Internal

132. Which of the following is NOT one of the ANSI/SPARC three levels?

A. External B. Conceptual C. Internal D. Network

Answer: D. Network

### Topic C — Data Independence and Mappings

133. Changing file organization without changing the conceptual schema illustrates:

A. Logical data independence B. Physical data independence C. External mapping D. Data duplication

Answer: B. Physical data independence

134. Changing the conceptual schema without requiring corresponding changes to external schemas illustrates:

A. Physical data independence B. Logical data independence C. Parallel processing D. Centralized storage

Answer: B. Logical data independence

135. Which mapping connects the external and conceptual levels?

A. Conceptual–internal mapping B. External–conceptual mapping C. Client–server mapping D. Storage–network mapping

Answer: B. External–conceptual mapping

136. Which mapping connects the conceptual and internal levels?

A. External–conceptual mapping B. Conceptual–internal mapping C. User–application mapping D. Client–presentation mapping

Answer: B. Conceptual–internal mapping

137. According to the chapter explanation, mapping descriptions are maintained in the:

A. Data dictionary B. Keyboard C. Monitor D. Network cable

Answer: A. Data dictionary

### Topic D — Three-Tier Architecture

138. Which tier is responsible for the user interface?

A. Data tier B. Presentation tier C. Application tier D. Internal level

Answer: B. Presentation tier

139. Which tier contains the application logic in the three-tier architecture?

A. Presentation tier B. Application tier C. Data tier D. External level

Answer: B. Application tier

140. Which of the following is a disadvantage of three-tier architecture?

A. Easier maintenance B. Improved scalability C. Increased complexity D. Improved data integrity

Answer: C. Increased complexity

141. Which of the following is an advantage of three-tier architecture?

A. Increased network traffic B. Improved security C. Additional implementation effort D. Greater complexity

Answer: B. Improved security

### Topic E — Data Models

142. Which data model organizes records in a tree-like structure?

A. Relational B. Hierarchical C. Network D. Object-oriented

Answer: B. Hierarchical

143. Which model supports interconnected records with multiple-parent relationships?

A. Hierarchical B. Network C. Relational D. Physical

Answer: B. Network

144. Which model represents entities and the relationships between them?

A. ER model B. Physical model C. Hierarchical model D. Parallel architecture

Answer: A. ER model

145. In the chapter’s ER diagram, which relationship connects Teacher and Department?

A. Studies in B. Works for C. Stores in D. Connects through

Answer: B. Works for

146. Which data model represents data in tables consisting of rows and columns?

A. Network B. Hierarchical C. Relational D. Object-oriented

Answer: C. Relational

147. Which data model is associated with classes, objects, methods, and inheritance?

A. Physical B. Object-oriented C. Hierarchical D. ER

Answer: B. Object-oriented

### Topic F — Database System Architectures

148. Which database system architecture uses a central site to manage the database?

A. Distributed B. Centralized C. Parallel D. Client/server

Answer: B. Centralized

149. Which database system architecture uses multiple processors to support database operations?

A. Parallel database system B. Hierarchical data model C. ER model D. External-level architecture

Answer: A. Parallel database system

150. Which database system architecture involves multiple sites connected through a network?

A. Centralized B. Distributed C. Hierarchical D. Relational

Answer: B. Distributed

# DBMS Chapter 2 — MCQ Question Bank

## MCQs 151–175

This batch continues revising database architecture, schema levels, data models, and database system types.

### Topic A — Schema and Instance

151. Which statement about a database schema is correct?

A. It describes the database structure. B. It contains only the current values of records. C. It represents a network cable. D. It is another name for a processor.

Answer: A. It describes the database structure.

152. Which term refers to the actual data present in a database at a particular time?

A. Schema B. Instance C. Mapping D. Data model

Answer: B. Instance

153. A sub-schema represents:

A. A user-relevant view or portion of a database B. The entire physical computer C. A processor's memory D. A database network cable

Answer: A. A user-relevant view or portion of a database

### Topic B — Three-Level Architecture

154. Which level of the ANSI/SPARC architecture is closest to the end user?

A. Internal B. Conceptual C. External D. Physical

Answer: C. External

155. Which level describes the overall logical structure of a database?

A. External B. Conceptual C. Internal D. Presentation

Answer: B. Conceptual

156. Which level describes the physical organization of data?

A. External B. Conceptual C. Internal D. Application

Answer: C. Internal

157. What is the correct top-to-bottom sequence of the three levels?

A. Conceptual → Internal → External B. Internal → External → Conceptual C. External → Conceptual → Internal D. External → Internal → Conceptual

Answer: C. External → Conceptual → Internal

### Topic C — Data Independence and Mappings

158. Which type of data independence allows changes to physical storage without changing the conceptual schema?

A. Logical B. Physical C. External D. Network

Answer: B. Physical

159. Which type of data independence allows changes to the conceptual schema without requiring changes to external schemas?

A. Logical B. Physical C. Storage D. Instance

Answer: A. Logical

160. Which mapping connects external schemas to the conceptual schema?

A. Conceptual–internal B. External–conceptual C. Client–server D. Presentation–data

Answer: B. External–conceptual

161. Which mapping connects the conceptual schema to the internal schema?

A. External–conceptual B. Conceptual–internal C. External–internal D. Client–application

Answer: B. Conceptual–internal

162. Which resource contains descriptions of database mappings, according to the chapter explanation?

A. Data dictionary B. Monitor C. Keyboard D. Processor bus

Answer: A. Data dictionary

### Topic D — Three-Tier Architecture

163. Which tier is responsible for presenting information to users?

A. Data tier B. Application tier C. Presentation tier D. Internal level

Answer: C. Presentation tier

164. Which tier handles application logic between the presentation and data tiers?

A. Application tier B. External level C. Physical level D. Conceptual level

Answer: A. Application tier

165. Which of the following is an advantage of three-tier architecture?

A. Increased complexity B. Improved scalability C. Increased network traffic D. Additional implementation effort

Answer: B. Improved scalability

166. Which of the following is a disadvantage of three-tier architecture?

A. Easier maintenance B. Improved integrity C. Increased complexity D. Improved security

Answer: C. Increased complexity

### Topic E — Data Models

167. Which data model arranges data in a tree-like structure?

A. Relational B. Hierarchical C. Object-oriented D. Physical

Answer: B. Hierarchical

168. Which data model supports interconnected records and multiple-parent relationships?

A. Hierarchical B. Network C. Relational D. Physical

Answer: B. Network

169. Which model represents data using entities, attributes, and relationships?

A. ER model B. Physical model C. Hierarchical model D. Parallel system

Answer: A. ER model

170. Which data model represents information using tables?

A. Network B. Relational C. Hierarchical D. Object-oriented

Answer: B. Relational

171. Which model uses concepts such as objects, classes, methods, and inheritance?

A. Physical B. Object-oriented C. Hierarchical D. ER

Answer: B. Object-oriented

### Topic F — Database System Types

172. A database is maintained at one central location, and remote locations access it. Which system is this?

A. Distributed B. Centralized C. Parallel D. Object-oriented

Answer: B. Centralized

173. Which database system uses multiple processors to support database processing?

A. Parallel database system B. Hierarchical model C. ER model D. External-level architecture

Answer: A. Parallel database system

174. Which database system uses clients communicating with a database server?

A. Client/server database system B. Hierarchical database model C. Relational data model D. Physical data model

Answer: A. Client/server database system

175. Which database system architecture involves multiple database sites connected through a network?

A. Centralized B. Distributed C. Hierarchical D. Relational

Answer: B. Distributed


# DBMS Chapter 2 — MCQ Question Bank

## MCQs 176–200

This batch continues revision of the verified content from Database Architecture. Each question includes its answer immediately afterward.

### Topic A — Schemas and Instances

176. Which of the following describes the organization of a database rather than its current data values?

A. Instance B. Schema C. Tuple D. Record value

Answer: B. Schema

177. Which term refers to the database contents at a specific moment?

A. Schema B. Instance C. Mapping D. Data model

Answer: B. Instance

178. A user needs access to only a particular portion of a database. Which concept is most relevant?

A. Sub-schema B. Data bus C. Physical processor D. Parallel storage

Answer: A. Sub-schema

### Topic B — ANSI/SPARC Architecture

179. How many levels are present in the ANSI/SPARC three-level architecture?

A. One B. Two C. Three D. Five

Answer: C. Three

180. Which level provides user-specific views of a database?

A. Internal B. Conceptual C. External D. Physical

Answer: C. External

181. Which level represents the overall logical database structure?

A. External B. Conceptual C. Internal D. Presentation

Answer: B. Conceptual

182. Which level is concerned with the physical storage of data?

A. External B. Conceptual C. Internal D. Application

Answer: C. Internal

### Topic C — Data Independence

183. Which type of data independence permits changes to internal storage without affecting the conceptual schema?

A. Logical data independence B. Physical data independence C. External data independence D. Instance independence

Answer: B. Physical data independence

184. Which type of data independence permits conceptual schema changes without requiring changes to external schemas?

A. Logical data independence B. Physical data independence C. Network independence D. Storage independence

Answer: A. Logical data independence

185. What is the main purpose of data independence?

A. To make every user see identical data B. To separate certain changes at one database level from other levels C. To remove the need for database schemas D. To store all data on one processor

Answer: B. To separate certain changes at one database level from other levels

### Topic D — Mappings

186. Which mapping connects the external and conceptual levels?

A. Conceptual–internal mapping B. External–conceptual mapping C. Client–server mapping D. Application–data mapping

Answer: B. External–conceptual mapping

187. Which mapping connects the conceptual and internal levels?

A. External–conceptual mapping B. Conceptual–internal mapping C. External–application mapping D. Presentation–server mapping

Answer: B. Conceptual–internal mapping

188. Where are mapping descriptions maintained, according to the chapter explanation?

A. Data dictionary B. CPU register C. Keyboard memory D. Network cable

Answer: A. Data dictionary

### Topic E — Three-Tier Architecture

189. Which tier presents information to the user?

A. Presentation tier B. Application tier C. Data tier D. Internal level

Answer: A. Presentation tier

190. Which tier contains the application logic?

A. Data tier B. Application tier C. External level D. Physical level

Answer: B. Application tier

191. Which tier is responsible for storing or managing database data?

A. Presentation tier B. Application tier C. Data tier D. External level

Answer: C. Data tier

192. Which of the following is an advantage of three-tier architecture?

A. Increased network traffic B. Greater complexity C. Easier maintenance D. Additional implementation effort

Answer: C. Easier maintenance

193. Which of the following is a disadvantage of three-tier architecture?

A. Improved scalability B. Improved security C. Increased complexity D. Improved data integrity

Answer: C. Increased complexity

### Topic F — Data Models

194. Which data model represents records using a tree structure?

A. Network B. Hierarchical C. Relational D. Object-oriented

Answer: B. Hierarchical

195. Which data model represents interconnected records and can support multiple-parent relationships?

A. Hierarchical B. Network C. Physical D. Relational

Answer: B. Network

196. Which model uses entities, attributes, and relationships?

A. ER model B. Physical model C. Hierarchical model D. Parallel system

Answer: A. ER model

197. Which data model represents information using relations or tables?

A. Object-oriented B. Network C. Relational D. Hierarchical

Answer: C. Relational

198. Which model includes classes, objects, attributes, methods, and inheritance?

A. Physical B. Object-oriented C. ER D. Hierarchical

Answer: B. Object-oriented

### Topic G — Database System Types

199. Which database system type uses multiple processors, memory, and storage components to support processing?

A. Centralized B. Parallel C. Hierarchical D. Client/server only

Answer: B. Parallel

200. Which database system type involves multiple sites connected through a network?

A. Centralized B. Distributed C. Relational D. Hierarchical

Answer: B. Distributed

Progress: 200 MCQs completed.

# DBMS Chapter 2 — MCQ Question Bank

## MCQs 201–225

This batch continues your revision of Database Architecture. Each MCQ has its answer immediately below it.

### Topic A — Schemas and Instances

201. Which of the following represents the logical structure of a database?

A. Instance B. Schema C. Data bus D. Processor

Answer: B. Schema

202. The actual data stored in a database at a particular time is called:

A. Schema B. Instance C. Mapping D. Architecture

Answer: B. Instance

203. Which concept provides a particular user with a relevant portion or view of a database?

A. Sub-schema B. Physical processor C. Data bus D. Parallel storage

Answer: A. Sub-schema

### Topic B — ANSI/SPARC Architecture

204. Which level is primarily concerned with individual user views?

A. External B. Conceptual C. Internal D. Physical

Answer: A. External

205. Which level describes the overall logical structure of a database?

A. External B. Conceptual C. Internal D. Presentation

Answer: B. Conceptual

206. Which level is concerned with the physical organization of data?

A. External B. Conceptual C. Internal D. Application

Answer: C. Internal

207. Which sequence correctly lists the three levels from highest to lowest?

A. Internal → External → Conceptual B. Conceptual → Internal → External C. External → Conceptual → Internal D. External → Internal → Conceptual

Answer: C. External → Conceptual → Internal

### Topic C — Data Independence and Mappings

208. Which type of data independence allows physical storage changes without requiring changes to the conceptual schema?

A. Logical B. Physical C. External D. Network

Answer: B. Physical

209. Which type of data independence allows conceptual schema changes without requiring changes to external schemas?

A. Logical B. Physical C. Storage D. Instance

Answer: A. Logical

210. Which mapping connects the external level to the conceptual level?

A. Conceptual–internal mapping B. External–conceptual mapping C. Client–server mapping D. Presentation–data mapping

Answer: B. External–conceptual mapping

211. Which mapping connects the conceptual level to the internal level?

A. External–conceptual mapping B. Conceptual–internal mapping C. User–application mapping D. Network–client mapping

Answer: B. Conceptual–internal mapping

212. Which resource stores descriptions of database mappings according to the chapter explanation?

A. Data dictionary B. Keyboard C. Monitor D. Network cable

Answer: A. Data dictionary

### Topic D — Three-Tier Architecture

213. Which tier is responsible for the user interface?

A. Presentation tier B. Application tier C. Data tier D. Internal level

Answer: A. Presentation tier

214. Which tier contains application logic between the presentation and data tiers?

A. Presentation tier B. Application tier C. Data tier D. External level

Answer: B. Application tier

215. Which tier manages access to the database in the three-tier architecture?

A. Presentation tier B. Application tier C. Data tier D. External level

Answer: C. Data tier

216. Which of the following is an advantage of three-tier architecture?

A. Increased network traffic B. Greater implementation complexity C. Improved scalability D. Additional implementation effort

Answer: C. Improved scalability

217. Which of the following is a disadvantage of three-tier architecture?

A. Improved security B. Easier maintenance C. Increased complexity D. Improved data integrity

Answer: C. Increased complexity

### Topic E — Data Models

218. Which model represents data in a tree-like structure?

A. Relational B. Hierarchical C. Network D. Object-oriented

Answer: B. Hierarchical

219. Which model supports interconnected records and multiple-parent relationships?

A. Hierarchical B. Network C. Relational D. Physical

Answer: B. Network

220. Which data model uses entities, attributes, and relationships?

A. ER model B. Physical model C. Hierarchical model D. Parallel architecture

Answer: A. ER model

221. Which data model represents data through tables, rows, and columns?

A. Network B. Relational C. Hierarchical D. Physical

Answer: B. Relational

222. Which model uses objects, classes, methods, and inheritance?

A. Physical B. Object-oriented C. ER D. Hierarchical

Answer: B. Object-oriented

### Topic F — Database System Types

223. Which database system maintains its database at a central site?

A. Distributed B. Centralized C. Parallel D. Object-oriented

Answer: B. Centralized

224. Which database system uses multiple processors connected through a data bus in the chapter diagram?

A. Centralized B. Parallel C. Client/server D. Distributed

Answer: B. Parallel

225. Which database system architecture uses clients that communicate with a database server?

A. Client/server B. Hierarchical C. Relational D. ER

Answer: A. Client/server


# DBMS Chapter 2 — Final MCQ Batches

I’ll finish the remaining MCQs in one response so we can move on to the mark-wise question banks. The questions below continue from 226 and focus on the chapter topics already identified from your PPT. I’ll avoid inventing questions about the unverified DBMS components/functions section.

## MCQs 226–250

226. Which term refers to the logical design of a database?

A. Instance B. Schema C. Data bus D. Tuple

Answer: B. Schema

227. What is a database instance?

A. The database structure B. The data stored at a particular time C. The physical processor D. The mapping between tiers

Answer: B. The data stored at a particular time

228. Which ANSI/SPARC level provides different views for different users?

A. Internal B. Conceptual C. External D. Physical

Answer: C. External

229. Which level describes the overall logical structure of a database?

A. External B. Conceptual C. Internal D. Presentation

Answer: B. Conceptual

230. Which level is concerned with the physical storage of data?

A. External B. Conceptual C. Internal D. Application

Answer: C. Internal

231. How many levels are present in the ANSI/SPARC architecture?

A. Two B. Three C. Four D. Five

Answer: B. Three

232. Which type of data independence allows changes to physical storage without changing the conceptual schema?

A. Logical B. Physical C. External D. Network

Answer: B. Physical

233. Which type of data independence allows changes to the conceptual schema without requiring changes to external schemas?

A. Logical B. Physical C. Storage D. Instance

Answer: A. Logical

234. Which mapping connects the external and conceptual levels?

A. Conceptual–internal B. External–conceptual C. Client–server D. Application–data

Answer: B. External–conceptual

235. Which mapping connects the conceptual and internal levels?

A. External–conceptual B. Conceptual–internal C. User–application D. Client–presentation

Answer: B. Conceptual–internal

236. Where are mapping descriptions maintained, according to the chapter explanation?

A. Data dictionary B. Keyboard C. Monitor D. Processor

Answer: A. Data dictionary

237. Which tier is responsible for displaying information to users in three-tier architecture?

A. Presentation B. Application C. Data D. Internal

Answer: A. Presentation

238. Which tier handles application logic?

A. Presentation B. Application C. Data D. External

Answer: B. Application

239. Which tier is responsible for database access and data management?

A. Presentation B. Application C. Data D. External

Answer: C. Data

240. Which of the following is an advantage of three-tier architecture?

A. Increased complexity B. Increased network traffic C. Easier maintenance D. Additional implementation effort

Answer: C. Easier maintenance

241. Which is a disadvantage of three-tier architecture?

A. Improved scalability B. Improved security C. Increased complexity D. Easier modification

Answer: C. Increased complexity

242. Which data model organizes records in a tree structure?

A. Network B. Hierarchical C. Relational D. Object-oriented

Answer: B. Hierarchical

243. Which data model supports interconnected records and multiple-parent relationships?

A. Hierarchical B. Network C. Relational D. Physical

Answer: B. Network

244. Which model represents data using entities, attributes, and relationships?

A. ER model B. Physical model C. Hierarchical model D. Parallel system

Answer: A. ER model

245. Which model represents data using tables, rows, and columns?

A. Network B. Relational C. Hierarchical D. Object-oriented

Answer: B. Relational

246. Which model uses objects, classes, methods, and inheritance?

A. Physical B. Object-oriented C. ER D. Hierarchical

Answer: B. Object-oriented

247. Which model focuses on physical implementation and storage structures?

A. ER B. Physical data model C. Relational D. Hierarchical

Answer: B. Physical data model

248. Which database system maintains its database at a central site?

A. Distributed B. Centralized C. Parallel D. Client/server

Answer: B. Centralized

249. Which database system uses multiple processors, memory, and storage to support processing?

A. Centralized B. Parallel C. Hierarchical D. ER

Answer: B. Parallel

250. Which database system architecture involves multiple sites connected through a network?

A. Centralized B. Distributed C. Relational D. Hierarchical

Answer: B. Distributed

## MCQs 251–300 — Final Revision Set

### Topic A — Database Architecture and Definitions

251. Which term refers to a description of the database structure?

A. Instance B. Schema C. Tuple D. Record value

Answer: B. Schema

252. Which of the following can change frequently as database records are modified?

A. Database instance B. ANSI/SPARC level count C. Data model classification D. Database architecture definition

Answer: A. Database instance

253. Which concept represents a specific view or portion of a database?

A. Sub-schema B. Data bus C. Processor D. Physical model

Answer: A. Sub-schema

254. Which of the following is NOT one of the three ANSI/SPARC levels?

A. External B. Conceptual C. Internal D. Application

Answer: D. Application

255. Which level is also called the view level?

A. External B. Conceptual C. Internal D. Physical

Answer: A. External

256. Which level describes the overall logical database structure?

A. External B. Conceptual C. Internal D. Presentation

Answer: B. Conceptual

257. Which level describes how data is physically organized?

A. External B. Conceptual C. Internal D. Application

Answer: C. Internal

258. Which statement about the three-level architecture is correct?

A. It separates user views, logical structure, and physical storage. B. It eliminates the need for database storage. C. It contains only one level. D. It is a type of relational table.

Answer: A. It separates user views, logical structure, and physical storage.

### Topic B — Data Independence and Mappings

259. Changing a storage method without changing the conceptual schema illustrates:

A. Logical data independence B. Physical data independence C. External mapping D. Database instance creation

Answer: B. Physical data independence

260. Changing the conceptual schema without requiring changes to external schemas illustrates:

A. Logical data independence B. Physical data independence C. Parallel processing D. Database distribution

Answer: A. Logical data independence

261. Which mapping connects an external schema with the conceptual schema?

A. Conceptual–internal B. External–conceptual C. Client–server D. Presentation–application

Answer: B. External–conceptual

262. Which mapping connects the conceptual schema with the internal schema?

A. External–conceptual B. Conceptual–internal C. User–application D. Client–presentation

Answer: B. Conceptual–internal

263. Which resource maintains descriptions of mappings in the chapter explanation?

A. Data dictionary B. Keyboard C. Monitor D. Data bus

Answer: A. Data dictionary

264. What is the primary purpose of schema mappings?

A. To establish correspondence between database levels B. To delete all records C. To replace the database with a network D. To eliminate user views

Answer: A. To establish correspondence between database levels

265. Which statement best describes physical data independence?

A. Physical storage changes can be made without changing the conceptual schema. B. Every user must see the same data. C. Every database must use tables. D. External views cannot exist.

Answer: A. Physical storage changes can be made without changing the conceptual schema.

### Topic C — Three-Tier Architecture

266. Which tier is closest to the user?

A. Presentation B. Application C. Data D. Internal

Answer: A. Presentation

267. Which tier processes application logic?

A. Presentation B. Application C. Data D. External

Answer: B. Application

268. Which tier is associated with database storage and access?

A. Presentation B. Application C. Data D. External

Answer: C. Data

269. Which sequence correctly represents communication through a typical three-tier architecture?

A. Data → Presentation → Application B. Presentation → Application → Data C. Application → Data → Presentation D. Internal → External → Conceptual

Answer: B. Presentation → Application → Data

270. Which is an advantage of three-tier architecture?

A. Improved scalability B. Increased network traffic C. Greater implementation complexity D. Additional implementation effort

Answer: A. Improved scalability

271. Which is another advantage of three-tier architecture?

A. Improved maintenance B. Increased complexity C. Increased network traffic D. Extra implementation effort

Answer: A. Improved maintenance

272. Which of the following is a disadvantage of three-tier architecture?

A. Improved security B. Improved data integrity C. Increased complexity D. Easier modification

Answer: C. Increased complexity

273. Which disadvantage was specifically mentioned in the chapter explanation?

A. Increased network traffic B. Elimination of the data tier C. Inability to maintain data D. Removal of application logic

Answer: A. Increased network traffic

274. Which option includes only advantages of three-tier architecture mentioned in the chapter?

A. Scalability, performance, and easier maintenance B. Complexity, effort, and network traffic C. Network traffic, complexity, and proxy requirement D. Additional effort and complexity

Answer: A. Scalability, performance, and easier maintenance

### Topic D — Data Models

275. Which data model represents records in a tree structure?

A. Hierarchical B. Network C. Relational D. Object-oriented

Answer: A. Hierarchical

276. Which data model supports interconnected records and multiple-parent relationships?

A. Hierarchical B. Network C. Relational D. Physical

Answer: B. Network

277. Which data model represents entities, attributes, and relationships?

A. ER B. Physical C. Hierarchical D. Parallel

Answer: A. ER

278. What does ER stand for?

A. External Record B. Entity–Relationship C. Electronic Register D. Entity Retrieval

Answer: B. Entity–Relationship

279. Which data model represents data using tables?

A. Hierarchical B. Network C. Relational D. Object-oriented

Answer: C. Relational

280. What is a row in a relational table commonly called?

A. Attribute B. Tuple C. Method D. Schema

Answer: B. Tuple

281. What does a column in a relational table represent?

A. Attribute B. Tuple C. Data bus D. Database site

Answer: A. Attribute

282. Which key uniquely identifies a row in a relational table?

A. Foreign key B. Primary key C. External key D. Network key

Answer: B. Primary key

283. Which key establishes a reference to a key in another or related table?

A. Primary key B. Foreign key C. Internal key D. Schema key

Answer: B. Foreign key

284. Which model uses classes and objects to represent data?

A. Hierarchical B. Network C. Object-oriented D. Physical

Answer: C. Object-oriented

285. Which concept allows a class to inherit characteristics or behavior from another class?

A. Mapping B. Inheritance C. Tuple D. Data independence

Answer: B. Inheritance

286. In an object-oriented data model, what is a method?

A. An operation associated with an object or class B. A database row C. A physical storage device D. A remote database site

Answer: A. An operation associated with an object or class

287. Which model focuses on physical implementation and storage structures?

A. ER B. Physical data model C. Relational D. Hierarchical

Answer: B. Physical data model

### Topic E — Diagram Identification

288. A diagram shows a root node with several child branches representing shoe categories. Which model is illustrated?

A. Relational B. Hierarchical C. Object-oriented D. Physical

Answer: B. Hierarchical

289. A diagram shows interconnected college, CSE, library, and student records. Which model does it illustrate?

A. Network B. Relational C. Physical D. Three-tier

Answer: A. Network

290. A diagram connects Teacher and Department through “Works for.” Which model does it represent?

A. Hierarchical B. ER C. Parallel D. Client/server

Answer: B. ER

291. A diagram displays an Employee table with fields arranged in rows and columns. Which model is represented?

A. Network B. Relational C. Hierarchical D. Distributed

Answer: B. Relational

292. A diagram represents Employee and Department using classes, attributes, and methods. Which model is represented?

A. Object-oriented B. Hierarchical C. Network D. Centralized

Answer: A. Object-oriented

### Topic F — Database System Types

293. Which database system maintains the database primarily at a central site?

A. Centralized B. Distributed C. Parallel D. Client/server

Answer: A. Centralized

294. Which database system uses multiple processors, memory, and storage components to support processing?

A. Centralized B. Parallel C. Hierarchical D. ER

Answer: B. Parallel

295. Which database system uses clients communicating with a database server?

A. Client/server B. Hierarchical C. Relational D. Physical

Answer: A. Client/server

296. Which database system involves multiple sites connected through a network?

A. Centralized B. Distributed C. Hierarchical D. Object-oriented

Answer: B. Distributed

297. Which system type is associated with a diagram showing a central site and remote locations such as Chicago, San Francisco, New York, Los Angeles, and Atlanta?

A. Parallel B. Centralized C. Object-oriented D. Hierarchical

Answer: B. Centralized

298. Which system type is represented by processors, a data bus, memory, and storage?

A. Distributed B. Parallel C. Client/server D. Relational

Answer: B. Parallel

299. Which system type is represented by multiple sites such as A, B, and C?

A. Centralized B. Distributed C. Hierarchical D. Object-oriented

Answer: B. Distributed

300. Which option correctly lists the four database system types covered in the chapter?

A. Hierarchical, network, ER, relational B. Centralized, parallel, client/server, distributed C. External, conceptual, internal, physical D. Presentation, application, data, conceptual

Answer: B. Centralized, parallel, client/server, distributed

## MCQ section complete




# DBMS Chapter 2 — 1-Mark Questions and Answers

Topic: Database Architecture These short questions are for quick revision and cover the key definitions, concepts, differences, and diagrams from your chapter.

## Section 1: Basic Concepts

Q1. What is a database schema? Answer: A database schema is the overall logical structure or design of a database.

Q2. What is a subschema? Answer: A subschema is the part of a database schema that describes the view of a particular user or application.

Q3. What is a database instance? Answer: A database instance is the actual data stored in the database at a particular time.

Q4. What is database architecture? Answer: Database architecture describes how a database system is structured and how its components or levels interact.

Q5. What is the ANSI/SPARC architecture? Answer: It is a database architecture that divides the database into three levels: external, conceptual, and internal.

Q6. Name the three levels of ANSI/SPARC architecture. Answer: External level, conceptual level, and internal level.

Q7. Which level is also called the view level? Answer: The external level.

Q8. Which level describes the overall logical structure of a database? Answer: The conceptual level.

Q9. Which level describes how data is physically stored? Answer: The internal level.

Q10. What is a user view? Answer: A user view is the part of the database visible to a particular user.

## Section 2: Database Architecture and Data Independence

Q11. What is three-tier architecture? Answer: Three-tier architecture organizes an application into three layers: presentation, application logic, and data.

Q12. Name the three tiers of three-tier architecture. Answer: Presentation tier, application tier, and data tier.

Q13. What is the presentation tier? Answer: It is the layer through which users interact with the application.

Q14. What is the application tier? Answer: It processes application logic and user requests.

Q15. What is the data tier? Answer: It manages data storage and database operations.

Q16. State one advantage of three-tier architecture. Answer: It improves scalability.

Q17. State one disadvantage of three-tier architecture. Answer: It increases system complexity.

Q18. What is data independence? Answer: Data independence is the ability to change a database schema at one level without requiring changes at the next higher level.

Q19. Name the two types of data independence. Answer: Logical data independence and physical data independence.

Q20. What is logical data independence? Answer: It is the ability to change the conceptual schema without changing external views or application programs.

Q21. What is physical data independence? Answer: It is the ability to change the internal storage structure without changing the conceptual schema.

Q22. Which type of data independence is generally harder to achieve? Answer: Logical data independence.

Q23. What is mapping in database architecture? Answer: Mapping defines the correspondence between schemas at different levels.

Q24. Name the two mappings in the three-level database architecture. Answer: External–conceptual mapping and conceptual–internal mapping.

Q25. What does external–conceptual mapping connect? Answer: The external level and the conceptual level.

Q26. What does conceptual–internal mapping connect? Answer: The conceptual level and the internal level.

Q27. Where are schema mappings described or recorded, according to the chapter explanation? Answer: In the data dictionary.

## Section 3: Data Models

Q28. What is a data model? Answer: A data model defines how data is organized, represented, and related in a database.

Q29. What is a hierarchical data model? Answer: It organizes data in a tree-like structure with parent–child relationships.

Q30. What is a network data model? Answer: It organizes data as records connected through links, allowing more complex relationships than a simple tree.

Q31. What is an ER model? Answer: An Entity–Relationship model represents entities, their attributes, and the relationships between them.

Q32. What does ER stand for? Answer: Entity–Relationship.

Q33. What is a relational data model? Answer: It organizes data into tables consisting of rows and columns.

Q34. What is an object-oriented data model? Answer: It represents data as objects containing attributes and, where applicable, methods.

Q35. What is a physical data model? Answer: It describes how data is physically stored and organized.

Q36. Which data model organizes data in tables? Answer: The relational data model.

Q37. Which data model uses a tree-like structure? Answer: The hierarchical data model.

Q38. Which model represents entities and relationships? Answer: The ER model.

Q39. In an ER diagram, what does an entity represent? Answer: A real-world object or concept about which data is stored.

Q40. What is an attribute? Answer: An attribute is a property or characteristic of an entity.

## Section 4: Database Systems

Q41. What is a centralized database system? Answer: A database system in which the database is maintained at a central location.

Q42. What is a parallel database system? Answer: A database system that uses multiple processors or storage resources to perform database operations in parallel.

Q43. What is a client/server database system? Answer: A database system in which clients request services and a server processes requests or manages database services.

Q44. What is a distributed database system? Answer: A database system in which data is stored across multiple interconnected sites.

Q45. In a client/server system, what is a client? Answer: A computer or application that requests services from a server.

Q46. In a client/server system, what is a server? Answer: A computer or system that provides services or database resources to clients.

Q47. What is a remote site in a centralized database system? Answer: A location that accesses the database maintained at the central site.

Q48. What is the main feature of a distributed database system? Answer: Data is stored across multiple interconnected sites.

Q49. Which database system uses multiple processors to execute operations in parallel? Answer: A parallel database system.

Q50. Which database system has a central database location? Answer: A centralized database system.

## Section 5: Quick One-Line Revision

Q51. Which architecture separates the user view from physical storage? Answer: ANSI/SPARC three-level architecture.

Q52. Which level is closest to the end user? Answer: The external level.

Q53. Which level is concerned with physical storage details? Answer: The internal level.

Q54. What does scalability mean in database architecture? Answer: The ability of a system to handle growth in users, workload, or data.

Q55. What does database integrity mean? Answer: Maintaining the accuracy and consistency of data.

Q56. What is a database view? Answer: A representation of selected database information for a particular user or purpose.

Q57. What is the purpose of schema mapping? Answer: To describe how information corresponds between different schema levels.

Q58. What is the parent–child relationship associated with? Answer: The hierarchical data model.

Q59. Which model can represent objects with attributes and methods? Answer: The object-oriented data model.

Q60. What is the purpose of database architecture? Answer: To organize database components and define how data is represented, accessed, and stored.



# DBMS Chapter 2 — 2-Mark Questions and Answers

Topic: Database Architecture

These answers are written in simple, exam-friendly language. For a 2-mark question, aim to write the definition and one or two important points.

## Section 1: Basic Database Concepts

Q1. Define schema and instance.

Answer:

* Schema: The overall design or logical structure of a database.

* Instance: The actual data stored in the database at a particular time.

Q2. Differentiate between schema and subschema.

Answer:

| Schema                                    | Subschema                                      |
| ----------------------------------------- | ---------------------------------------------- |
| Describes the overall database structure. | Describes a particular user's view.            |
| Covers the database as a whole.           | Covers only the required part of the database. |

Q3. What is database architecture?

Answer: Database architecture describes the structure of a database system and the way its different levels or components interact. It helps organize how data is viewed, processed, and stored.

Q4. Explain ANSI/SPARC architecture.

Answer: ANSI/SPARC is a three-level database architecture that separates the database into:

1. External level

2. Conceptual level

3. Internal level

This separation helps provide data abstraction and data independence.

Q5. Explain the external level.

Answer: The external level describes how individual users view the database. Different users can have different views depending on their requirements.

Q6. Explain the conceptual level.

Answer: The conceptual level describes the overall logical structure of the database, including the data and relationships, without focusing on physical storage details.

Q7. Explain the internal level.

Answer: The internal level describes how data is physically stored in the database, including storage organization and access-related details.

Q8. What is the purpose of the three-level architecture?

Answer: The three-level architecture separates user views, the overall logical structure, and physical storage. This separation makes the database easier to manage and supports data independence.

## Section 2: Three-Tier Architecture

Q9. What is three-tier architecture?

Answer: Three-tier architecture divides an application into three separate layers:

1. Presentation tier: User interface.

2. Application tier: Application logic.

3. Data tier: Database storage and operations.

Q10. State any two advantages of three-tier architecture.

Answer:

1. Scalability: Each tier can be developed or scaled according to requirements.

2. Easy maintenance: Changes in one tier can often be made without major changes to the others.

Q11. State any two disadvantages of three-tier architecture.

Answer:

1. It increases system complexity.

2. Communication between tiers can introduce network overhead.

Q12. Differentiate between three-level and three-tier architecture.

Answer:

| Three-level architecture                                      | Three-tier architecture                                                 |
| ------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Describes external, conceptual, and internal database levels. | Describes presentation, application, and data tiers.                    |
| Focuses on data abstraction and independence.                 | Focuses on application organization and separation of responsibilities. |

## Section 3: Data Independence and Mapping

Q13. Define data independence.

Answer: Data independence is the ability to change a schema at one level without requiring changes at the next higher level. It reduces the impact of database modifications.

Q14. Explain logical data independence.

Answer: Logical data independence is the ability to change the conceptual schema without changing external views or application programs. For example, adding a new field to the logical database design may not require changes to every user's view.

Q15. Explain physical data independence.

Answer: Physical data independence is the ability to change the internal storage structure without changing the conceptual schema. For example, changing the storage organization should not require changing the logical database design.

Q16. Differentiate between logical and physical data independence.

Answer:

| Logical data independence                | Physical data independence                      |
| ---------------------------------------- | ----------------------------------------------- |
| Changes the conceptual schema.           | Changes the internal schema.                    |
| External views should remain unaffected. | The conceptual schema should remain unaffected. |

Q17. What is schema mapping?

Answer: Schema mapping defines the correspondence between schemas at different levels of database architecture. It helps the DBMS relate a user's view to the overall logical structure and physical storage.

Q18. Explain external–conceptual mapping.

Answer: External–conceptual mapping connects an external schema with the conceptual schema. It describes how a particular user's view corresponds to the overall logical database.

Q19. Explain conceptual–internal mapping.

Answer: Conceptual–internal mapping connects the conceptual schema with the internal schema. It describes how the logical database structure corresponds to its physical storage.

Q20. What is a data dictionary?

Answer: A data dictionary is a collection of metadata, or information about database structures. The chapter explanation identifies it as the place where schema mapping descriptions are recorded.

## Section 4: Data Models

Q21. Define a data model and state its purpose.

Answer: A data model defines how data is represented, organized, and related in a database. It provides a structured way to design and understand database information.

Q22. Explain the hierarchical data model.

Answer: The hierarchical data model organizes data in a tree-like structure. Each parent can have child records, representing parent–child relationships.

Q23. Explain the network data model.

Answer: The network data model organizes data as records connected through links. It can represent more complex relationships than a simple tree structure.

Q24. Explain the ER model.

Answer: The Entity–Relationship model represents:

* Entities: Real-world objects or concepts.

* Attributes: Properties of entities.

* Relationships: Associations between entities.

Q25. Explain the relational data model.

Answer: The relational data model stores data in tables. Each table contains rows representing records and columns representing attributes.

Q26. Explain the object-oriented data model.

Answer: The object-oriented data model represents data as objects. Objects can contain attributes and methods that describe their properties and behavior.

Q27. Explain the physical data model.

Answer: The physical data model describes how data is stored and organized at the physical level. It focuses on storage-related details rather than only the logical representation.

Q28. Differentiate between hierarchical and network data models.

Answer:

| Hierarchical model                       | Network model                                      |
| ---------------------------------------- | -------------------------------------------------- |
| Organizes data in a tree-like structure. | Organizes data using interconnected records.       |
| Represents parent–child relationships.   | Supports more complex connections between records. |

Q29. Differentiate between the ER and relational models.

Answer:

| ER model                                            | Relational model                                        |
| --------------------------------------------------- | ------------------------------------------------------- |
| Represents entities, attributes, and relationships. | Represents data using tables, rows, and columns.        |
| Commonly used for conceptual database design.       | Commonly used to organize data in relational databases. |

Q30. What are entities and attributes? Give an example.

Answer: An entity is an object about which data is stored, while an attribute is a property of that object. For example, `Student` is an entity and `Student_ID` is an attribute.

## Section 5: Database System Types

Q31. Explain a centralized database system.

Answer: A centralized database system maintains its database at one central location. Users at remote locations can access the central database through a network.

Q32. State two characteristics of a centralized database system.

Answer:

1. The database is maintained at a central site.

2. Remote users or locations can access the central database.

Q33. Explain a parallel database system.

Answer: A parallel database system uses multiple processors or storage resources to perform database operations in parallel. This can improve processing performance for suitable workloads.

Q34. Explain a client/server database system.

Answer: In a client/server database system, clients send requests to a server. The server provides database services and returns the required results.

Q35. State two roles of a client in a client/server system.

Answer:

1. It provides the user-facing application or interface.

2. It sends requests to the server and receives results.

Q36. State two roles of a server in a client/server system.

Answer:

1. It receives and processes client requests.

2. It provides database services or access to stored data.

Q37. Explain a distributed database system.

Answer: A distributed database system stores data across multiple interconnected sites. These sites communicate to support access to the distributed data.

Q38. Differentiate between centralized and distributed database systems.

Answer:

| Centralized system                            | Distributed system                                 |
| --------------------------------------------- | -------------------------------------------------- |
| Database is maintained at a central location. | Data is stored across multiple sites.              |
| Remote users access the central database.     | Multiple sites participate in the database system. |

Q39. Differentiate between parallel and distributed database systems.

Answer:

| Parallel database system                                  | Distributed database system                                 |
| --------------------------------------------------------- | ----------------------------------------------------------- |
| Uses parallel processing resources to execute operations. | Uses multiple interconnected sites to store or manage data. |
| Focuses on parallel execution.                            | Focuses on data and processing across sites.                |

Q40. What is the difference between a client and a server?

Answer: A client requests services or data, while a server provides those services or data in response to client requests.

## Section 6: Diagram-Based Questions

Q41. Name the three levels shown in the ANSI/SPARC architecture diagram.

Answer: External level, conceptual level, and internal level.

Q42. What relationship is illustrated in the Teacher–Department ER diagram?

Answer: The diagram illustrates a `Works for` relationship between the `Teacher` and `Department` entities.

Q43. What does the Employee table illustrate in the relational model?

Answer: It illustrates how employee information is represented in rows and columns.

Q44. What does the Employee–Department object-oriented diagram illustrate?

Answer: It illustrates objects with attributes and methods, representing data and behavior.

Q45. What do multiple interconnected sites represent in the distributed database diagram?

Answer: They represent a distributed database system in which data is stored or managed across multiple sites.

## Quick Revision: Most Important Differences

| Comparison                         | Key distinction                                  |
| ---------------------------------- | ------------------------------------------------ |
| Schema vs. instance                | Database design vs. actual data                  |
| External vs. conceptual level      | User-specific view vs. overall logical structure |
| Conceptual vs. internal level      | Logical structure vs. physical storage           |
| Logical vs. physical independence  | Conceptual changes vs. storage changes           |
| Hierarchical vs. network model     | Tree structure vs. interconnected records        |
| Centralized vs. distributed system | Central site vs. multiple sites                  |
| Client vs. server                  | Requests services vs. provides services          |

Completed: 45 two-mark questions and answers.

Type next to continue with the 3-mark questions and answers.


# DBMS Chapter 2 — 3-Mark Questions and Answers

Topic: Database Architecture

These answers are designed for 3-mark exam questions. Write the definition, followed by the main points or an example where appropriate.

## Section 1: Database Concepts and Architecture

Q1. Explain schema, subschema, and instance with examples.

Answer:

1. Schema: The overall design of a database. Example: a Student database containing student ID, name, and course.

2. Subschema: A specific user's view of the database. Example: a teacher's view showing student names and marks.

3. Instance: The actual data stored at a particular time. Example: a record containing student ID 101, name Rahul, and course BCA.

Q2. Explain the three levels of ANSI/SPARC architecture.

Answer:

1. External level: Describes the database view available to an individual user.

2. Conceptual level: Describes the overall logical structure of the database and its relationships.

3. Internal level: Describes how data is physically stored and accessed.

These levels separate user views from logical design and physical storage.

Q3. Explain the importance of the three-level database architecture.

Answer:

1. It separates user-specific views from the overall database structure.

2. It hides unnecessary physical storage details from users.

3. It supports data independence, making certain database changes easier to implement.

Q4. Differentiate between the external, conceptual, and internal levels.

Answer:

| Level      | Main purpose                   | Example                                 |
| ---------- | ------------------------------ | --------------------------------------- |
| External   | Provides user-specific views   | Teacher views student marks             |
| Conceptual | Describes the logical database | Student and Course entities             |
| Internal   | Describes physical storage     | Storage organization and access methods |

Q5. What is a database view? Explain its importance.

Answer: A database view is a representation of selected database information for a particular user or purpose.

Its importance includes:

1. Showing users only the information they need.

2. Simplifying interaction with the database.

3. Supporting controlled access to database information.

## Section 2: Three-Tier Architecture

Q6. Explain the three tiers of three-tier architecture with examples.

Answer:

1. Presentation tier: Provides the user interface, such as a college website.

2. Application tier: Processes the application's rules and requests, such as checking student login details.

3. Data tier: Stores and retrieves data, such as student records in a database.

These tiers separate the user interface, application processing, and data management.

Q7. Explain any three advantages of three-tier architecture.

Answer:

1. Scalability: Individual tiers can be scaled according to demand.

2. Maintainability: Changes to one tier may require fewer changes to other tiers.

3. Security and integrity: Separating application logic and database access can help control access and validate data.

Q8. Explain any three disadvantages of three-tier architecture.

Answer:

1. Complexity: Multiple tiers make the system more complicated to design and maintain.

2. Network overhead: Communication between tiers can increase response time.

3. Additional effort: Separate layers and infrastructure may require more development and administration.

Q9. Differentiate between three-level and three-tier architecture.

Answer:

| Three-level architecture                  | Three-tier architecture                             |
| ----------------------------------------- | --------------------------------------------------- |
| External, conceptual, and internal levels | Presentation, application, and data tiers           |
| Focuses on database abstraction           | Focuses on application organization                 |
| Supports data independence                | Supports separation of application responsibilities |

## Section 3: Data Independence and Mapping

Q10. Explain logical and physical data independence.

Answer:

1. Logical data independence: The conceptual schema can be changed without requiring changes to external views or application programs.

2. Physical data independence: The internal storage structure can be changed without requiring changes to the conceptual schema.

3. Both help reduce the effect of database modifications on other levels.

Q11. Why is data independence important? Give three points.

Answer:

1. It reduces the need to modify application programs when certain database changes occur.

2. It makes database maintenance easier.

3. It allows changes to database design or storage with less impact on higher levels.

Q12. Explain the two types of schema mapping.

Answer:

1. External–conceptual mapping: Connects an external user view to the conceptual schema.

2. Conceptual–internal mapping: Connects the conceptual schema to the internal storage schema.

3. These mappings describe the correspondence between the different database levels.

Q13. What is a data dictionary? Explain its role.

Answer: A data dictionary stores metadata, which is information about the database.

Its role includes:

1. Recording information about database structures.

2. Helping the DBMS manage schema-related information.

3. According to the chapter explanation, recording descriptions of schema mappings.

## Section 4: Data Models

Q14. Explain the hierarchical data model with an example.

Answer: The hierarchical data model organizes records in a tree-like structure.

1. It uses parent–child relationships.

2. Data is arranged in levels.

3. Example: a shoe catalogue with `Shoes` as the parent category and `Sports Shoes` and `Formal Shoes` as child categories.

Q15. Explain the network data model with an example.

Answer: The network data model represents records connected through links.

1. It supports interconnected records.

2. It can represent more complex relationships than a simple tree.

3. Example: a college database connecting students, departments, and library records.

Q16. Explain the Entity–Relationship model with an example.

Answer: The ER model represents entities, attributes, and relationships.

1. Entity: A real-world object, such as Teacher.

2. Attribute: A property, such as Teacher_ID.

3. Relationship: An association, such as a teacher Works for a department.

Q17. Explain the relational data model with an example.

Answer: The relational model organizes data into tables.

1. Rows represent individual records.

2. Columns represent attributes.

3. Example:

| Employee_ID | Name | Department |
| ----------- | ---- | ---------- |
| 101         | Amit | IT         |
| 102         | Neha | HR         |

Q18. Explain the object-oriented data model with an example.

Answer: The object-oriented data model represents information as objects.

1. Objects contain attributes describing their properties.

2. Objects can also contain methods describing their behavior.

3. Example: an Employee object may contain `Employee_ID` and `Name` attributes and a method such as `displayDetails()`.

Q19. Explain the physical data model.

Answer: The physical data model describes how data is stored and organized physically.

1. It focuses on storage-related details.

2. It describes how data is organized for storage and access.

3. It is concerned with physical implementation rather than only conceptual representation.

Q20. Compare hierarchical, network, and relational data models.

Answer:

| Model        | Organization           | Main feature               |
| ------------ | ---------------------- | -------------------------- |
| Hierarchical | Tree                   | Parent–child structure     |
| Network      | Interconnected records | Complex record connections |
| Relational   | Tables                 | Rows and columns           |

Q21. Differentiate between the ER model and object-oriented model.

Answer:

| ER model                                       | Object-oriented model                             |
| ---------------------------------------------- | ------------------------------------------------- |
| Uses entities, attributes, and relationships   | Uses objects, attributes, and methods             |
| Commonly represents conceptual database design | Represents data together with associated behavior |
| Example: Teacher–Department relationship       | Example: Employee object with `displayDetails()`  |

## Section 5: Database System Types

Q22. Explain a centralized database system with an example.

Answer: A centralized database system maintains its database at one central location.

1. Data is maintained at a central site.

2. Users at remote locations can access the central database.

3. Example: a company maintains its main database in Chicago and allows offices in other cities to access it.

Q23. Explain a parallel database system.

Answer: A parallel database system uses multiple processors or storage resources to execute database operations in parallel.

1. Multiple processing resources participate in operations.

2. Work can be divided among those resources.

3. Parallel execution can improve performance for suitable workloads.

Q24. Explain a client/server database system with a diagram.

Answer: In this system, clients request database services from a server.

* The client sends a request.

* The server processes the request.

* The server returns the result.

Diagram:

```
+----------+       +----------+
| Client 1 | ----> |          |
+----------+       |          |
                   |  Server  |
+----------+       |          |
| Client 2 | ----> |          |
+----------+       +----------+
```

Q25. Explain a distributed database system with an example.

Answer: A distributed database system stores or manages data across multiple interconnected sites.

1. Multiple sites participate in the database system.

2. The sites communicate through a network.

3. Example: a company database distributed across its Ahmedabad, Mumbai, and Delhi offices.

Q26. Compare centralized and distributed database systems.

Answer:

| Centralized system                                      | Distributed system                                                           |
| ------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Database is maintained at a central location.           | Data is stored across multiple sites.                                        |
| Remote users access the central database.               | Multiple sites participate in data management.                               |
| Central-site failure can affect access to the database. | Availability depends on the design and condition of the participating sites. |

Q27. Compare parallel and distributed database systems.

Answer:

| Parallel database system                        | Distributed database system                        |
| ----------------------------------------------- | -------------------------------------------------- |
| Uses multiple processing resources in parallel. | Uses multiple interconnected sites.                |
| Focuses on parallel execution of operations.    | Focuses on data and operations across sites.       |
| Can improve processing performance.             | Can support data access across multiple locations. |

Q28. Differentiate between centralized and client/server database systems.

Answer:

1. A centralized system describes where the database is maintained: at a central location.

2. A client/server system describes how clients request services from a server.

3. A centralized database may be accessed through a client/server arrangement; the concepts describe different aspects of a system.

## Section 6: Diagram-Based Questions

Q29. Explain the ANSI/SPARC architecture diagram.

Answer: The diagram represents three database levels:

```
External Level
      |
      | External–Conceptual Mapping
      v
Conceptual Level
      |
      | Conceptual–Internal Mapping
      v
Internal Level
```

1. The external level represents user views.

2. The conceptual level represents the overall logical structure.

3. The internal level represents physical storage.

Q30. Explain the Teacher–Department ER diagram.

Answer:

1. `Teacher` and `Department` are entities.

2. `Works for` represents the relationship between them.

3. Attributes describe properties of the entities, such as teacher or department details.

Q31. Explain the Employee table shown in the relational model.

Answer:

1. The Employee table represents employee information in tabular form.

2. Each row represents an employee record.

3. Each column represents an attribute, such as employee ID or name.

Q32. Explain the Employee–Department object-oriented diagram.

Answer:

1. Employee and Department are represented as objects or object types.

2. Their attributes store information about them.

3. Methods can define behavior or operations associated with the objects.

Q33. What does the parallel database system diagram illustrate?

Answer:

1. It shows multiple processing resources.

2. These resources work together on database operations.

3. The diagram illustrates parallel processing to improve execution performance.

Q34. What does the centralized database diagram illustrate?

Answer:

1. The database is maintained at a central site.

2. Remote locations connect to the central site.

3. Users at these locations can access the central database.

## Section 7: Important 3-Mark Revision Questions

Q35. List the types of data models covered in the chapter.

Answer:

1. Hierarchical data model

2. Network data model

3. Entity–Relationship (ER) model

4. Relational data model

5. Object-oriented data model

6. Physical data model

Q36. List the four advantages of three-tier architecture mentioned in the chapter explanation.

Answer:

1. Scalability

2. Improved performance

3. Easier maintenance and modification

4. Improved integrity and security

Q37. List the disadvantages of three-tier architecture mentioned in the chapter explanation.

Answer:

1. Increased system complexity

2. Additional infrastructure requirements, including a separate proxy server as described in the PPT explanation

3. Increased development or maintenance effort

4. Network traffic between tiers

Q38. State the main purpose of each database system type.

Answer:

1. Centralized: Maintains the database at a central location.

2. Parallel: Executes database operations using multiple processing resources.

3. Client/server: Provides database services through a server in response to client requests.

4. Distributed: Stores or manages data across multiple interconnected sites.

## Quick exam-writing tips

* For a definition question, write a clear definition plus one key feature.

* For a comparison question, use a small table.

* For a diagram question, draw and label the diagram, then explain its main parts.

* For data independence, remember: logical means conceptual-schema changes; physical means internal-storage changes.



# DBMS Chapter 2 — 4-Mark and 5-Mark Questions and Answers

Topic: Database Architecture

These are longer, exam-style answers for revision and final-exam preparation. Use headings, numbered points, comparison tables, and diagrams wherever appropriate.

# Part A — 4-Mark Questions and Answers

## Q1. Explain the three-level ANSI/SPARC database architecture with a diagram.

Answer:

The ANSI/SPARC architecture divides a database into three levels to separate user views, logical structure, and physical storage.

```
        +----------------------+
        |   External Level     |
        |   User Views         |
        +----------------------+
                  |
       External–Conceptual
             Mapping
                  |
        +----------------------+
        |  Conceptual Level    |
        | Overall Logical DB   |
        +----------------------+
                  |
       Conceptual–Internal
             Mapping
                  |
        +----------------------+
        |    Internal Level    |
        |  Physical Storage    |
        +----------------------+
```

1. External level: Provides individual users with their required views of the database.

2. Conceptual level: Describes the overall logical structure and relationships of the database.

3. Internal level: Describes how data is physically stored.

4. Mappings: Connect the external and conceptual levels, and the conceptual and internal levels.

Conclusion: This architecture supports data abstraction and data independence.

## Q2. Explain logical and physical data independence with examples.

Answer:

Data independence is the ability to make changes at one database level without requiring changes at the next higher level.

1. Logical data independence

* Allows changes to the conceptual schema without changing external views or application programs.

* Example: Adding a new attribute to a database may not require changes to every user's view.

2. Physical data independence

* Allows changes to the internal storage structure without changing the conceptual schema.

* Example: Changing the storage organization without changing the logical database design.

| Logical independence                    | Physical independence                      |
| --------------------------------------- | ------------------------------------------ |
| Changes the conceptual schema           | Changes the internal schema                |
| External views should remain unaffected | Conceptual schema should remain unaffected |

## Q3. Explain three-tier architecture, including its advantages and disadvantages.

Answer:

Three-tier architecture divides an application into three layers:

1. Presentation tier: Provides the interface through which users interact with the application.

2. Application tier: Processes application logic and user requests.

3. Data tier: Stores and retrieves data.

Advantages:

* Improves scalability.

* Makes maintenance and modification easier.

* Can improve security and data integrity.

* Allows tiers to be developed or scaled separately.

Disadvantages:

* Increases system complexity.

* May require additional infrastructure.

* Requires more development and maintenance effort.

* Communication between tiers can introduce network overhead.

## Q4. Explain the different types of data models.

Answer:

A data model defines how data is represented, organized, and related in a database.

1. Hierarchical model: Organizes data in a tree-like structure with parent–child relationships.

2. Network model: Organizes records through interconnected links.

3. ER model: Represents entities, attributes, and relationships.

4. Relational model: Stores data in tables containing rows and columns.

5. Object-oriented model: Represents data as objects with attributes and methods.

6. Physical model: Describes how data is physically stored and organized.

## Q5. Explain a centralized database system with its characteristics.

Answer:

A centralized database system maintains its database at one central location.

Characteristics:

1. The database is maintained at a central site.

2. Remote locations can access the central database through a network.

3. Database management is concentrated at the central site.

4. If the central site becomes unavailable, access to the database may be affected.

Example: A company maintains its main database at its Chicago office while offices in other cities access it remotely.

## Q6. Explain a parallel database system.

Answer:

A parallel database system uses multiple processors or storage resources to perform database operations in parallel.

Characteristics:

1. Multiple processing resources participate in database operations.

2. Work can be divided among processing resources.

3. Parallel execution can improve processing speed for suitable workloads.

4. The system coordinates the resources involved in processing.

Example: A database uses multiple processors to process a large query.

## Q7. Explain a client/server database system with a diagram.

Answer:

A client/server database system uses clients to request services and a server to provide them.

```
+------------+         +----------------+
|  Client 1  | ------> |                |
+------------+         |                |
                       | Database       |
+------------+         | Server         |
|  Client 2  | ------> |                |
+------------+         +----------------+
```

Working:

1. The client sends a request.

2. The server receives and processes the request.

3. The server accesses the required database information.

4. The result is returned to the client.

Example: A student accesses a college portal, which retrieves student details from a database server.

## Q8. Explain a distributed database system.

Answer:

A distributed database system stores or manages data across multiple interconnected sites.

Characteristics:

1. Multiple sites participate in the database system.

2. Sites communicate through a network.

3. Data can be stored or managed at different locations.

4. Users may access data across participating sites, depending on the system's design.

Example: A company operates database sites in Ahmedabad, Mumbai, and Delhi.

## Q9. Differentiate between centralized, parallel, client/server, and distributed database systems.

Answer:

| System        | Main feature                                                 |
| ------------- | ------------------------------------------------------------ |
| Centralized   | Database maintained at one central location                  |
| Parallel      | Multiple processing resources execute operations in parallel |
| Client/server | Clients request services from a server                       |
| Distributed   | Data is stored or managed across multiple sites              |

These systems describe different aspects of database organization and processing; they are not necessarily mutually exclusive.

## Q10. Explain schema, subschema, and instance with suitable examples.

Answer:

1. Schema: The overall design of a database. Example: a Student database containing ID, name, and course fields.

2. Subschema: A particular user's view of the database. Example: a teacher sees student names and marks.

3. Instance: The actual data stored at a particular time. Example: a record containing ID 101, name Rahul, and course BCA.

4. Relationship: The schema defines the structure, the subschema selects a view, and the instance contains the current data.

## Q11. Explain schema mapping and its types.

Answer:

Schema mapping describes the correspondence between different levels of database architecture.

Types:

1. External–conceptual mapping: Connects an external user view to the conceptual schema.

2. Conceptual–internal mapping: Connects the conceptual schema to the internal storage schema.

Importance:

* Connects the database levels.

* Describes how views relate to the logical database.

* Describes how the logical structure corresponds to physical storage.

The chapter explanation identifies the data dictionary as a place where mapping descriptions are recorded.

## Q12. Explain the ER model with an example.

Answer:

The Entity–Relationship model is used to represent entities, their attributes, and relationships.

Main components:

1. Entity: A real-world object, such as Teacher.

2. Attribute: A property of an entity, such as Teacher_ID.

3. Relationship: An association between entities.

4. ER diagram: A visual representation of these entities, attributes, and relationships.

Example:

```
+-----------+     Works for     +------------+
|  Teacher  | ----------------- | Department |
+-----------+                   +------------+
     |                                |
 Teacher_ID                     Department_ID
 Name                            Department_Name
```

# Part B — 5-Mark Questions and Answers

## Q13. Explain the three-level architecture and discuss how it supports data independence.

Answer:

The ANSI/SPARC three-level architecture separates the database into external, conceptual, and internal levels.

1. External level

* Represents individual user views.

* Different users may see different parts of the database.

2. Conceptual level

* Describes the overall logical structure.

* Defines the data and relationships in the database.

3. Internal level

- Describes physical storage and access-related details.

Diagram:

```
External Level
      |
      v
External–Conceptual Mapping
      |
      v
Conceptual Level
      |
      v
Conceptual–Internal Mapping
      |
      v
Internal Level
```

Data independence:

* Logical data independence: Allows conceptual-schema changes without requiring changes to external views or application programs.

* Physical data independence: Allows internal-storage changes without requiring changes to the conceptual schema.

Conclusion: The separation of levels makes database modification and maintenance easier by reducing the impact of changes across levels.

## Q14. Discuss the advantages and disadvantages of three-tier architecture.

Answer:

Three-tier architecture separates an application into the presentation, application, and data tiers.

### Advantages

1. Scalability: Tiers can be scaled according to workload.

2. Performance: Separating responsibilities can help optimize different parts of the application.

3. Maintainability: Changes can often be made within one tier with limited effects on other tiers.

4. Integrity and security: Application logic can validate data and control database access.

### Disadvantages

1. Complexity: Multiple tiers increase design and management complexity.

2. Infrastructure: Additional servers or other infrastructure may be needed.

3. Maintenance effort: Separate tiers require coordination and administration.

4. Network overhead: Communication between tiers can affect response time.

Conclusion: Three-tier architecture provides clear separation of responsibilities but requires careful design and management.

## Q15. Describe all six data models covered in the chapter.

Answer:

A data model defines how data is organized and represented.

1. Hierarchical data model

* Organizes data in a tree.

* Uses parent–child relationships.

* Example: a category tree.

2. Network data model

* Organizes records through links.

* Supports complex record connections.

* Example: interconnected college records.

3. Entity–Relationship model

* Uses entities, attributes, and relationships.

* Commonly used for conceptual design.

* Example: Teacher works for Department.

4. Relational data model

* Stores data in tables.

* Uses rows and columns.

* Example: an Employee table.

5. Object-oriented data model

* Represents data as objects.

* Objects can contain attributes and methods.

* Example: an Employee object with a `displayDetails()` method.

6. Physical data model

* Describes physical storage organization.

* Focuses on implementation details.

* Helps explain how data is stored and accessed.

## Q16. Compare the four database system types shown in the chapter.

Answer:

| Feature        | Centralized                  | Parallel                                 | Client/server                      | Distributed                     |
| -------------- | ---------------------------- | ---------------------------------------- | ---------------------------------- | ------------------------------- |
| Main idea      | Central database location    | Parallel processing                      | Clients request server services    | Multiple sites                  |
| Main resources | Central database site        | Multiple processors or storage resources | Clients and server                 | Interconnected sites            |
| Main focus     | Centralized management       | Processing performance                   | Service requests and responses     | Multi-site data management      |
| Example        | One central company database | Multiple processors handle a query       | College portal and database server | Company databases across cities |

Conclusion: Each type emphasizes a different aspect of database organization, processing, or access.

## Q17. Explain centralized and distributed database systems with diagrams.

Answer:

### Centralized database system

A centralized system maintains the database at a central location.

```
+-------------+       +----------------+
| Remote Site | ----> | Central        |
+-------------+       | Database       |
                      +----------------+
+-------------+
| Remote Site | ---->
+-------------+
```

Features:

1. Data is maintained centrally.

2. Remote users access the central site.

3. Management is concentrated at one location.

### Distributed database system

A distributed system stores or manages data across interconnected sites.

```
+----------+       +----------+
| Site A   | ----- | Site B   |
+----------+       +----------+
     |                  |
     |             +----------+
     +-------------| Site C   |
                   +----------+
```

Features:

1. Multiple sites participate.

2. Sites communicate over a network.

3. Data is managed across locations.

## Q18. Explain client/server database architecture and its working.

Answer:

Client/server architecture separates the requester of a service from the provider of that service.

Components:

1. Client: Provides the user-facing application and sends requests.

2. Server: Receives requests and provides database services.

3. Network: Connects clients and the server.

4. Database: Stores the information required by the application.

Working:

1. A user performs an action in the client application.

2. The client sends a request to the server.

3. The server processes the request and accesses the database as needed.

4. The server sends the result back to the client.

5. The client displays the result to the user.

Diagram:

```
+----------+          +----------+          +----------+
|  Client  | -------> |  Server  | -------> | Database |
|          | <------- |          | <------- |          |
+----------+          +----------+          +----------+
       Requests and results flow between the components
```

## Q19. Explain logical and physical data independence and state their differences.

Answer:

Data independence reduces the impact of database changes on higher levels.

### Logical data independence

It is the ability to change the conceptual schema without changing external views or application programs.

Example: modifying the logical structure while keeping existing user views unaffected.

### Physical data independence

It is the ability to change the internal storage structure without changing the conceptual schema.

Example: changing how records are physically organized without changing the logical database design.

| Basis                  | Logical                   | Physical                  |
| ---------------------- | ------------------------- | ------------------------- |
| Schema changed         | Conceptual                | Internal                  |
| Higher level protected | External                  | Conceptual                |
| Main concern           | Logical database design   | Physical storage          |
| General difficulty     | Usually harder to achieve | Usually easier to achieve |

## Q20. Explain the role of mappings in the ANSI/SPARC architecture.

Answer:

Mappings connect the three levels of database architecture.

1. External–conceptual mapping

* Connects an external schema to the conceptual schema.

* Describes how a user view corresponds to the overall logical database.

2. Conceptual–internal mapping

* Connects the conceptual schema to the internal schema.

* Describes how the logical structure corresponds to physical storage.

Importance:

1. Maintains correspondence between levels.

2. Helps the DBMS translate between views and the underlying structure.

3. Supports separation between user views, logical design, and physical storage.

The chapter explanation states that mapping descriptions are recorded in the data dictionary.

## Q21. Explain the relational and object-oriented data models with examples.

Answer:

### Relational model

The relational model represents data using tables.

* Rows represent records.

* Columns represent attributes.

* Example:

| Employee_ID | Name |
| ----------- | ---- |
| 101         | Amit |
| 102         | Neha |

### Object-oriented model

The object-oriented model represents data using objects.

* Objects contain attributes.

* Objects can contain methods.

* Example: an Employee object with `Employee_ID`, `Name`, and a `displayDetails()` method.

Difference: The relational model organizes data in tables, whereas the object-oriented model organizes data as objects that can include both data and behavior.

## Q22. Explain the purpose of a data model and describe its major types.

Answer:

A data model provides a way to organize, represent, and understand database information.

The major types covered in the chapter are:

1. Hierarchical: Tree-like structure.

2. Network: Interconnected records.

3. ER: Entities, attributes, and relationships.

4. Relational: Tables with rows and columns.

5. Object-oriented: Objects with attributes and methods.

6. Physical: Physical storage organization.

Each model provides a different way of representing data and its structure.

## Q23. Explain how the database diagrams in the chapter represent different models and architectures.

Answer:

The chapter includes diagrams representing several database models and system types.

1. Hierarchical model: Shows categories arranged in a tree-like parent–child structure.

2. Network model: Shows interconnected college, department, student, or library records.

3. ER model: Shows Teacher and Department entities connected by a `Works for` relationship.

4. Relational model: Shows employee information in a table.

5. Object-oriented model: Shows Employee and Department objects with attributes and methods.

6. Database system diagrams: Illustrate centralized, parallel, client/server, and distributed systems.

Conclusion: The diagrams help distinguish how data is represented from how database systems are organized and accessed.

## Q24. Write a detailed note on database architecture and data models.

Answer:

Database architecture describes the organization of a database system, while a data model describes how database information is represented.

### Database architecture

The ANSI/SPARC architecture contains three levels:

* External: User-specific views.

* Conceptual: Overall logical database structure.

* Internal: Physical storage structure.

Mappings connect these levels, and data independence reduces the impact of changes between them.

### Three-tier architecture

Three-tier architecture separates the presentation, application, and data tiers. It can improve scalability and maintainability, although it introduces additional complexity and communication overhead.

### Data models

The chapter covers hierarchical, network, ER, relational, object-oriented, and physical data models. These models represent data through trees, interconnected records, entities and relationships, tables, objects, or physical storage structures.

### Database system types

The chapter also describes centralized, parallel, client/server, and distributed database systems.

Conclusion: Understanding both architecture and data models helps explain how databases are structured, represented, stored, and accessed.

