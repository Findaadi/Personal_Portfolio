# Documentation 

This week we were introduced to proper documentation and got more information on writing clean code.
Here, I will summarize some of the priciples of clean code along with some examples of them from my codes. Along with it
I will also provide some insights on use of doxygen comments and will also highlight some examples from my code where i have adhered to
the princiles of clean code eliminating the need for comments. 

## Principles of Clean Code

There are various principles of clean code, amogst which i have summarize six of them here. The issues task was finished after
the introduction to the clean code as there was some unforeseen problem delayed our workflow, which made me follow the clean
code principles in the first instance. I have used some examples from them to explain the clean code principles below:

**1. Meaningful Names:**

Names used in the code for functions, methods, variables, classes or others should be meaningful and explain its purpose
via its name. As an example, 'OnSaveClicked' here relays its purpose clearly via its name. 

```
    async void OnSaveClicked(object sender, EventArgs e)
    {
        if (string.IsNullOrWhiteSpace(Item.Name))
        {
            await DisplayAlert("Name required", "Please enter Room Type.", "Okay");
            return;
        }

        await database.SaveItemAsync(Item);
        await Shell.Current.GoToAsync("..");
    }
```

**2. Single Responsibility Principle:**

A function is best when it has a single and well-defined purpose or task. This keeps the function small and precise making it
easier to understand and to debug if necessary. Here in the example below, the purpose of 'OnDeleteClicked' is to delete the specific object from the database.

```
    async void OnDeleteClicked(object sender, EventArgs e)
    {
        if (Item.ID == 0)
            return;
        await database.DeleteItemAsync(Item);
        await Shell.Current.GoToAsync("..");
    }
```

**3. Useful Comments:**



# Documentation

This section is related to your work on clean code and documentation in week 5.

First, choose six rules of clean code and explain them. For each one,

* Summarise the rule in your own words.
* Provide an example from the code that you wrote in week 2 and then refined in week 4.
* Explain how your code implements the rule. 

Second, copy the doxygen comments from your code into your portfolio and provide some 
descriptive commentary on their purpose and structure. Use screenshots showing the HTML 
content that is generated from your code to illustrate your explanation.

Finally, highlight three examples from your code where you have eliminated the need
for comments by adhering to the principles of clean code.
 
