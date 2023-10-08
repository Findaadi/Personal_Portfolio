# Documentation 

This week we were introduced to proper documentation and got more information on writing clean code.
Here, I will summarize some of the priciples of clean code along with some examples of them from my codes. Along with it
I will also provide some insights on use of doxygen comments and will also highlight some examples from my code where i have adhered to
the princiles of clean code eliminating the need for comments. 

## Principles of Clean Code

There are various principles of clean code, amogst which i have summarize six of them here. The issues task was finished after
the introduction to the clean code as there was some unforeseen problem delayed our workflow, which made me follow the clean
code principles in the first instance. I have used some examples from them to explain the clean code principles below:

***1. Meaningful Names:***

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

***2. Single Responsibility Principle:***

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

***3. Useful Comments:***

Use of comments on a code is benefitial to explain its complex logic and clairfy the purpose of the code if its not self explanatory.
The best practice is to make the code self explanatory where there is no use of additional comment, but there could be instances where the
code can benifit from additional comments to further clarify its purpose, in those cases use of comments is okay. 

```
        // Method to return a database connection
        public SQLiteConnection DBconn()
        {
            // Retrieve the applications system path.
            var systempath = AppDomain.CurrentDomain.BaseDirectory;

            // Combine the system path with the Database filename
            var fullpath = Path.Combine(systempath, "UNDAC.db");

            // Instantiate an SQLite connection passing the Database file path. 
            SQLiteConnection conn = new SQLiteConnection(fullpath);

            // Return the created database connection
            return conn;
```

***4. Don't Repeat Yourself (DRY):***

You must strive to eliminate any code duplication in the codebase. Code duplication increases the risk of the code being difficult to maintain
and also makes it harder to maintain. Its advisable to make use of encaptulation to encaptulate similar functionalites into resuable functions. 

***5. Formatting:***

Its best practice to follow a consistent coding style or format within your codebase. This makes the code more readable, and it specially
helpful when there are multiple developers working in the same code base. 

I got to have a more handon experience with this when i was given to opportunity to shadow a team of developers in a large financial instituion for
a month. The software engineering team had a strict set of rules to follow in their codebase, and it had to be adhered to when making
any changes to the existing code.

***6. Keep It Simple Stupid (KISS):***

This principle adheres to keeping the code simple and not add any unnecessary complexity to the code. The focus should be on making the code
simpler and maintanable for future. 

```
    public class RoomType
    {
        [PrimaryKey,AutoIncrement]
        public int ID {get; set;}
        public string Name {get; set;}
    }


```

## Doxygen: Code Documentation

![Doxygen](https://github.com/Findaadi/Personal_Portfolio/blob/main/images/doxygen.jpg)

I used doxygen for documenting my code as per the instructions provided. I have attached an image here representing the structure of the code in HTML content. 
This is a basic use of this, and I am yet to explore the use of it properly which will come with me using it more.

### Code Examples

These are some of the codes that are in-line with the coding principles which are self explanatory and doesn't require additional
use of comments.

```
﻿using SQLite;

namespace UNDAC_App.Models
{
    public class RoomType
    {
        [PrimaryKey, AutoIncrement]
        public int ID { get; set; }
        public string Name { get; set; }
    }
}
```

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

    async void OnDeleteClicked(object sender, EventArgs e)
    {
        if (Item.ID == 0)
            return;
        await database.DeleteItemAsync(Item);
        await Shell.Current.GoToAsync("..");
    }

    async void OnCancelClicked(object sender, EventArgs e)
    {
        await Shell.Current.GoToAsync("..");
    }
```
