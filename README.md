# sqr_counts

Keeping track of a single count in SQR is easy, just add a line like 'let #cnt = #cnt + 1'.  Adding a couple of more is just as easy, and not too hard to track.  But, what if you want to start tracking number of employees or salaries in a department by location?  Then you have to get into the use of an array.  Want to count something else, then you need 2 arrays and so on.
This pair of array definitions and SQR procedures, provide the ability to do this with a couple of consistent procesdure calls.  The first to define what you are counting, and the second to add to that count definition.

Here is an example of defining a new count definition to count by the combination (concatentation) of (employee) status, year (of hire), and a field.  In this case, field will take on different values per the logic of the program:
   do define-new-cat('MissCountsYear', '"Status","Year","Field"', #r3pgIdx, 'Y')
These are really just labels and it is up to you as the programmer to make sure that your provide values to the counting procedure that are consistent and logical to provide accurate results.
   
During the execution of the program, at some point where queries are run and data is being analyzed, counts will be incremented by call such as this:
   let $cntStr = '"Active","' || $year || '","' || 'Def HM' || '"'   !Create the counting parameters
   do add-count-value('MissCountsYear', $cntStr, 1)                  !Count the number of these

In this example, we are doing a simple accumulation count, which is what the '1' represents, but it could be anything such as comp rate or another numeric value.  The comma separated values represent the index to what is being counted.  The count procedures will track a count at Active-Year-Def HM, as well as Active-Year, and just Active.  Default procedures will present the results in a basic HTML table.
