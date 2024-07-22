The book is around 400 pages, 17 chapters

*Chapter List*
1. Clean Code
2. Meaningful Names
3. Functions
4. Comments
5. Formatting
6. Objects & Data Structures
7. Error Handling
8. Boundaries
9. Unit tests
10. Classes
11. Systems
12. Emergence
13. Concurrency
14. Successive Refinement
15. J-Unit Internals
16. Refactoring `SerialDate`
17. Code-Smells and Heuristics

# Chapter 1: Clean Code
- Makes an interesting note on how people want machines to do what they *want* not what they *say* because communication is fundamentally imperfect
- Talks a bit about how being rushed --> more hacky code --> harder to maintain and build on --> increase dev time --> increased pressure --> loop
- Talks a bit about "The Grand Redesign in the Sky" and seeing some similarities here to our own redesign process (re: maintaining current system, building on old and new system, unable to transition until new system has 100% utility parity)

## Attitude
- "Why does good code rot so quickly into bad code? We have lots of explanations for it."
	- "We complain that requirements changed in ways that thwart the original design. We bemoan the schedules that were too tight to do things right. We blather about stupid managers and intolerant customers and useless marketing types … but the fault is not in our stars, but in ourselves..."
	- "The managers look to *us* for the information they need to make promises and commitments... They may defend the schedule and requirements with passion; but that's their job. It's your job to defend the code with equal passion."

## What Actually Is Clean Code
- Bjarne Stroustrup, Inventor of C++
	- "Clean code is *focused*. Each function, class, and module exposes a single-minded attitude that remains entirely undistracted and unpolluted by the surrounding details."
	- "Bad code *tries to do too much*, has muddled intent, and has *ambiguity* of purpose."
- Grady Booch, author of Object Oriented Analysis & Design with Applications
	- Similar definition, but add this notion of readability
- Dave Thomas, founder of OTI
	- Adds "can be read and enhanced by a developer other than its original author"
	- Adds "has unit and acceptance tests"

## We Are Authors
- Talks about how, when you really think about development workflows on most tasks, you're spending far more time reading than writing, easily 10x more time reading
	- "Because that ratio is so high, we want reading the code to be easy, even if it makes the writing harder"
	- "Of course, there's no way to write code without reading it, thus making it easier to read actually makes it easier to write"

## The Boy Scout Rule
- "Leave the campground cleaner than you found it" --> Apply this to your codebase

## Prequels & Principles
- He notes that this book is sort of a "prequel" to his 2002 book Agile Software Development: Principles, Patterns, and Practices
- Notes that there will be some references to...
	- SRP :: Single-Responsibility Principle
	- OCP :: Open-Closed Principle
	- DIP :: Dependency-Inversion Principle
	- "and others... described in depths \[in the other book\]"

## Chapter 2: Meaningful Names
Two Examples -- Same Logic -- Consider the impact of variable naming

Original, Rough Example
```java
public List<int[] getThem> getThings() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x: theList)
		if(x[0] == 4)
			list1.add(x)
	return list
}
```

What could be improved here?
- We don't get much of a transparent understanding of the values in `theList`
- What is the significance of the 0th element?
- What is the significance of the value `4`?
- How is one expected to use the list being returned?

Same Example :: Clearer Naming
```java
public List<int[]> getFlaggedCells() {
	final int STATUS_VALUE = 0;
	final int FLAGGED = 4;
	
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell: gameBoard)
		if(cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell)
	return flaggedCells
}
```

In this case, 
- We've added some constants to help avoid "magical numbers"
- Swapping `x` to `cell` helps us keep aware of what our iterator is representing
- We could probably improve things even more by adding a small class for cells that helps us better reveal the intention of the logic that checks if something is flagged

Same Examples :: Now Benefitting From Class Mechanics
```java
public List<Cell> getFlaggedCells() {
	final int STATUS_VALUE = 0;
	final int FLAGGED = 4;
	
	List<Cell> flaggedCells = new ArrayList<Cell>();
	for (Cell cell: gameBoard)
		if(cell.isFlagged())
			flaggedCells.add(cell)
	return flaggedCells
}
```

## Avoiding Disinformation
- Be intentional on if you're including special terms in your variable names
	- If you're calling something `petList`, is sure as hell better be of type `List`
- "Beware of using names which vary in small ways. How long does it take to spot the subtle difference between"
	- `XYZControllerForEfficientHandlingOfStrings`
	- `XYZControllerForEfficientStorageOfStrings`
	- keeping in mind that, especially if appearing a bit further from each other, they start and end similarly and, when parsing, have very similar shapes

## Pronounceable, Meaningfully-Varied Names
- If you have similar variables, `a1` and `a2` is abysmal
	- `ProductData` and `productInfo` aren't much better
- Minor variations like that are referred to adding *Noise Words* 

## Use Searchable Names
left off at the bottom of page i53 // 22