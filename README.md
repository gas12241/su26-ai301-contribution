# Contribution 1: Translate django-modern-rest to your native language! #718

**Contribution Number:** 1

**Student:** George  

**Issue:** https://github.com/wemake-services/django-modern-rest/issues/718 

**Status:** Phase 2 Complete

---

## Why I Chose This Issue

I chose this issue because it seems like a great first issue to have. It is documented well (has steps for setups and how to contribute to the project), allows me to use a different skill I enjoy (Spanish), and the creators are active and enjoyable to hear back from. I also think it'll give me time to work on my documentation process as well (since on paper, the issue doesn't seem too bad).

---

## Understanding the Issue

### Problem Description

There's technically not a problem per se, in the sense that there isn't a bug to fix. This issue requires the solver(me) to translate error messages into a different language that you're native/proficient in. I chose to do Spanish specific to Mexico, since that is the language I grew up speaking.

### Expected Behavior

There should be a file that has translations specific to Spanish from Mexico (es_MX)

### Current Behavior

There is no file with Spanish specific to Mexico currently.

### Affected Components

When running commands given to us in the issue description, a new folder is made inside the dmr/locale directory that is specific to the language being translated to. It is in this folder that I will be doing work!

---

## Reproduction Process

### Environment Setup

1. I cloned the fork of the repo
2. Made a branch that I could work from
3. Created a virtual environment and ran it
4. pip installed Django
5. Tried running the steps listed below
6. Ran into an issue where uv was not a recognized command
7. Installed uv using brew (am on a mac)
8. Installed just
9. Followed the steps below.

### Steps to Reproduce

#### NOTE: This was taken straight from the issue page. It really was as simple as these instructions (after installing uv, of course)!

1. Run uv sync --all-groups --all-extras
2. Run uv run django-admin makemessages -l YOUR_LOCALE, for example: uv run django-admin makemessages -l ru_RU, full list of locales: https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes
3. Translate the new file created in dmr/locale/${YOUR_LOCALE}/LC_MESSAGES/django.po
4. Run uv run django-admin compilemessages
5. Done! You are awesome, submit the PR :)

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/gas12241/django-modern-rest
- **Screenshots/logs:**
<img width="1349" height="716" alt="image" src="https://github.com/user-attachments/assets/ec96075f-99d3-4876-aa34-59aed02d6198" />
- **My findings:** The file comes with some things that I need to take out (which I referenced from multiple other translations that have happend, including after they've updated their terminal commands in the issue description).

---

## Solution Approach

### Analysis

I need to come up with translations for the error messages in the file pictured above. Then I need to cross reference them with something or someone who also speaks Mexican Spanish.

### Proposed Solution

Do the translations by hand and get them checked by a second source (Will probably ask someone I know).

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** File that was made when I ran their terminal commands is missing translations

**Match:**
Other translations exist in the parent directory. Will use those to format my translations.

**Plan:** (Steps 3-5 from the "Steps to Reproduce" section above)
1. Translate the new file created in dmr/locale/${YOUR_LOCALE}/LC_MESSAGES/django.po
2. Run uv run django-admin compilemessages
3. Done! You are awesome, submit the PR :)

**Implement:** https://github.com/gas12241/django-modern-rest/tree/fix-issue-mx-spanish-translation

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]
The CONTRIBUTING.md file tells you pretty much the same things as their issue description does, so yes, it does follow the project's contribution guidelines.

**Evaluate:** If it gets merged. So far there hesn't been many problems from other people doing the same thing as me, and the "manager" of the issue has been active so I should know fairly quickly.

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
