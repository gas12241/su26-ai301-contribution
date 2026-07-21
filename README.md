# Contribution 1: Translate django-modern-rest to your native language! #718

**Contribution Number:** 1

**Student:** George  

**Issue:** https://github.com/wemake-services/django-modern-rest/issues/718 

**Status:** Phase 4 Completed!

---

## Why I Chose This Issue

I chose this issue because it seems like a great first issue to have. It is documented well (has steps for setups and how to contribute to the project), allows me to use a different skill I enjoy (Spanish), and the creators are active and enjoyable to hear back from. I also think it'll give me time to work on my documentation process as well (since on paper, the issue doesn't seem too bad).

---

## Understanding the Issue

### Problem Description

**What's broken?**
There is a lack of Error labels for exceptions in other languages (including Mexican Spanish).

**Why does this issue matter?**
This issue matters because adding error labels for exceptions means that people who do not speak english can interact with the codebase. This can then lead to even more contributions since the pool of people who can contribute, grows with every added language. 

**Why did I choose this issue?** Making the codebase more accessible for people that speak the language I grew up speaking is more than enough foa reason to want to contribute in this way!

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

#### NOTE: This was taken straight from the issue page. I ran into no issues, and it really was as simple as these instructions (after installing uv, of course)! As a sidenote, since the language I chose was Spanish specific to Mexico, the new file made for me was named:

```dmr/locale/es_MX/LC_MESSAGES/django.po```

1. Run uv sync --all-groups --all-extras
2. Run uv run django-admin makemessages -l YOUR_LOCALE, for example: uv run django-admin makemessages -l ru_RU, full list of locales: https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes
3. Translate the new file created in dmr/locale/${YOUR_LOCALE}/LC_MESSAGES/django.po
4. Run uv run django-admin compilemessages
5. Done! You are awesome, submit the PR :)

### Reproduction Evidence

- **Commit showing reproduction (my fork, the branch is linked below):** https://github.com/gas12241/django-modern-rest
- **Screenshots/logs:**
<img width="1349" height="716" alt="image" src="https://github.com/user-attachments/assets/ec96075f-99d3-4876-aa34-59aed02d6198" />
- **My findings:** The file comes with some things that I need to take out (which I referenced from multiple other translations that have happend, including after they've updated their terminal commands in the issue description).

---

## Solution Approach

### Analysis

I need to come up with translations for the error messages in the file pictured above. Either I will use Claude for them and manually check them, or I'll do them myself and run them by a second source (another person preferably, but possibly Claude).

### Proposed Solution

Do the translations by hand and get them checked by a second source.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** File that was made when I ran their terminal commands is missing translations. I have to add them, compile them, and turn them in.

**Match:**
Other translations exist in the parent directory. Will use those to format my translations.

**Plan:** (Steps 3-5 from the "Steps to Reproduce" section above)
1. Translate the new file created in dmr/locale/es_MX/LC_MESSAGES/django.po
2. Run uv run django-admin compilemessages
3. Done! You are awesome, submit the PR :)

**Implement:** https://github.com/gas12241/django-modern-rest/tree/issue-718

I changed the name of the branch I was working in to follow the branch naming conventions stated in their CONTRIBUTING.md file.

**Review:**
The CONTRIBUTING.md file tells you pretty much the same things as their issue description does, so yes, it does follow the project's contribution guidelines.

**Evaluate:** If it gets merged. So far there hasn't been many problems from other people doing the same thing as me, and the maintainer of the issue has been active so I should know fairly quickly. I will admit that not many tests have been written for translations (of the 7+ translations that are in the codebase, only two included integration tests. Of those two, none included unit tests). I think if I can get my pull request merged, I would be setting an example of the tests (By furthering the integration tests, and providing an example of a unit test).

**Root Cause:** No one had contributed an es_MX locale yet. The project's i18n infrastructure already supported adding new languages, but Mexican Spanish translations for error messages (authentication failures, rate limiting, CSRF errors, etc.) hadn't been written.

**Specific files to modify**

The file ```dmr/locale/es_MX/LC_MESSAGES/django.po``` will be where we make our translations.

The file ```dmr/locale/es_MX/LC_MESSAGES/django.mo``` will host the compilation of the translations.

---

## Testing Strategy

### Unit Tests

NOTE: I am writing this after I got my pull request merged. I was actually asked to remove my tests from my pull request in order for my code to be merged. That being said, I will leave the tests I wrote below to describe what I tried before they were eventually deleted.

- [ ] Test case 1: The only unit test I did for my translations included getting a specific error back, and then certifying that the error message given back, is the same as the translated message that I gave in my translation.

### Integration Tests

- [ ] For the Integration test, I will include comments from Claude. In essence, there are several calls back to back that make sure the previous language's error codes aren't bleeding into the next.
- [ ] Claude's comment: The test body is five sequential requests on the same client, in the same test function, each checking that a POST with no auth token returns 401 Unauthorized with a JSON error body translated into whatever language was requested... This - my addition to the test - is deliberately placed last in the chain, because the point of ending on a non-default locale is to prove the test doesn't rely on reset_language silently resetting state back to English between requests — each request's translation must come from that request's own header, not leftover state from the previous one.


### Manual Testing

I don't know if this counts as manual testing, but running their tests (using their command in their README) showed that the tests I added passed as well. There were 26 tests that failed, but after some prompting from Claude, I found out that those tests were not related to my work at all, and had to do with running a Redis Server

---

## Implementation Notes

### Week 3 Progress

