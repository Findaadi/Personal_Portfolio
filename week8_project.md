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
<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/review2.png" width="500" height="100">

Views/MainPage.xaml
<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/review3.png" width="500" height="100">



In week 8, you are exercising all the principles and techniques that have been discussed in the module so far. 
Your portfolio entry should demonstrate your ability to integrate the various dimensions of software engineering into your practice. 
It should include:

A descriptive summary of the issue that you worked on.
Snippets from your code with commentary showing how you have used good software design practice.
A descriptive summary of the test code that you have written.
A reflective summary of any changes that were requested during the code review along with your fixes.
A descriptive summary of any issues you found with the code that you were asked to review.
A general reflective section that identifies, for example,
New things you have realised this week
Common problems that can arise in a team development situation
How your practice compares to other people's
etc.
Be sure to include links to the original items in the team's GitHub repository.

Marking
The marks for this portfolio entry will be split as follows:

Timeliness: 5 marks (one mark will be deducted for each day or partial day that the submission is late).
Description: 2 marks are awarded for the descriptive content. Please remember that this material will be useful to you in the end-of-module interview, 
so it is in your interests to make the content detailed and easy to follow.
Reflection: 3 marks are awarded for the quality of reflection. Again, you should think of this as preparation for the interview assessment.