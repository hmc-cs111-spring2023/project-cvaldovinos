# Design notebook entry

## Last week's critique

Fill in this part with a summary and reflection on the critique you received for
last week's work. Answer questions such as:  How, specifically, did the feedback help
improve the project? Did the feedback point out or offer something you hadn't considered?
Did it help you make a design decision? Was it helpful in addressing the most pressing
issues in your project? How will you incorporate the feedback into your work? Will you
change something about the design, implementation, or evaluation as a result?

In last week's notebook feedback, Brandon suggested either adding another parser or subgroups to my existing parser to extract keywords from the "inputs" and "functionName" values I was extracting.

This feedback was very helpful for completing my work from last week of creating a parser as it allows me to have properly formatted inputs into the evaluator which I began implementing this week. I incorporated a mix of both of the suggested approaches which can be seen in the addition of another parsing function called operationParser [here](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/2edcf0947fa0f9674ddbfa38cf657a9939a0dc1d/finParser.py#L39) and the inputFormatter [here](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/2edcf0947fa0f9674ddbfa38cf657a9939a0dc1d/finParser.py#L17) which uses grouping to reduce the operations into valid Python code.

## Description

Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

The work I did this week was primarily:
1. Completing the parser I started creating last week.
2. Began implementing an evaluator.

The entirety of the changes I made this week are visible on a pull request I created [here](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/pull/1/files). Though it is a lot to go through so I would only recommend looking over it broadly as below I will break down in further detail the work I did:

### Completing Parser
So I began the week by responding to the feedback provided by Brandon and I wanted to reduce the "inputs" or arguments I will be passing to from directly what the user typed in to viable Python code. To do so, I added the parsing methods already mentioned above: [operationParser](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/2edcf0947fa0f9674ddbfa38cf657a9939a0dc1d/finParser.py#L39) and [inputFormatter](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/2edcf0947fa0f9674ddbfa38cf657a9939a0dc1d/finParser.py#L17). These each required a significant amount of work because I had to create regex patterns for each of the viable expression formats I am allowing users to input these arguments. Since there were a variety of expressions for each of the valid arguments, I approached this by taking on one argument then ccreating each of the regex patterns for the viable ways of inputting that argument which I originally outlined in my design document [here](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/WEEK-3-progress/design/examples-ideal.txt).

In doing so, I got the chance to improve upon my existing code which was almost entirely under one function called `parse`. While this was an accurate name, the parser become much cleaner after extracting some of the processes to section off the functionality.

While expanding upon my existing parser, I realized there were some use cases that I had not been testing and hence were missing from my test cases, like some values including decimals and dollar signs in certain scenarios (i.e. 10.25 instead of just 10 or -$100 and $-100 both being used to express the same expression). So I accounted for these cases and added them to my parser as well as editing my test cases to include these expressions in my test file. These changes can be seen in my edited test cases [here](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/WEEK-3-progress/test.py).

However, I noticed taking the more natural language approach led to a lot of more work in the parser than I had anticipated. Thus, I am currently planning on moving on to aim to complete the existing functionality and not try to implement the other features I included in my list of potential features. This will allow me to ensure I can create a complete DSL which fully functions for the existing use cases I have been working on the past few weeks and if I have extra time afterwards assuming all goes well with my implementation of the evaluator, I will return to these features and go one by one trying to add them to the parser and evaluator and writing sufficient test cases to verify they are fully function.

I have completed my parser to obtain fully parsed inputs and have all my parser test cases generating equal outputs now matching for equivalent inputs.

### Evaluator
Once I completed my parser, I moved on to passing the fully parsed values which are strings of valid Python code into an evaluator. My goal for this week was to have my evaluator fully function for at least one of the 4 functions I am working on and I was able to achieve exactly that as I have gotten it working for the `IRR` function which can be seen [here](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/139201899ded70767a879ca020a6a751cf5c10a2/evaluator.py#L14).

While the code in my evaluator is only complete for one of the functions, the major progress was in getting through the flow for converting the parsed values into the corresponding code which I knew ultimately needed to be calling the `numpy_financial` library's `irr` function. 

One of the major issues I was struggling with was that I was unable to call it with the parsed input, and I spent far too long debugging this because I was only printing the values to compare my parsed values to the expected values and it wasn't until I printed the types of each that I realized that the parsed values were invalid because it was a string. This was specific to the cash_flows argument as that is the only one which allows the input to be an array. However, I was able to work through this and get my `irr` function working.

What remains to be done in the evaluator is still a significant amount of work. One of my design decisions is to allow users to put in arguments in any order which will require me to verify each of the expected arguments is provided. This was not something I had to consider for `irr` as it only takes in one argument, so this is one difference I will need to consider when implementing these other functions.

For the upcoming week, I plan to:
- Implement the evaluator for the remaining functions
- Add a brief README description that:
  - Describes what my language does
  - Explains the expected formats for inputs
  - Provides some example calls
- Add error handling both to the parser and evaluator so that users cannot break out of the calculator.

## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I need to implement my evaluator for the functions which allow unordered arguments. While I know this is possible, I do not yet have an approach in mind but it is crucial I get this done because I have not accounted for argument order so far and if I cannot implement this easily, it would require a large amount of work to return to my parser and reduce inputs to have to have arguments in a certain order. I fully expect to be able to do so, but it is the last "unknown" for my project so once I have this cleared up I will at least be certain that I will have a complete DSL that I can add functionality to later.

**What questions do you have for your critique partners? How can they best help
you?**

As I am starting to get to a point where I may be able to complete my current functionality I would like to make sure that my use cases make sense. I would greatly appreciate it if my critique partners could look over my test cases and provide feedback if that is a reasonable format to expect users to input calculations or if I should edit/add any cases.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the work?**

I spent about 7 hours working on the project this week.

**Compared to what you wrote in your contract about what you want to get out of this
project, how did this week go?**

This week went very well relative to my plan, I am on pace. However, I did hope to have made more significant progress on the evaluator to be able to add more functionality which I was not able to, so I hope to be able to achieve all my plans for this upcoming week so that next week I can be in a state where the project feels much more like I have developed a complete DSL which I can functionality to later.