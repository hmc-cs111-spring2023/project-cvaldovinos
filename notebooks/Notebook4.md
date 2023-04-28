# Design notebook entry

## Last week's critique

Fill in this part with a summary and reflection on the critique you received for
last week's work. Answer questions such as:  How, specifically, did the feedback help
improve the project? Did the feedback point out or offer something you hadn't considered?
Did it help you make a design decision? Was it helpful in addressing the most pressing
issues in your project? How will you incorporate the feedback into your work? Will you
change something about the design, implementation, or evaluation as a result?

I found two comments from last week's critique to be the most helpful to my project this week so I will address them below:

1. The first point which Brandon brought up in responding to my progress was the question of if my language is succeeding in regards to being able to cover areas which are missed by current tools in the domain. Brandon believes I have been successful in accomplishing that with my language and I would agree that I have been able to implement many of the features which I originally brought up as lacking with existing software for the domain of finance calculations. However, it is good to keep this vision in mind, and that is a part of what motivated my testing this week, as I wanted to ensure that I am not allowing users to get stuck behind errors which they may not understand as non programmers.

2. The second comment was that the test cases seemed good though it is not ideal to have someone outside of Economics/Finance look over them. While it can be helpful to get the perspective of a user of the language, I was more so aiming to get feedback from someone who is just looking at the tool for the first time so I appreciated the approval from that perspective. Additionally, this comment included discussion of arranging test cases with varying orders so I accounted for those in my test case edits this week.


## Description

Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

This week my work was focused on:
1. Adding error handling to my DSL
2. Adding test coverage to my DSL
3. Fixing any unexpected/erroneous behavior in my DSL in response to the test cases generated

I created a pull request to view all the changes I made this week which can be accessed via this [link](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/pull/2/files). However, I recognize it is not a great overview of all these changes so I will explore the changes here:

### Error Handling

To find out where my code could produce errors, I tried some statements that I thought could cause errors. Because of the implementation of my language, after doing so, I found a few points where my DSL was not accounting for behavior but it was very easy to add statements to print out to the user what they did wrong. This is because of how I parse inputs, I always check if an expression matches the regex pattern so for these cases, it was essentially always inserting else cases. There was some more edge case behavior, like if a user puts in multiple invalid inputs which I had to handle, which I decided should only print out one error as can be seen around [these lines](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/WEEK-4-progress/main.py#L37-#L48). Overall, this did not require much code to implement and there was more time spent testing the behavior than having to implement it.

### Test coverage + Fixing DSL behavior

In addition to the manual testing described above, I wanted to add unit tests to go through the many lines to verify that each step returns the expected result based upon the user's inputs. However, since much of my code is similar (regex patterns checking for many similar expressions), I wanted to ensure that I was covering each line of code I wrote. Thus, I looked to find tools which would help me do so. I have experience working with test coverage in an existing codebase but not in something I had created on my own so I took this opportunity to learn something I had been wanting to learn to do on my own and apply it to this case where I needed it. To do so, I learned about using pytest and pytest-cov to produce html showing me the exact lines being covered by my test cases. Setting this up and learning to use this tool to validate print statements took me a long time and many attempts. 

Due to this, testing was where the majority of my work was focused this week. However, I do think it was ultimately worth it as I was able to find many cases where I had not accounted for behavior and was able to fix them. Some of these were due to my error when copy + pasting the regex patterns from one expression to another where they didn't apply, and others were due to missing use cases which I had not yet tried with my prior test cases. While this took me a lot of time, likely more than it would have to manually look over my code and try these cases, it allowed me to learn to use this new tool to test code and more importantly for the project, I am significantly more confident in the behavior of my DSL as I know that each expression is being parsed accurately and that users are getting the appropriate error messages when they input invalid expressions.

I was able to get 100% test coverage for my parser. However, for my evaluator, I was only able to reach 46% test coverage because I could not find out how to test the input function in the test cases I was writing. This is the last behavior I would like to test with my unit tests but I do not think it is too crucial, as it is a minor part of the implementation and I have tested it manually. It would be better to have test cases so I do not have to worry about breaking the behavior with future changes but it won't be an issue for my DSL if I do not cover this code.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I think the most pressing issue for my project is getting a good README to accompany it. While I think that the DSL is fairly complete, expecting errors to guide users is not ideal. Especially since my target users are non-programmers, I would like to make a README which teaches them how to use the DSL and what some examples of valid inputs are. I think this will really make the DSL more accessible to these users and make the project feel like a complete product.

**What questions do you have for your critique partners? How can they best help
you?**

Do my critique partners have experience writing unit tests for calls to input in Python? I spent a long time reading responses to questions with this which suggested some imports but I was not able to get any to work so getting some interactive feedback to work through this would be helpful.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the work?**

I spent about 9 hours on the project this week.

**Compared to what you wrote in your contract about what you want to get out of this
project, how did this week go?**

Compared to what I wrote in my contract I am definitely on pace. I was able to make more progress than I expected as far as error handling and testing edge cases but I am behind on the README I hoped to complete this week. Since the project is nearly complete, I will be prioritizing it as it will be an important part of my project and once it is complete, if I have more capacity then I will add more features to the DSL and revise the documentation.