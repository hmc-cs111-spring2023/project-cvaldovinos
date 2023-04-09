# Design notebook entry

## Last week's critique

Fill in this part with a summary and reflection on the critique you received for
last week's work. Answer questions such as:  How, specifically, did the feedback help
improve the project? Did the feedback point out or offer something you hadn't considered?
Did it help you make a design decision? Was it helpful in addressing the most pressing
issues in your project? How will you incorporate the feedback into your work? Will you
change something about the design, implementation, or evaluation as a result?

I will be replying directly to two comments from the critique on last week's work:
"Did you end up creating a prioritized list of features? If so, that could be a good thing to include / link to in the notebook!"

I had not yet formalized my prioritize list of features so that was where I began my work this week. In doing so, I realized that I am likely going to be able to incorporate more of the features from my list than I had originally anticipated. This made it very useful for me to have a clear image of where I am along the plan I originally outlined in my project contract.

"I would work both sides and meet in the middle. I think you already have a strong base for the back end using the numpy library. Now you can start working on the front side. Mapping out examples of what your language might look like building a test file for such and starting to build methods that link from parts of your language to parts of the numpy library. This will give you a great start on what you will need for your parser as well as simplify the needs of your parser."

This feedback was in response to my question on how to get started with implementing my external DSL. I had not had experience doing so from scratch and thus I was intimidated by getting started but this feedback was good to get a better understanding of how to approach the task. 

Additionally, Prof. Ben had a discussion with me and said that the language design flow would likely be something like the following:

Concrete syntax -----Parse-----> Intermediate Representation -----Evaluator-----> numpy

This was very useful and much clearer on what I needed to do to get started because while I had ideas of each step, for how I wanted the syntax to generally look and how I would generally be using the numpy library, I had yet to formalize any of that plan (i.e. building the bridge between the two). After this discussion, I immediately began with step 1 and I formalized some concrete examples of syntax I would like to allow users to implement.

## Description

Fill in this part with information about your work this week:
important design decisions, changes to previous decisions, open questions,
exciting milestones, preliminary results, etc. Feel free to include images
(e.g., a sketch of the design or a screenshot of a running program), links to
code, and any other resources that you think will help clearly convey your
design process.

After the Monday discussion, I began my work for the week by generating my list of possible functionality to implement.

List of functionality to implement (in order of priority):
1. FV
2. PV
3. NPV
4. IRR
5. Arithmetic operations (+,-,*,/) between functions. i.e. allowing users to say NPV(7%,[100,200]) + NPV(5%,[200,400])
6. Assignment to variables. i.e. allowing users to say x = NPV(7%,[100,200])
7. PMT
8. RATE
9. NPER

The first few are various functions I would like to implement and have users call, then if I can do so successfully, I would like to work on some functionality which is more similar to programming, like allowing operations between the types of results and assignment of them to variables. Finally, if I am able to do both of those and have extra room for design, I would continue by implementing some of the less common functions which may have a bit more complexity in their implementation. While there is more detail in what each of these items require, like aliases for these functions and other design considerations. Those are described in the prototyping I have done which is part of the next thing I worked on this week.

On Wednesday in our studio session, Prof. Ben provided me some advice for implementing an external DSL and the roadmap which can be seen below:
<IMAGE OF ROADMAP>

This discussion was very helpful and highlighted the importance of having a set of clear examples for the syntax I want to allow in my DSL. Thus I began working on examples for my first few planned functions. For each function, I described a use case, what it looks like to perform that operation with the numpy_financial library, and then I created examples of what the user may be able to type in the DSL, this included some examples I thought were easy and reasonable to design, and some which were a bit more like natural language and hence would be a stretch goal as they are not crucial. These design decisions and the accompanying examples produced can be seen on the following [file](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/main/examples-ideal.txt).

Then on Friday and Saturday I began designing a parser uses regex to convert the user's input into an intermediate representation which I can use with an evaluator to call the desired functions in the numpy_financial library.

You can now run the code and enter a sentence and get the given values (i.e. the inputs to the numpy function) and then the function name you provided (i.e. the numpy function to be used).

The program can be run using instructions on the following [file](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/main/main.py).

The parser can be accessed at the following [link](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/main/finParser.py).

I also wrote test cases to ensure that as I change my regex patterns. Since my natural language design will be allowing for various methods of inputting the same calculation, there are many example use cases and I need to ensure that implementing a new one does not negate a prior one so having these tests was easier than manually running each example. The test cases can be viewed and run with the instructions on the following [link](https://github.com/hmc-cs111-spring2023/artifact-cvaldovinos/blob/main/test.py).



## Questions

**What is the most pressing issue for your project? What design decision do
you need to make, what implementation issue are you trying to solve, or how
are you evaluating your design and implementation?**

I now need to work on the evaluator for my DSL. While I can parse input sentences and extract the given values and the function being called, there is still a lot of work left to ensure that this information can be transformed into the calculation which will be performed with the numpy financial library and yield the values which the user will be returned.

**What questions do you have for your critique partners? How can they best help
you?**

I do not have any direct questions for my critique partners at the time, since I think my parser is mostly complete and now I just need to get started on the evaluator.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the work?**

I spent approximately 8-9 hours this week on the project.

**Compared to what you wrote in your contract about what you want to get out of this
project, how did this week go?**

This week went very well relative to the plan from my contract. While I was more behind than I had realized last week, since I only had one "end of the bridge" in the exploration of the numpy library and I had not actually formally defined my syntax yet, I was able to do so successfully and I began building the bridge to the point where I reached the intermediate representation, which effectively places me "halfway". I would like to have built a working evaluator by next week for at least one of the highest priority functions, because that is the last unclear aspect of my language design and once I have done so I can repeat the same for other functions and do some cleaning up of my language in the form of error handling and testing of the evaluation.