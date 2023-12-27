# Security Considerations

Automated submission and evaluation inevitably runs head-first into security issues.
Some of these issues can be handled semi-automatically through good file permissions hygiene, which **`asgn`** attempts to do when possible, but automation cannot fully replace a thoughtful approach to security.

Enumerated below are some major security considerations that have been considered, what **`asgn`** does (or does not) do to address them, and what you can do to fill in the gaps.

## Permissions in Course File Structures

As noted previously, the **refresh** sub-command re-asserts the correct file permissions across a course's directory structure.
It is designed to be non-destructive so that it may be used liberally.
If you think you may have messed up the file permissions, running a **refresh**


## Access to Grader/Instructor Sub-commands

As part of startup, before any arguments are evaluated, `asgn` assigns a **role** to the user.
There are four different roles:

- Instructor
- Grader
- Student
- Other

The **instructor** of a course is defined in terms of who owns a course's `course.toml` file (located in the `.info` subdirectory of the course's root directory.)
Without root privileges, the designated owner of this file should not be changeable, so whoever initially created a course's `course.toml` file should remain the instructor.

A user is designated as a **grader** in a course if their username is contained by the `graders` list in the course's `course.toml` file.

A user is designated as a **student** in a course if their username is contained by the `students` list in the course's `course.toml` file.
(The `graders` list supersedes the `students` list, when it comes to defining roles.)

A user is designated the **other** role if they are not the course's instructor and their username is not contained by either the `graders` list or the `students` list of the course's `course.toml` file.
The **other** role is granted no subcommands.


## Distributing Code through Object Files


## Running Untrusted Commands with `unshare`

