---
tags:
  - note
  - pwsh
---
# `= this.file.name `
---

Get-Content

```
gc {path} -{head / tail} {line-count}
```

Ex.
```
gc .\A_year_of_pizza_sales_from_a_pizza_place_872_68.csv -head 10
╰─ 
	X,id,date,time,name,size,type,price
	1,2015-000001,1/1/2015,11:38:36,hawaiian,M,classic,13.25
	2,2015-000002,1/1/2015,11:57:40,classic_dlx,M,classic,16
	3,2015-000002,1/1/2015,11:57:40,mexicana,M,veggie,16
	4,2015-000002,1/1/2015,11:57:40,thai_ckn,L,chicken,20.75
	5,2015-000002,1/1/2015,11:57:40,five_cheese,L,veggie,18.5
	6,2015-000002,1/1/2015,11:57:40,ital_supr,L,supreme,20.75
	7,2015-000003,1/1/2015,12:12:28,prsc_argla,L,supreme,20.75
	8,2015-000003,1/1/2015,12:12:28,ital_supr,M,supreme,16.5
	9,2015-000004,1/1/2015,12:16:31,ital_supr,M,supreme,16.5
```



---
Created: June 15, 2024
Last Modified: `= this.file.mtime`
