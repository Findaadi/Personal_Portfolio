# Project work 1

In week 8, the teams are introduced with the group project to work on for the next 3 weeks. The project is to work on creating a
UN Disaster Assesment and coordination (UNDAC) App. More information on it can be found here: **[UN App](https://github.com/edinburgh-napier/SET09102/blob/main/practicals/scenario.md)**. 
There are a bunch of issues provided to the team to work on for the development of this application. **[Issues](https://github.com/edinburgh-napier/SET09102/blob/main/practicals/issues/week_8.md)**

In our team, the issues are imported to the team repo and kept on the project board by assigning ourself to the issues we want to work on. 

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/board1.png" width="500" height="400">

## Issue worked on

For this week, I took the assigned myself to work on the following issue:
```
As an UNDAC Team Support and Logistics Manager, I want to view current stock level of OSOCC resources (food, medical supplies, cleaning products, etc.) to 
ensure supplies are sufficient
```

__Some of my codes for this issue:__

```
namespace UNDAC_App
{
    public partial class ViewStockLevel : ContentPage
    {
        public ObservableCollection<ResourceItem> Resources { get; set; }

        public ViewStockLevel()
        {
            InitializeComponent();

            Resources = new ObservableCollection<ResourceItem>
            {
                new ResourceItem { ResourceType = "Food", CurrentStock = 500 },
                new ResourceItem { ResourceType = "Medical Supplies", CurrentStock = 300 },
                new ResourceItem { ResourceType = "Cleaning Products", CurrentStock = 750 },
                //add new resource types and items. 
            };

            stockLevelListView.ItemsSource = Resources; 
        }
    }

    public class ResourceItem
    {
        public string ResourceType { get; set; }
        public int CurrentStock { get; set; }
    }
}
```
This code is from ViewStockLevel.xaml.cs, which i have added to the code base to add the functionality to view the current stock level of OSOCC resources.
This initializes a page displaying the stock levels of various recources. It contains 'Resources' of 'observablecollection'  type to store
'ResourceItem' objects. The resouce items hold information about the resources type and their current stock level. 
Additional resources can be added to this. The code has meaningful names which improves readability and simple logic to the program not making it too complex,
removing the need to add additional comments. 

There were also some codes added to the existing classes in order to add a button for the user to navigate to the 'ViewStockLevel' page.
The following codes were added to MainPage, that are self explanatory. 

```
//existing code

 <Button
                x:Name="StockLevelButton"
                Text="View Current Stock Level"
                SemanticProperties.Hint="View Current Stock Level"
                Clicked="StockLevelButton_Clicked"
                HorizontalOptions="Center" />
//existing code
```

```
 private async void StockLevelButton_Clicked(object sender, EventArgs e)
        {
            // Navigate to View resources stock level page
            await Navigation.PushAsync(new ViewStockLevel());
        }

```

## Code Review

This weeks task was to do a code review for someone else's code and to also request for a code review on your code. I reviewed the code for a team member
 who's task was to view a list of all local media agencies. I requested my code to be reviewed to one of the team member to receive feedback for any potential changes. 

### Code I reviewed

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/mark1.png" width="500" height="400">

For mediaAgencyListButton_clicked in MainPage.xaml.cs

The method nagivates to the “MediaAgecyList” page and it also announces the action for screen readers. 
It is good practice to separate the concerns by creating separate method for screen reader announcements, 
but looking at the other methods, this way of handling the screen reader seems to be normal practice. 
It is also good practice to have a try catch block for better error handling if the navigation fails. 

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/mark2.png" width="500" height="400">

For MediaAgencyList.xaml.cs:

this class sets up a collection of agencies and assigns it as the item source for mediaAgencyListView. 
For better redability and potential improvement, it can be considered to keep the addition of agencies in a 
separate method, which is also better for maintability in future. Additionally, a try catch block can be added for 
setting the itemsource for better error handling. 

### Code Review Feedback

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/review1.png" width="500" height="400">

For my code, I received the above feedback that involved a change to be made. Accordingly, I kept the 'ResourceItem' class
seperately in the Models folder. The Code after this update was as such: 

__ViewStockLevel.xaml.cs__
```
using System.Collections.ObjectModel;
using Microsoft.Maui.Controls;
using UNDAC_App.Models;

namespace UNDAC_App
{
    public partial class ViewStockLevel : ContentPage
    {
        public ObservableCollection<ResourceItem> Resources { get; set; }

        public ViewStockLevel()
        {
            InitializeComponent();

            Resources = new ObservableCollection<ResourceItem>
            {
                new ResourceItem { ResourceType = "Food", CurrentStock = 500 },
                new ResourceItem { ResourceType = "Medical Supplies", CurrentStock = 300 },
                new ResourceItem { ResourceType = "Cleaning Products", CurrentStock = 750 },
                //... other resource types
            };

            stockLevelListView.ItemsSource = Resources; 
        }
    }


}
```
__ResouceItem.cs__

```
using SQLite;

namespace UNDAC_App.Models
{
    public class ResourceItem
    {
        public string ResourceType{get; set; }
        public int CurrentStock { get; set; }
    }
}
```

Furthermore, the following feedback was provided on the same file:

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/review4.png" width="500" height="100">

__The other reviews I received for my code are as follows:__ 

ViewStockLevel.xaml

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/review2.png" width="500" height="150">

Views/MainPage.xaml

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/review3.png" width="500" height="150">


## Reflection

This weeks task accumulated all the knowledge and skills i was taught so far to put it in practice. It was challenging, but
at the same time very much intresting to go through it. I am still learning how to work with git/github and this was made easier with
the help of some of my class mates who described and showed me how to use github with details. Seeing someone do it, made it easier for me
to understand compared to learning it in theory or trying to figure it out myself. 

The issue i assigned myself for this week was to view the stock level of resources. We as a team didn't have a SQL database setup in time, which
we thought we would have it earlier. However, we were asked to use SQLite if the SQL database can't be setup on time, and i did exactly that.

This issue wasn't a major challenge in terms of its functionality, but i wanted it to be in accordance to the code we have in our main branch. 
I followed the coding style which was pushed to the main branch after code reviews of other team members, having different coding convention/style
wouldn't work well when there are multiple programmers working on the same code base, use of similar coding patterns makes the code base more readable.

Upon following this, I wrote my code and pushed it my branch and went on to review the code of one of my teammates. I then discovered i need to make some changes to
my own code as the code review i provided for my fellow teammate, would benifit my code as well.

```
public partial class ViewStockLevel : ContentPage
    {
        public ObservableCollection<ResourceItem> Resources { get; set; }

        public ViewStockLevel()
        
            InitializeComponent();
            InitializeResources();
            DisplayStockLevels();
        }

        private void InitializeResources()
        {
            Resources = new ObservableCollection<ResourceItem>
            {
                new ResourceItem { ResourceType = "Food", CurrentStock = 500 },
                new ResourceItem { ResourceType = "Medical Supplies", CurrentStock = 300 },
                new ResourceItem { ResourceType = "Cleaning Products", CurrentStock = 750 },
                //add more resources
            };
        }

        private void DisplayStockLevels()
        {
            try
            
                stockLevelListView.ItemsSource = Resources;
            }
            catch (Exception ex)
            {   
                Console.WriteLine("An error occurred while displaying stock levels: " + ex.Message
            }
        }
    }
```

Here, I made the changes that i had suggested in the code review to my team mate. I kept the methods seperate to Initialize resouces and
to display the stock level. I also added a try catch block for error handling if an error was to occur when displaying stock levels. 

These tasks are making me more efficient in identifying which part of the code can be made better and what changes can be made to make the code cleaner. 
I still struggle with naming the exact principles the code is violating, but i can point out if something isn't right, then go and look for what the principle is exactly called for it.

To conclude, the indivial learning is getting better week after week, but i am still struggling with the team working aspect. The teamwork seems to be less valued than the individual portfolio task, 
making the team members focus more on submitting the portfolio on time, rather than on team bonding work. I also feel hesitant at times to ask questions about something to the team if i don't understand it
 well in the first instance when it comes to task for the team, and spend time later to figure it out. This feels as an actual corporate environment where it sometimes is difficult to have humility and ask for
 help when needed, but with time you have to learn to do it which will ultimately help you get better at your job and work more efficiently.