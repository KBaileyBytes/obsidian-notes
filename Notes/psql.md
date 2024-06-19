---
tags:
  - note
---
# **`= this.file.name `**
---

`````ad-abstract
title: Cheatsheet






`````

| Exporting Data  | `COPY (SELECT * FROM your_table) TO '/path/to/file.csv' WITH CSV HEADER;`                                                                               | CSV, JSON, XML         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| Inserting Data  | Full Row - `INSERT INTO <table> VALUES (<value-list>);`<br>Partial Row - `INSERT INTO <table> (column-list) VALUES (<value-list>)` (default value fill) | Output -> `INSERT 0 1` |
| Load File Data  | `COPY <table> FROM <path> DELIMITER <delimiter> NULL <null-string> CSV`                                                                                 |                        |
| Delete Row      | `DELTE FROM <table> WHERE <condition>`                                                                                                                  |                        |
| Add Foreign Key | `ALTER TABLE <table-1> ADD CONSTRAINT Foreign Key (<fkey-columns>) REFERENCES <table-2> (<pkey-columns>);`                                              |                        |
| Update Data     | `UPDATE <table> SET <column> = <value> WHERE <condition>`                                                                                               |                        |

---
Created: June 11, 2024
Last Modified: `= this.file.mtime`
