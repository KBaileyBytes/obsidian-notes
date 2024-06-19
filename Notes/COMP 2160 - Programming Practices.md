---
tags:
  - course
course_name: COMP2160 - Programming Practices
instructor:
  - Franklin Bristow
category: C/Unix/Bash
total_hours: 40
link_to: https://www.youtube.com/playlist?list=PLGqzRfI3gmje2f9SN2OBtfgb3bqnVkzg1
sections: 28
lectures: 28
status: Ongoing
current_lecture: "1"
textbook:
  - "[[Advanced.Programming.in.the.UNIX.Environment.3rd.Edition.0321637739.pdf]]"
---
# `= this.file.name`
---

**`= round(number(this.current_lecture) / number(this.lectures) * 100, 2)`% Lectures Complete!**
`= "<progress class='progress' value='" + this.current_lecture + "' max= '" + this.lectures + "'></progress>"`

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

