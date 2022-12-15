![Pasted image 20221130221751](attachments/Pasted%20image%2020221130221751.png)




#engineering/coding #sandbox 



```dataview
TABLE Aliases AS "TAGS", foo AS "Summary", tag as "t" FROM #engineering/coding 
SORT rating DESC
```

```dataview
TABLE file.mtime AS "Last Modified", state AS "Status" WHERE state = "inProgress" SORT file.mtime DESC
```

```dataview
TABLE file.mtime WHERE state = "inProgress" SORT file.mtime DESC
```

