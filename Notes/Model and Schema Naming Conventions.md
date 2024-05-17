---
tags:
  - note
Framework: Mongoose
---
# `=this.file.name`
---

Consistency in naming helps improve code readability and maintainability. 

Here are some common conventions:

1. **Model Naming**:
    - Models represent collections in your MongoDB database. They should be named in **singular** form, using *PascalCase*.
    - Example: `User`
    - Mongoose actually takes the model name you provide, and it converts it to lowercase and it pluralizes it "behind-the-scenes". It then uses that as the collection name.

1. **Schema Naming**:
    - Schemas define the structure of documents within a collection. They should also be named in singular form, but using *camelCase*.
    - Example: `userSchema`


---
Created: April 18, 2024
Last Modified: `= this.file.mtime`
