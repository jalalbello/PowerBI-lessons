# Distinct Count, Calculate and Divide measure

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

 

**Divide** example:

 ```js
 TOTAL FG PERCENTAGE = DIVIDE([Total FG Made], [TOTAL FG ATTEMPTED], 0)

 // 0 = Alternate result for whenever we have to divide by 0 ```
 
