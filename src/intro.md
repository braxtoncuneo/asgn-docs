# Overview

**`asgn`** is a program which can manage the submission and evaluation of software for classes that use a shared Linux server environment.


**`asgn`** uses a simple directory structure to store submitted files and to store the files governing courses/assignments.
This is done to make courses easy to create, maintain, and troubleshoot.

All configuration files are stored in a **`.toml`** format, which can be read and manipulated by both humans and software in a straightforward manner.

Access to the different directories in a course's file structure, as well as access to the submission / configuration files within, are all enforced through file permissions, meaning student information should be as secure as the OS itself.
The directory structure used by **`asgn`** is defined in such a way that there should be no ambiguity over which permissions a directory or file should have.
Furthermore, **`asgn`** provides a simple mechanism to re-assert these "correct" permissions at any time.

In addition to managing submission, **`asgn`** allows instructors to use **`make`** to define actions to automate the building and evaluation of assignments.
The metrics produced by these automated evaluations may be posted to a public course-wide ranking as a **score**, provided to students for private use as a **check**, or may be reserved for use by instructors as a **grade**.

## Requirements

**Platform:**
Currently, **`asgn`** is only tested on **Linux**.
As the project matures, support may be extended to other \*NIX systems.
Support for Windows server environments is not planned.

**Dependencies:**
Currently, **`asgn`** only provides automated building/evaluation for an assignment through that assignment's `Makefile`.
As the project matures, support may be extended to other mechanisms.


## **`asgn`** for Students

Functionality granted to students is viewable in the [**`asgn`** for Students](./students.md) subchapter.

## **`asgn`** for Graders

Functionality granted to graders is described in the [**`asgn`** for Graders](./graders.md) subchapter.
If you are a grader, be sure to review the subchapter for students, since you also have access to all student-related functionality.

## **`asgn`** for Instructors

Functionality granted to instructors is viewable in the [**`asgn`** for Instructors](./instructors/main.md) subchapter.
If you are an instructor, be sure to review the subchapters for graders and students, since you also have access to all student/grader-related functionality.

