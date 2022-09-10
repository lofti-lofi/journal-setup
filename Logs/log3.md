[[README]] / [[Journal]] / [[log3|Log3]]

# Log3
![[nav]]

Group by field

>[!log]
> ```dataview
> TASK FROM "Journal" WHERE contains(text, "[[log3]]") AND !complete GROUP BY field AS T SORT T ASC
> ```