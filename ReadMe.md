Assignment: Code complexity, coverage

1  Goal

In this assignment, you will experiment with complexity and coverage metrics. The goals are to get an understanding and appreciation of the benefits and drawbacks of metrics and their tools, and to create new test cases or to enhance existing tests that improve statement or branch coverage. You will perform these tasks on an open-source project of reasonable size and complexity (see below).

Deliverables

You will fork or clone the source code repository of the project of your choice, and perform modifications there. The URL of the cloned repository will be submitted on Canvas. You can use the report template from Canvas. You are free to adapt it or use a different format as long as you cover the same content. The report is uploaded as a file.

2  Open source metrics tools

We recommend [lizard ](https://pypi.org/project/lizard/)as tool to measure metrics. It supports

- C/C++ (incl. C++14), • Swift, • Scala,
- Java, • Python, • GDScript,
- C# (C Sharp), • Ruby, • Golang,
- JavaScript (ES6 and JSX), • TTCN-3, • Lua,
- Objective-C, • PHP, • Rust.

The [github repository ](https://github.com/terryyin/lizard)of the project has the latest version, but we recommend using the latest stable release. The program has a simple command line interface, which gives you an immediate overview of key metrics such as NCLOC (non-comment lines of code) and CCN (cyclomatic complexity number).

If you are using a programming language that is not supported by lizard and for which you cannot get a measurement tool, you can use the command “wc -l” to count the lines of code (incl. comments) per file.

Open source coverage measurement tools

Several [code coverage tools for Java ](https://en.wikipedia.org/wiki/Java_Code_Coverage_Tools)are available. A shortlist:

- [Cobertura: ](https://cobertura.github.io/cobertura/)Support for ant, command line, maven.
- [OpenClover: ](http://openclover.org/)Support for ant, maven, grails, Eclipse, IntelliJ.
- [jacoco:](https://www.jacoco.org/jacoco/) Integrated with Eclipse.

For Python, we recommend [Coverage.py. ](https://coverage.readthedocs.io/)For gcc users, [gcov ](https://en.wikipedia.org/wiki/Gcov)is well integrated with the compiler itself.

3  Tasks
1. Part 0: Project choice

Choose a project, or a module of a project, written in a programming language you would like to work with. We will only consider code written in that language. Use an open source project which

- uses an [open source initiative-approved license;](https://opensource.org/licenses)
- uses automated unit or system testing on the part written in your language of choice;
- existing branch coverage (by the given tests) must be clearly less than 100%;
- has at least two contributors outside your own course group;
- the programming language must be a Turing-complete language, not a markup language; and
- has at least 10,000 lines of code (10K LOC); this applies to the programming language you are using, as counted by “ cloc”; files in other languages than the one you use do not count.

Please register your project in the project sheet (see Canvas for the link). At most three groups should work on the same project, to avoid overburdening the community! If four or more groups end up choosing the same large project, you can choose different sub-modules, as long as they are larger than 10K lines each.

2. How to find a project

Note: Before you dive in deep, ensure that the project fulfills the requirements of this lab! The links below

are just suggestions. Lists of projects may also include projects that are not suitable for this assignment; you are free to use your own choice as long as the criteria above are fulfilled.

1. Choose a project you are using yourself (e.g., a program or library).
1. Choose from a [list of beginner-friendly projects. ](https://github.com/MunGell/awesome-for-beginners)Note: A lot of these projects are too small for this assignment, so count the lines of code first before you start!
1. Choose an [Apache project. ](https://projects.apache.org/)Choose from t[his list. ](https://docs.google.com/spreadsheets/d/1D9YABkqNUk1KT95x1zv69dwqMvjnnLePS0kIZK8j05g/edit?usp=sharing)Note that these projects have not been fully vetted for test automation, so please ensure you can automatically run all necessary tests.

Other suggestions:

- [NASA Open Source: ](https://code.nasa.gov/)over 350 space-related open source projects (not all of which are big/active enough to be suitable!), using different programming languages.
- [LyX,](http://www.lyx.org/) a document editor with a LaTeX back-end (C++ with GUI).
- [RTEMS, ](https://www.rtems.org/)a light-weight real-time OS (C). Warning: This is a difficult project because it requires building the whole cross-compilation tool chain itself from scratch.
- [Wesnoth, ](http://wesnoth.org/)a turn-based strategy game (mostly C++, some Lua).
3. Onboarding

How good is the “onboarding” documentation?

1. How easily can you build the project? Briefly describe if everything worked as documented or not:
1) Did you have to install a lot of additional tools to build the software?
1) Were those tools well documented?
1) Were other components installed automatically by the build script?
1) Did the build conclude automatically without errors?
1) How well do examples and tests run on your system(s)?
2. Do you plan to continue or choose another project?
4. Part 1: Complexity measurement

Run a complexity measurement tool such as lizard on the code base. If you cannot find a tool for your platform, run “wc -l” to measure the lines of code per file, and count the lines of code for some large functions using a text editor.

Count the [cyclomatic complexity ](https://en.wikipedia.org/wiki/Cyclomatic_complexity)of large functions of the code (not necessarily the largest ones, in case you cannot sort them automatically by size). Exclude third-party code and generated code in this. If you have a tool, list ten (10) functions or methods with high complexity. In addition to that (or if you have

no tool), count the cyclomatic complexity of five complex functions by hand, either by choosing five out of the ten functions shown by the tool, or, if no tool was available, five functions that appear to be complex.

Note: This document assumes your group has five members; if your group is smaller, total numbers scale

with the group size: 8 functions with four active group members, or six with three active members.

Note: Use at least two group members to count the complexity separately, to get a reliable results. Use a

third member if the two counts differ.

1. What are your results? Did everyone get the same result? Is there something that is unclear? If you have a tool, is its result the same as yours?
2. Are the functions/methods with high CC also very long in terms of LOC?
2. What is the purpose of these functions? Is it related to the high CC?
2. If your programming language uses exceptions: Are they taken into account by the tool? If you think of an exception as another possible branch (to the catch block or the end of the function), how is the CC affected?
2. Is the documentation of the function clear about the different possible outcomes induced by different branches taken?
5. Part 2: Coverage measurement & improvement

Identify one or two code coverage tools that work for your platform and use them on your chosen project.

1. Task 1: DIY

Implement branch coverage by manual instrumentation of the source code for five functions with high cyclomatic complexity. Use a separate development branch or repo for this, as this code is not permanent. The simplest method for this is as follows:

1. Identify all branches in the given functions; assign a unique number (ID) to each one.
1. Before the program starts (before the first instruction in “main” or as the first step in the unit test harness), create data structures that hold coverage information about specific branches.
1. Before the first statement of each branch outcome (including to-be-added “else” clauses if none exist), add a line that sets a flag if the branch is reached.
1. At the end of the program (as the last instruction in “main” or at the end of all unit tests), write all information about the taken branches taken to a file or console.

Note: It is perfectly fine if your coverage tool is inefficient (memory-wise or time-wise) and its output may

be hard to read. For example, you may allocate 100 coverage measurement points to each function, so you can easily divide the entries into a fixed-size array.

1. What is the quality of your own coverage measurement? Does it take into account ternary operators (condition ? yes : no) and exceptions, if available in your language?
1. What are the limitations of your tool? How would the instrumentation change if you modify the program?
1. If you have an automated tool, are your results consistent with the ones produced by existing tool(s)?
2. Task 2: Coverage improvement

In the five functions with high cyclomatic complexity, what is the current branch coverage? Is branch coverage higher or lower than in the rest of the code (if you have automated coverage)?

Keep a record (copy) of your coverage before you start working on new tests. Furthermore, make sure you add the new tests on a different branch than the one you used for coverage instrumentation.

Having identified “weak spots” in coverage, try to improve coverage with additional test cases.

1. Identify the requirements that are tested or untested by the given test suite.
1. Document the requirements (as comments), and use them later as assertions.

3

3. Create new test cases as needed to improve branch coverage function directly? Can you expand on existing tests? Do you h system (as public methods) to make it possible to set up test d
3. If you have 100 % branch coverage, you can choose other func may cover all branches in a function, but what does this mean f the existing tests by hand and check how they cover the branch

in the given functions. Can you call the ave to add additional interfaces to the ata structures?

tions or think about path coverage. You or the combination of branches? Consider

es (in which combinations).



3. Task 3: Refactoring plan

Is the high complexity you identified really necessary? Is it possible to split up the code (in the five complex functions you have identified) into smaller units to reduce complexity? If so, how would you go about this? Document your plan.

4. Task 4: Self-assessment

Assess your way of working (p.58 in the [Essence standard ](https://www.omg.org/spec/Essence/1.2/PDF)v1.2) by evaluating the checklist on p.60: In what state are you in? Why? What are obstacles to reach the next state? How have you improved during the course, and where is more improvement possible?

4  Grading criteria
1. Pass (P)
1. You provide a coherent account of your onboarding experience.
1. You identify ten functions/methods with high complexity, and document the purpose of them, and why the complexity should be high (or not).

You also manually count the complexity of five functions (on paper or as comments).

3. You clearly describe how to refactor five complex functions into smaller functions.
3. You create a working ad-hoc coverage tool that at least measures coverage of normal branches (if, while) for five functions.
3. Each group member writes at least two new tests that improve coverage, as evidenced by the coverage tool. All tests have at least one meaningful assertion (other than “assert(true)” or equivalent).
3. You provide a coherent account of your self-assessment according to the Essence standard.

4.1.1 Presentation In the grading session, the group has to

- present some of the complex functions in the grading session,
- show complexity metrics and explain their ramifications, and
- show coverage before and after the new tests (measured by external tools and their own tool).

Furthermore, the coverage measurement implementation and some of the new test cases will be inspected.

2. Pass with distinction (P+)

Note: It is possible to achieve a P+ individually in this project, as long as the whole group passes the

assignment. In this case, the points below apply individually. Use “Assignment #3, extra coverage” to submit your solution, and leave a comment on Canvas or in the statement of contributions.

4.2.1 3 out of these 5 points:

1. Each group member writes at least four new or enhanced unit tests (twice as many as for P).
1. You use your issue tracker and systematic commit messages to manage your project.
1. You carry out some of Task 3: you refactor at least two of the functions (per group member) with high cyclomatic complexity to reduce it by at least 35 % (for example, by splitting the functions).
1. You get a patch with new tests or a refactoring accepted. Note: the patch must be submitted by the assignment deadline, but it may be accepted later; as long as it is accepted by the end of the course, this point is counted. (Please notify us if this extra point is necessary for a P+.)

4

5. Something else that is extraordinary, at the discretion o
5  Ethics

Recall that the student code of conduct forbids any kind of pl based on content taken on the internet.

f the examiner.

agiarism, between groups in the course, or

