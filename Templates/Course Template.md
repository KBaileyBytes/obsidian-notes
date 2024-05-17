---
tags:
  - course
course_name: 
instructor: 
category: 
total_hours: 
link_to: 
sections: <% prompt = await tp.system.prompt("How many sections?", "0") %>
lectures: 
status: Archived
current_lecture: "0"
textbook:
---
# `= this.file.name`
---

**`= round(number(this.current_lecture) / number(this.lectures) * 100, 2)`% Lectures Complete!**
`= "<progress class='progress' value='" + this.current_lecture + "' max= '" + this.lectures + "'></progress>"`
<%*
for(let i = 0; i < prompt; i++) {
	await tp.file.create_new(tp.file.find_tfile("Module Template"), tp.file.title + " Module " + (i + 1)+ " - ", false, app.vault.getAbstractFileByPath("Notes"))
}
-%>

````ad-example
title: Curriculum
icon: book

```dataview
table choice(status = "Archived", "<span class='cm-formatting cm-formatting-hashtag cm-hashtag cm-hashtag-begin cm-meta cm-tag-tag'></span><span class='cm-hashtag cm-hashtag-end cm-meta cm-tag-tag'>Archived</span>",
choice(status = "Ongoing", "<span class='cm-formatting cm-formatting-hashtag cm-hashtag cm-hashtag-begin cm-meta cm-tag-tag'></span><span class='cm-hashtag cm-hashtag-end cm-meta cm-tag-tag' style='color:yellow !important;'>Ongoing</span>",
choice(status = "Complete", "<span class='cm-formatting cm-formatting-hashtag cm-hashtag cm-hashtag-begin cm-meta cm-tag-tag'></span><span class='cm-hashtag cm-hashtag-end cm-meta cm-tag-tag' style='color:green !important;'>Complete</span>", "other"))) as "Status",
"<progress max=" + lecture_count + " value=" + current_lecture + "> </progress> " as Progress,
link as Link
from [[#]]
sort status desc, number(file.name) asc
```

````

---
Created: January 4, 2024
Last Modified: `= this.file.mtime`

