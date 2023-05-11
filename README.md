# About this repository
Code for webscraping ticket availability for entry to the Colosseum, Roman Forum, and Palatine Hill in Rome from the official Colosseum website. 

### Jump to section: 
* [Background](#background)      
* [My suggested strategy for securing your tickets](#my-suggessted-strategy-for-securing-your-tickets)   
* [Ticket information](#ticket-information) 
  * [Ticket types](#ticket-types) 
  * [Ticket release times](#ticket-release-times)
  * [Best times to secure your tickets](#best-times-to-secure-your-tickets) 
* [Python code for tracking ticket availability](#python-code-for-tracking-ticket-availability) 

## Background
Tickets to enter the Colosseum are notoriusly difficult to obtain from the official website (https://www.coopculture.it/it/) as only a limited supply of timed entry tickets are released 30 days in advance, and those tickets are taken by third party bots within seconds of being posted. These third party sellers (e.g. Viator, Get Your Guide, etc.) then sell the tickets for a mark up, sometimes for more than 10x the original ticket price. The goal of this project was to determine when is optimal time to purchase a Colosseum ticket from the official website, avoiding the exorbitant fees incurred by using third party resellers. 

## My suggested strategy for securing your tickets
Based on my research and time spent tracking ticket availability using Python code, I suggest the following approach to purchasing tickets at the Colosseum:

First, determine which ticket you want to purchase: regular experinece, full experinece arena, or full experience undergrounds and arena (see ticket infromation below for more information on the difference between these ticket types). 

Follow these steps if you want the regular experience ticket:
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at a desirable time. Tickets are released on a rolling basis every 5 minutes starting at exactly 9:15am [CET]. Each batch of tickets will be sold within a minute of being released, but this should be enough time to secure a couple of tickets, especially if you are somewhat flexible on the entry time. A second batch of tickets will go on sale 7 days before the visit date and there will likely be some availability within 24 hours of the visit, but securing a specific time slot may be more challenging. 
  
Follow these steps if you want one of the full experience options: 
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at a desirable time. Tickets are released on a rolling basis, starting at 9:00am [CET] (see ticket infromation below for more information on ticket release times). Early morning tickets are nearly impossible to get, but you may get lucky with some afternoon availability. It is very likely that you could purchase tickets for entry after 5:30p, but the Colosseum closes at 7:00pm so your visit will be quite short.
  2) If that fails, the next step is to purchase tickets from a third party vendor (e.g. Get your Guide or Viator). These sites usually have an option to get a full refund on your tickets up to 24 hours in advance, which is good since there is still a possibility to get tickets from the official website. The markup on the tickets can be anywhere from 1.5-10x the original cost of the ticket.
  3) Periodically check the official website for ticket releases (or use the code in this repo to track ticket availablilty and automatically email you with any status changes). The most likley time to find a ticket is exactly 7 days before your visit time, when a second batch of tickets are released. It is also possible to find tickets available within 24 hours of your entry time, but that is cutting it too close and you will no longer have the option to return any tickets purchased from third party sites.

Will this approach work? It did for me:

## Ticket information 

### Ticket types
There are three main ticket types you can purchase: the ordinary ticket (€18), the full experience arena ticket (€24), and the full experience undergrounds and arena ticket (€24). The following description of each ticket type was adapted from the coopculture website (see Colosseum website for more details https://parcocolosseo.it/en/visit/opening-times-and-tickets/):

"""

**ADMISSION TICKETS**
**Regular experience ticket (€16 + €2 booking fee):**
Valid 24 h, it allows one entrance to the Colosseum and one entrance to the Forum - Palatine area.

**Full Experience Arena ticket (€22 + €2 booking fee):**
Valid for 2 days from the first use, it allows one entrance to the Colosseum with access to the Arena, one entrance to the Palatine Forum and SUPER sites.

**Full Experience Undergrounds and Arena ticket (€22 + €2 booking fee):**
Valid for 2 days from the first use, it allows one entrance to the Colosseum with access to the Undergrounds and Arena, one entrance to the Palatine Forum and SUPER sites. (NOTE FROM ME: These tickets are nominative and you will not be allowed to enter the underground unless your ID matches the name on the ticket.)

"""

Each ticket gives you one timed entry to the Colosseum and one entry to the Palatine-Forum area. You can visit the Palantine-Forum area before or after your Colosseum visit but it must be within 24 hours (for regular experience ticket) or 48 hours (for full experience ticket) of your timed entrance to the Colosseum.  It is not possible to enter the Colosseum at a time that is different than your listed time. The full experience also allows you access to the SUPER sites which are located within the Palantine-Forum area (see here for a list of which SUPER sites will be open during your visit).

Based on this information, it seems obvious that the full experience undergrounds and arena ticket is the best value, but as we will see below, the limited number of tickets and their high demand make these tickets the most difficult to secure.

A quick note: On the coop culture website you will also find regular experience and full experience undergrounds and arena tickets on sale with a guided tour included. These tours are typically offered 1-2 times a day and are given in french, spanish, italian, and english. For the purposes of this project, I only tracked the ticket availability for the English didactic tour and combined its availability with that of the ordinary or full experience ticket. 

### Ticket release times
Regular experience tickets are released exactly 30 days in advance in 5 minute intervals starting at 9:15am Rome time (left panel figure 1). The full experience tickets are not released every 5 minutes as in the regular entrance ticket, with underground access tickets only containing ~20 entry times spread out across the day (central and right panel of figure1). Again, tickets are released exactly 30 days from entry time, so you do not need to check the website every 5 minutes if you know what time slots will be available on that day. The time slots do change by the day, but there may be a weekly pattern (still need to collect this information).

<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/TicketTimeSlots.png" alt="drawing" width="800"/> 
</picture>
</p>

### Best times to secure your tickets

The initial release of regular experience tickets do sell out within one minute of each release time, but it should not be difficult to secure this type of ticket near your desired time so long as you are actively checking the website at the time of release. Moreover, there is usually an abundance of tickets released 7 days prior to entry date which do not sell out as fast.  

#### Regular experience tickets (30days and 7days)
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance_30Days_7Days.png" alt="drawing" width="800"/> 
</picture>
</p>

#### Regular experience tickets (1day and day of)
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance.png" alt="drawing" width="800"/> 
</picture>
</p>

The second challenge to gettign these tickets is that the sell fast. Really fast. So fast that, even if you refresh the webpage on the exact moment that tickets are released, by the time it takes you to add the ticket to the cart (select ticket time, select amount of tickets, and bypass reCAPTCHA) the tickets will be sold out and you will be displayed with a disheartening error message saying "tickets are no longer availble for your selected time." Even still, if you are a bit flexible on the day or time of your visit to the Colosseum and are very active in trying to secure tickets, I have had some success in getting the Full experience with arena access just by constantly checking the website, at least getting 2 tickets. Underground access remains challenging, but I have one more trick that will help you to beat the bots and actually secure your underground ticket.

#### Full experience initial 30 day release
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/single_day_combined.png" alt="drawing" width="800"/> 
</picture>
</p>

#### Full experinece entrance tickets (7days and day of)
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined.png" alt="drawing" width="800"/> 
</picture>
</p>




## Python code for tracking ticket availability 
There are two python scripts in this repository for tracking ticket information:

1) ticket_tracker_single_day.ipynb 

Contains an option to send email alerts.

3) ticket_tracker_all_days.ipynb 



