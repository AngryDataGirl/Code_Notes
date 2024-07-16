
#PowerBI 
#DataModel 


Days all out of order?

1. Create a dimension table 

| DAY NUM | WEEKDAY NAME |
| ------- | ------------ |
| 1       | Monday       |
| 2       | Tuesday      |
| 3       | Wednesday    |
| 4       | Thursday     |
| 5       | Friday       |
| 6       | Saturday     |
| 7       | Sunday       |
2. Link dimension DAY NUM to the DAY NUM of your fact table
3. Under **Data View** tab in **Column Tools**, select **Sort by column** as DAY NUM
4. Use the Weekday Name as your dimension 