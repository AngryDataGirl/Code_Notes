
#PowerBI #DAX

``` 
Count of CARD_NUMBER divided by Count of PRI =

# using quick measure to do a quick divide 
DIVIDE(
	
	# thing we are calculating in the numerator
    DISTINCTCOUNT('CARTE_ACCES'[CARD_NUMBER]),

    CALCULATE(
    
		# thing we are calulating in the denominator
        DISTINCTCOUNT(FACT_EMPLOYEE[PRI]),
		
		#filter clause
        FILTER(
	        FACT_EMPLOYEE,FACT_EMPLOYEE[Telework type] = "Hybrid" || 
	        FACT_EMPLOYEE[Telework type] = "Onsite"
	        )

		)
	)
```
