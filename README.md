# su26-ai301-contribution

# Contribution [#]: [Scala] Use scala generics to optimize tuple serialization #1060


**Contribution Number:** 1

**Student:** George Alvarado-Salinas

**Issue:** https://github.com/apache/fory/issues/1060

**Status:** Phase I as of Tuesday, June 9th (Currently in Progress).

---

## Why I Chose This Issue

I chose this topic because it seems like a decent learning opportunity for me, given what I have experience in. I do not have prior experience in Scala, but the issue seems straightforward enough that I think I can learn what I need to in order to help with the issue. I think this also gives me a good chance to practice some of the other things that I will need to know that aren't necessarily hard-skill related (like dealing with github, annotating my docs throughout the progress, and healthy use of AI in order to finish the open source contribution).

In the end, I hope to gain confidence using Git (because it can be a nightmare), help with a project database which isn't mine to begin with, and learn more about Scala.

---

## Understanding the Issue

### Problem Description

From my very broad understanding, implementing a tuple serializer that uses Scala Generics could lead to less overhead when serializing/deserializing, making the serializer code more efficient.

### Expected Behavior

After looking further into it, the behavior in general should stay the same. Implementing the Tuple Serializer using Scala Generics would just make things more efficient, as type tags would not have to be made at runtime.

### Current Behavior

Because of the way it is written, something like:
val tuple = Tuple2(100, 10000L)

Is seen as a tuple with a couple of objects in it, instead of a tuple with a known type of (int, long).

### Affected Components

[Which parts of the codebase are involved?]

There are a couple parts of the codebase that are involved. The file that they mention by name in the issue report,
"BaseObjectCodecBuilder," is in the Java side of the project. After that, most of the files that will be touched will be in the Scala side.

---

## Reproduction Process

### Environment Setup

I switched from looking at the code in VSCode to IntelliJ because I think it's what's most often used when working with Java/Scala
(I was also running into problems in VSCode that I believe were Java related). I ran the command "sbt test" which let me know that
the test files in the Scala directory were being ran. 

### Steps to Reproduce

Considering this isn't a bug, there aren't many steps to reproduce. I think I just needed to be able to get the tests to run on my computer
(verifying that any changes I make, alongside their respective tests, will be able to work).

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/gas12241/fory/tree/fix-issue-1060-scala-tuple-serializer
- **Screenshots/logs:** <img width="1709" height="1045" alt="image" src="https://github.com/user-attachments/assets/c852aeed-8cce-4f39-90fe-1ebdd54bf085" />
- **My findings:** I found out that my default JDK broke my project, and setting it to 21 fixed it.

---

## Solution Approach

### Analysis

I have to get more accustomed to the codebase and see what I need to change, specifically the "BaseObjectCodecBuilder" file
as it is massive and I'm hoping that by changing small parts of it, I won't run into any issues myself.

### Proposed Solution

Create a tuple serializer in a new file that doesn't change the current behavior, but allows it to run more efficiently. Will
be done by changing the "BaseObjectCodecBuilder" file to accept a ScalaTupleSerializer, and getting it to interact with the new
Tuple Serializer.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** Currently Scala Tuples are being serialized without knowing the type of the variables in the tuple. For example,
reading a Tuple blindly like (100, 1000L, "str") means that when serialized, there will be a type tag attached to each of the variables.
This leads to more things that need to be serialized/deserialized.

**Match:** From my research in the codebase, there exists a serializer that deals with homogenous lists, that I can base my work off of
(even if what I would be doing is working with tuples that include different types).

**Plan:** [Step-by-step implementation plan]
1. Finish the testing for Scala Tuples (someone did the first 6, and last 3, but didn't do the ones in between)

2. Create the Scala Serializer in the Scala part of the codebase.

3. Modify the "BaseObjectCodecBuilder" to accept the new serializer.

**Implement:** https://github.com/gas12241/fory/tree/fix-issue-1060-scala-tuple-serializer

**Review:** I believe it does. I will admit, I have read their AI contribution guidelines and will have to extensively talk about my contributions using it, as I'm not sure if I'll be able to contribute without it (given the size of the codebase and given my inexperience with Scala).

**Evaluate:** Run efficiency tests with and without the changes.

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
