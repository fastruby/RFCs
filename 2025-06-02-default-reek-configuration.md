# Default Reek Configuration

## The Problem

We like to use Reek in many of our projects as one of the tools to aid in improving the code quality, but we do not have a clear expected way to use Reek in the different projects we use and we have no clear guidelines about when to make exception or changes to its configuration.

## Proposed initial Reek configuration

This RFC is a proposal of a default Reek configuration file that we would use in established projects to reduce the number of warnings and the need of exceptions that we see with the [default configuration](https://github.com/troessner/reek/blob/a8649370ced77dd0e798b00dc97ff916f68bb002/docs/defaults.reek.yml), and to also define some guideline or expectation on how we can decide when to add exceptions and modifications for different needs.

### Default .reek configuration file

This file is meant to be added in the root of the project as `.reek.yml` to handle common cases of Reek warnings that will want either disabled or reconfigured based on what we've seen in many projects.

It's a combination of the [official `rails-friendly` configuration recommended in the Reek's README](https://github.com/troessner/reek?tab=readme-ov-file#working-with-rails) and some changes to the default rules.

```yml
detectors:
  DuplicateMethodCall:
    max_calls: 3 # original is 1
  IrresponsibleModule:
    enabled: false # we don't really add module descriptions ever
  NilCheck:
    enabled: false # in some projects were this was enabled, it was a false positive being ignored
  TooManyStatements:
    max_statements: 10 # original is 5
  UncommunicativeVariableName:
    accept:
      - e # common in `rescue => e` (short for `exception`)
      - x # common in one-liners
      - _ # common when ignoring a parameter
      - k # common when looping through hashes (short for `key`)
      - v # common when looping through hashes (short for `value`)
  UnusedPrivateMethod:
    enabled: true # default is false, we are still disabling it for controllers and models below
  UtilityFunction:
    public_methods_only: true # original is false

directories: # reek's recommendation for Rails applications unless a comment is added
  "app/controllers":
    InstanceVariableAssumption:
      enabled: false
    NestedIterators:
      max_allowed_nesting: 2
    TooManyInstanceVariables:
      enabled: false # instance variables are the way to pass data to views, it's expected
    TooManyStatements:
      enabled: false
    UnusedPrivateMethod:
      enabled: false
  "app/helpers":
    UtilityFunction:
      enabled: false
  "app/mailers":
    InstanceVariableAssumption:
      enabled: false
  "app/models":
    InstanceVariableAssumption:
      enabled: false
    TooManyStatements:
      enabled: false
    UnusedPrivateMethod:
      enabled: false

exclude_paths:
  - db/migrate
  - node_modules # in case any node package has a .rb file (like the styleguide)
  - vendor # in case gems are bundle inside the project's folder vendor folder
```

### Exceptions and :reek:\* Comments

When applying this configuration, projects will still need exceptions in some cases where the code smell is not flagging code we want to change or when there's a warning on code that's in the same file but out of the scope of the work done.

It is expected that the team working on a given project will keep an eye when these exceptions are used, and there should be a clear explanation to skip a code smell instead of fixing it (which is a valid thing to do, but shouldn't be done just in order to not address it).

## How is this going to impact our internal teams and their day to day?

In the near future we plan to adapt this configuration in these projects:

- FastRuby.io
- OmbuLabs.com
- Points

Other project will not adapt this configuration. We expect Ruby and Rails projects to reach certain maturity before we adapt these standards. Ops will decide when a project has reached this maturity.

## What projects are not a good fit for this new standard?

We do NOT want to adapt this standard on these types of projects:

- Prototypes
- Unproven MVPs that might be discarded
- One-off internal tools that might be obsolete in a year

## What this file is NOT

There will never be a single Reek configuration file to match the needs of all projects we have, this file is only a starting point with some known generic settings.

## What we are looking as comments

For this RFC we are expecting comments of different types:

- if you disagree with any of the proposed defaults, let us know
- if you think another setting that is not listed here should have a different config, let us know
- if you think it's not clear when a code smell can be skipped and you have some examples from public projects, we can try to discuss and improve the guidelines on when to skip them with links
- if you think any other common rails directory should have different rules, let us know
