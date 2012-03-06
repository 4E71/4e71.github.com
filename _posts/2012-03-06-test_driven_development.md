---
layout: post
categories : intro
---

Just as I favor composition over inheritance, I favor Test Driven Development (TDD) over unit testing. If you only have time to do one or the other… TDD.

###Why?

Lately I've been using TDD on my personal projects, not as a testing methodology per se, but as a design methodology, and I like how it helps me __write less code that works__. 

As a general principle, _more code means more bugs_.

###Pump the breaks, isn't TDD the same thing as unit testing?

I assert that TDD differs from unit testing in a subtle way. It's great for producing code that "is as simple as possible, but not simpler". In contrast, unit testing shines at stress testing code and identifying scenarios that it doesn't cover. Now, should your code actually handle all the multi-varied scenarios that tools like Pex exposes?

It depends. 

###What? 

Developers should exercise good judgement and determine where they should focus their efforts. For example, in my experience, developers who create LOB applications generally have great control over how application logic is used. As such, the logic doesn't necessarily have to handle all unlikely edge cases. This doesn't mean that code shouldn't fail gracefully when it hits an expected failure point, e.g., losing database connectivity. What this suggests is that developer time may be better spent building features or working on other value-add activities (like making the app faster!) instead of writing more code to handle unlikely scenarios. Again, __more code == more bugs__. 

###Where do we go from here?

I suggest using TDD to write the simplest code as possible to achieve the desired result and then use tools like Pex to highlight the possible failure points. This approach enables the developer to determine where the code sucks (and all code does) and whether or not to make it _suck less_. 

The workflow for using TDD might look like this:

Create your initial method/function.
{% highlight c# %}
// 1. Create a simple test method. 
// Example test harness calls:
// public static void AlgUtil_Harness() {
//	Test_CountTwos(232);
//	Test_CountTwos(-232);	
// }

private static void Test_CountTwos(int n) {

	Console.WriteLine("The number of twos in {0} are: {1}", n, AlgUtil.CountTwos(n));
}
{% endhighlight %}
 
Create your initial test method.
{% highlight c# %}
// 2. Create a skeleton method/function and test.

using System;

namespace Dsa
{
	public static class AlgUtil
	{
             // Counts the number of 2's in an integer.
             public static int CountTwos(int n) {

	        return -1;
	     }
        }
}
{% endhighlight %}

Test.
{% highlight bash %}
The number of twos in 232 are: -1
The number of twos in -232 are: -1

Press any key to continue...
{% endhighlight %}

Complete the implementation. 
{% highlight c# %}
using System;

namespace Dsa
{
	public static class AlgUtil
	{
            // Counts the number of 2's in an integer.
            public static int CountTwos(int n) {
		// I don't want to handle negative numbers atm.
		// Note: We should use Code Contracts if using .NET 4.0
		if (n < 0) return -1;

		string number = n.ToString();
		int count = 0;
		for (int i = 0; i < number.Length; i++) {
			if (number[i] == '2') count++;
		}

		return count;
	    }
        }
}
{% endhighlight %}

Re-Test. 
{% highlight bash %}
The number of twos in 232 are: 2
The number of twos in -232 are: -1

Press any key to continue...
{% endhighlight %}

Rinse and repeat as needed. 


__Learn More:__

[Pex] (http://research.microsoft.com/en-us/projects/pex/)
[TDD](https://en.wikipedia.org/wiki/Test-driven_development)


;