# Find the Longest Common Prefix (LCP)

## Introduction
We are tasked with trying to find the longest common prefix within a set of strings. While there are many ways to solve this problem such as simply storing each common prefix in a separate memory location and then choosing the longest item, there is a more efficient and dynamic way of getting the solution. 

## Example
Take for instance the input: [angel, angelic, angle, angler] 
If we wanted to find the longest prefix for this problem using a more conventional method, we’d have to make N comparisons over a max word length of M in the worse case where N is the number of words in the set. Think O(N * M).
The output we’d expect for the above input is ang. 

## The Solution
Step 1: Determine general strategy to solving the problem by breaking it down into smaller problems and solving them recursively from the bottom up.

Step 2: Think about your base cases for the problem before you start tackling the recursive aspect of the problem. 

Step 3: Divide the problem up into subproblems. Since this problem deals with String sets, think about the most logical way you’d break the problem up into smaller sub problems. 

### Steps In Detail

#### Step 1

1)	Since we are working with Strings and will be coding a solution at the end, we are going to be basing the steps off pseudocode. 

2)	One way to break the problem up is to continuously split the main String set into smaller string sets by cutting it at the midpoint until you reach a point where the “low” index value is equal to the “high” index value (this indicates that the subset is only a single element). 

3)	We then work our way up recursively by returning the biggest prefix at each recursive frame until we make it back where we start
#### Step 2

There are two base cases for this problem:

1)	A truly trivial base case that checks if the starting index (low) is somehow above the end index (high) and returns an empty String in our case.

2)	Checks to see if the low value is equal to the high value, which means either there is only 1 String, or we’ve hit the bottom recursive frame.

#### Step 3

1)	The most logical way to divide the problem into smaller problems is to find the midpoint of each String set.

2)	Keep dividing until you reach the point where there is only 1 String in the array, to which the longest prefix is the String itself.

3)	Go back up recursively and use a helper method to compare two Strings at a time that have come from the success recursive returns and see where the prefix identicality ends. 


### Midpoint Splitting Process

Break the main set into smaller sets until you reach atomic sets

![Table Depicting Midpoint Splitting Process][table1]

[table1]: https://github.com/loadingthecode/InterviewQuestionGuide/blob/master/Recursion_and_Divide-and-Conquer/Finding%20the%20Longest%20Common%20Prefix%20(LCP)/Images/table1.PNG

### Recursive Process

#### Starting at the 2nd Split:

	* Angel is the only element therefore LCP = Angel

	* Angelic is the only element therefore LCP = Angelic
  
	* Angle is the only element therefore LCP = Angle
  
	* Angler is the only element therefore LCP = Angler

#### Go back up to 1st Split:
	* Compare Angel and Angelic --> LCP = Angel
	* Compare Angle and Angler --> LCP = Angle
#### Back at the original set:
	* Compare Angel and Angle --> LCP = Ang
#### Conclusion:

	* LCP of entire set is Ang	

## Midpoint Knowledge Check
Before we move on, let’s try and write a pseudocode method that takes two strings and finds the longest common prefix between them. While this method does not solve the problem entirely, having it encapsulated in a helper method will make it easier to see the divide and conquer strategy being implemented when it is called in the main method. I have outlined the method header for you:
public String LCP(String x, String y) {
. . .
}

## Pseudocode Before Code

<img src="https://github.com/loadingthecode/InterviewQuestionGuide/blob/master/Recursion_and_Divide-and-Conquer/Finding%20the%20Longest%20Common%20Prefix%20(LCP)/Images/pseudocode.PNG" width="75%">

## The Code
Base cases first!

```
		// if the low index is above the high index
		if (l > h) {
			return "";
		}
		
		// if there is only 1 string in the set
		if (l == h) {
			return strings.get(l);
		}
```

Next, find the midpoint and start the split/recursive process!

```
		// finding the middle index for splitting
		int m = midpoint(l, h);
		
		// split/recursive phase
		// similar concept to a binary search
		String a = loopLCP(strings, l, m);
		String b = loopLCP(strings, m + 1, h);
		
		// return the LCP between x and y using the helper method LCPCompare
		return LCPCompare(a, b);
		
```

Make sure to make the LCPCompare method or an equivalent implementation to compare each letter one-by-one between both Strings!

```
	// method for finding the LCP between 2 strings
	public static String LCPCompare(String a, String b) {
		
		// initialize 2 pointers at 0
		// each counter keeps track of the index for each string
		int i = 0;
		int j = 0;
		
		// keep looping until you reach the end of either string
		while (i < a.length() && j < b.length()) {
			
			// if the character at both indices are the same, increment both counters
			// else stop immediately and return the substring
			if (a.charAt(i) == b.charAt(j)) {
				i++; 
				j++;
			} else {
				break;
			}
		}
		
		String LCP = a.substring(0, i);
		
		return LCP;
		
	}
```

## Now Let’s Review!
Now that we’ve gone through finding the LCP in a dynamic programming perspective, try to apply this same thought process to a similar problem:
How can we find the Longest Common Suffix Within a Set of Strings?
Don’t write the full code implementation. Instead, just sketch out general pseudocode for your solution.

## Sources

*	https://www.techiedelight.com/find-longest-common-prefix-lcp-strings/

*	https://www.geeksforgeeks.org/longest-common-prefix-using-binary-search/

*Guide compiled by Oliver Luo*
