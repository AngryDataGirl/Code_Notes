
#SQL #Normalization #Database

> [!Tip]
"Normalize till it hurts, denormalize till it works."

Here’s a quote from Kimball, The Data Warehouse Toolkit, page 8:

> 3NF structures are immensely useful in operation processing because an update or is set touches the database in only one place. 
> Normalized models, however, are too complicated for BI queries. Users can’t understand, navigate, or remember normalized models that resemble a map of the LA freeway. Likewise, most relational database management systems can’t efficiently query a normalized model. “

So there’s a pretty clear division there already: human accessibility vs computer accessibility. Are you building a data warehouse that will ultimately be queried by a human being, who is going to want to put together a bunch of arbitrarily complex views and slices of the data? Or is this just transactional data that needs to be logged and left alone?

If you're using the same piece of data repeatedly but in one table and one table only, then honestly, normalising it out might be more trouble than it's worth. Experienced this exact problem where if you normalise everything for the sake of normalising everything, you end up with something which is borderline impossible for humans to maintain or understand.