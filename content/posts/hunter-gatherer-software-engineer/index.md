---
title: Hunter-gatherer software engineer
date: 04-03-2023
cover:
  image: oracle-temet-nosce-sign.png
  alt: Temet nosce - know thyself - the Oracle's sign in The Matrix movie
  caption: Temet nosce - know thyself - the Oracle's sign in The Matrix movie
  relative: true
---

#### Introduction

Before we start talking strictly about software engineering, let's talk about ourselves as humans from the perspective of evolution, as I believe there are some behaviors we share with our ancestors, which strongly affects the way we work today. I believe we should be aware of our evolutionary legacy and conciously act in harmony with them to make our work easier and be more productive.

According to [Wikipedia](https://en.wikipedia.org/wiki/Hunter-gatherer), humans started hunting and gathering around 1.8 million years ago and mostly ended around 10,000 years ago. From the evolution point of view, this 10,000 years which has passed was likely not enough to cause significant changes in human anatomy or behaviors, as for example present-day brain shape has only been reached around [35,000 years ago](https://www.science.org/doi/10.1126/sciadv.aao5961#:~:text=Our%20data%20show%20that%2C%20300%2C000,100%2C000%20and%2035%2C000%20years%20ago.). Taking this into account, I think understanding how hunter-gatherer humans lived and behaved thousands of years can help explain some of our present behaviors, which we will explore. This topic has also been mentioned many times in ["Sapiens: A Brief History of Humankind"](https://en.wikipedia.org/wiki/Sapiens:_A_Brief_History_of_Humankind) book by Yuval Noah Harari.

Of course characteristics mentioned here do not only affect software engineering but everything we do in life.

#### Working memory

There has been many studies, as reviewed in article ["Up to the magical number seven: An evolutionary perspective on the capacity of short term memory"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8113705/), which explores human cognition from the perspective of capacity of short term (or working) memory. The studies show, that human brain can hold and reason about very limited number of different information chunks. The number of chunks one can handle is usually between 5 and 9, sometimes stated as mentioned above 7, but sometimes even limited to just 5 elements.

To give you an example of information chunks, let's try to solve a [child logic puzzle](https://logiclike.com/en/logic-puzzles) below in memory, so without taking any notes etc.:

> Charlie and Oleg are brothers.
> Each of them has two sisters.
> How many children are there in their family?

At first, we can see that we get 2 chunks of information: "Charlie and Oleg are brothers." and "Each of them has two sisters.", followed by a question for a conclusion we should make. We can try breaking it down further into something like:
- Charlie and Oleg are brothers.
- Charlie has two sisters.
- Oleg has two sisters.

Even if we count an intermediate conclusion, that both sisters of Charlie and Oleg should be the same children, this is still not a difficult puzzle to solve. This low difficulty comes exactly from the small number of elements we have to consider.

This puzzle may stil be hard to solve, for example for small children or who can't count, but it remains simple because of way it's structured.

#

Now, let's have a look at the puzzle on the opposite side of the spectrum, a classic [Zebra Puzzle](https://en.wikipedia.org/wiki/Zebra_Puzzle). And remember, try to solve it by only using your memory:

> 1. There are five houses.
> 2. The Englishman lives in the red house.
> 3. The Spaniard owns the dog.
> 4. Coffee is drunk in the green house.
> 5. The Ukrainian drinks tea.
> 6. The green house is immediately to the right of the ivory house.
> 7. The Old Gold smoker owns snails.
> 8. Kools are smoked in the yellow house.
> 9. Milk is drunk in the middle house.
> 10. The Norwegian lives in the first house.
> 11. The man who smokes Chesterfields lives in the house next to the man with the fox.
> 12. Kools are smoked in the house next to the house where the horse is kept.
> 13. The Lucky Strike smoker drinks orange juice.
> 14. The Japanese smokes Parliaments.
> 15. The Norwegian lives next to the blue house.
>
> Now, who drinks water? Who owns the zebra?
>
> In the interest of clarity, it must be added that each of the five houses is painted a different color, and their inhabitants are of different national extractions, own different pets, drink different beverages and smoke different brands of American cigarets [sic]. One other thing: in statement 6, right means your right.

You can probably immediately see here that this riddle is much more complex than the last one. Once we start drawing intermediate clues, the amount of information becomes incredibly overwhelming.

Now, if we start looking for reasons why our brain behaves like this, in the previously linked article, we can fragments mentioning, that during hunting there is no time for considering large amount of information and ability to make optimal decisions with small number of samples can be a deciding factor in a life-and-death situation, both for a hunter and a prey. Imagine that you are a hunter and you run through the forest to catch a goat running away. Around you is a waterfall, mud, trees, sticks on the ground and a goat. Making an optimal decision on which path to take to catch an animal in such situation can make a difference between falling of a cliff and having a decent dinner.

#

Great, but how all of this is even remotely related to software engineering? Well, let's have a look into some code puzzles then.

> How would you name a function containing following piece of code?
> ```go
> if version == 4 {
>   if blockSize < 20 || blockSize > 32 {
>	  log.Errorf("Invalid blocksize %d for version %d", blockSize, version)
>	  utils.Terminate()
>   }
> } else if version == 6 {
>	if blockSize < 116 || blockSize > 128 {
>	  log.Errorf("Invalid blocksize %d for version %d", blockSize, version)
>	  utils.Terminate()
>	}
> } else {
>	log.Errorf("Invalid ip version specified (%d) when validating blocksize", version)
>	utils.Terminate()
> }
> ```
> Code taken from [Project Calico](https://github.com/projectcalico/calico/blob/b8323b2ffec48ecdc7a326bfeb8abff7b30ea00a/node/pkg/lifecycle/startup/startup.go#LL637-L651C3).

If we extract some information from it, we get:
- We operate on a block size and a version.
- Version can be either 4 or 6.
- Version 4 can have block size between 20 and 32.
- Version 6 can have block size between 116 and 128.
- Other parameters from ones described above are invalid.

If we attempt to name this function, original name `validateBlockSize` or it's variant will probably be an acceptable answer.

And now, let's have a look into more complex one:

> How would you name a function containing following piece of code?
> ```go
> sshConfig := &ssh.ClientConfig{
> 	Auth:            e.authMethods,
> 	Timeout:         e.timeout,
> 	User:            e.user,
> 	HostKeyCallback: ssh.InsecureIgnoreHostKey(), // nolint:gosec
> }
>
> address := fmt.Sprintf("%s:%d", e.host, e.port)
>
> output, executionError, err := executeSSH(sshConfig, address, e.command)
>
> // If no error occurred or execution error occurred and we are told to ignore it, just return the result.
> if err == nil || (err != nil && executionError && e.ignoreExecuteErrors) {
> 	return output, nil
> }
>
> // If error occursed and we are told to not retry, return the error.
> if err != nil && !e.retry {
> 	return nil, fmt.Errorf("execution error: %w", err)
> }
>
> start := time.Now()
>
> // Try again until we timeout.
> for time.Since(start) < e.retryTimeout {
> 	output, executionError, err = executeSSH(sshConfig, address, e.command)
> 	// If command executed successfully, we can finish.
> 	if err == nil {
> 		break
> 	}
> 	// Wait specified interval between attempts.
> 	time.Sleep(e.retryInterval)
> }
>
> // If command returned error, check if we can tolerate it.
> if err != nil && !(executionError && e.ignoreExecuteErrors) {
> 	return nil, err
> }
>
> return output, nil
> ```
> Taken from [terraform-provider-sshcommand](https://github.com/invidian/terraform-provider-sshcommand/blob/a7e459c6ddd5401a173986f434b54e7e314e799a/sshcommand/ssh_executor.go#L72).

If we start extracting individual chunks of information out of it, we again quickly get a pretty large list of facts we have to consider while naming this block of code. The original name for this function is `execute`, which I think very poorly describes what is actually happening inside it, as there are various error handling flows, retries, timeouts etc.

#

From the few specific behaviors I describe here, I think this one has the biggest impact on (software) engineering work, as when we create and maintain software, it is crucial to be able to reason about it to make concious decisions how it changes.

https://www.youtube.com/watch?v=LKtk3HCgTa8

https://logiclike.com/en/logic-puzzles

https://www.rd.com/article/einsteins-riddle-solve-it/



#### Sleeping on a problem

https://www.youtube.com/watch?v=f84n5oFoZBc

#### Conserving energy

#### Favoring short term gains and instant gratification

- Thinking, Fast and Slow

- Dopamine effect?

