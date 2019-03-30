This month, I will read [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) book and I will share the summary of each section here.

The book is consisting of 19 chapters and this post is the summary of first and second chapters.

### Chapter 1: Clean Code

- **Do we know what mess is?**
 
 If you have 2+ years of experience as a software developer, then you have probably encountered with a situation that you can't manage new changes since someone created a messy code. This type of situations decrease productivity of you and your team's as well.
 
The only way to make deadline -the only way to go fast- is to keep code as clean as at all times.

Being able to recognize clean code from dirty code does not mean that we know how to write clean code!

A quote from Ron Jeffries; "I focus mostly on duplication. When the same thing is done over and over, it’s a sign that there is an idea in our mind that is not well represented in the code. I try to figure out what it is. Then I try to express that idea more clearly."

 Indeed, the ratio of time spent reading vs. writing is well over 10:1.
We are constantly reading old code as part of the effort to write new code.
Because this ratio is so high, we want the reading of code to be easy, even if it makes the writing harder. Of course there’s no way to write code without reading it, so making it easy to read actually makes it easier to write.

It’s not enough to write the code well. The code has to be kept clean over time. 
The Boy Scouts of America have a simple rule that we can apply to our profession.
Leave the campground cleaner than you found it.5
If we all checked-in our code a little cleaner than when we checked it out, the code simply could not rot.

Books on art don’t promise to make you an artist. All they can do is give you some of the tools, techniques, and thought processes that other artists have used. So too this book can- not promise to make you a good programmer. It cannot promise to give you “code-sense.” All it can do is show you the thought processes of good programmers and the tricks, tech- niques, and tools that they use.

### Chapter 2: Meaningful Names

**Use intention-revealing names**

Choosing good names takes time but saves more than it takes.
The name of a variable, function, or class, should answer all the big questions. It should tell you why it exists, what it does, and how it is used.

```java
int d; // elapsed time in days
```
The name `d` reveals nothing. We should choose a name that specifies what is being measured and the unit of that measurement:

```java
int elapsedTimeInDays; 
int daysSinceCreation;
int daysSinceModification; 
int fileAgeInDays;
```
Why is it hard to tell what this code is doing? There are no complex expressions..

```java
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
			list1.add(x);
	return list1;
}
```

The problem isn’t the simplicity of the code but the implicity of the code. The code implicitly requires that we know the answers to questions such as:

1. What kinds of things are in `theList`?
2. What is the significance of the zeroth subscript of an item in `theList`?
3. What is the significance of the value `4`?
4. How would I use the list being returned?

The answers to these questions are not present in the code sample, but they could have been. Say that we’re working in a mine sweeper game. We find that the board is a list of cells called theList. Let’s rename that to gameBoard.

Each cell on the board is represented by a simple array. We further find that the zeroth subscript is the location of a status value and that a status value of 4 means “flagged.” Just by giving these concepts names we can improve the code considerably:

```java
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	return flaggedCells;
}
```


Notice that the simplicity of the code has not changed. It still has exactly the same number of operators and constants, with exactly the same number of nesting levels. But the code has become much more explicit.

We can go further and write a simple class for cells instead of using an array of ints. It can include an intention-revealing function (call it `isFlagged`) to hide the magic num- bers. It results in a new version of the function:

```java
public List<Cell> getFlaggedCells() {
	List<Cell> flaggedCells = new ArrayList<Cell>();
	for (Cell cell : gameBoard)
	if (cell.isFlagged())
		flaggedCells.add(cell);
	return flaggedCells;
}
```

With these simple name changes, it’s not difficult to understand what’s going on. This is the power of choosing good names.

**Make Meaningful Distinctions**

If names must be different, then they should also mean something different.

Imagine that you have a `Product` class. If you have another called `ProductInfo` or `ProductData`, you have made the names different without making them mean anything different. `Info` and `Data` are indistinct noise words like `a`, `an`, and `the`.

**Use Pronounceable Names**

From

```java
class DtaRcrd102 {
private Date genymdhms;
private Date modymdhms;
private final String pszqint = "102";
}
```

to

```java
class Customer {
private Date generationTimestamp;
private Date modificationTimestamp;
private final String recordId = "102";
}
```
Intelligent conversation is now possible: 
> Hey, Mikey, take a look at this record! 
> The generation timestamp is set to tomorrow’s date! How can that be?

**Use Searchable Names**

The intentionally named code makes for a longer function, but consider how much easier it will be to find `WORK_DAYS_PER_WEEK` than to find all the places where `5` was used and filter the list down to just the instances with the intended meaning.

**Interfaces and Implementations**

 Say you are building an `ABSTRACT FACTORY` for the creation of shapes. This factory will be an interface and will be implemented by a concrete class.
 
 What should you name them? `IShapeFactory` and `ShapeFactory`? The preceding `I`, so common in today’s legacy wads, is a distraction at best and too much information at worst. I don’t want my users knowing that I’m handing them an interface. I just want them to know that it’s a `ShapeFactory`. So if I must encode either the interface or the implementation, I choose the implementation. Calling it `ShapeFactoryImp`, or even the hideous `CShapeFactory`, is pref- erable to encoding the interface.
 
