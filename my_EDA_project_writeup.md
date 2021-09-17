Women Tech Women Yes International + MTA Turnstile Data Analysis
Abstract:
The goal of this project is to recommend to the WTWY gala street team members the best train stations to stand near to optimize the number of email addresses collected for their annual gala. The tools used to answer this goal was exploratory data analysis with SQL and pandas and with Python visualization libraries like matplotlib and seaborn. 

Design:
The data was provided via the NY MTA Turnstile Database. Recommending the best train stations for our client would allow them to maximize the amount of signatures they receive with the limited street team members and limited time they have.

Data:
The dataset contains 478 unique stations across 14 weeks. Each row in the MTA Turnstile Dataset records the cumulative exit and cumulative entries every 4 hours of a single turnstile at a specific train station. The columns that I focused on in my analysis are: C/A, STATION, LINENAME, DATE, TIME, DESC, EXITS. 

Assumption:
The amount of people who do not exit via the turnstile and instead take an exit door is minimal and the data can still be used. 
Analyzing train stations with traffic slightly above the median will result in more signatures as the street team members are more likely to catch people. 

Tools:
Pandas and SQL for Exploratory Data Analysis
Matplotlib and Seaborn for Visualization

Algorithm:
I began my analysis by gathering 14 weeks of MTA Turnstile Data into a dataframe. Then I took the cumulative Exit values from the first audit event of each day (usually around 4:00AM). Therefore I isolated the Exits to one cumulative value per each day. I decided to examine Exits more closely over Entries, as I believe people are more likely to stop and interact with the street team members on their way out of the station than on their rush in.
 I then calculated the difference between each cumulative exit to receive the approximate amount of people exiting each train station each day. Additionally, I used a SQL query to confirm the differences I calculated in pandas were approximately equal across all days and stations. 
I noticed that for almost all differences in exits on 4/23/2021 (first date in my analysis), I received a very large negative number.  I realized that because the diff() function was always taking the difference of the previous row, on 4/23/2021 it was always taking the difference of another turnstile. I decided to remove all rows with a 4/23/2021 date in order to fix this issue. I also noticed some very large differences in exits on 4/24/2021 at certain stations and removed all rows with a 4/24/2021 date from all stations. 

After examining the data more deeply, I decided to remove any rows with missed audits that were recovered late (denoted via DESC == ‘RECOVR AUD’), and any difference in exits that were either less than 0 or greater than 1000000. 
I then calculated the sum of the difference in exits by each station (or the total new exits over the 14 week period) and extrapolated the 20 stations with sums that were slightly above the median (median over all stations = 275,134). I decided to analyze the stations between approximately the 50th and 75th percentile as I believe the street team members will have a better chance of receiving more signatures at those stations than at more busy train stations. Within the 20 stations we extrapolated previously, I calculated the control area (bank of turnstiles) with the highest number of exits. This information can be used to provide which exit (nearest that specific C/A) each street team member should stand near in order to maximize the number of signatures they receive. Lastly, I calculated the best days for the street team members to stand outside the 20 train stations I narrowed down in order to optimize the days the street team members were present.

Communication:
The powerpoint slides attached separately will best demonstrate this section. The slides will be presented to the WTWY team.
