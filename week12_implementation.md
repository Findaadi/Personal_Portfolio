# Project work 5

This week is the last week of the green team working on the issues for UN Disaster Assesment and coordination
(UNDAC) App. In this week I worked on a issue that can use my knowledge from a previous issue i had worked on. 

## Issue worked on

```
As an UNDAC Team Member, I want to view a personal calendar of events so that I can manage my time effectively
```

The objective of this weeks issue is so that a user can manage their personal calendar with their events so they can manage
their time effectively. I had previously used on an issue that made use of calendar, which was to manage staff rota. 
I decided to use something similar as I had experience in it, and using something similar which is tried and tested 
and has been merged into the main branch is considerably better than experimenting with something different which wouldn't
match the theme of the application.
To start with it, I needed to make some changes to the previous issue. In the staff rota management task, i had hardcoded the list
of staff which can then be selected and be inserted in the rota. 

For this issue, this needed to be changed as an event could be anything set by the user, which i can't pre-determine in order to hard code 
them like the staff member list. I decided to let the user enter their event as a string and save that as an event in the selected calendar date. 

__Some of my code for this issue:__

```
    public class Event
    {
        public DateTime Date { get; set; }
        public string EventDetails { get; set; }

        public Event(DateTime date, string eventDetails)
        {
            Date = date;
            EventDetails = eventDetails;
        }
    }
```

```
    public partial class PersonalEvents : ContentPage
    {
        List<Event> events = new List<Event>();

        public PersonalEvents()
        {
            InitializeComponent();

            Calender.DateSelected += OnCalenderSelected;
            Add.Clicked += Add_click;
            Delete.Clicked += Delete_click;
        }

        private void OnCalenderSelected(object sender, DateChangedEventArgs e)
        {
            DateTime selectedDate = e.NewDate;

            var eventsForSelectedDate = events.Where(evt =>
            evt.Date.Date == selectedDate.Date).ToList();
            DisplayEventInformation(eventsForSelectedDate);
        }

        //to display the user entered personal events
        private void DisplayEventInformation(List<Event> eventList)
        {
            if (eventList.Any())
            {
                information.Text = "Events for the selected date";
                eventin.Text = string.Join(Environment.NewLine, eventList.Select(evt => evt.EventDetails));
            }
            else
            {
                information.Text = "No events for the selected date";
                eventin.Text = string.Empty;
            }
        }

        //to add an event user has entered
        private async void Add_click(object sender, EventArgs e)
        {
            if (Calender.Date != null)
            {
                DateTime selectedDate = Calender.Date;

                // Use an input dialog to get the event details from the user
                var enteredEventDetails = await DisplayPromptAsync("Enter Event Details", "Type the details of the event:", "OK", "Cancel", "Event Details");

                if (!string.IsNullOrEmpty(enteredEventDetails) && enteredEventDetails != "Cancel")
                {
                    events.Add(new Event(selectedDate, enteredEventDetails));
                    var eventsForSelectedDate = events.Where(evt =>
                    evt.Date.Date == selectedDate.Date).ToList();
                    DisplayEventInformation(eventsForSelectedDate);
                }
            }
        }

        //to delete the selected event
        private async void Delete_click(object sender, EventArgs e)
        {
            if (Calender.Date != null)
            {
                DateTime selectedDate = Calender.Date;

                var eventsForSelectedDate = events.Where(evt =>
                    evt.Date.Date == selectedDate.Date).ToList();

                if (eventsForSelectedDate.Any())
                {
                    string selectedEvent;
                    if (eventsForSelectedDate.Count > 1)
                    {
                        selectedEvent = await DisplayActionSheet("Select Event to Delete", "Cancel", null, eventsForSelectedDate.Select(evt => evt.EventDetails).ToArray());
                    }
                    else
                    {
                        selectedEvent = eventsForSelectedDate[0].EventDetails;
                    }

                    if (selectedEvent != "Cancel")
                    {
                        var eventToDelete = eventsForSelectedDate.FirstOrDefault(evt => evt.EventDetails == selectedEvent);
                        if (eventToDelete != null)
                        {
                            events.Remove(eventToDelete);
                            DisplayEventInformation(eventsForSelectedDate);
                        }
                    }
                }
                else
                {
                    information.Text = "No events for the selected date";
                    eventin.Text = string.Empty;
                }
            }
        }
    }
```

__The Personal Event Management page:

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/staffrotaPage.png" width="700" height="400">

User in this page can select the date clicking on the date, which will bring up a calender to select. When a date is selected, it will display a list of events for the selected date
. If there is no pre-existing event, it will display a message that there is no event for the day. When the date is selected, the user can
click on "Add Event" button which brings up a prompt to write an event and save it for the selected date. Once the users are saves an event,
it will update the event that are for the date. The user can also click on the "Delete Event" which will bring up a list of the events on that day, and select
the ones they want to delete from the calander for that date. 

## Code Review Feedback

I received the following feedback in my code review for this issue. The pull request didn't have any conflicts with the main 
branch, and there was no requested change. The pull request was successfully merged and the issue was closed. 

<img src="https://github.com/Findaadi/Personal_Portfolio/blob/main/images/lastweek1.png" width="700" height="400">

## Reflection

This week i didnt have an available pull request on time to provide a code review, without it i wasn't able
to complete the part of assinment to do a code review. 

This was the last week of working on these issues, and without even realizing, i have learnt so much 
about what goes into everyday work of a software developer. There are alot of improvements needed in
this task we have been given as a team, but overall, this was an amazing experience. 
A major change needed in this assinment that i would make if i had the control would be to assign a title to
the team members and give them tasks to handle. We need to have a pre-determined team leader, scrum lead and developers at least, which immitates
an actual team that works in a coorporate environment. A team leader would primarily be someone with better technical knowledge and they are there for assisting developers in the team,
who come across issues. Scrum lead can organizing the team workflow and developers will work on the issues assigned and nothing more additional to it. 
