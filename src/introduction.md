# Introduction

Run your Bamboo-Specs locally! Why would you want to do this? Two reasons:

- **Fast Feedback** - Rather than having to commit/push every time you want
  to test out the changes you are making to your `.bamboo-specs` files
  (or for any changes to embedded bamboo tasks), you can use `actoo`
  to run the actions locally. The environment variables are configured
  to match what Bamboo provides.

# How Does It Work?

When you run `actoo` it reads in your Bamboo-Specs from `.bamboo-specs/` and
determines the set of actions that need to be run. It uses the Docker API
to either pull or build the necessary images, as defined in your workflow
files and finally determines the execution path based on the dependencies
that were defined. Once it has the execution path, it then uses the Docker API
to run containers for each action based on the images prepared earlier.

Let's see it in action with a [sample repo](https://github.com/rjchicago/bamboo-specs-demo)!
