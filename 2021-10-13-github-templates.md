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

Come up with a consistent set of Github templates. The templates should include prompts for
only the ESSENTIAL information we require. We want to make sure that we don't ask for more
information than we require - as this will discourages contributions.

## Templates:

### Pull Requests

```
    ## Description
    <!--- Describe your changes in detail -->

    ## Motivation and Context
    <!--- Why is this change required? What problem does it solve? -->
    <!--- If it fixes an open issue, please link to the issue here. -->

    ## How Has This Been Tested?
    <!--- Include any relevant details about your testing environment and the steps you followed -->
    <!--- For example: I am using [Safari|Firefox|Chrome] then I visit [the users path] -->

    ## Screenshots:
    <!-- Add screenshots (applicable to any UI changes) -->

    **I will abide by the [code of conduct](<LINK TO CODE OF CONDUCT HERE>)**
```


### Issues: Bug Reports

```
    <!--- Before creating a bug report, please, answer the following questions -->
    <!--- Did you check the documentation for answers? -->
    <!--- Did you make sure that this bug has not already been reported? -->

    ## Expected Behavior
    <!--- Tell us what should happen -->
    <!--- For example: When I [do X], it should [produce Y] -->

    ## Actual Behavior
    <!--- Tell us what happens instead -->
    <!--- For example: When I [did X], it [produced Y] -->

    ## Possible Fix
    <!--- Optionally suggest a fix or work around -->

    ## To Reproduce
    <!--- Optionally provide a link to a live example -->

    <!--- Otherwise, please provide a set of reproduction steps -->
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
    <!--- Before creating a feature request, please, answer the following questions -->
    <!--- Did you check the documentation for this feature? -->
    <!--- Did you make sure that this feature has not already been requested? -->

    ## Description
    <!--- Provide a description of the change or addition you are proposing -->

    ## Possible Implementation
    <!--- Optionally suggest an idea to implement or a workaround to fix the issue -->

    ## Resources:
    <!--- If you have resources related to the implementation or research for this feature, add them here. -->
    <!--- If possible, include any mockup ideas related to the requested feature. -->

    **I will abide by the [code of conduct](<LINK TO CODE OF CONDUCT HERE>)**
```

## Next steps:

We recommend that each project contains a contributing.md. When someone opens a pull
request or creates an issue, github will show them a link to that file.

If we don't add a contributing.md we need to guide users to the README, like this:
```
<!--- Please read the README before submitting pull requests for this project. -->
```

Repetitive prmpts can be moved to the contributing.md file. Things we might want in the contributing.md instead include:
<!--- Before creating a feature request, please, answer the following questions -->
<!--- Did you check the documentation for this feature? -->
<!--- Did you make sure that this feature has not already been requested? -->

Another idea is to simplify the steps needed to add templates to a project. One solution suggested by Ernesto is to add a shell script.
We can execute the shell script like this:

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/fastruby/install/templates/install.sh)



## References

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

### External template examples
- [forem - examples](https://github.com/forem/forem/tree/main/.github)
