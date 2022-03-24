---
layout: post
title: "Setting an out of office during a strike period - sending replies only to the people on your university"
date: 2022-03-23
time: "20:20:00"
blog: "true"
categories: ["strikes", "university", "software"]
---

Yesterday's post ended with a question about how to send the answers only to the
people sending you emails from your university. Let's look how we can implement it!

We are starting from [the flow that we created yesterday][OoO-1] - so, if you haven't
done it yet, then start there. I'll wait for you here.

Our previous power automate wokflow looked like this:

<img height="200px" src="/gallery/images/2022/03/2022-03-23-power-automate-whole-workflow.png" />

Now, we want to introduce a condition before sending these "personalised"
replies only to senders from a particular domain, for example,
`youruniversity.ac.uk`. In programming this is call [control
flow][wiki-controlflow], in particular the conditional expression. 

```
IF some conditions happens 
  THEN do x 
  ELSE do y
```

So, in our case this could be as

```
IF the email of the sender ends by `youruniversity.ac.uk`
  THEN send a reply
  ELSE do nothing
```

Let's try to code this into our flow. First we need to think where we want to
include it. Certainly we want it after the receive email box (the trigger of the
flow) and before the "send email" action. We have two options, just after the
email is received, or after the excel spreadsheet is loaded. Since the
spreadsheet only contains the messages for when we want to send the reply, then
it makes sense to make it before that. However, if we were to also automate the
responses to external people, then we would want it after the row from the excel
file is extracted.

When editing the flow, we can add a new step by clicking in the button at the
bottom, or by clicking the plus symbol that appears when hovering in the
connectors between the steps, as shown by this image:

<img height="200px" src="/gallery/images/2022/03/2022-03-24-power-automate-add-intermediate.png" />

We are going to create a condition action before getting the excel row. Choose add
an action, and from the menu, choose Control. Inside the Control menu, pick condition.

<img height="200px" src="/gallery/images/2022/03/2022-03-24-power-automate-add-control.png" /> 
<img height="200px" src="/gallery/images/2022/03/2022-03-24-power-automate-add-condition.png" />


The flow should look like:

<img height="200px" src="/gallery/images/2022/03/2022-03-24-power-automate-flow-after-control.png" />

And by dragging and dropping the excel and send email actions into the "yes"
box, should then look like this:


<img height="200px" src="/gallery/images/2022/03/2022-03-24-power-automate-flow-after-control-drag.png" />


We've got so far the skeleton of what we want to happen.

```
1. Trigger the flow when an email is received
2. IF <condition to create> happens
     THEN
        - extract the row for today
        - send a reply with the personalised message
     ELSE
        - do nothing
```

What we are missing is to set the condition. Remember, we want to only reply
emails that comes from our own institution. Therefore, we need to look up the
address of the sender and check if the end of the email is like
`youruniversity.ac.uk`. 

To do this step, we need to fill the three fields under the condition action.
The first one is the value we want to compare. Clicking there you'll see all the
dynamic content generated from the previous action, and between these the "From"
field - i.e., the email of the sender. In the second field we are going to set
the condition. From all the options there, the simplest one for our needs is
"ends with" and the last field we set the pattern we want the address of the
sender to match. `youruniversity.ac.uk`. At the end, it should look like:


<img height="200px" src="/gallery/images/2022/03/2022-03-24-power-automate-add-condition-filled.png" />

And that's it! Now only the emails from a sender with a domain as specified in
the condition will get through the "If yes" branch and get a reply.


One more thing! Remember to turn the workflow off when you don't want to process
your incoming email. You won't be sending replies if there's not a date matched
on the spreadsheet, but we probably won't like to have some machine somewhere in
the world running these workflows once and again to fail all the times.



[OoO-1]: {% post_url /2022/03/23/2022-03-23-an-out-of-office-during-strike-period %}
[wiki-controlflow]: https://en.wikipedia.org/wiki/Control_flow
