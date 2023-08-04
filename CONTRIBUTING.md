<p align="center">
  <a href="https://about.codecov.io" target="_blank">
    <img src="https://about.codecov.io/wp-content/themes/codecov/assets/brand/sentry-cobranding/logos/codecov-by-sentry-logo.svg" alt="Codecov by Sentry logo" width="280" height="84">
  </a>
</p>

# Contributing

**Welcome to the Codecov Community!**

Below are the guidelines for contributing to any of Codecov's repositories. Please review them before committing to the repository, opening a pull request, or creating an issue.

#### Table of Contents:

- [Commit Messages](#commit-messages)
  - [General Rules](#general-rules)
  - [Squashing](#squashing)
  - [Commit Message Format](#commit-message-format)
  - [Type](#type)
  - [Subject](#subject)
  - [Body](#body)
  - [Footer](#footer)
- [Code Review](#code-review)
  - [Who should be reviewing code?](#who-should-be-reviewing-code)
  - [Why Pull Requests](#why-pull-requests)
  - [Commit Guidelines](#commit-guidelines)
  - [Code Reviews are for ...](#code-reviews-are-for)
  - [Code Reviews are not for ...](#code-reviews-are-not-for)
  - [Guidelines for _Submitters_](#guidelines-for-submitters)
  - [Guidelines for _Reviewers_](#guidelines-for-reviewers)

# Commit Messages

We have precise rules over how our git commit messages can be formatted. This leads to more readable messages that are easy to follow when looking through the project history.

## General Rules

1. Separate subject from body with a blank line
2. Limit the subject line to 70 characters
3. Capitalize the subject line
4. Do not end the subject line with a period
5. Use the imperative mood in the subject line
6. Use the body to explain what and why vs. how
7. Each commit should be a single, stable change

[Return to top](#contributing)

## Squashing

When you are squashing your branch, it’s important to make sure you update the commit message. If you’re using GitHub’s UI it will by default create a new commit message which is a combination of all commits and **does not follow the commit guidelines.**

If you’re working locally, it often can be useful to --amend a commit, or utilize rebase -i to reorder, squash, and reword your commits.

[Return to top](#contributing)

## Commit Message Format

> **Note**: This commit message format is only for the squash merge commit that occurs when you merge your PR on GitHub

```text
<type>: <subject> (<pr-number>)
```

The **header** should be set to the squash merge title which will be the commit title.

```text
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

Any line of the commit description should not be longer 100 characters! This allows the description to be easier to read on GitHub as well as in various git tools.

The footer should contain a closing reference to an issue as well as a relevant Codecov issue if any.

Example:

![Screenshot 2023-07-19 at 10 13 20 AM](https://github.com/codecov/contributing/assets/105234307/88424f25-208e-4bf2-9e3b-0ca2b430ca74)

[Return to top](#contributing)

## Type

| Type         | Definition                                                                                             |
| ------------ | ------------------------------------------------------------------------------------------------------ |
| **build:**   | Changes that affect the build system or external dependencies (example scopes: webpack, python, npm)   |
| **ci:**      | Changes to our CI configuration files and scripts (example scopes: CircleCI, etc.)                     |
| **docs:**    | Documentation only changes                                                                             |
| **feat:**    | A new feature                                                                                          |
| **fix:**     | A bug fix                                                                                              |
| **perf:**    | A code change that improves performance                                                                |
| **ref:**     | A code change that neither fixes a bug nor adds a feature (refactor)                                   |
| **style:**   | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc) |
| **test:**    | Adding missing tests or correcting existing tests                                                      |
| **meta:**    | Some meta information in the repo changes (example scopes: owner files, editor config etc.)            |
| **license:** | Changes to licenses                                                                                    |

[Return to top](#contributing)

## Subject

The subject contains a succinct description of the change:

- Use the imperative, present tense: “change” not “changed” nor “changes”
- Capitalize the first letter
- No dot (.) at the end

[Return to top](#contributing)

## Body

Just as in the **subject**, use the imperative, present tense: “change” not “changed” nor “changes”. The body should include the motivation for the change and contrast this with previous behavior.

[Return to top](#contributing)

## Footer

The footer should contain any information about **Breaking Changes** and is also the place to reference GitHub issues that this commit **Closes**.

Breaking Changes should start with the word `BREAKING CHANGE:` with a space or two newlines. The rest of the commit message is then used for this.

[Return to top](#contributing)

# Code Review

Code review is mandatory at Codecov. This adds overhead to each change, but ensures that simple, often overlooked problems are more easily avoided. Code review helps build shared context and collective ownership. It is also an opportunity to collaborate with other teams. Finally, code review can identify several classes of problem before customers are exposed to them.

Code review is managed via GitHub’s Pull Requests (see below for rationale). Templates may exist on repositories, but if they do not, consider [creating one](https://help.github.com/articles/creating-a-pull-request-template-for-your-repository/).'

[Return to top](#contributing)

## Who should be reviewing code?

All engineers should be reviewing code. As you gain more experience and context on the products we build and technologies we use, you can provide valuable feedback to other engineers who may be working in areas that are new to them but familiar to you.

Code review is an opportunity to improve your mentoring and communication skills. Code review can have the important function of teaching engineers about the languages, frameworks and technologies we use in a collaborative environment that is about the changes being made.

When creating a pull request, reference any tickets or Codecov issues which are being addressed. Additionally **@mention** an appropriate team (or teams) for review.

[Return to top](#contributing)

## Why Pull Requests

Because Codecov is a public project maintained via GitHub we want to ensure that the barrier to entry for external contributions is minimal. By using GitHub features when possible, we make it easy for developers familiar with other projects on GitHub.

[Return to top](#contributing)

## Commit Guidelines

See the [Commit Messages](#commit-messages) section.

[Return to top](#contributing)

## Code Reviews are for …

### Identifying problematic code

Above all, a code review should try to identify potential bugs that could cause the application to break – either now, or in the future.

- Uncaught runtime exceptions (e.g. potential for an index to be out of bounds)
- Obvious performance bottlenecks (e.g. `O(n^2`) where `n` is unbounded)
- Code alters behavior elsewhere in an unanticipated way
- API changes are not backwards compatible (e.g. renaming or removing a key)
- Complex ORM interactions that may have unexpected query generation/performance
- Security vulnerabilities
- Missing or incorrect Permissions or Access Control.

### Improving Design

When reviewing code, consider if the interactions of the various pieces in the change make sense together. If you are familiar with the project, do the changes conflict with other requirements or goals? Could any of the methods being added be promoted to module level methods? Are methods being passed properties of objects when they could be passed the entire object?

### Tests Included

Look for tests. There should be functional tests, integration tests or end-to-end tests covering the changes. If not, ask for them. At Codecov we rely on our test suite to maintain a high quality bar and ship rapidly.

When reviewing tests double check that the tests cover the requirements of the project or that they cover the defect being fixed. Tests should avoid branching and looping as much as possible to prevent bugs in the test code from gaining a foothold.

Functional tests that simulate how a user would call our APIs or use our UX are key to preventing regressions and avoiding brittle tests that are coupled to the internals of the products we ship.

Tests are also the ideal place to ensure that the changes have considered permissions and access control logic.

### Assessing and approving long-term impact

If you’re making significant architectural, schema, or build changes that will have long-term ramifications to the software or data, it is necessary to solicit a senior engineer’s acknowledgment and blessing.

- Large refactors
- Database schema changes, like adding or removing columns and tables
- API changes (including JSON schema changes)
- Adopting new frameworks, libraries, or tools
- New product behavior that may permanently alter performance characteristics moving forward

### Double-checking expected behavior

The reviewer should make a genuine attempt to double-check that the goals of the PR appear to be satisfied by the code submitted. This requires the submitter to write a good description of the expected behavior, and why. See also: [Guidelines for submitters below.](#guidelines-for-submitters)

### Information sharing and professional development

Code reviews are an opportunity for more people to understand forthcoming code changes, so that they might in turn teach others down the road, and be in a position to fix something if/when the original author is not be available.

Additionally, code reviews are an opportunity to learn about new techniques or approaches, and be exposed to code you might otherwise not have an opportunity to browse.

### Reducing code complexity

Research shows that LOC is correlated with a higher bug count. If reviewers see an easy opportunity to significantly reduce the amount of code that is submitted, they should suggest a different approach.

For example, if a submitter has written a `for` loop to find an item in an array:

```js
for (let i = 0; i < arr.length; i++) {
  if (arr[i] === "thing-i-want") return i;
}
return undefined;
```

It’s fair game to suggest they instead use:

```js
return arr.find((x) => x === "thing-i-want");
```

This is a mostly objective improvement: there are fewer variables, fewer statements, and fewer branches, and the method name `find` communicates intent. Suggesting these types of uncontroversial improvements is encouraged.

Be careful though – it’s easy to go down a rabbit hole of re-writing code to be as small as possible, and in the end winding up with something ultimately more complicated. Be pragmatic and strive to reach a good balance. See also: ["Code reviews are not for getting it perfect"](#code-reviews-are-not-for).

### Enforcing coding standards

As much as possible, we use automation to enforce code style and test coverage, but there are exceptions that cannot necessarily be automated (or perhaps more accurately, we haven’t automated them yet):

- Variable, file, metric, and logger names are sensible, readable, and consistent with existing code
- Migrations have a deployment plan
- Unused or superfluous code isn’t committed accidentally

[Return to top](#contributing)

## Code Reviews are not for …

### Passing responsibility onto the reviewer

It is not the responsibility of the reviewer that your code is correct, is bug free, or achieves its goals. Reviewers are there to help you, but if something is wrong, it’s your responsibility to correct it.

### Boasting about your programming knowledge

As a reviewer, try to stick to objective improvements and make a best-intent assumption that the submitter has done their homework. Codecov is a No Flex Zone™.

### Introducing long-term architectural changes for the first time

While code reviews are great for discussion, they’re not the place to introduce large, long-term changes for the first time. Before dropping a PR that implements those changes, you should write a proposal and reach out to the relevant parties beforehand.

### Getting it perfect

Code reviews are expensive. Every time you request a change, you’re probably delaying that PR by 24 hours or more. This can severely inhibit our ability to move fast.

The goal of code reviews is to **reduce risk**, not to produce perfect code. It’s okay to ship code in stages, and to commit to improving something later. If you’re thinking – _if we don’t get it correct up-front, we’ll never come back to it_ – consider that if it never needs coming back to, perhaps those changes were never necessary in the first place.

Please be pragmatic, and consider the cost of each incremental request for changes.

[Return to top](#contributing)

## Guidelines for _Submitters_

[Return to top](#contributing)

### Try to organize your work in a way that makes it conducive to review

- Ideally, a pull request is limited to only a single feature or behavior change.
- This might feel like more work up-front, but it can make code review faster, reduce risk by letting you ship in stages, and ultimately end up being quicker.

### Describe what your PR does in a few sentences in the description field

- Additionally explain why we’re making these changes.
- If applicable, explain why other approaches were explored but not settled on.
- This gives the reviewer context, and prevents them going down the same rabbit holes that that submitter may have already explored when creating the code.

### Annotate specific lines in your PR

- If you can, give context to specific lines of code that could use elaboration.

### Where appropriate, label in-progress PRs as WIP (work in progress) for early feedback

- Labeling your work as WIP helps set expectations about the state of the PR.
- WIP PRs are good for having someone check-in to make sure you’re on the right path.
- Additionally, this is an opportunity to verify CI passes before involving a reviewer.

### Be your own first reviewer

- After you’ve put up your PR on GitHub, walk through the code yourself, before assigning an external reviewer.
- You’ll often catch code mistakes you didn’t see when writing it.
- This is also a good time to leave comments and refresh your memory in order to write a more helpful description.

### Assign Relevant for Review

- To ensure the correct people get their eyes on the PR, please request the review of the respective team to review the PR
- If your work spans multiple teams (and thus, many reviewers), consider breaking up your PR into multiple compatible patches (e.g. a back-end change and a front-end change).

### Avoid rebasing unnecessarily

- After a rebase, previous review comments will be orphaned from their now non-existent parent commits, making review more difficult
- Rewriting history makes it difficult for reviewers to isolate the scope of their review

### Let reviewers know that you’ve made changes

- Request review again via the "Reviewers" dropdown (There should be a yellow dot next to their name again).
- Don’t rely on reviewers' mind-reading skills to know that you’re ready to have them look things over again.
- Leave comment resolution to the reviewer so they can easily reference sections that you have addressed.

[Return to top](#contributing)

## Guidelines for _Reviewers_

[Return to top](#contributing)

### Be polite and empathetic

- Avoid accusatory and/or judgmental comments like: “You should have done X”

### Provide _actionable_ feedback

- Instead of _“This is bad”_, try _“I feel this could be clearer. What if you renamed variable X to Y?”_

### Distinguish between “requires changes” and “nitpicks”

- Consider marking a PR as approved if the only requested changes are minor nits, so as not to block the author in another asynchronous review cycle.

### Respond promptly to code review requests

- We recommend checking for open code reviews at the start and end of every day.
- [Github's Review Requests tab](https://github.com/pulls/review-requested) can be a helpful place to keep track of these.
- Resolve comments when submitter has resolved the issue.

[Return to top](#contributing)
