# Week 3: Code review

This week, we were given the task to do some code review to determine if a code is following clean coding practices and coding conventions. I have chosen one of the code from the task and have
done a descriptive commentary on it to identify the problems in it, along with identify the principles it follows. 

## Code: 

```

using System;

namespace MyApplication
{
  class Program
  {
    static bool check(Int i) 
    {
        if (i % 2 == 0)
        {
            return true;
        }
        return false;
    }

    static void Main(string[] args)
    {
        //... Code not shown - ignore this line
    }  
  }
}

```

This is the code to be reviewied. I have identified some issues in this code which are as follows: 

```
Current Code:
static bool check(Int i)

fix:
static bool check(int i) 
```
- The code is violating C# coding convention as it used type 'Int' instead of 'int' for the check method. 

```
Current Code:
static bool check(Int i) 

Fix:
static bool IsEvenNumber(Int i) 
```
- The "check" method isn't making itself very clear. Appropriate name should be used for the method, in this case "IsEvenNumber" would be a better choice of name for this method. 


## Improved Version

```
using System;

namespace MyApplication
{
  class Program
  {
    static bool IsEvenNumber(int i) 
    {
        if (i % 2 == 0)
        {
            return true;
        }
        return false;
    }

    static void Main(string[] args)
    {
        //... Code not shown - ignore this line
    }  
  }
}
```


1. Choose the code review challenge which best demonstrates your skills.
2. Copy the code into your portfolio using a Markdown
   [fenced code block](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).
3. Provide some descriptive commentary that identifies the problems.
4. Show your improved version of the code in a second code block.
5. Explain in one or more paragraphs why your solution is a good one.

**DO**

* Use grammatically correct sentences and paragraphs for your commentary.
* Make clear reference to the code in your commentary. GitHub Markdown does not support
  line numbers and so you need to make sure that the reader knows which line you are
  referring to from your description.
* Refer to recognised principles or rules when describing your solution. "I thought it
  would be better that way" is not sufficient: you need to have specific reasons.

**DON'T**

* Include multiple examples. Make the decision about which example shows your best
  work and use that one.
