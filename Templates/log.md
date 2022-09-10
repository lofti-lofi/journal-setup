<%*
name = tp.file.title
if (name.includes("Untitled")) {
	name = await tp.system.prompt("Title of Log")
	await tp.file.rename(name)
}
-%>
[[README]] / [[Journal]] / [[<%tp.file.title%>|<%tp.file.title.slice(0,1).toUpperCase()%><%tp.file.title.substring(1)%>]]

# <%name.slice(0,1).toUpperCase()%><%name.substring(1)%>
![[nav]]

>[!log]
> ```dataview
> TASK FROM "Journal" WHERE contains(text, "[[<%tp.file.title%>]]") AND !complete SORT file.name DESC
> ```