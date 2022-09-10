<%*
input = await tp.system.suggester(["log1", "log2", "log3"], ["log1", "log2", "log3"])
// **correlate field with select input**
if (input == "log3") { // **filter notes with certain frontmatter data, press ESC to create a new note**
	const started = app.vault.getMarkdownFiles().reduce((acc, file) => {
	  const frontmatter = app.metadataCache.getFileCache(file)?.frontmatter;
	  if (frontmatter?.status === "key") {
	    return [...acc, file];
	  }
	  return acc; 
	}, []);
	file = await tp.system.suggester(
	  (choice) => choice.basename,
	  started.filter((file) => file.path.includes("Notes"))
	);
    if (file == null) { // **if no file is selected, create a new note using a prompt, press ESC to exit prompt**
        file = await tp.system.prompt("")
        if (file == null) {
           append = "" 
        } else {
            path = this.app.vault.getAbstractFileByPath("Notes")
            // **template for new file**
            await tp.file.create_new('---\nstatus: key\n---\n[[README]] / [[Notes]] / `=this.file.link`\n\n>[!log]\n>```dataview\n>TASK FROM "Journal" WHERE contains(field, [[]]) SORT complete ASC\n>```\n\n\n', file, false, path) 
            append = "(field:: [["+ file +"]])"    
        }
    } else {
        append = "(field:: [["+ file.basename + "]])"
    }
} else {
	append = ""
}

-%>[[<%input%>]]<%append%> 