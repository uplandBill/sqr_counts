# sqr_counts

Keeping track of a single count in SQR is easy, just add a line like let #cnt = #cnt + 1.  Adding a couple of more is just easy, and not too hard to track.  But, what if you want to start tracking number of employees or salaries in a department by location?  Then you have to get into the use of an array.  Want to count something else, then you need 2 arrays and so on.
This pair of array definitions and SQR procedures, provides the ability to do this will 2 couple of consistent procesdure calls.  The first to define what you are counting, and the second to add to that count definition.

Here is an example of defining a new count to count by the combination of (employee) status, year (of hire), and a field.  In this case, field will take on different values per the logic of the program:
   do define-new-cat('MissCountsYear', '"Status","Year","Field"', #r3pgIdx, 'Y')
   
during the main execution of the program, at some point where queries are run and data is being analyzed, counts will be incremented by call such as this:
   let $cntStr = '"Active","' || $year || '","' || 'Def HM' || '"'   !Create the counting parameters
   do add-count-value('MissCountsYear', $cntStr, 1)                  !Count the number of these

In this example, we are doing a simple accumulation count, which is what the '1' represents, but it could be anything such as comp rate or another numeric value.
