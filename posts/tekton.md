# Tekton & CICD


- fundamentally what is Tekton? & history
- what is CICD?
- what is Tekton trying to solve?
- Is Tekton a good player in the CICD space?

## The History

Tekton blah blah KNative, something something


## What is ~~CICD~~/Build Automation?

Before we can talk more about Tekton and its place in the CICD world first we need to have another look at what CICD is.
So let's start with the aim of CICD, perhaps we can even move away from CICD and focus on what we are interested in: Build Automation, I won't get into Deploy Automation as there is so much information about what the right and wrong way to go about this is.


With that out of the way, what is Build Automation? Simply put we want to automate the building of our artifacts.
Ultimately we want to enforce a set of preconditions before our artifact reaches the 'ready to publish' state, and these preconditions may have preconditions of their own.

In short; Build Automation is a set of ordered steps that, when sucessfully executed result in a final artifact. (TODO link to wiki page on Build Automation)

## What is Tekton trying to Solve?

Tekton at first glance comes across as a CICD tool following the Kubernetes ideology. But it is closer to something like Concourse a generic 'doer of things'. There are defined inputs and outputs which can be piped into tasks, and glued together to make pipelines.
This should start looking familiar, a task with a defined set of inputs and outputs, which can be composed with other tasks to achieve a thing. Isn't that just a program?

Yes! It's a glorified (simplified) YAML-based programming language (yay?). And why would you want something like this? Because pipelines need to be recognised as an important part of the software lifecycle, a critical part in many companies, and it should be treated as such, with a full language, proper abstraction and software engineering principles.

But I'm getting carried away, Tekton feels like a taste of what CICD could and should be, but it feels too clunky and challenging to use directly. There needs to be something on top to hide away all the.
