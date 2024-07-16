# get letters only from a string
```
[[:alpha:]]*
```

# get everything up until char
in this case it is a `,`
```
^([^,]*)
```
# get everything after char
```
[^,]*$
```

# name extracts
```
    /* try first initial of first name*/
    SUBSTR(SUBSTR(first_initials,1,1)||surname,1,8) as username1, 
    /* first initial of combo names */
    SUBSTR(SUBSTR(first_initials,1,2)||surname,1,8) as username2,
    /* try second initial of second name*/
    SUBSTR(SUBSTR(first_initials,2,1)||surname,1,8) as username3,
    /* try first two letters of first name */
    SUBSTR(SUBSTR(REGEXP_SUBSTR(NAME,'[^,]*$'),1,2)||surname,1,8) as username4, 
    /* first initial and truncated last name*/
    SUBSTR(first_initials,1,1)||SURNAME_TRUNC as username5,
    /*  third initial*/
    SUBSTR(SUBSTR(first_initials,3,1)||surname,1,8) as username6,
    /* first initial and 7 letters*/
    SUBSTR(SUBSTR(first_initials,1,1)||surname,1,7) as username7 
```