After getting the directory made for my specific language that I am making translations into, I added the translations to the file made for me. Then I compiled the file. After compiling the file, I made sure to run tests that already existed. After all the tests that needed to pass, passed, I created my own unit test, and added on to their integration test (These tests were taken out later on, as mentioned above in the Testing Strategy section).

### Code Changes

- **Files modified:**
- `dmr/locale/es_MX/LC_MESSAGES/django.po` — created and translated
- `dmr/locale/es_MX/LC_MESSAGES/django.mo` — compiled translation

- **Files modified, but later reverted back to their original states:**
- `django_test_app/server/settings.py` — registered `es-mx` in `LANGUAGES`
- `tests/test_integration/test_jwt_auth/test_jwt_i18n.py` — added es-MX case to the i18n integration test
- `tests/test_unit/test_i18n/test_strings.py` — added es-MX unit test

- **Key commits:**
- https://github.com/wemake-services/django-modern-rest/commit/0aa872704b3b83d07a485c429683fc7afc97d5bb
- In the above commit, I compiled the translations into the mo file that is needed for the project. This commit is significant because while it really is running a command to compile the translations, it signified the end of the "work that I needed to do"

NOTE: This commit was reverted, but at the time I thought it was significant given the lack of testing of the different languages.

- https://github.com/wemake-services/django-modern-rest/commit/b80182aa6c3ec380ab54998d1a946bacdabcf410
- In the above commit, I wrote the tests needed for the translations using the given tests as an example. There weren't many to base my tests off of, so if my PR gets accepted, I will be used as an example others can base their tests off of.

- **Approach decisions:** I think earlier I talked about doing the translations by hand and editing them alongside someone else or Claude. I realized that as someone who doesn't talk about these things with others in my native language, this was going to be hard. So I asked Claude for help translating and once I saw it written down, it was easier to modify them if I thought they weren't as correct as they could be. This was probably the best because my mind went blank when I saw the strings I needed to translate, but when I had something to build off of, I was able to do it seemlessly.

- **Challenges I faced:** I originally named my branch after what was given to us in our step-by-step guide, which then had to be changed to follow their branch naming conventions. I asked Claude what to do about it, and it was very helpful in "changing" the name of the branch (I put it in quotes because in it's own words, it made a new branch with the current work, named it what I needed it to be, switched me to that one, and deleted my old one). After helping me with changing the branch name, I asked Claude to walk me through what it did in order to know in the future what I might have to do if I'm stuck in the same predicament.
- Another challenge I faced happened in the Integration test portion, where Claude implemented a test that ran using only my translation. While it passed, I looked into the code for the other test and questioned why Claude separated my test from the other longer one that had multiple languages in it. While separating the languages would make it easier to bug fix if one of the languages went wrong, the point of that integration test was to test if any remnants of the last language persisted into a call done in a different language. I pointed this out and Claude was eager to fix the issue, becoming more in line with what was already in the code base. NOTE that this code ended up not being used in the end, but I think this was a good point in the project where I gave some push back to what Claude was originally suggesting I do.

---

## Pull Request

**PR Link:** https://github.com/wemake-services/django-modern-rest/pull/1137

**PR Description:**

DISCLAIMER: This is the template we are given to fill out when creating a pull request. I know on our submission sheet it says to create a pull request that has more details, but I followed this template (as well as the work of another recent pull request) to be in line with what works for the Code Reviewers. I hope to not lose points given that I am following what was done before me.

Below is the PR Description.

I have made things!

AI Policy
- I have read and agree to the AI Policy, removed any "Co-Authored-By" lines attributing coding agents, and manually reviewed the final result

Checklist
- I have double checked that there are no unrelated changes in this pull request (old patches, accidental config files, etc)
- I have created at least one test case for the changes I have made
- I have updated the documentation for the changes I have made

Related issues

Refs #718

I do not have any feedback!


**Maintainer Feedback:**
- 07/10: "Please, revert the test changes :) We only test that the translation works there, not all languages."
- 07/13: I asked the day I got the response if I needed to take out the unit test as well as the integration test (since it was tied to the line shown in the next piece of feedback). Without a response, I decided to remove both tests since most of the other languages that have been merged don't have a unit test either.

- 07/10: "This is not needed ;)" (and it points to the settings.py file where I added ex_MX as a language for an integration test)
- 07/13: Took out the line in settings.py that allowed Spanish to be tested in the integration test.

**Status:** As of Tuesday, July 14th, my Pull Request was merged!

---

## Learnings & Reflections

### Technical Skills Gained

I think most of the technical skills I have gained came from Git. Claude would suggest git commands to run given what I wanted to do, so before I ran them, I asked about what they would do (to learn, but also to make sure I wasn't doing something I shouldn't be on Git). On top of that, this isn't technical per se, but I would say I also gained some confidence in working with Git.

### Challenges Overcome

Installing Just for the project was a pain for me. For whatever reason, it wouldn't let me run just commands after installing it because it wasn't tied to my virtual environemnt. That was the hardest part of the assignment as most other things have been straightforward.

### What I'd Do Differently Next Time

Honestly I would have asked about testing when I first realized that many of the languages aren't tested. I stalled for a bit wondering if I should or shouldn't write tests given the lack of them in the codebase. I think I could have saved myself some time, as well as an iteration in my pull request if I had asked earlier.

---

## Resources Used

- The CONTRIBUTING.md file was helpful in letting me know what I needed to do to contribute translations specifically.
- I know that sometimes there are specific translations for technicaly terms that aren't 1 to 1 between languages. I leaned on my findings throughout Google to make sure that the words being used for technical terms were the norm, and not the literal translation from one language to another.
- I don't know if this counts, but I asked Claude to walk me through some of the git commands that it would recommend.
