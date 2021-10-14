# OmbuLabs Standard Github Templates

## Problem:

New and junior contributors might be unsure about the information we require to
efficiently review a PR. Similarly, it might be unclear what information is required when
a new BUG or FEATURE is logged as an issue in Github.

We have existing PR and ISSUE templates but they are inconsistent and might ask for
unnecessary information from the contributor.

The goal is to simplify  and streamline the steps required to make a contribution or log
an issue.

## Proposal:

Come up with a consistent set of Github templates. The templates should include prompts
only the ESSENTIAL information we require. We want to make sure that we don't ask for more
information than we require - as this will discourages contributions.

## Templates:

### Pull Requests

```
    <!--- Before we start... -->
    <!--- If you're unsure about any of these, don't hesitate to ask. We're here to help! -->
    <!--- Did you update any relevant documentation -->
    <!--- Did you add tests to cover new changes -->

    ## Description
    <!--- Describe your changes in detail -->
    <!--- Please read the README before submitting pull requests for this project. -->

    ## Motivation and Context
    <!--- Why is this change required? What problem does it solve? -->
    <!--- If it fixes an open issue, please link to the issue here. -->

    ## How Has This Been Tested?
    <!--- Include any relevant details about your testing environment and the steps you followed -->

    ## Screenshots (if appropriate):

    **I will abide by the [code of conduct](<LINK TO CODE OF CONDUCT HERE>)**
```


### Issues: Bug Reports

```
    <!--- Before we start... -->
    <!--- Did you check the documentation for answers? -->
    <!--- Did you make sure that this bug has not already been reported? -->

    ## Expected Behavior
    <!--- Tell us what should happen -->

    ## Actual Behavior
    <!--- Tell us what happens instead -->

    ## Possible Fix
    <!--- Optionally suggest a fix or reason for the bug -->

    ## Steps to Reproduce
    <!--- Provide a link to a live example, or an unambiguous set of steps to -->
    <!--- reproduce this bug. Include code to reproduce, if relevant -->
    1.
    2.
    3.
    4.

    ## Additional Information
    <!--- Include any relevant details about your environment (branch, browser, OS) -->
    <!--- and the bug (screenshots, logs, etc) -->

    **I will abide by the [code of conduct](<LINK TO CODE OF CONDUCT HERE>)**
```

### Issues: Feature Requests

```
    <!--- Before we start... -->
    <!--- Did you check the documentation for this feature? -->
    <!--- Did you make sure that this feature has not already been requested? -->

    ## Description
    <!--- Provide a description of the change or addition you are proposing -->

    ## Possible Implementation
    <!--- Optionally suggest an idea for implementing addition or change -->

    ## Resources:
    <!--- If you have resources related to the implementation or research for this feature, add them here. -->
    <!--- Include any mockup idea related to the requested feature if it applies. -->

    **I will abide by the [code of conduct](<LINK TO CODE OF CONDUCT HERE>)**
```

## Final thoughts:

For the sake of simplicity we would prefer to have a single set of templates. We might
find it necessary to provide two sets of templates: one for internal project and another
for open source projects.

## Existing templates

### Pull request templates

 - [skunk.fyi - pr template](https://github.com/fastruby/skunk.fyi/blob/main/pull_request_template.md)
 - [Points - pr template](https://github.com/fastruby/points/blob/main/pull_request_template.md)
 - [Dash - pr template](https://github.com/fastruby/dash/blob/main/pull_request_template.md)

### Bug report templates

 - [skunk.fyi - bug report](https://github.com/fastruby/skunk.fyi/blob/main/.github/ISSUE_TEMPLATE/bug_report.md)
 - [Points - bug report](https://github.com/fastruby/points/blob/main/.github/ISSUE_TEMPLATE/bug_report.md?plain=1)
 - [Dash - bug report](https://github.com/fastruby/dash/blob/main/.github/ISSUE_TEMPLATE/bug_report.md)

### Feature request templates

 - [skunk.fyi - feature request](https://github.com/fastruby/skunk.fyi/blob/main/.github/ISSUE_TEMPLATE/feature_request.md)
 - [Points - feature request](https://github.com/fastruby/points/blob/main/.github/ISSUE_TEMPLATE/feature_request.md)
 - [Dash - feature request](https://github.com/fastruby/dash/blob/main/.github/ISSUE_TEMPLATE/feature_request.md)
