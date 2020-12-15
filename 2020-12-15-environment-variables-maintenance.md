# Environment Variables Maintenance Proposal

## The Problems

### Documentation

Comment by Ernesto:
> I believe we need a policy or convention for environment variables. Right now in some projects we are using this policy: If you add a new env variable, you need to document it in both .env.sample and the RELEASE_NOTES file.

### Propagation of the change

It's also hard to maintain: when you pull updates you need to verify the RELEASE_NOTES and compare that with your env variables, you may miss that something changed or that something was added.

### Different requirements for different environments

Not all environment variables are required for development or testing. Currently we have no clear documentation regarding what is optional for development (sometimes a variable inside the .env.sample needs to be removed locally instead of leaving it blank for example).

## Possible solutions

Some suggestions by Ernesto and comments on Twitter were:

### Envied

URL: https://github.com/eval/envied

Pros:
- To use this gem we need to configure the variables in a `Envfile` (which is just ruby), and then run `ENVied.require` during the app boot.
- We can add different requirements for different environments on a single file.
- This can validate many formats.
- Has a task to check the heroku config against the config file
- Documentation can be added as comments on the Envfile

Cons:
- This does NOT support optional env variables (i.e.: variables that can be undefined but if present should have a specific format)

### Prius

URL: https://github.com/gocardless/prius

Pros:
- We can configure different variables for each environment
- Supports optional variables
- Documentation can be added as comments for each variable

Cons:
- To use this gem we need to call `Prius.load(:some_var)` for all env variables we want to use (we could extract this method calls into a separated file and require that file so we don't pollute the boot files though, not that big of a deal)
- It can validate only a few types of values

### Custom made gem

We could also create a custom gem or fork any of those if we think it's worth it. The main idea is that, when adding a new env variable, we should be able to add some configuration and documentation related to that variable and check it during boot. That way we can be sure everyone will have the right env variables.

Pros:
- We would have full control on what it supports and how it's used to adapt it to our needs

Cons:
- It will take some time to get things right and it then needs to be maintained

## What these gems don't do

These gems would be used to configure which variables are needed and the format of the values but these WON'T provide default values. For that we'll keep using dotenv and the `.env` and `.env.sample` file for quick setup of defaults.
