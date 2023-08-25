### About this project: Goals, techniques, and key findings
The goal of this project was to devise a strategy that optimizes your chances of securing Colosseum tickets from the official website ([Coopculture](https://ecm.coopculture.it/index.php?lang=en)), avoiding the exorbitant fees incurred by using third-party resellers who use bots to purchase all tickets within seconds of being released. To this effect, I wrote a computer program (using Python and Selenium) to track the ticket availability for entry into the Colosseum from the official website. Ticket availability was queried for 14 consecutive days in intervals between 3 seconds and one minute, depending on the time of day. The main findings of this work show that tickets are released on a rolling basis exactly 30 days, 7 days, and 1 day before the timed ticket entry. We find that the initial release of tickets sells out the fastest and tickets released 7 days and 1 day before the entry time are available for longer.  

Based on these findings, a detailed plan is proposed to ensure that you get your tickets, including a strategy for optimizing how you navigate the website when searching for tickets since every second counts. In the final section of this ReadMe.md file, we discuss the code in detail and its main features, including my approach to collecting, storing, organizing, manipulating, and visualizing the data as well as the feature of the code that allows the user to be sent instantaneous email alerts with embedded links when tickets become available.

### Jump to section: 
1) [Introduction](#introduction)
   * [General background and motivation](#general-background-and-motivation)  
   * [Ticket types](#ticket-types)
2) [Methods](#methods)
   * [Tracking ticket availability using Python and Selenium](#tracking-ticket-availability-using-Python-and-Selenium)      
3) [Summary of webscraped data](#summary-of-webscraped-data) 
   * [Ticket entry times](#ticket-entry-times)
   * [Ticket release times and availability](#ticket-release-times-and-availability) 
4) [Conclusions](#conclusions)
   * [My suggested strategy for securing your tickets](#my-suggested-strategy-for-securing-your-tickets)
   * [A time-saving hack for scoring your tickets](#a-time-saving-hack-for-scoring-your-tickets)
5) [Details on the Python code for tracking ticket availability](#python-code-for-tracking-ticket-availability) 

## Introduction

### General background and motivation
Tickets to enter the Colosseum are notoriously difficult to obtain from the official website ([coopculture](https://ecm.coopculture.it/index.php?option=com_snapp&view=products&snappTemplate=template3&catalogid=A4CC149C-BEE1-5773-5E59-01675F3EA81C&lang=en)) as only a limited supply of timed entry tickets are released 30 days in advance, and the majority of those tickets are scooped up by third party bots within seconds of being posted. These third-party resellers (e.g. Viator, Get Your Guide, Tiqets, etc.) then sell the tickets for a markup, sometimes for more than 10x the original ticket price. 

<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Colosseum_in_Rome_wikipedia_image.jpg" alt="drawing" width="49.5%"/> <img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Colosseum_in_Rome_inside_view_flickr.jpg" alt="drawing" width="49.5%"/> 

*Figure 1: Images of the outside (left - photo credit: wikipedia) and interior (right - phot credit: flikr) of the Colosseum in Rome. In the photo on the right, you can see the underground ruins which was located beneath the arena floor and is where the gladiators, animals, and special effect workers would plan for the show. Also shown in this photo is the reconstructed arena floor (tan floor in the right-center of the photo) where the battles took place.*

### Ticket types
There are three main ticket types you can purchase: the regular experience ticket (€18), the full experience arena ticket (€24), and the full experience undergrounds and arena ticket (€24). The following description of each ticket type was adapted from the coopculture website (see the Colosseum website for more details [PARCO](https://parcocolosseo.it/en/visit/opening-times-and-tickets/)):

"""
**ADMISSION TICKETS**

**Regular experience ticket (€16 + €2 booking fee):**
Valid for 24hrs from the first use, it allows one entrance to the Colosseum and one entrance to the Palatine Hill-Roman Forum area.

**Full Experience Arena ticket (€22 + €2 booking fee):**
Valid for 48hrs from the first use, it allows one entrance to the Colosseum with access to the Arena, one entrance to the Palatine Hill-Roman Forum area, and entrance to all the S.U.P.E.R sites within the Palatine Hill-Roman Forum area.

**Full Experience Undergrounds and Arena ticket (€22 + €2 booking fee):**
Valid for 48hrs from the first use, it allows one entrance to the Colosseum with access to the Undergrounds and Arena, one entrance to the Palatine Hill-Roman Forum area, and entrance to all the S.U.P.E.R sites within the Palatine Hill-Roman Forum area. These tickets are nominative and you will not be allowed to enter the underground unless your ID matches the name on the ticket.
"""

NOTES: 
1) The Palatine Hill-Roman Forum area is located right next to the Colosseum and contains the ruins of ancient Rome. The Palatine Hill section is where the emperors of ancient Rome built their palaces and contains some nice views of the Circus Maximus and the Roman Forum section. The Roman Forum section is where all the political meetings and social gatherings of ancient Rome took place. The two sections are connected and the boundary between them is not perceptible (i.e. you can walk between the two sections without knowing it). 
2) The S.U.P.E.R (Seven Unique Places to Experience in Rome) sites are special attractions inside the Palatine Hill-Roman Forum area which are only accessible with a full experience ticket. The S.U.P.E.R sites include House of Augustus, House of Livia (Augustus' wife), Palatine museum, Temple of Romulus, Neronian Cryptoporticus, the Aula Isiaca, and the Santa Maria Antiqua. See the [PARCO](https://colosseo.it/en/) website for more details on these sites including dates of closure for maintenance.
3) Each ticket gives you one timed entry to the Colosseum and one entry to the Palatine Hill-Roman Forum area. You can visit the Palatine Hill-Roman Forum areas before or after your Colosseum visit, but it must be within 24 hours (for regular experience ticket) or 48 hours (for full experience ticket) of your timed entrance to the Colosseum.  It is not possible to enter the Colosseum at a time that is different than your listed time. 

Based on this information, the full experience undergrounds and arena ticket is the best value, but the limited number of tickets and their high demand make these tickets the most difficult to secure, especially during the summer months.



## Methods

### Tracking ticket availability using Python
To gain insight into the optimal time to purchase your desired tickets, I used a computer program written in Python to track the release time of tickets and how long the tickets are available before they are sold out. I found it useful to use two different programs: one for tracking tickets at the initial release time where I would query the website every few seconds and one for tracking tickets across all available days where I would query the website once every minute. More details about the specifics of the Python scripts used for tracking the ticket availability are presented in the final section of this ReadMe. You could also read the Python scripts directly on this repository as they are commented.

Each time the website was queried for a specific ticket type, the program first checks if there are any days with tickets available and then records the ticket information such as ticket type, entry date and time, and the number of tickets available at the time the website was queried. After collecting the data for all available tickets, the page is refreshed and the available ticket information is collected again.

A quick note: On the coop culture website you will also find regular experience and full experience tickets with a guided tour included. These tours are typically offered 1-2 times a day and are given in French, Spanish, Italian, and English. For the purposes of this project, I only tracked the ticket availability for the English didactic tour and combined its availability with that of the ordinary or full experience ticket. Additionally, the Colosseum offers a limited number of tickets for visiting the Colosseum at night (8:30PM CET) only on certain days. These tickets are equivalent to the full experience English didactic tour tickets. In the analysis presented below, these tickets were tracked and the data was combined with the full experience tickets.

## Summary of webscraped data

### Ticket entry times
In Figure 1, I show selected entry times for Regular experience tickets (left panel), full experience arena tickets (central panel), and full experience undergrounds and arena tickets (right panel). For regular experience tickets, the entry times are spaced in 5 minute intervals starting at 9:15am CET (Rome time). The full experience tickets are not available every 5 minutes as in the regular experience ticket, with underground access tickets only containing 19 entry times for the whole day. Since only about 20 tickets are released per time slot for full experience with underground access tickets, that means that less than 400 out of the almost 20,000 daily visitors can visit the Colosseum's undergrounds. At present, I do not have a way of determining which time slots will be available for a given day before they are released, as the entry times vary from day to day and week to week. It seems that 9:00am CET is always the first time slot available for underground access and 9:15am CET for arena-only access and regular experience tickets, but more exploration is needed to confirm this. 

<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/TicketTimeSlots.png" alt="drawing" width="99.5%"/> 

*Figure 2: Available ticket times for the three main ticket types: regular experience (left panel), full experience arena (central panel), and full experience undergrounds and arena (right panel). The regular experience and full experience arena plots only show a subset of available times for that day, while the full experience undergrounds and arena ticket shows all available times for that day.*

### Ticket release times and availability
For both the regular experience and full experience options, tickets are released on a rolling basis precisely 30 days from the timed entry. For example, tickets for a 9:00am CET timed entry on July 31st will be released at precisely 9:00am CET on July 1st. Similarly, tickets for a 1:30pm CET timed entry on July 31st will be released at precisely 1:30pm CET on July 1st.

#### Regular experience tickets
Figure 2 illustrates the regular experience ticket availability when the website was queried 30 days before the entry date, 7 days before the entry date, 1 day before the entry date, and the day of the entry date. These illustrations (heatmaps) should be interpreted as follows: each cell block contains the maximum number of tickets available during the two weeks (April 21st, 2023 - May 5th, 2023) that the search was performed for an entry time within the time given by the width of the block and when the website was queried during the time interval given by the height of the block. For example, the 17 in the upper left cell of Figure 2a means that there was a maximum of 17 tickets available at any given moment between April 22nd, 2023 - May 5th, 2023 for entry times between 9:15am and 9:45am when I queried the website between 9:15am and 9:45am. A blank cell means no tickets were ever detected during that query timed interval.

As seen in the upper left heatmap, which illustrates the number of tickets available 30 days before your visit, tickets are released on a rolling basis exactly 30 days before the ticket entry time which is why the upper right portion of this heatmap is blank. Early morning entry times sell out the fastest, usually within a few seconds of being posted. Sometimes residual tickets are found at later times, which I think happens because people cancel their cart or something goes wrong with the transaction. For entry times later than 17:00CET, tickets do not sell out as quickly and are probably your best chance of getting tickets for a larger group, say a family of 6. As I discuss below in the additional notes section, I don't see any issue with purchasing these later entry time tickets, so long as you plan your day appropriately. The last timed entry is one hour before closing, which should be enough time to explore most of what the Colosseum has to offer.

Interestingly, there is a second batch of tickets that is released on a rolling basis exactly 7 days prior to the ticket's entry time (figure 2b). So if you missed the initial ticket release and all of the tickets were sold out, you can still wait to secure tickets 7 days before your visit. Finally, there is a good chance of securing tickets within 24 hours of the entry time (Figures 2c and 2d), which I would definitely recommend doing instead of trying to get tickets at the ticket office. You should start checking 8:00pm CET the night before the day of your visit.

All in all, it should be possible to secure this type of ticket near your desired time so long as you are actively checking the website at the time of release and have a reasonable internet connection. To optimize your chances of getting your ticket, follow the strategy provided in the conclusions section of this post.


<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance_30Days_7Days.png" alt="drawing" width="95%"/> 
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance.png" alt="drawing" width="95%"/> 

*Figure 3: Heatmaps illustrating the regular experience ticket availability when the website was queried (a) 30 days before the entry date, (b) 7 days before the entry date, (c) 1 day before the entry date, and (d) the day of the entry date. These heatmaps should be interpreted as follows: each cell block contains the maximum number of tickets available during the two weeks (April 21st, 2023 - May 5th, 2023) that the search was performed for an entry time within the time given by the width of the block and when the website was queried during the time interval given by the height of the block. All times are shown in CET (local Rome time).* 

#### Full experience tickets
Securing full experience tickets is a somewhat different story. The main challenge to getting these tickets is that they sell fast. Really fast. So fast that, even if you refresh the webpage on the exact moment that tickets are released, by the time it takes you to add the ticket to the cart (select ticket time, select amount of tickets, and bypass reCAPTCHA) the tickets will be sold out and you will be displayed with a disheartening error message saying "tickets are no longer available for your selected time." Even still, if you are a bit flexible on the day or time of your visit to the Colosseum, are very active in trying to secure tickets, and have a strong internet connection, there is a chance of securing a couple of the full experience with arena access tickets. To get the full experience with underground and arena access, you need all of the former plus luck. During my visit to the Colosseum, I asked one of the Colosseum's underground accompanying guides about the number of underground tickets and she said that only 15-20 tickets are released per time slot. It might also be true that 'official partners' (e.g. Get Your Guide, Viator) get priority access to the tickets that they want, but I cannot prove this.  

Figure 2 illustrates the full experience ticket availability when the website was queried (a) 30 days before the entry date, (b) 30 days before the entry date but only tickets with underground access are shown, (c) 7 days before the entry date, and (d) the day of the entry date. In Figures 3a and 3b, the empty columns centered at 10:00am and 1:30pm in Figure 3a and 10:00am, 11:30am, 1:30pm, and 2:30pm in Figure 3b are expected because the full experience tickets are not released in five-minute intervals as with regular experience tickets as we first saw in Figure 1 above. Figures 3a and 3b illustrate the difficulty in obtaining full-experience tickets on the day that they are released, especially if you are interested in underground access. The best time to lock down your tickets is the instant they are released, with an even better chance of getting tickets if you choose an evening time slot. Also, frequently one will find single tickets available at random entry times throughout the day. My guess is that most people go to the Colosseum with more than one ticket so these tickets linger. 

As with the regular experience tickets, a second batch of tickets is released 7 days in advance and the day before your visit. These tickets tend to not sell out as fast as the ones released 30 days before your visit. I have never seen the availability of tickets from 29 days - 8 days or 6-2 days before the ticket date, so I would not even bother checking the official website for these tickets.

  <img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/single_day_combined.png" alt="drawing" width="95%"/> 
  <img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined.png" alt="drawing" width="95%"/> 


*Figure 2: Heatmaps illustrating the full experience ticket availability when the website was queried (a) 30 days before the entry date, (b) 30 days before the entry date but only including tickets with underground access, (c) 7 days before the entry date, and (d) the day of the entry date. These heatmaps should be interpreted as follows: each cell block contains the maximum number of tickets available during the two weeks (April 22nd, 2023 - May 5th, 2023) that the search was performed for an entry time within the time given by the width of the block and when the website was queried during the time interval given by the height of the block. All times are shown in CET (local Rome time).* 

## Conclusions

### My suggested strategy for securing your tickets
Based on my research and time spent tracking ticket availability using Python code, I recommend the following approach to secure your tickets to the Colosseum:

First, you should decide which ticket you want to purchase: regular experience, full experience arena, or full experience undergrounds and arena (see the section on ticket information above for the details of each ticket type). 

Follow these steps if you want **regular experience** tickets:
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at your desired time. Tickets are released on a rolling basis every 5 minutes starting at exactly 9:15am [CET]. Each batch of tickets will be sold within seconds of being released, but there should be enough time to secure a couple of tickets, especially if you follow the query hack explained below. A second batch of tickets will go on sale 7 days before the visit date and there will likely be availability within 24 hours of the visit, but securing a specific time slot may be more challenging. 
  
Follow these steps if you want **full experience** tickets: 
  1) **Exactly 30 days before your visit:** Constantly check the official website for available tickets at your desired time. Tickets are released on a rolling basis, starting at 9:00am [CET], but not every 5 minutes as with the regular experience tickets (see the section on ticket entry times above for more details on ticket release times). Early morning tickets are nearly impossible to procure, but you may get lucky with some afternoon availability. It is likely that you could purchase tickets for one of the last entry times, which can work out just fine if you plan your day accordingly (see points 1 and 2 in the section "Other details for planning your trip to the Colosseum" below). Since every second counts when trying to secure these tickets, I have devised a plan of attack to snipe tickets as soon as they are posted to the website - see "A hack for scoring full experience tickets" section below.
  2) **Between 8 days and 30 days before your visit:** If you fail to obtain tickets on the release date, then I am afraid you will have to wait until 7 days before your trip before tickets will become available again on the official website. You can still hope to get lucky and periodically check the official website for ticket releases (or use the code in this repo to track ticket availability and automatically email you with any status changes). Another option is to purchase tickets from a third party vendor (e.g. [Get your Guide](https://www.getyourguide.com/-l2619/?cmp=brand&cq_src=google_ads&cq_cmp=16347902802&cq_con=140138745257&cq_term=get%20your%20guide%20colosseum&cq_med=&cq_plac=&cq_net=g&cq_pos=&cq_plt=gp&campaign_id=16347902802&adgroup_id=140138745257&target_id=aud-1393039795420%3Akwd-330551615914&loc_physical_ms=9003941&match_type=e&ad_id=628087479995&keyword=get%20your%20guide%20colosseum&ad_position=&feed_item_id=&placement=&device=c&partner_id=CD951&gclid=CjwKCAjwx_eiBhBGEiwA15gLN8p4A82rhyJEmiCAALMUMy_mdeXz0BvXwF_N1l2TG1ohiWQxsvzujhoCH_cQAvD_BwE) or [Viator](https://www.viator.com/Rome-tourism/d511-r53012372528-s955139426?mcid=28353&supbk=1&tsem=true&supci=-1275353003&supag=53012372528&supsc=aud-435409373039:kwd-315492548805&supai=228142181740&supap=&supdv=c&supnt=g&supti=aud-435409373039:kwd-315492548805&suplp=9003941&supli=&m=28353&supag=53012372528&supsc=aud-435409373039:kwd-315492548805&supai=228142181740&supap=&supdv=c&supnt=nt:g&suplp=9003941&supli=&supti=aud-435409373039:kwd-315492548805&tsem=true&supci=aud-435409373039:kwd-315492548805&supap1=&supap2=&gclid=CjwKCAjwx_eiBhBGEiwA15gLN3utr3qVZmIqBk9jTQX0_R73eAGXx_t4mVKSHDgH_FzAQnCOmyPQzhoC-8UQAvD_BwE)). These sites usually have an option to get a full refund on your tickets up to 24 hours in advance, which is good since there is still a possibility to get tickets from the official website. The markup on the tickets can be anywhere from 1.5-10x the original cost of the ticket, with underground access being especially costly. Also, sometimes these sites don't actually give you a ticket, but instead meet you outside of the Colosseum and Palatine Hill-Roman Forum area to let you in, which is not ideal if you want to explore on your own schedule.
  3) **Exactly 7 days before your visit:** The most likely time to find a ticket on the official Colosseum website is exactly 7 days before your visit time when a second batch of tickets is released on a rolling basis as was done on the initial release date. Again, follow the same strategy as you did in step 1 and you may have some more luck since these tickets don't appear to go as fast. It is also possible to find tickets available within 24 hours of your entry time, but that is cutting it too close for me and you will no longer have the option to return any tickets purchased from third-party sites.

Finally, there is still a chance to get tickets on the day of your visit, but expect long Queues and limited availability.

Will this approach work? It did for me!

### A time-saving hack for scoring your tickets
Given that both regular experience and full experience tickets sell out within a few seconds, every second counts when trying to secure your tickets. The mistake I think most people will make is to refresh the whole page when they are waiting for tickets to be refreshed. This will force the browser to render all the graphics on the webpage and then you will have to use the calendar to navigate to the correct month. The more efficient approach is to use the calendar arrows to repeatedly switch between the current month and the month that you want to get your tickets. If you are lucky enough to see the day turn green, and hence become clickable, you can then repeatedly click the calendar day as it will remain clickable even if there are no available tickets at that time. 

Here is a video of me implementing this strategy by hand: 

The code in this repo (described in more detail below) can easily be adapted to implement this strategy algorithmically. One could even launch several instances simultaneously (in parallel) to maximize the chances of getting the calendar day to turn green. In words, the algorithm will be something like this:
1) Launch several instances of the website and repeatedly navigate between two neighboring months, one of them should be the month of the day you want to buy tickets for. Each time you navigate, check to see if the calendar day has turned green, indicating that tickets were released. Click the calendar day and try to add any available tickets to your cart, but obtaining them may be difficult as you may have not refreshed at exactly the right moment. However, the goal with this first step is not to necessarily get tickets at the first time slot but rather to see the calendar date turn green and hence become clickable for all remaining time slots.
2) When tickets are about to be released at the next time slot, repeatedly click the calendar day until the ticket availability box displays some tickets. 
3) Working quickly, add the desired amount of tickets to your cart and bypass recapture.
4) Repeat steps 2 and 3 every 5 minutes until you secure the tickets.

## Other details for planning your trip to the Colosseum
1) You can visit the Palatine Hill-Roman Forum area before or after your Colosseum visit but it must be within 24 hours (for regular experience ticket) or 48 hours (for full experience ticket) of your timed entrance to the Colosseum.  It is not possible to enter the Colosseum at a time that is different than your listed time. However, this means that it is not essential to secure early morning tickets since you can plan to visit the Palatine Hill-Roman Forum area before your visit to the Colosseum. Of the three sites, the Colosseum requires the least amount of walking so it could actually make sense to save it for last. 
2) In terms of planning your day, it will take between 4.5-6 hours to fully explore the three sites (Colosseum, Palatine Hill, and Roman Forum), spending between 1.5-2 hours at each site. It is a lot of walking and can be especially tough on your heels because most of the ground is cobblestone. On my visit to the Colosseum, I took 18,000 steps and climbed 20 flights of stairs according to my iPhone Health app. One nice feature of the Palatine Hill-Roman Forum area is that there are several water fountains to refill your bottles with cold water and shady benches to sit and relax.
3) Note that the full experience undergrounds and arena tickets are nominative (i.e. contains the ticket holder's name) and you must provide this information during the checkout process. This is especially important to note if you are buying the ticket for someone else or for many people. You will not be allowed into the undergrounds if your ID does not match the name on the ticket and you cannot change the name on the ticket once it has been sold to you. 
4) You can still see the Undergrounds from above with a full experience arena ticket, but you will not get to walk through the undergrounds. So not getting an underground access ticket is not the end of the world. In fact, I would not pay the extra money to buy a ticket with underground access from a third-party reseller if I can get the full experience arena ticket from the official site.
5) Despite the widespread claim online that the website is 'glitchy' or 'buggy', I have not found this to be the case. Tickets sell out very fast, so even if you see tickets available at one moment in time, they may be sold out by the time you hit 'add to cart' and bypass Recaptcha. This can be quite frustrating, but I would not call it a bug. Once you have the tickets in the cart, they are secure for 15 minutes while you check out and you should not have any problems from this point on. 
6) The website slows down considerably near ticket release times when page requests are highest (we are not the only ones who are trying to buy tickets). 

## Python code for tracking ticket availability 
There are two Python scripts in this repository for tracking ticket information, where both scripts use Selenium to automate web browsing and extract ticket availability. Each time the website is queried, the collected ticket availability information is stored in a Pandas dataframe which is depicted below. Each row of the dataframe reports the number of tickets available for a given timeslot and is indexed by a string of the form 'queryDate_queryTime_ticketType'. The columns have two levels (hierarchical indexing) where the outer level is for the ticket date and the inner level is for the entry time of that date. The outer level is dropped when tracking ticket availability on a single date. Given that most queries will return no ticket availability, this dataframe is quite sparse (greater than 99% of entries are NaN) and so we use the Pandas built-in sparsity datatype (dtype = Sparse[float64, nan]). See [sparse_date_structures](https://pandas.pydata.org/docs/user_guide/sparse.html) for more information on sparse data types in Pandas.


<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/dataframe.png" alt="drawing" width="99.5%"/> 

*Figure 4: Snippet of the Panda's dataframe used for storing ticket availability. NaN means that there were no tickets available for that time slot.*

Each script has several control parameters to set query frequency, email frequency, ticket type to track, which dates to track, and how frequently to save dataframe (saved as .pkl files).

**1) ticket_tracker_single_day.ipynb:** This script is optimized for tracking ticket availability on the release date, which is useful if you are trying to obtain specific ticket type on a specific date and time. It contains functionality to send email alerts containing ticket information, including ticket type, entry date and time, number of tickets available, and link to the ticket. 

**2) ticket_tracker_all_days.ipynb:** This script is meant to track the ticket availability across all 30 days for which tickets have been released and for all ticket types of interest. This script is less useful for securing specific tickets for a specific date and more useful for collecting data on ticket availability as a function of time. If not for this script, I may not have learned about the second batch of tickets released 7 days in advance of entrance time.  

**3) eda_single_day_plotsV0.ipynb:** Notebook used to create heatmaps presented in this repository based on data collected using ticket_tracker_single_day.ipynb script. 

**4) eda_all_days_plotsV0.ipynb:** Notebook used to create heatmaps presented in this repository based on data collected using ticket_tracker_all_days.ipynb script. Also provides some functions for manipulating the panda.s dataframes with a hierarchical column structure.

<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Email_FEA_tickets.png" alt="drawing" width="99.5%"/> 
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Email_FEUA_ticket.png" alt="drawing" width="99.5%"/> 


*Figure 5: Examples of emails when tickets became available. FEUA = full experience undergrounds and arena access, FEA = full experience arena access*


