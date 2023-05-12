### About this repository
Wrote an algorithm to track the ticket availability for entry into the Colosseum on the official Colosseum website, where tickets are notoriously difficult to secure. Ticket availability was queried for 10 consecutive days in intervals between 3 seconds and one minute, depending on the time of day. Based on the collected data, a detailed plan is proposed to ensure that you get the best available tickets. Other features of the code allow for the user to be updated by email when tickets for a particular date go on sale.

### Jump to section: 
* [Background](#background)      
* [My suggested strategy for securing your tickets](#my-suggessted-strategy-for-securing-your-tickets)   
* [Ticket information](#ticket-information) 
  * [Ticket types](#ticket-types) 
  * [Ticket release times](#ticket-release-times)
  * [Best times to secure your tickets](#best-times-to-secure-your-tickets) 
* [Python code for tracking ticket availability](#python-code-for-tracking-ticket-availability) 

## Background
Tickets to enter the Colosseum are notoriusly difficult to obtain from the official website (https://www.coopculture.it/it/) as only a limited supply of timed entry tickets are released 30 days in advance, and those tickets are taken by third party bots within seconds of being posted. These third party sellers (e.g. Viator, Get Your Guide, Tiqets, etc.) then sell the tickets for a mark up, sometimes for more than 10x the original ticket price. The goal of this project was to devise a strategy which optimizes your chances of securing Colosseum tickets from the official website, avoiding the exorbitant fees incurred by using third party resellers. 

## My suggested strategy for securing your tickets
Based on my research and time spent tracking ticket availability using Python code, I suggest the following approach to securing your tickets to the Colosseum:

First, determine which ticket you want to purchase: regular experinece, full experinece arena, or full experience undergrounds and arena (see the section on ticket information below for the details on the differences between these ticket types). 

Follow these steps if you want **regular experience** tickets:
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at your desired time. Tickets are released on a rolling basis every 5 minutes starting at exactly 9:15am [CET]. Each batch of tickets will be sold within a minute of being released, but there should be enough time to secure a couple of tickets, especially if you are actively refreshing the ticket page and flexible on the entry time. A second batch of tickets will go on sale 7 days before the visit date and there will likely be availability within 24 hours of the visit, but securing a specific time slot may be more challenging. 
  
Follow these steps if you want **full experience** tickets: 
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at your desired time. Tickets are released on a rolling basis, starting at 9:00am [CET] (see the section on ticket infromation below for more details on ticket release times). Early morning tickets are nearly impossible to procure, but you may get lucky with some afternoon availability. It is likely that you could purchase tickets for entry after 5:30p, but the Colosseum closes at 7:00pm so your visit will be quite short.
  2) If you fail to obtain tickets on the release date then I am afraid you will have to wait until 7 days before your trip before ticket swill become available again. One option is to purchase tickets from a third party vendor (e.g. [Get your Guide](https://www.getyourguide.com/-l2619/?cmp=brand&cq_src=google_ads&cq_cmp=16347902802&cq_con=140138745257&cq_term=get%20your%20guide%20colosseum&cq_med=&cq_plac=&cq_net=g&cq_pos=&cq_plt=gp&campaign_id=16347902802&adgroup_id=140138745257&target_id=aud-1393039795420%3Akwd-330551615914&loc_physical_ms=9003941&match_type=e&ad_id=628087479995&keyword=get%20your%20guide%20colosseum&ad_position=&feed_item_id=&placement=&device=c&partner_id=CD951&gclid=CjwKCAjwx_eiBhBGEiwA15gLN8p4A82rhyJEmiCAALMUMy_mdeXz0BvXwF_N1l2TG1ohiWQxsvzujhoCH_cQAvD_BwE) or [Viator](https://www.viator.com/Rome-tourism/d511-r53012372528-s955139426?mcid=28353&supbk=1&tsem=true&supci=-1275353003&supag=53012372528&supsc=aud-435409373039:kwd-315492548805&supai=228142181740&supap=&supdv=c&supnt=g&supti=aud-435409373039:kwd-315492548805&suplp=9003941&supli=&m=28353&supag=53012372528&supsc=aud-435409373039:kwd-315492548805&supai=228142181740&supap=&supdv=c&supnt=nt:g&suplp=9003941&supli=&supti=aud-435409373039:kwd-315492548805&tsem=true&supci=aud-435409373039:kwd-315492548805&supap1=&supap2=&gclid=CjwKCAjwx_eiBhBGEiwA15gLN3utr3qVZmIqBk9jTQX0_R73eAGXx_t4mVKSHDgH_FzAQnCOmyPQzhoC-8UQAvD_BwE)). These sites usually have an option to get a full refund on your tickets up to 24 hours in advance, which is good since there is still a possibility to get tickets from the official website. The markup on the tickets can be anywhere from 1.5-10x the original cost of the ticket. Also, sometimes these sites don't actually give you a ticket, but instead meet you outside of the Colosseum and Forum-Palantine area to let you in, which is not ideal if you want to be on your own schedule.
  3) Periodically check the official website for ticket releases (or use the code in this repo to track ticket availablilty and automatically email you with any status changes). The most likley time to find a ticket is exactly 7 days before your visit time, when a second batch of tickets are released. It is also possible to find tickets available within 24 hours of your entry time, but that is cutting it too close and you will no longer have the option to return any tickets purchased from third party sites.

Will this approach work? It did for me!

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
Regular experience tickets are released exactly 30 days in advance in 5 minute intervals starting at 9:15am CET (Rome time) (figure 1, left panel). The full experience tickets are not released every 5 minutes as in the regular entrance ticket, with underground access tickets only containing ~20 entry times spread out across the day (central and right panel of figure 1). Again, tickets are released exactly 30 days from entry time, so you do not need to check the website every 5 minutes if you know what time slots will be available on that day. I do not yet have a way of determining which time slots will be available before they are released as the entry times seem to vary by the day and week. It does seem that 9:00am CET is always the first time slot available for underground access and 9:15am CET for arena-only access. 

<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/TicketTimeSlots.png" alt="drawing" width="800"/> 
</picture>
</p>
Figure 1: Available ticket times for the three main ticket types:regular experience (left panel), full experience arena (central panel), and full experience undergrounds and arena (right panel). The regular experience and full experience arena plots only show a subset of available times for that day, while the full experience undergrounds and arena ticket shows all available times for that day.

### Best times to secure your tickets

#### Regular experience tickets
The initial release of regular experience tickets do sell out within thirty seconds of each release time, but it should be possible to secure this type of ticket near your desired time so long as you are actively checking the website at the time of release. Moreover, there is usually an abundance of tickets released 7 days prior to entry date which do not sell out as fast. The following two figures plot the regular experience ticket availability. Each row The plot should be interpreted as follows: each cell block contains the maximum number of tickets available during that block's time interval over the two weeks (April 22nd, 2023 - May 5th, 2023) that the search was performed. For example, the 17 in the left panel of figure 2 means that there was a maximum of 17 tickets available for entry times between 9:15am and 9:45am when I queried the website between 9:15am and 9:45am in ~1minute intervals. A blank cell means no tickets were ever detected during when the website was queried during this time interval.

There are several take home messages from these heatmaps:
1) Tickets are released on a rolling basis
2) There is a good chance of securing tickets within 24 hours of the entry time and for a reasonable time. You should start checking 8:00pm the night before your rome visit.

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
There are two python scripts in this repository for tracking ticket information. Both scripts use Selenium to automate web browsing and ticket availability extraction. Each time the website is queried, the collected ticket availbility information is stored in a Pandas dataframe which is depicted below. Each row of the dataframe reports the number of tickets available for a given timeslot and are indexed by 'queryDate_queryTime_ticketType'. The columns have two levels (hierarchical indexing) where the outer level is for the ticket date and t. The outer level is dropped when tracking ticket availability on a single date. Given that most queries will return no ticket availablility, this dataframe is quite sparse (greater than 99% of entries are NaN) and so we use the builtin sparsity datatype (dtype = Sparse[float64, nan]) available in Panadas [sparse_date_structures](https://pandas.pydata.org/docs/user_guide/sparse.html#:~:text=pandas%20provides%20data%20structures%20for,%2C%20including%200)%20is%20omitted.)  

Each script has several control parameters to set query frequency, email frequency, ticket type to track, which dates to track, and how frequently to save dataframe (saved as .pkl file).

**1) ticket_tracker_single_day.ipynb:** This script is optimized for tracking ticket availability on the release date, which is useful if you are trying to obtain specific ticket type on a specific date and time. It contains functionality to send email alerts containing ticket information, including ticket type, entry date and time, number of tickets available, and link to the ticket. 

**2) ticket_tracker_all_days.ipynb:** This script is meant to track the ticket availability across all 30 days for which tickets have been released and for all ticket types of interest. This script is less useful for securing specific tickets for a specific date and more useful for collecting data on ticket availability as a function of time. If not for this script, I may not have learned about the second batch of tickets released 7 days in advnace of entrance time.  

**3) eda_all_days_plotsV0.ipynb:** Notebook used to create heatmaps presented in this repository based on data collected using ticket_tracker_all_days.ipynb script. Also provides some functions for manipulating the pandas dataframes with a hierarchical column structure.

**4) eda_single_day_plotsV0.ipynb:** Notebook used to create heatmaps presented in this repository based on data collected using ticket_tracker_single_day.ipynb script. 
