# Measures


Structuring measures in a layered way makes it much easier to go back, troubleshoot, and fix when errors occur, especially across multiple measures.


[Refrain from using inplict measures whenever possible(Expect in Key influencers visual and some other exceptions)](https://radacad.com/explicit-vs-implicit-dax-measures-in-power-bi)



<h2>

**Distinctcount** example:

</h2>

This calculates how many shots steph curry made by summing the number of rows in the collumn

 ```js
 TOTAL FG ATTEMPTED = DISTINCTCOUNT(CurryShots[Shot ID])

 //Defined once to be refrenced and filtered in other measures
 ```
> 

<h2>

**Calculate** example:

</h2>

Calculate is one of the most important functions in DAX, due to its ability to alter how measures are calculated, and precisely why its essenential and good practice to make `explicit measures` reusable


 ```js
 TOTAL FG MADE = CALCULATE(CurryShots[TOTAL FG ATTEMPTED],CurryShots[Outcome] = 1 )
 
 3PT FG ATTEMPTED = CALCULATE([TOTAL FG ATTEMPTED], CurryShots[Shot_Value] = 3)

 // This tell Power BI to filter on rows where the shot value is equal to 3
 // 
 ```

 ```js
 3PT FG MADE = CALCULATE(CurryShots[3PT FG ATTEMPTED],CurryShots[Outcome] = 1 )
 
 3PT FG MADE = CALCULATE(CurryShots[TOTAL FG MADE],CurryShots[Shot_Value] = 3 )
 
 //Two ways of calculating 3 pts shots made

 ```

 ```js
Population = CALCULATE(SUM(Indicators[Value]), Indicators[Indicator] = "SP.POP.TOTL")

GDP = CALCULATE(SUM(Indicators[Value]), Indicators[Indicator] = "NY.GDP.MKTP.CD")

// We are saying only SUM this ammount when using the population indicator or GDP indicator
 ```
 ```js
Expenses = CALCULATE([Transaction Ammount], FILTER(transactions, transactions[Type] = "debit"), transactions[Category] <> "transfer", Category[Category] <> "Credit Card Payment")

// <> Means !=
// its nice to visualise financial info with waterfall charts, it looks like crypto prices
 ```

 
<h2>

**Divide** example:

</h2>

 ```js
 TOTAL FG PERCENTAGE = DIVIDE([Total FG Made], [TOTAL FG ATTEMPTED], 0)

 // 0 = Alternate result for whenever we have to divide by 0 ```
 
```
<h2>

**Format** example:

</h2>


``` html
Syntax

FORMAT(<value>, <format_string>[, <locale_name(optional!)>])

```
 ```js
 Month = FORMAT('Date'[Day],"MMM")

 MMM = Display the month as an abbreviation (Jan-Dec). Localized.

 // This will make the Format

 Quarter = "Q" & FORMAT(QUARTER('Date'[Date]), "")

 // String Q ++ (The method format with method quarter)

"" == use basic number format
```
<h2>

**Comparison Operator** example:

</h2>

> **Less** than or equal sign

 ```js
Dates With Transactions = 'Date'[Date] <= MAX(transactions[Date])

 // Creating a column with this formula gives False on Dates that do not have a transaction
 
```
<h2>

**Calculate Table** example:

</h2>

 ```js
Expenses YTD = 
CALCULATE (
    [Expenses],
    CALCULATETABLE(
        DATESYTD('Date'[Date],"30/06")
    )
) 

// similar to calculate, it takes whatever table we give it, and allows us to filter it
 
```
 ```js
Expenses YTD = 
CALCULATE (
    [Expenses],
    CALCULATETABLE(
        DATESYTD('Date'[Date]),
        'Date'[Dates With Transactions] = True
    )
) 

// We added the Measure [Dates With Transactions] to filter on rows that have transactions, we also gave the table that the transaction is in, cuz it is required in this DAX function 
```
<h2>

**SUMMARIZE** example:

</h2>

This function takes a given collumn, and groups its values toghether into a unique list

 ```js
Monthly Budget =
SUMMARIZE('Date', 'Date'[YearMonth])

---

The result of this is another table where we have a single row per year per month (We used create table)


// the First Arg is the table we want to SUMMARIZE, the second arg is the one that we group by
// This is offten used to aggregate data from calculated tables
 
```
Lets say you have a table with color and a table with ammout

The SUMMARIZE Function will crunch the table until its one row per color, and we then we can sum the ammount for each color
<br><br>

<h2>

**CROSSJOIN** example:

</h2>

It takes two tables and merges them Toghether, creating another Table that contains all possible combinations of all rows from the original two tables

 ```js
Monthly Budget =
CROSSJOIN(SUMMARIZE('Date', 'Date'[YearMonth]),Budget)

/// This will display one row, per year and month, and budget category
```

*Example* If we take a table of 4 rows and CROSSJOIN into another table containing 10 rows, the resulting table will be 40 rows, in math its known as Cartesian product

<p align="center">
  <img src="img/Cartesian%20product.png" style="invert:(100%)" />
</p>


<br><br>
    <h1>https://docs.microsoft.com/en-us/dax/format-function-dax</h1>

<br>