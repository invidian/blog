---
title: Simple, complex, easy and hard (difficult)
date: 22-03-2023
---

I believe the purpose of engineering, including software engineering, is to help people with their problems and to improve their lives. Developed solutions should bring as much benefit as possible with as little burden as possible. And while many engineering fields are regulated to ensure safety, software engineering still mostly remains a wild west, where quality varies a lot, depending on a project, product or company, often because of time constraints, ever-growing demand or constant influence of new, not experienced enough developers.
Because of limited quality, people are affected by bugs or outages every day, regardless if they are aware of this or not. Website pop-ups which cannot be closed, confusing error messages, applications suddenly crashing, confusing validation rules etc., the list could go on. I'm sure anybody working with software every day can recall something which was not working in the past week.

Putting more effort into the quality of created software would definitely help reduce the amount of these kinds of errors, but with constant pressure of time, it might be difficult to achieve, especially that there are a lot of different software qualities, which can be considered beneficial and selecting on which to focus is generally not easy.

Testing, documentation, cohesion, ease of use, security, connascence, the list could go on and on. Over time, I plan to discuss as many important software qualities as possible, highlight their costs and benefits, describe best practices while working on them and propose some workflows to ensure their quality.

However, I would like to start by talking about _simplicity_ defined as below, which I believe is the single most important software quality one can achieve. I will talk about it together with commonly conflated _easiness_, as both of those terms will often be used in upcoming articles with this specific meaning described here. I believe establishing a common language by explaining certain terms will help to fully understand the meaning of upcoming posts by clarifying the intent.



I consider "simplicity" as a fundamental property of good software, a property which brings us the most benefit. WHY?
- Simplicity does not require any other traits or cannot be improved by other traits.
- Simplicity affects all others code traits.
- Lack of simplicity blocks the reasoning. Is the ability to reason the most important then?
- Simplicity enables shared understanding by enabling reasoning.
- Reasoning builds confidence.
- Shared understanding builds collective confidence.
- Shared understanding enables collaboration.
- Shared understanding is a source of human success as a race, building culture and civilisation, as it builds common believes.
- Simplicity in a described sense reduces the current working set, which makes ensuring all other software qualities easier.

Simplifying logic is reducing accidental complexity.

How do you define the simplest solution?

If simplicity is about intertwining, how do you measure using better or worse tool for solving the problem. The same problem can be solved with just functions or classes, what's the difference then? Do you measure the complexity of the tools itself? Or if the same problem can be solved in 2 different ways with flat complexity, how do you choose between them?

- It seems the answer would be that we take more dependencies than it's necessary, as e.g. class has more features than a standalone function.
- With flat complexity, I'd weight solutions by other factors, like number of components, their extensibility, reusability etc.
