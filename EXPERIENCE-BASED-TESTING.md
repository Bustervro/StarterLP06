Learning Practice 6 — Experience-Based Testing
Application: North Vacation Booking (airbnb-clone-ts)
Feature tested: Adding a booking and checking it on the Bookings page
Date tested: November 9, 2026
Tester: Aden
Documented testing window: 10:29:16 AM–10:40:39 AM (11 minutes and 23 seconds between screenshots)

The time above is based on my first and last screenshots from that testing window. It shows the elapsed time between screenshots, not proof that I tested continuously for every minute. I also worked on fixing the rental dropdown and checked a successful booking later.
Step 1 — Error Guessing
Before and during testing, I thought of three things that could go wrong:
1. The website might let me book without selecting a rental.
2. The website might accept an invalid number of guests, such as -1.
3. The Bookings page might show missing or incorrect booking information.
Step 2 — Exploratory Testing
My goal: I wanted to see whether I could select a rental, choose a date, enter the number of guests, make a booking, and see the correct information on the Bookings page. I also wanted to see whether invalid information was blocked.
What I tried	What happened	What I checked next
Opened the Add Booking page	The booking form showed fields for rental, date, and guests.	I tried submitting without a date.
Submitted with an empty date	The browser displayed “Please fill out this field” and blocked the booking.	I tried an invalid guest number.
Entered -1 guests	The browser said the value must be at least 1.	I checked the Bookings page.
Made bookings without choosing a rental	Bookings showed dates and guest numbers, but the rental names were blank.	I checked why the rental dropdown was empty.
Checked the Home page and rental connection	Rentals did not load correctly at first. After changing the fetch connection and Vite proxy settings, rental cards appeared on Home.	I checked Add Booking again.
Updated and used the Rental dropdown	I was able to choose Cozy Cabin. I also made the rental field required in the code.	I submitted a booking with a selected rental.
Booked Cozy Cabin for November 25, 2026, with 2 guests	The Bookings page showed Cozy Cabin, the date, and 2 guests together.	I noted the earlier incomplete bookings and other cases to test later.


Problem I found: In the first version, the app allowed bookings with no rental selected, and the Bookings page showed blank rental names. I changed the data connection and updated the rental field. A later booking showed the Cozy Cabin name correctly. I did not repeat the blank-rental submission test after the fix, so I cannot confirm that particular validation check passed afterward.

Other ideas I did not test: Booking with a past date, entering exactly 0 guests, creating duplicate bookings, refreshing the page to check whether a booking stays saved, and turning off the rental server.
Step 3 — Checklist-Based Testing
What I checked	Result	What I observed
The Add Booking page opens.	Passed	The booking form appeared.
The form blocks an empty date.	Passed	The browser showed a required-field warning.
The form blocks -1 guests.	Passed	The browser required at least 1 guest.
A submitted booking appears on the Bookings page.	Passed	Booking entries appeared in the list.
The form prevents a booking without selecting a rental.	Failed in the first version	Some bookings had blank rental names. I did not retest this exact case after editing the form.
A rental can be selected after the connection fix.	Passed	I selected Cozy Cabin.
The Bookings page shows the selected rental, date, and guests.	Passed	Cozy Cabin, November 25, 2026, and 2 guests appeared together.
A booking stays after refreshing the browser.	Not tested	I did not record a full refresh test.


Step 4 — Acceptance Testing
Test 1 — Valid booking: Passed
Given I am on the Add Booking page and rentals are available,
When I choose Cozy Cabin, November 25, 2026, and 2 guests and confirm,
Then the Bookings page should show the rental name, date, and number of guests.

Actual result: The booking showed all three details correctly.
Test 2 — Empty date: Passed
Given I am filling out a booking,
When I try to submit without a date,
Then the website should stop me and ask me to enter a date.

Actual result: The browser showed “Please fill out this field” and blocked submission.
Test 3 — Negative guests: Passed
Given I am filling out a booking,
When I enter -1 guests and submit,
Then the website should reject that number.

Actual result: The browser displayed a message saying the value must be 1 or higher.
Test 4 — No rental selected: Failed in the first version
Given I have not selected a rental,
When I try to confirm a booking,
Then the website should not create a booking.

Actual result: The earlier version created bookings with blank rental names. I later added a required rental selection, but I did not retest this same invalid case after the change.
Reflection
This activity helped me learn how to find problems by trying different things on a website. The date and guest checks worked, but I noticed bookings could appear without a rental name. I worked on the rental dropdown and the connection to the rental data. After making changes, I booked Cozy Cabin and saw the correct information on the Bookings page. Next time, I would test more invalid dates, zero guests, and whether bookings stay saved after refreshing.
AI Transparency
I used GitHub Codespaces and VS Code  to help me understand parts of the assignment and put my testing report together. I tested the booking website myself and checked what worked and what did not work. The results in this report are based on what I actually observed.
