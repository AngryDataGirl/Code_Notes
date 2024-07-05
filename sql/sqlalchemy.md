[python - SQLAlchemy: engine, connection and session difference - Stack Overflow](https://stackoverflow.com/questions/34322471/sqlalchemy-engine-connection-and-session-difference)
### Running .execute()

When executing a plain `SELECT * FROM tablename`, there's no difference in the result provided.

The differences between these three objects do become important depending on the context that the `SELECT` statement is used in or, more commonly, when you want to do other things like `INSERT`, `DELETE`, etc.

### When to use Engine, Connection, Session generally

- **Engine** is the lowest level object used by SQLAlchemy. It [maintains a pool of connections](http://docs.sqlalchemy.org/en/latest/core/pooling.html) available for use whenever the application needs to talk to the database. `.execute()` is a convenience method that first calls `conn = engine.connect(close_with_result=True)` and the then `conn.execute()`. The close_with_result parameter means the connection is closed automatically. (I'm slightly paraphrasing the source code, but essentially true). _edit: [Here's the source code for engine.execute](https://github.com/sqlalchemy/sqlalchemy/blob/d514c032cd0349afc93f89d5b99835198ae70112/lib/sqlalchemy/engine/base.py#L2165-L2166)_
    
    You can use engine to execute raw SQL.
    
    ```python
      result = engine.execute('SELECT * FROM tablename;')
      # what engine.execute() is doing under the hood:
      conn = engine.connect(close_with_result=True)
      result = conn.execute('SELECT * FROM tablename;')
    
      # after you iterate over the results, the result and connection get closed
      for row in result:
          print(result['columnname']
    
      # or you can explicitly close the result, which also closes the connection
      result.close()
    ```
    
    This is covered in the docs under [basic usage](http://docs.sqlalchemy.org/en/latest/core/connections.html#basic-usage).
    
- **Connection** is (as we saw above) the thing that actually does the work of executing a SQL query. You should do this whenever you want greater control over attributes of the connection, when it gets closed, etc. An important example of this is a [transaction](http://docs.sqlalchemy.org/en/rel_1_0/core/connections.html#using-transactions), which lets you decide when to commit your changes to the database (if at all). In normal use, changes are auto-committed. With the use of transactions, you could (for example) run several different SQL statements and if something goes wrong with one of them you could undo all the changes at once.
    
    ```python
      connection = engine.connect()
      trans = connection.begin()
      try:
          connection.execute(text("INSERT INTO films VALUES ('Comedy', '82 minutes');"))
          connection.execute(text("INSERT INTO datalog VALUES ('added a comedy');"))
          trans.commit()
      except Exception:
          trans.rollback()
          raise
    ```
    
    This would let you undo both changes if one failed, like if you forgot to create the datalog table.
    
    So if you're executing raw SQL code and need control, use connections
    
- **Sessions** are used for the Object Relationship Management (ORM) aspect of SQLAlchemy (in fact you can see this from how they're imported: `from sqlalchemy.orm import sessionmaker`). They use connections and transactions under the hood to run their automatically-generated SQL statements. `.execute()` is a convenience function that passes through to whatever the session is bound to (usually an engine, but can be a connection).
    
    If you're using the ORM functionality, use a session. If you're only doing straight SQL queries not bound to objects, you're probably better off using connections directly.