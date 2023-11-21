# Project 4

This weeks task consisted of updating a part of a pre existing functionality to inhance its ususage.

## Issue worked on

The issue i worked on this week is:
```
As an UNDAC Disaster Management Coordinator, I want to view a list of current needs so that I can make priority judgements
```

There was a functionality in the app prior to working on this task i.e., a user could add a disaster management need, modify it or delete it.
This issue's objective is to add a functionality so user can view and make priority judgement. My plan to deal with this issue is by adding a couple of additinal buttons
; up and down, to the list of needs. In the list of needs, user will then be able to move the needs up or down to change its priority. The ones on top of the list will be 
the one at highest priority. 

__Some of my codes for this issue:__ 

```
       private void OnMoveUpClicked(object sender, EventArgs e)
        {
            var button = sender as Button;
            var selectedNeed = button?.CommandParameter as DisasterManagementNeeds;

            if (selectedNeed != null)
            {
                var index = disasterManagementNeedsList.IndexOf(selectedNeed);
                if (index > 0)
                {
                    disasterManagementNeedsList.Move(index, index - 1);
                }
            }
        }

        private void OnMoveDownClicked(object sender, EventArgs e)
        {
            var button = sender as Button;
            var selectedNeed = button?.CommandParameter as DisasterManagementNeeds;

            if (selectedNeed != null)
            {
                var index = disasterManagementNeedsList.IndexOf(selectedNeed);
                if (index < disasterManagementNeedsList.Count - 1)
                {
                    disasterManagementNeedsList.Move(index, index + 1);
                }
            }
        }
```

__Change made in disaster management needs page:__

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/disaster1.png" width="700" height="400">

__Clicked on Up Button to raise its priority higher in the list.__

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/disaster2.png" width="700" height="400">


User in this page will initially have to add needs, if they dont exist. If there are multiple of these needs, the user will be able to make changes to the 
rankings, which determine the priority of the needs. 

## Code review Feedback

I received the following feedback in my code for this issue, The pull request didn't have any conflicts to the main branch, and there was no requested changes. 
Reviewer wanted to clarify some issues before merging, which was clarified by me that it wasnt a problem raised by an edit i had made, and github didnt have any conflicts while merging
my branch to the main branch.

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/cleancode3.png" >



## Code I reviewed

I reviewed a change requested on a code review on a prior weeks issue a team member was working on, they were requested to change the data
type to an appropriate one in their code. They made the changes and the branch was good to merge to the main branch. 

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/aidan57.png" width="700" height="400">

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/aidan58.png" width="700" height="250">


## Reflection

This weeks issue i worked on is the kind of issue we would probably be exposed the most to in a working enviroment. 
Having to oppurtunity to be a part of a professional software engineering team in a big financial institution, the SE1 and SE2 level
engineers were mostly involved in such issues that inhances the current functionality rather than developing a completely new functionality on their own.

While working on this, i initially planned on creating a different file to view the list of needs, which was due to my bad planning
as i didnt completely go through the existing codes for the needs, which took me longer to code as in the last moment i had to change everything. 
Taught me the valuable lesson to go through the exitisting code base, understand it clearly before planning your actions.
