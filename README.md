# Colosseum Tickets
Code for webscraping ticket availability for entry to the Colosseum, Roman Forum, and Palatine Hill in Rome from the official Colosseum website. 

## Background
Tickets to enter the Colosseum are notoriusly difficult to obtain from the official website (https://www.coopculture.it/it/) as only a limited supply of timed entry tickets are released 30 days in advance, and those tickets are taken by third party bots within seconds of being posted. These third party users then sell the tickets for a mark up, sometimes by up to 10x the original ticket price (). The goal of this code was to determine when is optimal time to purchase a Colosseum ticket from the official website, avoiding the exorbitant fees incurred by using a third party resellers. 

## Conclusions
In conclusion, I suggest the following approach to purchasing tickets at the Colosseum:
  1) Exactly 30 days before your visit, constantly check the official website for available tickets at a desirable time. Tickets are released on a rolling basis, starting at 9:00am [CET] (see ticket infromation below for more information on ticket release times). Early morning tickets are nearly impossible to get, but you may get lucky with some afternoon availability. It is very likley that you could purchase tickets for entry after 5:30p, but the Colosseum closes at 7:00pm so your visit will be quite short.
  2) If that fails, the next step is to purchase tickets from a third party vendor (e.g. Get your Guide or Viator). These sites usually have an option to get a full refund on your tickets up to 24 hours in advance, which is good since there is still a possibility to get tickets from the official website. The markup on the tickets can be anywhere from 2-10x the original cost of the ticket. The full experience with underground are usually more than $130.
  3) Periodically check the official website for ticket releases (or use the code in this repo to track ticket availablilty and automatically email you with any status changes). The most likley time to find a ticket is exactly 7 days before your visit time, when a second batch of tickets are released. It is also possible to find tickets available within 24 hours of your entry time, but that is cutting it too close and you will no longer have the option to return any tickets purchased from third party sites.

## Ticket information (see Colosseum website for more details https://parcocolosseo.it/en/visit/opening-times-and-tickets/)
There are two main types of tickets you can purchase: the regular entrance (16 euros) and the full experience (24 euros). The regular entrance ticket allows one timed entry into the Colosseum and one entrance to the archaelogical area which contains the Roman Forum and Palantine. The Full experience has two types of tickets: one that adds access to the arena of the Colosseum and one that adds access the the arena and the underground, where the gladiators would prepare for battle. 

Regular experience tickets are released exactly 30 days in advance in 5 minute intervals starting at 9:15am Rome time (left panel figure 1). The initial release of these tickets do sell out within one minute of each release time, but it should not be difficult to secure this type of ticket near your desired time so long as you are actively checking the website at the time of release. Moreover, there is usually an abundance of tickets released 7 days prior to entry date which do not sell out as fast.

Obtaining the full experience tickets are a different story. For one thing, the tickets are not released every 5 minutes as in the regular entrance ticket, with underground access tickets only containing ~20 entry times spread out across the day (central and right panel of figure1). Again, tickets are released exactly 30 days from entry time, so you do not need to check the website every 5 minutes if you know what time slots will be available on that day. The time slots do change by the day, but there may be a weekly pattern (still need to collect this information). The second challenge to gettign these tickets is that the sell fast. Really fast. So fast that, even if you refresh the webpage on the exact moment that tickets are released, by the time it takes you to add the ticket to the cart (select ticket time, select amount of tickets, and bypass reCAPTCHA) the tickets will be sold out and you will be displayed with a disheartening error message saying "tickets are no longer availble for your selected time." 

Even till, if you are a bit flexible on the day or time of your visit to the Colosseum and are very active in trying to secure tickets, I have had some success in getting the Full experience with arena access just by constantly checking the website, at least getting 2 tickets. Underground access remains challenging, but I have one more trick that will help you to beat the bots and actually secure your underground ticket.

<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/TicketTimeSlots.png" alt="drawing" width="800"/> 
</picture>
</p>
## Webscraping details

## Results

### When do tickets initially go on sale and how long are they available for?
### Full experience initial 30 day release
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/single_day_combined.png" alt="drawing" width="800"/> 
</picture>
</p>

### Full experinece entrance tickets (7days and day of)
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined.png" alt="drawing" width="800"/> 
</picture>
</p>

### Regular entrance tickets (30days and 7days)
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance_30Days_7Days.png" alt="drawing" width="800"/> 
</picture>
</p>

### Regular entrance tickets (1day and day of)
<p align="center">
<picture>
<img src="https://github.com/nfasano/colosseumTickets/blob/main/figures/AllDaysCombined_RegularEntrance.png" alt="drawing" width="800"/> 
</picture>
</p>







