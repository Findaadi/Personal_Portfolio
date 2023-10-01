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

1) Inconsistent type
```
Current Code:
static bool check(Int i)

fix:
static bool check(int i) 
```
- The code is violating C# coding convention as it used type 'Int' instead of 'int' for the check method. 

2) Unclear method
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


## Explanation

The provided code had some issues including inconsistent type and a unclear name of the method, which have been fixed in the improved version.
The changes included the change of method name to "IsEvenNumber" and the correction of "Int" to "int". These changed improve the code readability and adhere to coding conventions. 
Besides this, the code seems to be consistent with general clean code principles and doesn't violate them. 


