### About this repository
Wrote an algorithm to track the ticket availability for entry into the Colosseum from the official website ([Coopculture](https://ecm.coopculture.it/index.php?lang=en)), where tickets are notoriously difficult to secure. Ticket availability was queried for 14 consecutive days in intervals between 3 seconds and one minute, depending on the time of day. Based on the collected data, a detailed plan is proposed to ensure that you get the best available tickets. Other features of the code allow for the user to be sent instantaneous email alerts with embedded links when tickets become available.

### Jump to section: 
* [Background](#background)      
* [My suggested strategy for securing your tickets](#my-suggessted-strategy-for-securing-your-tickets)   
* [Ticket information](#ticket-information) 
  * [Ticket types](#ticket-types) 
  * [Ticket release times](#ticket-release-times)
  * [Best times to secure your tickets](#best-times-to-secure-your-tickets) 
* [Python code for tracking ticket availability](#python-code-for-tracking-ticket-availability) 

## Background
Tickets to enter the Colosseum are notoriusly difficult to obtain from the official website ([coopculture](https://ecm.coopculture.it/index.php?option=com_snapp&view=products&snappTemplate=template3&catalogid=A4CC149C-BEE1-5773-5E59-01675F3EA81C&lang=en)) as only a limited supply of timed entry tickets are released 30 days in advance, and the majority of those tickets are scooped up by third party bots within seconds of being posted. These third party resellers (e.g. Viator, Get Your Guide, Tiqets, etc.) then sell the tickets for a mark up, sometimes for more than 10x the original ticket price. The goal of this project was to devise a strategy which optimizes your chances of securing Colosseum tickets from the official website, avoiding the exorbitant fees incurred by using third party resellers. 

<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Colosseum_in_Rome_wikipedia_image.jpg" alt="drawing" width="405"/> 
</picture>
 
 <picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Colosseum_in_Rome_inside_view_flickr.jpg" alt="drawing" width="406"/> 
</picture>
</p>

*Figure 0: Images of the outside (photo credit: wikipedia) and interior (phot credit: flikr) of the Colosseum in Rome. In the photo on the right, you can see the underground ruins which was located beneath the arena floor and is where the gladiators, animals, and special effect workers would plan for the show. Also shown is the reconstructed arena floor (tan floor in the right-center of the photo) where the battles took place.*

## My suggested strategy for securing your tickets
Based on my research and time spent tracking ticket availability using Python code, I suggest the following approach to securing your tickets to the Colosseum:

First, determine which ticket you want to purchase: regular experience, full experience arena, or full experience undergrounds and arena (see the section on ticket information below for the details of each ticket types). 

Follow these steps if you want **regular experience** tickets:
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at your desired time. Tickets are released on a rolling basis every 5 minutes starting at exactly 9:15am [CET]. Each batch of tickets will be sold within seconds of being released, but there should be enough time to secure a couple of tickets, especially if you are actively refreshing the ticket page and flexible on the entry time. A second batch of tickets will go on sale 7 days before the visit date and there will likely be availability within 24 hours of the visit, but securing a specific time slot may be more challenging. 
  
Follow these steps if you want **full experience** tickets: 
  1) **Exactly 30 days before your visit:** Constantly check the official website for available tickets at your desired time. Tickets are released on a rolling basis, starting at 9:00am [CET], but not every 5 minutes as with the regular experience tickets (see the section on ticket infromation below for more details on ticket release times). Early morning tickets are nearly impossible to procure, but you may get lucky with some afternoon availability. It is likely that you could purchase tickets for entry after 5:30pm, but the Colosseum closes at 7:00pm so your visit will be quite short. Since every second counts when trying to secure these tickets, I have devised a plan of attack to snipe tickets as soon as they are posted to the website - see this section of the readMe.md file for details and a video.
  2) **Between 8 days and 30 days before your visit:** If you fail to obtain tickets on the release date, then I am afraid you will have to wait until 7 days before your trip before tickets will become available again on the official website. You can still hope to get lucky and periodically check the official website for ticket releases (or use the code in this repo to track ticket availablilty and automatically email you with any status changes). Another option is to purchase tickets from a third party vendor (e.g. [Get your Guide](https://www.getyourguide.com/-l2619/?cmp=brand&cq_src=google_ads&cq_cmp=16347902802&cq_con=140138745257&cq_term=get%20your%20guide%20colosseum&cq_med=&cq_plac=&cq_net=g&cq_pos=&cq_plt=gp&campaign_id=16347902802&adgroup_id=140138745257&target_id=aud-1393039795420%3Akwd-330551615914&loc_physical_ms=9003941&match_type=e&ad_id=628087479995&keyword=get%20your%20guide%20colosseum&ad_position=&feed_item_id=&placement=&device=c&partner_id=CD951&gclid=CjwKCAjwx_eiBhBGEiwA15gLN8p4A82rhyJEmiCAALMUMy_mdeXz0BvXwF_N1l2TG1ohiWQxsvzujhoCH_cQAvD_BwE) or [Viator](https://www.viator.com/Rome-tourism/d511-r53012372528-s955139426?mcid=28353&supbk=1&tsem=true&supci=-1275353003&supag=53012372528&supsc=aud-435409373039:kwd-315492548805&supai=228142181740&supap=&supdv=c&supnt=g&supti=aud-435409373039:kwd-315492548805&suplp=9003941&supli=&m=28353&supag=53012372528&supsc=aud-435409373039:kwd-315492548805&supai=228142181740&supap=&supdv=c&supnt=nt:g&suplp=9003941&supli=&supti=aud-435409373039:kwd-315492548805&tsem=true&supci=aud-435409373039:kwd-315492548805&supap1=&supap2=&gclid=CjwKCAjwx_eiBhBGEiwA15gLN3utr3qVZmIqBk9jTQX0_R73eAGXx_t4mVKSHDgH_FzAQnCOmyPQzhoC-8UQAvD_BwE)). These sites usually have an option to get a full refund on your tickets up to 24 hours in advance, which is good since there is still a possibility to get tickets from the official website. The markup on the tickets can be anywhere from 1.5-10x the original cost of the ticket, where underground access can be especially costly. Also, sometimes these sites don't actually give you a ticket, but instead meet you outside of the Colosseum and Forum-Palantine area to let you in, which is not ideal if you want to explore on your own schedule.
  3) **Exactly 7 days before your visit:** The most likley time to find a ticket on the official Colosseum website is exactly 7 days before your visit time, when a second batch of tickets are released on a rolling basis as was done on the initial release date. Again, follow the same strategy as you did in step 1 and you may have some more luck since these tickets don't appear to go as fast. It is also possible to find tickets available within 24 hours of your entry time, but that is cutting it too close and you will no longer have the option to return any tickets purchased from third party sites.

Will this approach work? It did for me!

## Ticket information 

### Ticket types
There are three main ticket types you can purchase: the ordinary ticket (€18), the full experience arena ticket (€24), and the full experience undergrounds and arena ticket (€24). The following description of each ticket type was adapted from the coopculture website (see the Colosseum website for more details https://parcocolosseo.it/en/visit/opening-times-and-tickets/):

"""
**ADMISSION TICKETS**

**Regular experience ticket (€16 + €2 booking fee):**
Valid 24 h, it allows one entrance to the Colosseum and one entrance to the Forum - Palatine area.

**Full Experience Arena ticket (€22 + €2 booking fee):**
Valid for 2 days from the first use, it allows one entrance to the Colosseum with access to the Arena, one entrance to the Palatine Forum and SUPER sites.

**Full Experience Undergrounds and Arena ticket (€22 + €2 booking fee):**
Valid for 2 days from the first use, it allows one entrance to the Colosseum with access to the Undergrounds and Arena, one entrance to the Palatine Forum and SUPER sites. (NOTE FROM ME: These tickets are nominative and you will not be allowed to enter the underground unless your ID matches the name on the ticket.)
"""

Each ticket gives you one timed entry to the Colosseum and one entry to the Palatine-Forum area. You can visit the Palantine-Forum area before or after your Colosseum visit but it must be within 24 hours (for regular experience ticket) or 48 hours (for full experience ticket) of your timed entrance to the Colosseum.  It is not possible to enter the Colosseum at a time that is different than your listed time. The full experience also allows you access to the SUPER sites which are located within the Palantine-Forum area (see [PARCO](https://colosseo.it/en/) website for more details on the sites to see in the Colosseum and Palatine-Forum area).

Based on this information, it seems obvious that the full experience undergrounds and arena ticket is the best value, but as we will see below, the limited number of tickets and their high demand make these tickets the most difficult to obtain, especially during the summer months.

A quick note: On the coop culture website you will also find regular experience and full experience tickets with a guided tour included. These tours are typically offered 1-2 times a day and are given in french, spanish, italian, and english. For the purposes of this project, I only tracked the ticket availability for the English didactic tour and combined its availability with that of the ordinary or full experience ticket. 

### Ticket release times
Regular experience tickets are released exactly 30 days in advance in 5 minute intervals starting at 9:15am CET (Rome time) (Figure 1, left panel). The full experience tickets are not released every 5 minutes as in the regular experience ticket, with underground access tickets only containing ~20 entry times spread out across the day (central and right panel of figure 1). Again, tickets are released exactly 30 days from entry time, so you do not need to check the website every 5 minutes if you know what time slots will be available on that day. I do not yet have a way of determining which time slots will be available before they are released, as the entry times seem to vary by the day and week. It does seem that 9:00am CET is always the first time slot available for underground access and 9:15am CET for arena-only access, but more exploration is needed to confirm this. 

<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/TicketTimeSlots.png" alt="drawing" width="800"/> 
</picture>
</p>

*Figure 1: Available ticket times for the three main ticket types: regular experience (left panel), full experience arena (central panel), and full experience undergrounds and arena (right panel). The regular experience and full experience arena plots only show a subset of available times for that day, while the full experience undergrounds and arena ticket shows all available times for that day.*

### Best times to secure your tickets

#### Regular experience tickets
The initial release of regular experience tickets do sell out within thirty seconds of each release time, but it should be possible to secure this type of ticket near your desired time so long as you are actively checking the website at the time of release and have reasonable internet connection. Moreover, there is usually an abundance of tickets released 7 days prior to entry date which do not sell out as fast. The following two figures plot the regular experience ticket availability for 30 days (initial release), 7 days, 1 day, and the day of your visit. The heatmaps should be interpreted as follows: each cell block contains the maximum number of tickets available during the two weeks (April 22nd, 2023 - May 5th, 2023) that the search was performed for an entry time within the time given by the width of the block and when the website was queried during the time interval given by the the height of the block. For example, the 17 in the left panel of figure 2 means that there was a maximum of 17 tickets available for entry times between 9:15am and 9:45am when I queried the website between 9:15am and 9:45am during the two weeks. A blank cell means no tickets were ever detected during that query timed interval.

There are several take home messages from these heatmaps:
1) Tickets are released on a rolling basis
2) There is a good (possibly even better) chance of securing tickets within 24 hours of the entry time. You should start checking 8:00pm the night before your rome visit.
3) 

#### Regular experience tickets
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance_30Days_7Days.png" alt="drawing" width="750"/> 
</picture>
 
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance.png" alt="drawing" width="750"/> 
</picture>
 
</p>
Figure 2: 


Securing full experience tickets is a somewhat different story. The main challenge to getting these tickets is that they sell fast. Really fast. So fast that, even if you refresh the webpage on the exact moment that tickets are released, by the time it takes you to add the ticket to the cart (select ticket time, select amount of tickets, and bypass reCAPTCHA) the tickets will be sold out and you will be displayed with a disheartening error message saying "tickets are no longer availble for your selected time." Even still, if you are a bit flexible on the day or time of your visit to the Colosseum and are very active in trying to secure tickets and have a strong internet connect, there is a decent chance of securing a couple of the full experience with arena access tickets. To get the full experience with underground and arena access, you need all of the former plus lots of luck. 

The following two figures show the full experience ticket availability for the same two weeks as the figures above. The first plot shows the availability of tickets when the website was queried on the released date (30 days in advance). The left plot shows all types of full expereince tickets while the right plot only shows availability for full expreince tickets that include underground access. The empty times lost for the underground access is expected because of the time gaps in availble ticket entry times as we saw in figure 1 above. As with the regular experience tickets, a second batch of tickets are released 7 days in advance and the day before your visit (Figure 5). I have never seen availability of tickets from 29days - 8days or 6-2 days before the ticet date, so I would not even bother checking the official website for these tickets.

#### Full experience initial 30 day release
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/single_day_combined.png" alt="drawing" width="750"/> 
</picture>
 
 <picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined.png" alt="drawing" width="750"/> 
</picture>
 
</p>
Figure 4:



### A hack for scoring full experience tickets
Given that the full experience tickets sell out within a few seconds, every second counts when trying to secure your tickets. By far the step that slows us down is refreshing the page near the availability time and then advancing the month forward. If you are lucky enough to see the calendar day turn green and become clickable, you will likely be too late to purchase the tickets. The mistake I think most people will make is to then refresh the whole page again, which will cause the calendar day to become red again and not clickable. However, it is much faster to just repeatedly click the calendar day, which will remain clickable and will update with new tickets even if there is no availability. 

The code in this repo can be eaily adapted to implement this strategy algorithmically. One could even launch several instances simultaneously (in parallel) to maximize chances of getting the calendar day to turn green. In words the algorihtm will be somthing like this:
1) Launch several instances of the website and repeatedly refresh the webpage until you detect the calendar turn from green to red. Click the calendar day and if there are any availble tickets, then try to purchase them, but the goal with this first step is to not necessarily get tickets at the first time slot, but rather just to see the calendar date turn green and hence become clickable for all remaining time slots.
2) When tickets are about to be released at the next time slot, repeatedly click the calendar day until the tickey availbility box displays some tickets. 
3) Working quickly, add the desired amount of tickets to your cart and bypass recapture.
4) Repeat steps 2 and 3 every 5 minutes until you secure the tickets.

## Other details for planning your trip to the Colosseum
1) You can visit the Palantine-Forum area before or after your Colosseum visit but it must be within 24 hours (for regular experience ticket) or 48 hours (for full experience ticket) of your timed entrance to the Colosseum.  It is not possible to enter the Colosseum at a time that is different than your listed time.
2) Note that the full experience undergrounds and arena tickets are nominative (i.e. contains the ticket holders name) and you must provide this information during the checkout process. This is especially important to note if you are buying the ticket for someone else or for many people. You will not be allowed into the undergrounds if your ID does not match the name on the ticket and you cannot change the name on the ticket once it has been sold to you. 
3) You can still see the Undergrounds from above with a full experience arena ticket, but you will not get to walk through the undergrounds. So not getting underground access ticket is not the end of the world. In fact, I would not pay the extra money to buy a ticket with underground access from a third party reseller if I can get the full experience arena ticket for cheaper.
4) Despite the widespread claim online that the website is 'glitchy' or 'buggy', I have not found this to be the case. Tickets sell out very fast, so even if you see tickets available at one moment in time, they may be sold out by the time you hit 'add to cart' and bypass Recaptcha. This can be quite frustrating, but I would not call it a bug. However, once you have the tickets in the cart, they are secure for 15 minutes while you check out and you should not have any problems from this point on. 

5) The website slows down considerably near ticket release times when page requests are highest (we are not the only ones whoar e trying to buy tickets). 

## Python code for tracking ticket availability 
There are two python scripts in this repository for tracking ticket information. Both scripts use Selenium to automate web browsing and ticket availability extraction. Each time the website is queried, the collected ticket availbility information is stored in a Pandas dataframe which is depicted below. Each row of the dataframe reports the number of tickets available for a given timeslot and are indexed by 'queryDate_queryTime_ticketType'. The columns have two levels (hierarchical indexing) where the outer level is for the ticket date and t. The outer level is dropped when tracking ticket availability on a single date. Given that most queries will return no ticket availablility, this dataframe is quite sparse (greater than 99% of entries are NaN) and so we use the builtin sparsity datatype (dtype = Sparse[float64, nan]) available in Panadas [sparse_date_structures](https://pandas.pydata.org/docs/user_guide/sparse.html).  

Each script has several control parameters to set query frequency, email frequency, ticket type to track, which dates to track, and how frequently to save dataframe (saved as .pkl file).

**1) ticket_tracker_single_day.ipynb:** This script is optimized for tracking ticket availability on the release date, which is useful if you are trying to obtain specific ticket type on a specific date and time. It contains functionality to send email alerts containing ticket information, including ticket type, entry date and time, number of tickets available, and link to the ticket. 

**2) ticket_tracker_all_days.ipynb:** This script is meant to track the ticket availability across all 30 days for which tickets have been released and for all ticket types of interest. This script is less useful for securing specific tickets for a specific date and more useful for collecting data on ticket availability as a function of time. If not for this script, I may not have learned about the second batch of tickets released 7 days in advance of entrance time.  

**3) eda_all_days_plotsV0.ipynb:** Notebook used to create heatmaps presented in this repository based on data collected using ticket_tracker_all_days.ipynb script. Also provides some functions for manipulating the pandas dataframes with a hierarchical column structure.

**4) eda_single_day_plotsV0.ipynb:** Notebook used to create heatmaps presented in this repository based on data collected using ticket_tracker_single_day.ipynb script. 


<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Email_FEA_tickets.png" alt="drawing" width="800"/> 
</picture>
 
 <picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/Email_FEUA_ticket.png" alt="drawing" width="800"/> 
</picture>
 
</p>
Figure 4: Examples of emails when tickets became available. FEUA = full experience undergrounds and arena access, FEA = full experience arena access

