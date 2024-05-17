---
tags:
  - "#daily"
code: 0
applications: 0
spending: 0
workout: 0
read: 0
pomodoro_count: 0
---
# `= this.file.name `
---

<< [[Timestamps/<% tp.date.yesterday() %>|Yesterday]] | [[Timestamps/<% tp.date.tomorrow() %>|Tomorrow]] >>

## Daily Logs 💭
---
#### What did you do [[Timestamps/<% tp.date.yesterday() %>|Yesterday]]?
- 

#### 🎉What are you excited to do today?
- 

#### 🚀 Thing(s) I plan to accomplish today...
- [ ] 

#### 👎One thing I'm struggling with today is...
- 


### Notes Created Today
---

```dataview
List FROM "Notes" WHERE file.cday = this.file.cday and this.file.name != file.name
```


### Edited Today
---
```dataview
List from "" where file.mday = this.file.cday and this.file.name != file.name
```

