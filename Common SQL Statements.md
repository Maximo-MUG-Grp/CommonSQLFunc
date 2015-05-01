Title: SQL
Category: Maximo
Tags: SQL, Date, BIRT
Date: 2015-03-19 14:16
Revised: 2015-05-01 08:54

###SQL Statements
This page was originally an [article on the site](http://mygeekdaddy.net/2013/04/17/javascript-date-functions-in-birt/) to hold a list of common and unique SQL statements. This page is a more permanent spot to reference SQL statements related queries, searches, or reports in IBM Maximo. There are two types of statements listed:

* _SQL Server Function:_ Lists the syntax to get the value in a Maximo Where Clause, BIRT selection statement or querying the database directly.
* _Javascript Function:_ Lists the syntax to get a value as data value used in BIRT's Expression Builder.

####Date of last Saturday
My company uses a maintenance reporting period of Saturday through Friday, so a common query is to know what's happened since last Saturday. This statement is used in conjunction with other date fields (e.g. `reportdate`, `orderdate`, etc), to show any records since the previous Saturday at 00:00am.

_SQL Server Function:_

	dateadd( week, datediff( week, 0, dateadd(day, +1 ,getdate()) ),-2);

_Javascript Function:_

	TBD

####Number of days since Saturday
A variant to the query above, this gives a decimal value of how many days it's been since Saturday.

_SQL Server Function:_

	select (cast(getdate() as float) - cast(dateadd( week, datediff( week, 0, dateadd(day, +1 , getdate() ) ),-2) as float));
	
_Javascript Function:_

	TBD

####Midnight next day:
Functions for setting a date at midnight for the next day.

_SQL Server Function:_

	dateadd(d,0,datediff(d,-1,getdate()))

_Javascript Function:_

	TBD

####First day of the previous month:
Functions look for the first day of the previous month, based on what the date is today.

_SQL Server Function:_

	dateadd(month,datediff(month,1,getdate()) -1,0)

_Javascript Function:_

	now = new Date();
	if (now.getMonth() == 0) {
 	   current = new Date(now.getFullYear() - 1, 11, 1);
	} else {
	    current = new Date(now.getFullYear(), now.getMonth() - 1, 1);
	}
	
####Last day of previous month:
Functions look for the last day of the previous month, based on what the date is today.

_SQL Server Function:_

	dateadd(day, -1, dateadd(month,datediff(month,1,getdate()) +0,0))

_Javascript Function:_

	now = new Date();
	if (now.getMonth() == 0) {
	    current = new Date(now.getFullYear() - 1, 11, 31);
	} else {
	    current = new Date (new Date(now.getFullYear(), now.getMonth(), 1) - 1);
	}
	
####First day of current month:
Functions look for the first day of the current month, based on what the date is today.

_SQL Server Function:_

	dateadd(month,datediff(month,1,getdate()) +0,0)

_Javascript Function:_

	now = new Date();
	new Date(now.getFullYear(), now.getMonth(), 1);
	
####Last day of current month:
Functions look for the last day of the current month, based on what the date is today.

_SQL Server Function:_

	dateadd(day, -1, dateadd(month,datediff(month,1,getdate()) +1,0))

_Javascript Function:_

	now = new Date();
	new Date (new Date(now.getFullYear(), now.getMonth() +1 , 1) - 1);
	
####First day of next month:
Functions look for the first day of the next month, based on what the date is today.

_SQL Server Function:_

	dateadd(month,datediff(month,1,getdate()) +1,0)

_Javascript Function:_

	now = new Date();
	if (now.getMonth() == 11) {
	    current = new Date(now.getFullYear() + 1, 1, 1);
	} else {
	    current = new Date(now.getFullYear(), now.getMonth() +1 , 1);
	}
	
####Last day of next month:
Functions look for the last day of the next month, based on what the date is today.

_SQL Server Function:_

	dateadd(day, -1, dateadd(month,datediff(month,1,getdate()) +2,0))

_Javascript Function:_

	now = new Date();
	if (now.getMonth() == 11) {
	    current = new Date(now.getFullYear() + 1, 1, 31);
	} else {
	    current = new Date(new Date(now.getFullYear(), now.getMonth() +2 , 1) -1 );
	}

####Exactly 'x' months ago:
Functions will give a date/time value of exactly 1 month ago.

_SQL Server Function:_

	dateadd(month,-1,getdate())
	
Change the `-1` to adjust how many months back the date/time value should be. Using a `+x` value to give a future date/time value.

_Javascript Function:_

	TBD
	
####Exactly 'x' days ago:
Similar to the function above, this statement will give a date/time value of exactly 30 days ago.

_SQL Server Function:_

	dateadd(day,-30,getdate());
	
Change the `-30` to adjust how many days back the date/time value should be. Using a `+x` value to give a future date/time value.

_Javascript Function:_

	TBD
