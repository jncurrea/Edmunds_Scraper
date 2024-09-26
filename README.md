# Edmunds Scraper
## By Jose Currea, Ramzi Kattan, Hadley Krummel, Evan Hadd, and Jenna Ferguson

![Edmunds](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/download.jpeg)

<br>
This project uses web-scraping techniques with the goal of providing advice/insights based on Edmunds.com forum discussions. It's aim is to perform market research for any entry-level luxury brand that wants to break into the automotive field.
<br>
This project was separated into several tasks that allow easy reading for people who want to reference the project and easy troubleshooting. The steps were:

- Build the scraper for Edmund's Forum (Tools used: BeautifulSoup)
- Tokenizing comments and making sure Zipf's law holds
- Finding the top 10 popular brands by number of mentions
- Calculating lift values among brands to check association between brands (Is Brand B being mentioned when Brand A is mentioned?) 
- Calculating lift values between brands and common attribute (Is Brand A associated with luxury/performance/speed?)
- Calculating lift values between brands and "aspirational" messages (Is Brand A the brand that people aspire/want/wish for the most?)
- Conslusions and recommendations
<br>

### Step 1: Build Scraper
For this step, we built a scraper using BeautifulSoup. This scraper iterated over the first 300 pages of [Edmund's Discussion Forum](https://forums.edmunds.com/discussion/2864/general/x/entry-level-luxury-performance-sedans). <br> The flow we followed was:
- Iterate over each comment
- Append each message and respective date into a dictionary
- Go to next page <br>
For reference on the code, please refer to the [Source Code](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/edmunds_scraper.ipynb)

### Step 2: Tokenize and test Zipf's Law
For this step, we used the ".split()" method built in in python to tokenize the messages into list of words. One example of this method in action can be seen here: <br>
![Tokenization Example](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/tokenization.png)
<br>
After tokenizing, we moved on to test Zipf's Law on our data. Recall Zipf's Law states that the frequency of an item is inversely proportional to its rank, or that the frequency decreases as the rank increases. Basically, the most common word will appear about twice as often as the second most common word, three times as often as the third most common word, and so on.
<br>
The following plots show the behaviours of all our words and the top 100 words (ranked by frequency):
![All Words Zipf's Law](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/log_all_words.png)
![Top 100 Words Zipf's Law](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/log_top100.png)
<br>

#### Statistical Description

According to our statistical exploration, the slopes found in the previous problem are statistically different than the zipf's law slope of -1. Since the t scores are large and the p values are small, this means that we reject the null hypothesis. The standard deviations that result from the regression are extremely small, which is what causes a high t score and therefore a statistically significant difference between the slope produced and the -1 slope of the null hypothesis. 

### Step 3: Finding the top 10 popular brands by number of mentions
For this step, we scraped the [KBB Website](https://www.kbb.com/car-make-model-list/used/view-all/make/) to account for as most carbrands as we could. After scraping we performed a replacement process were we replaced specific models of a brand, for the actual brand name (e.g replacing m3 for BMW).<br> Refer to the [Make Model CSV](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/merged-1.csv) for more examples. <br> After performing this scraping process, we proceeded to find the top 10 brands by frequency of mentions in the comments. These brands are the following: <br>
![Top 10 Brands](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/top_10_brands.png)

### Step 4: Calculating lift values among brands to check for association
Now we start building data driven insights for any entry-level luxury brand that wants to break into the automotive field. Let's recall that lift values is a measurement used to check association between words. When we talk about association we are making reference to how often a word is mentioned when another word is mentioned (e.g how often is BMW mentioned when Audi is present in the same comment?) <br>
![Lift Formula](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/lift_formula.png)
<br>
After performing this analysis and plotting the lift values, we can give some insights regarding brand perception and brand clustering

![Lift between brands](https://github.com/jncurrea/Edmunds_Scraper/blob/main/Assignment1/Reference_Images/lift_brands.png)

#### Brand Perception
- Lexus, Infiniti, and Acura are positioned close to each other in the MDS plot, indicating that consumers often mention these brands together. This suggests that they are perceived similarly in terms of features, quality, or value proposition in the entry-level luxury segment. JD Power should consider these brands as direct competitors and further investigate the specific attributes that consumers associate with them.
- Audi and BMW are relatively close in the plot but distinctly separate from other brands, indicating a strong presence in the luxury segment with unique positioning. These brands are likely competing for the same high-performance and luxury-focused consumer base. Any marketing or product strategy for these brands should focus on their performance and luxury heritage.

#### Brand Clustering
- Toyota, Nissan, and Honda are clustered away from the core luxury segment, indicating that while they may offer entry-level luxury models, they are primarily perceived as value-oriented or non-luxury brands. This could be due to their broader product range that includes more economy and family-oriented vehicles. JD Power could explore the potential for these brands to further penetrate the entry-level luxury market by enhancing luxury features or branding these specific models more distinctly.
- Chrysler is positioned separately from the other brands, which may reflect its divergence from the entry level luxury market. This distinct positioning can be an advantage, but JD Power should monitor whether Chrysler’s brand perception aligns with entry-level luxury or if it is viewed more as a niche brand.
