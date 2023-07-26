## 1. Importing the Data
![nyc](https://github.com/WuCandice/NYC-Airbnb-Data-Analysis/assets/127648422/77270e89-fae0-4610-9dc4-9bdc552299b9)


<br>
Welcome to New York City (NYC), one of the most-visited cities in the world. 
As a result, there are many <a href="https://www.airbnb.com/"><em>Airbnb</em></a> listings to meet the high demand for temporary lodging for anywhere between a few nights to many months. 
In this notebook, we will take a look at the NYC Airbnb market by combining data from multiple file types like <code>.csv</code>, <code>.tsv</code>, and <code>.xlsx</code>.</p>
<p><br><br>
We will be working with three datasets:</p>
<ol>
<li><p><code>"datasets/airbnb_price.csv"</code></p></li>
<li><p><code>"datasets/airbnb_room_type.xlsx"</code></p></li>
<li><p><code>"datasets/airbnb_last_review.tsv"</code></p></li>
</ol>
<p><br><br>
Our goals are to convert untidy data into appropriate formats to analyze, and answer key questions including:</p>
<ul>
<li>What is the average price, per night, of an Airbnb listing in NYC? </li>
<li>How does the average price of an Airbnb listing, per month, compare to the private rental market? </li>
<li>How many adverts are for private rooms? </li>
<li>How do Airbnb listing prices compare across the five NYC boroughs?</li>

## 2. Cleaning the price column
<p>Now the <code>DataFrames</code> have been loaded, the first step is to calculate the average price per listing by <code>room_type</code>. </p>
<p>You may have noticed that the <code>price</code> column in the <code>prices</code> DataFrame currently states each value as a string with the currency (dollars) following, i.e.,</p>
<pre><code>price
225 dollars
89 dollars
200 dollars</code></pre>
<p></p>
<p>We will need to clean the column in order to calculate the average price.</p>

## 3. Calculating average price
<p>We can see three quarters of listings cost \$175 per night or less. </p>
<p>However, there are some outliers including a maximum price of \$7,500 per night! </p>
<p>Some of listings are actually showing as free. Let's remove these from the <code>DataFrame</code>, and calculate the average price.</p>

## 4. Comparing costs to the private rental market
<p>Now we know how much a listing costs, on average, per night, but it would be useful to have a benchmark for comparison. 
According to <a href="https://www.zumper.com/rent-research">Zumper</a>, a 1 bedroom apartment in New York City costs, on average, $3,100 per month. Let's convert the per night prices of our listings into monthly costs, so we can compare to the private market. </p>

## 5. Cleaning the room type column
<p>Unsurprisingly, using Airbnb appears to be substantially more expensive than the private rental market. We should, however, consider that these Airbnb listings include single private rooms or even rooms to share, as well as entire homes/apartments. 
<br><br>
Let's dive deeper into the <code>room_type</code> column to find out the breakdown of listings by type of room. The <code>room_type</code> column has several variations for <code>private room</code> listings, specifically: </p>
<ul>
<li>"Private room"</li>
<li>"private room"</li>
<li>"PRIVATE ROOM"</li>
</ul>
<p>We can solve this by converting all string characters to lower case (upper case would also work just fine). </p>

## 6. What timeframe are we working with?
<p>It seems there is a fairly similar sized market opportunity for both private rooms (45% of listings) and entire homes/apartments (52%) on the Airbnb platform in NYC.
<br><br></p>
<p>Now let's turn our attention to the <code>reviews</code> DataFrame. The <code>last_review</code> column contains the date of the last review in the format of "Month Day Year" e.g., May 21 2019. We've been asked to find out the earliest and latest review dates in the DataFrame, and ensure the format allows this analysis to be easily conducted going forwards. </p>

## 7. Joining the DataFrames.
<p>Now we've extracted the information needed, we will merge the three DataFrames to make any future analysis easier to conduct. Once we have joined the data, we will remove any observations with missing values and check for duplicates.</p>

## 8. Analyzing listing prices by NYC borough
<p>Now we have combined all data into a single DataFrame, we will turn our attention to understanding the difference in listing prices between <a href="https://en.wikipedia.org/wiki/Boroughs_of_New_York_City">New York City boroughs</a>. 
We can currently see boroughs listed as the first part of a string within the <code>nbhood_full</code> column, e.g., </p>
<pre><code>Manhattan, Midtown
Brooklyn, Clinton Hill
Manhattan, Murray Hill
Manhattan, Hell's Kitchen
Manhattan, Chinatown</code></pre>
<p></p>
<p>We will therefore need to extract this information from the string and store in a new column, <code>borough</code>, for analysis.</p>

## 9. Price range by borough
<p>The above output gives us a summary of prices for listings across the 5 boroughs. In this final task we would like to categorize listings based on whether they fall into specific price ranges, and view this by borough. 
<br><br>
We can do this using percentiles and labels to create a new column, <code>price_range</code>, in the DataFrame.
Once we have created the labels, we can then group the data and count frequencies for listings in each price range by borough.
<br><br>
We will assign the following categories and price ranges:</p>
<table>
<thead>
<tr>
<th>label</th>
<th>price</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Budget</code></td>
<td>\$0-69</td>
</tr>
<tr>
<td><code>Average</code></td>
<td>\$70-175</td>
</tr>
<tr>
<td><code>Expensive</code></td>
<td>\$176-350</td>
</tr>
<tr>
<td><code>Extravagant</code></td>
<td>&gt; \$350</td>
</tr>
</tbody>
</table>
