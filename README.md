# Contribution 1: Translate django-modern-rest to your native language! #718

**Contribution Number:** 1

**Student:** George  

**Issue:** https://github.com/wemake-services/django-modern-rest/issues/718 

**Status:** Phase 3 Complete

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

**Implement:** https://github.com/gas12241/django-modern-rest/tree/issue-718

I changed the name of the branch I was working in to follow the branch naming conventions stated in their CONTRIBUTING.md file.

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]
The CONTRIBUTING.md file tells you pretty much the same things as their issue description does, so yes, it does follow the project's contribution guidelines.

**Evaluate:** If it gets merged. So far there hesn't been many problems from other people doing the same thing as me, and the "manager" of the issue has been active so I should know fairly quickly. I will admit that not many tests have been written for translations (of the 7+ translations that are in the codebase, only two included integration tests. Of those two, none included unit tests). I think if I can get my pull request merged, I would be setting an example of the tests (By furthering the integration tests, and providing an example of a unit test).

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: The only unit test I did for my translations included getting a specific error back, and then certifying that the error message given back, is the same as the translated message that I gave in my translation.

### Integration Tests

- [ ] For the Integration test, I will include comments from Claude. In essence, there are several calls back to back that make sure the previous language's error codes aren't bleeding into the next.
- [ ] Claude's comment: The test body is five sequential requests on the same client, in the same test function, each checking that a POST with no auth token returns 401 Unauthorized with a JSON error body translated into whatever language was requested... This - my addition to the test - is deliberately placed last in the chain, because the point of ending on a non-default locale is to prove the test doesn't rely on reset_language silently resetting state back to English between requests — each request's translation must come from that request's own header, not leftover state from the previous one.


### Manual Testing

I don't know if this counts as manual testing, but running their tests (using their command in their README) showed that the tests I added passed as well. There were 26 tests that failed, but after some prompting from Claude, I found out that those tests were not related to my work at all, and had to do with running a Redis Server

---

## Implementation Notes

### Week 3 Progress

After getting the directory made for my specific language that I am making translations into, I added the translations to the file made for me. Then I compiled the file. After compiling the file, I made sure to run tests that already existed. After all the tests that needed to pass, passed, I created my own unit test, and added on to their integration test.

### Code Changes

- **Files modified:**
- `dmr/locale/es_MX/LC_MESSAGES/django.po` — created and translated
- `dmr/locale/es_MX/LC_MESSAGES/django.mo` — compiled translation
- `django_test_app/server/settings.py` — registered `es-mx` in `LANGUAGES`
- `tests/test_integration/test_jwt_auth/test_jwt_i18n.py` — added es-MX case to the i18n integration test
- `tests/test_unit/test_i18n/test_strings.py` — added es-MX unit test

- **Key commits:**
- https://github.com/wemake-services/django-modern-rest/commit/0aa872704b3b83d07a485c429683fc7afc97d5bb
- In the above commit, I compiled the translations into the mo file that is needed for the project. This commit is significant because while it really is running a command to compile the translations, it signified the end of the "work that I needed to do"

- https://github.com/wemake-services/django-modern-rest/commit/b80182aa6c3ec380ab54998d1a946bacdabcf410
- In the above commit, I wrote the tests needed for the translations using the given tests as an example. There weren't many to base my tests off of, so if my PR gets accepted, I will be used as an example others can base their tests off of.

- **Approach decisions:** I think earlier I talked about doing the translations by hand and editing them alongside someone else. I realized that as someone who doesn't talk about these things with others in my native language, this was going to be hard. So I asked Claude for help translating and once I saw it written down, it was easier to modify them if I thought they weren't as correct as they could be. This was probably the best because my mind went blank when I saw the strings I needed to translate, but when I had something to build off of, I was able to do it seemlessly.

- **Challenges I faced:** I originally named my branch after what was given to us in our step-by-step guide, which then had to be changed to follow their branch naming conventions. I asked Claude what to do about it, and it was very helpful in "changing" the name of the branch (I put it in quotes because in it's own words, it made a new branch with the current work, named it what I needed it to be, switched me to that one, and deleted my old one). After helping me with changing the branch name, I asked Claude to walk me through what it did in order to know in the future what I might have to do if I'm stuck in the same predicament. Another challenge I faced happened in the Integration test portion, where Claude implemented a test that ran using only my translation. While it passed, I looked into the code for the other test and questioned why Claude separated my test from the other longer one that had multiple languages in it. While separating the languages would make it easier to bug fix if one of the languages went wrong, the point of that integration test was to test if any remnants of the last language persisted into a call done in a different language. I pointed this out and Claude was eager to fix the issue, becoming more in line with what was already in the code base.

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
