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

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/staffrotaPage.png" width="600" height="400">



Week 10 is the third and last week in a series in which the goal is to improve your 
personal software engineering practice. Your portfolio entry has the same general content
as last week's, including:

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

In the reflective sections this week, you should highlight ways that you persona practice
has improved as before. It would also be good to reflect on any improvements that have
been made to the agreed team workflow and related procedures. Are things working
better than they were? What further improvements could be made in the future?
