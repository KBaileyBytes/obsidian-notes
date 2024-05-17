---
tags:
  - course
course_name: Algorithms, Part 1 - Princeton University
instructor:
  - Old Guy
category: Theory
total_hours: 
link_to: https://www.coursera.org/learn/algorithms-part1/home/week/1
sections: 6
lectures: 11
status: Ongoing
current_lecture: "1"
textbook:
  - "[[Algorithhms 4th Edition by Robert Sedgewick, Kevin Wayne.pdf]]"
  - https://algs4.cs.princeton.edu/home/
glossary / answers: https://algs4.cs.princeton.edu/code/
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
from "Notes"
where contains(file.name, this.file.name) and file.name != this.file.name
sort status desc, number(file.name) asc
```

````

```ad-abstract
title: Console: Redirecting and Piping Data

![redirection and piping from the command line | center | 800](https://algs4.cs.princeton.edu/11model/images/redirect.png)

```



---
Created: January 4, 2024
Last Modified: `= this.file.mtime`

