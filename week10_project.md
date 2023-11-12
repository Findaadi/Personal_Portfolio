# Project work 3

This week is also a continous task as per the last week. For this week I wanted to work on a different type of issue than i have worked on in prior weeks. 
In previous weeks it has mostly been about working on a functionality to view. For a change I got an issue from the backlog to create and manage staff rotas. 

## Issue worked on

The issue for this week i worked on is: 

```
As an UNDAC Team Support and Logistics Manager, I want to create and manage staff rotas so that essential OSOCC functions are operational at all times.
```

The objective of this weeks issue is to assign the staffs to to a scheduled rota which ensures essential functions are operational. For this, I had to first plan 
the layout of the screen to acomodate this feature and its functions. I decided to have a calender which a user can choose and select the staffs that are to work
 on that specific date that is selected. I also needed a list of staff, which so far through the development of the app wasn't available due to which i needed to
 create a list of the staff that are available to work so they could be added to the rota. 

__Some of my code for this issue:__

```
    public class Rota
    {
        public DateTime Date { get; set; }
        public string StaffName { get; set; }

        public Rota(DateTime date, string staffname)
        {
            Date = date;
            StaffName = staffname;
        }
    }

```

```
    public partial class StaffRota : ContentPage
    {
        List<Rota> rota = new List<Rota>();
        //add the list of available staffs to work on the list
        List<string> availableStaff = new List<string> { "Hari", "Ram", "Sam", "Geeta", "Sita" };

        public StaffRota()
        {
            InitializeComponent();

            Calender.DateSelected += OnCalenderSelected;
            Add.Clicked += Add_click;
            Delete.Clicked += Delete_click;
        }

        private void OnCalenderSelected(object sender, DateChangedEventArgs e)
        {
            DateTime selectedDate = e.NewDate;

            var staffForSelectedDate = rota.Where(assignedStaff =>
                assignedStaff.Date.Date == selectedDate.Date).ToList();

            DisplayStaffInformation(staffForSelectedDate);
        }


        private void DisplayStaffInformation(List<Rota> staffList)
        {
            if (staffList.Any())
            {
                information.Text = "Staff Assigned to work";
                staffin.Text = string.Join(", ", staffList.Select(s => s.StaffName));
            }
            else
            {
                information.Text = "No Staff Assigned to work";
                staffin.Text = string.Empty;
            }
        }

        private async void Add_click(object sender, EventArgs e)
        {
            if (Calender.Date != null)
            {
                DateTime selectedDate = Calender.Date;

                var selectedStaff = await DisplayActionSheet("Select Staff to Assign", "Cancel", null, availableStaff.ToArray());

                if (selectedStaff != "Cancel")
                {
                    rota.Add(new Rota(selectedDate, selectedStaff));

                    var staffForSelectedDate = rota.Where(assignedStaff =>
                        assignedStaff.Date.Date == selectedDate.Date).ToList();

                    DisplayStaffInformation(staffForSelectedDate);
                }
            }
        }

        private async void Delete_click(object sender, EventArgs e)
        {
            if (Calender.Date != null)
            {
                DateTime selectedDate = Calender.Date;

                var staffForSelectedDate = rota.Where(assignedStaff =>
                    assignedStaff.Date.Date == selectedDate.Date).ToList();

                if (staffForSelectedDate.Any())
                {
                    string selectedStaff;
                    if (staffForSelectedDate.Count > 1)
                    {
                        selectedStaff = await DisplayActionSheet("Select Staff to Delete", "Cancel", null, staffForSelectedDate.Select(s => s.StaffName).ToArray());
                    }
                    else
                    {
                        selectedStaff = staffForSelectedDate[0].StaffName;
                    }

                    if (selectedStaff != "Cancel")
                    {
                        var staffToDelete = staffForSelectedDate.FirstOrDefault(assignedStaff => assignedStaff.StaffName == selectedStaff);
                        if (staffToDelete != null)
                        {
                            rota.Remove(staffToDelete);
                            DisplayStaffInformation(staffForSelectedDate);
                        }
                    }
                }
                else
                {
                    information.Text = "No Staff Assigned to work";
                    staffin.Text = string.Empty;
                }
            }
        }
    }
```

__The staff rota page:__

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/staffrotaPage.png" width="700" height="400">

User in this page can select the date clicking on the date, which will bring up a calender to select. When a date is selected, it will display any staff
working on the day. If there is no-one working, it will display a message that there is no staff assigned to work. When the date is selected, the user can
click on "Add Staff" button which brings up the list of all staffs that are available to work, which can be selected to add to the day's rota. Once the users are selected,
it will update the users that are scheduled to work for that date. The user can also click on the "Delete Staff" which will bring up a list of staff working on that day, and select
the ones they want to delete from the rota for that date. 

## Code Review Feedback

I received the following feedback in my code review for this issue. The pull request didn't have any conflicts to the main branch, and there was no requested changes. 
The pull request was successfully merged and closed. 

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/merged10.png" width="700" height="400">

## Reflection

This week, i took a different task than usual which was amazing to work on, and i enjoyed writing the code for it. I initially planned what approach to take for this, 
decided a design which alligned with other parts of the program to make it look similarly theamed, got to know a new thing i.e. adding calender to the MAUI applciation. 
Wrote the code and had to spend alot of time on this, making this the longest time i have spent in an issue so far. 

This week, i didn't get the oppurtunity to give a code review as the code review partner i had for this week in the team couldn't manage to make any progress to make a pull request
on their issue. Since this module is making us used to the actual everyday workings of a software engineer on the job, this is also a likely scenario where a team member
might not to able to push a code on time because, life happens, to everyone including software engineers. 
Similarly, if due to such scenario, or if the issues can't get covered in a given sprint, it goes to the backlog of the team to work on in further sprints. 
