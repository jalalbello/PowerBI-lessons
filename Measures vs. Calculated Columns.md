# Measures vs. Calculated Columns

<h2> The diffrence is in the context</h2>

<br>

<h3>When we created a calculated collumn with DAX we were creating a formula that gets evaluated for <strong>Each Row</strong></h3>

> This is why they are good with date tables

So we should use **Calculated Columns** when we want to evaluate the data for each row in our table

<h3><strong>Measures</strong> gets calculated within the context of table / collumn card / Matrix ... </h3>

> Can be attactched to any table and do not store any data

> For example in a Matrix visual with years for each row and months for each collumn, add a mesure in there that averages our total expenses, **the formula will be evaluated for each combination** of year and month

> This why measures are incredibly fast and the perefered method for analysis in power BI, the values are being calculated dynamiclly, using our formula and no additional data is being created or stored in our data model, calculations are being created in Real Time as we are interacting with our data

>We should Use measures when we want to aggregate our data, like summing averaging and so on.

> Creating a new table to **move our measures** is a common trick power BI developpers use to organise, particularrly in larger reports, where we have alot of measures to keep track off

<strong> <h3>Calculated collumns/table</h3>
</strong> 

> They only get recallculated when we **refresh our data model** from its data source, and they **store their output** in our Data Model, if we add more to our files we need to refresh our data model to import the new collumns to see them in our report, (It will add the rows during the refresh most likely)

> We can Create Relationships **between a calculated Table and the other Tables** in our model that are not calculated