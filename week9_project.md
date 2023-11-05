# Project work 2

This week I am continuing with the team project I did last week. The previous issue was merged to the main branch which added the functionality to the program
to view the current stock levels of OSSOC resources to ensure supplies are sufficient. 

## Issue worked on

This week i have assined myself to a new issue to work on. **[Issue this week](https://github.com/wardliii/Green-Team/issues/63)**
```
As an UNDAC Deputy Team Leader I want to view the stock levels of existing resources so that I can ensure sufficient supplies at all times.
```

The issue for this week alligns alot with the issue i worked on the previous week. The previous weeks issue was to have a functionality to view the OSSOC resources
supply stocks and for this weeks issues its to view the stock levels of existing resources i.e. all other resources beyond OSSOC resources. 
My idea for this weeks issue is to allign my previous week's code to include the other resources stock current supplies. 

__Some of my code for this issue:__

_ViewStockLevel.xaml.cs_
```
namespace UNDAC_App
{
    public partial class ViewStockLevel : ContentPage
    {
        public ObservableCollection<ResourceItem> Resources { get; set; }

        public ViewStockLevel()
        {
            InitializeComponent();
            DisplayStockLevels();
        }

        private void DisplayStockLevels()
        {
            try
            {
                var resourceManager = new ResourceManager();
                Resources = resourceManager.GetAllResources();
                stockLevelListView.ItemsSource = Resources;
            }
            catch (Exception ex)
            {
                Console.WriteLine("An error occurred while displaying stock levels: " + ex.Message);
            }
        }
    }

    public class ResourceManager
    {
        public ObservableCollection<ResourceItem> GetAllResources()
        {
            ObservableCollection<ResourceItem> resources = new ObservableCollection<ResourceItem>();

            //get OSOCC resources
            foreach (var item in GetOSOCCResources())
            {
                resources.Add(item);
            }

            //get Other resources
            foreach (var item in GetOtherResources())
            {
                resources.Add(item);
            }

            return resources;
        }

        private ObservableCollection<ResourceItem> GetOSOCCResources()
        {
            return new ObservableCollection<ResourceItem>
            {
                new ResourceItem { ResourceType = "Food", CurrentStock = 500 },
                new ResourceItem { ResourceType = "Medical Supplies", CurrentStock = 300 },
                new ResourceItem { ResourceType = "Cleaning Products", CurrentStock = 750 },
            };
        }

        private ObservableCollection<ResourceItem> GetOtherResources()
        {
            return new ObservableCollection<ResourceItem>
            {
                new ResourceItem { ResourceType = "Hand Sanitizers", CurrentStock = 383 },
                new ResourceItem { ResourceType = "Blankets", CurrentStock = 300 },
                new ResourceItem { ResourceType = "Books", CurrentStock = 950 },
            };
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

In the code in ViewStockLevel.xaml.cs file i have added the functionality to view other resouces alongside the OSSOC resources. 
I have kept adding and viewing the OSSOC resources and other resources seperate in the code, since there was a different issue specific
for the each of them to be worked on. 
I have changed the code so it promotes reusability as i have encaptulated the logic for resouce retrival in a seperate class i.e.
('ResourceManager') which was hardcoded directly within the 'ViewStockLevel' constructor previously.

## Code Review

This weeks task was to do a code review for someone else's code and to also request for a code review on your code. I reviewed the code for a team member
who's task was to view the current status of all OSOCC accomodation to ensure all personal and operational space needs are met. 
I requested my code to be reviewed to one of the team member to receive feedback for any potential changes. 

### Code I reviewed

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/aidanCodereview1.png" width="500" height="400">

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/aidanCodereview2.png" width="500" height="400">

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/aidanCodereview2.png" width="500" height="400">

I have requested for a change in the code. The changes requested are: 

- Create a separate method to update the AccomodationStatusList. 
- Use appropriate numeric data type for the capacities. 

### Code Review Feedback



In week 9, you are continuing with the team project. Your portfolio entry should 
demonstrate how your software engineering practice is improving. It should include
much the same content as last week's:

* A descriptive summary of the issue that you worked on.
* Snippets from your code with commentary showing how you have used good software design 
  practice.
* A descriptive summary of the test code that you have written.
* A reflective summary of any changes that were requested during the code review along 
  with your fixes.
* A descriptive summary of any issues you found with the code that you were asked to review.
* A general reflective section that identifies, for example,
  * New things you have realised this week
  * Common problems that can arise in a team development situation
  * How your practice compares to other people's
  * etc.

Be sure to include links to the original items in the team's GitHub repository.

In the reflective sections, try to identify things that you have done better this week. 
This could include, for example,

* Better application of the principles of clean code.
* Avoiding the repetition of previous mistakes.
* More comprehensive test coverage.
* Adoption of a more systematic personal workflow.
* Improved identification of problems in other people's code.
* etc.
