# NBA_analytics
Web Scraping NBA player statistics

Ball don’t lie and neither do data.

I have always been an avid fan of basketball but my love of the game has never intersected with any of my data science work. Here, I attempt to consolidate my two interests by conducting a fun and easy analysis on player statistics from 1980 to 2021 by scraping every player's data using Beautiful Soup, available on Basketball Reference( https://www.basketball-reference.com/) -- This site is essentially an encyclopedia for all things NBA stats. I hope to answer some of the age old debates in basketball such as:

-Who is better player: MJ (Michael Jordan) or LeBron James?

-Which year had the best draft class?

-How do player's performance differ between the regular season and the playoffs?

BeautifulSoup is a web scraper that allows us to search through the HTML of a webpage and extract the information we need. From there, we will store the data we scraped onto a DataFrame using pandas. The page on Basketball Reference looks like this:
<img width="1063" alt="Screen Shot 2021-06-29 at 4 16 53 AM" src="https://user-images.githubusercontent.com/67875208/123762475-d8419900-d890-11eb-8498-c704c4f9ced2.png">


As you can see, the data is already organized into a table. Now we will use urlopen that we imported from the urllib.request library, then create a BeautifulSoup object by passing through html to BeautifulSoup().
![Image 6-29-21 at 4 15 AM](https://user-images.githubusercontent.com/67875208/123762358-bb0cca80-d890-11eb-8317-a95be7f90522.jpg)

Here, the BeautifulSoup function passed through the entire web page in order to convert it into an object. Now we will trim the object to only include the table we need.
The next step is to organize the column headers. We want to extract the text content of each column header and store them into a list. We do this by inspecting the HTML (right-clicking the page and selecting “Inspect Element”) we see that the 2nd table row is the one that contains the column headers we want. By looking at the table, we can see the specific HTML tags that we will be using to extract the data:
<img width="1066" alt="Screen Shot 2021-06-29 at 4 18 05 AM" src="https://user-images.githubusercontent.com/67875208/123762645-01fac000-d891-11eb-9ffd-86927f45a75d.png">

Now, we go back to BeautifulSoup. By using findAll(), we can get the first 2 rows (limit = 2) and pass the element we want as the first argument, in this case ‘tr’, which is the HTML tag for table row. After using findAll(), we use the getText() to extract the table header, or ‘th’, text we need and organize it into a list:

![Image 6-29-21 at 4 18 AM](https://user-images.githubusercontent.com/67875208/123762802-23f44280-d891-11eb-88fc-9d8947ae8a76.jpg)

Next step, we will extract the data from the cells of the table in order to add it to our DataFrame. Although it is similar to extracting data from column header, the data within the cell, in this case player stats, is in a 2-dimensional format. Therefore, we must set up a 2-dimensional list:

![Image 6-29-21 at 4 19 AM](https://user-images.githubusercontent.com/67875208/123762933-471ef200-d891-11eb-9dbe-b8a7e52bd120.jpg)

Then, with the data and columns headers we have extracted from Basketball Reference, we create a simple DataFrame, containing NBA player statistics from 1980 - 2021.

Now for the exciting part:

How do we determine which draft class is the best? It’s easy to simply compare the career points, rebounds, and assists totals of players from each draft. Does that actually tell us that players from a certain draft class is better than the others? Probably not. To analyze the draft classes, I want to use stats that take into consideration other aspects of the game. These are the 3 best stats for the analysis: Player Efficiency Rating (PER), Value Over Replacement Player (VORP), and Win Shares Per 48 Minutes (WS/48).

Player Efficiency Rating (PER)
PER is a stat created by John Hollinger that takes into account accomplishments, such as field goals, free throws, 3-pointers, assists, rebounds, blocks and steals, and negative results, such as missed shots, turnovers and personal fouls. As stated in the name, this stat rates how effective a player’s impact is on the floor. Just to put this into perspective, Michael Jordan and Lebron James are the career leaders in PER. So, it’s a solid indicator for this analysis.

![download](https://user-images.githubusercontent.com/67875208/123763499-ddebae80-d891-11eb-9935-025e4a4a0d20.png)

Here we can see that the 2008 draft class leads PER category among all draft classes. 

Value Over Replacement Player (VORP)
VORP is a box score estimate of the points per 100 team possessions that a player contributed above a replacement level player, translated to an average team and prorated to an 82-game season. It is equivalent to WAR in baseball, where it indicates a players total contribution to their team.

![download (1)](https://user-images.githubusercontent.com/67875208/123763738-17bcb500-d892-11eb-8d04-c21be30ab50a.png)

Win Shares Per 48 Minutes (WS/48)
WS/48 is a stat that simplifies the number of win shares a player produces every 48 minutes (equal to 1 NBA game). Like VORP, win shares calculates the overall contribution of a player to a team’s win. Since every player does not play the same amount of minutes, WS/48 adjusts the stat to help compare among players.

![download (2)](https://user-images.githubusercontent.com/67875208/123763829-302ccf80-d892-11eb-844c-058d8e5b72a8.png)

Comparing PER, VORP, WS/48 for the best few draft classes...

![Picture1](https://user-images.githubusercontent.com/67875208/123764168-8994fe80-d892-11eb-93a6-f98db01c01a3.png)

![Picture1 2](https://user-images.githubusercontent.com/67875208/123764331-af220800-d892-11eb-91d2-84be9ab9cf4f.png)

![Picture1 3](https://user-images.githubusercontent.com/67875208/123764418-c3660500-d892-11eb-8795-4247c56bdad3.png)

Based on these features, the 2008 draft class seems to be the best overall draft class. Notable players include: Derrick Rose, Russell Westbrook, Kevin Love, Eric Gordon and DeAndre Jordan.

But what about the individual player stats? Let's dive right in. 

![Picture1 4](https://user-images.githubusercontent.com/67875208/123764699-07590a00-d893-11eb-8993-a73e6e992ea5.png)

![image](https://user-images.githubusercontent.com/67875208/123764849-2a83b980-d893-11eb-9ed9-5d597aa6aa6d.png)

![image](https://user-images.githubusercontent.com/67875208/123764869-31aac780-d893-11eb-8cd4-5eee6194b2d8.png)

![image](https://user-images.githubusercontent.com/67875208/123764962-4b4c0f00-d893-11eb-95b9-6a31cd075780.png)

Is there a difference between regular season performance and playoff performance stats?

![image](https://user-images.githubusercontent.com/67875208/123765085-6454c000-d893-11eb-81ad-82f9bd91df72.png)

![image](https://user-images.githubusercontent.com/67875208/123766684-e691b400-d894-11eb-85ed-0bb9cbf2e21d.png)

![image](https://user-images.githubusercontent.com/67875208/123766788-fb6e4780-d894-11eb-89e8-493c35dab83c.png)


![image](https://user-images.githubusercontent.com/67875208/123766836-05904600-d895-11eb-8a09-ec6fb77ff60a.png)


![image](https://user-images.githubusercontent.com/67875208/123766862-0c1ebd80-d895-11eb-9e68-b68d65f6ebc2.png)


![image](https://user-images.githubusercontent.com/67875208/123766890-10e37180-d895-11eb-81e4-1e1b0bd359ce.png)

![image](https://user-images.githubusercontent.com/67875208/123766917-15a82580-d895-11eb-9704-e8af5efd65a1.png)


![image](https://user-images.githubusercontent.com/67875208/123766935-19d44300-d895-11eb-9262-64901bc1b81c.png)







