# Time Intelligence

<h2>How to add more informations from the date Dimension</h2>

<br>

<h3>By exiting power query and going to the data home tab</h3>

<br>

<p align="center">
  <img src="img/new_table.png" style="width:100%;" />
</p>

  ```js

// Adding new collumns for month and year and day
 Year = YEAR('Date'[Date])

 //Defined once to be refrenced and filtered in other measures
 ```

Using weeknumber function in PWBI is tricky cuz sometimes the week ends in the next year, and that requires more advanced PWBI knowledge

We want to use Time intelligence for comparaisons like YTD, QTD, Year over year compairaison, Dax Makes it very easy it calculated, and the reason why is cuz we build our date table

Most of the time, Time intelligence Functions require a date continous date table, Dax needs to be able to evaluate our date and say for <i>example as of jan 6th ur expenses are 50 000dh</i>
or <i> we don't have transactions but we get no error </i>


<h2>

**DATESYTD** example

</h2>

 ```js
Expenses YTD = 
CALCULATE (
    [Expenses],
    CALCULATETABLE(
        DATESYTD('Date'[Date],"30/06")
    )
) 


// it returns a collumn of YTD, in whatever context we've set (slicers)

// Second arg(optional)"30/06" tell it wich day is the last day of the year (In case of june july fiscal years) 
```


<h2>

**SAMEPERIODLASTYEAR** example

</h2>

 ```js
Expenses PY = 
CALCULATE([Expenses], SAMEPERIODLASTYEAR('Date'[Date]))

//! Delcare the TABLE With single Quotes
// Reserve the double quotes for strings
```

<h3>

***Problem***, our budget does not span the entire years and months of our data model, its just being considered as a fixed value
</h3>

> Lets start by adding a year-month Calculated-collumn
>
>Format('Date'[date], "YYYY-MM")