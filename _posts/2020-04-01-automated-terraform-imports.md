---
layout: post
title: Automated Terraform Imports
categories: [Terraform]
---

I'm sure I'm not alone in having a large service that my company wants
to ingest into terraform for easier management. In theory this is
great, we get all the wonderful guarantees of terraform & the world is
right.


But reality isn't so simple, firstly, there is the process of
importing everything, how do you go through and take an inventory of
everything that already exists before even trying to capture it in a
set of terraform files. Not an easy task by any means.


Fortunately there are a few things that may be able to help you
simplify the task. The first is to look at a tool like
[terraformer](https://github.com/GoogleCloudPlatform/terraformer)
which is doing a great job of trying to capture a service's state and
dump it out into terraform for you to start managing everything.

This works great again in theory, but assumes that nobody is going to
be changing the state of the service except via terraform from that
point on, which for many of us simply isn't true.

I would love to say that I built a magical tool which with the click
of a button synchronises & updates everything until it is
'correct'.

But I can't.

I will instead show you a few tricks I cobbled together to put
together a system of 'synchronisation', and I mean this in a very
loose sense.

Let's take cloudflare as an example, you have hundreds, if not
thousands of DNS records, some dynamic, some static, some you don't
know who set them or why but you're afraid to touch them. Multiple
people are updating the records from your kubernetes cluster to the
marketing team & several external contractors who are working on a
project you have only distantly heard of.

I opted to pull down everything via the cloudflare api & store it for
processing. Once I had the raw json data for a zone, I then could
process it to strip out all dynamic logs, the advantage of dynamic
logs is they are normally pretty recognisable. Included below is a
snippet of the transformer.


```
processedData = reformatOutput(createProcessedNames(removeManagedRecords(parsedData)))


function removeManagedRecords(data) {
  var ownedRecords = data.filter((r) => {
    if (r.type === "TXT" && r.content.includes(`owner=`)) return true // external-dns
    if (r.type === "CNAME" && r.name.startsWith("auth-")) return true // auth endpoints (terraform)
    return false
  })
  
  
  ...
}
```
