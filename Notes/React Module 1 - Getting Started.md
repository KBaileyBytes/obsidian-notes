---
tags:
  - module
lecture_count: "10"
current_lecture: "10"
length: 41min
status: Complete
course_link: "[[React]]"
link: https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25595350?components=add_to_cart%2Cavailable_coupons%2Cbase_purchase_section%2Cbuy_button%2Cbuy_for_team%2Ccacheable_buy_button%2Ccacheable_deal_badge%2Ccacheable_discount_expiration%2Ccacheable_price_text%2Ccacheable_purchase_text%2Ccurated_for_ufb_notice_context%2Ccurriculum_context%2Cdeal_badge%2Cdiscount_expiration%2Cgift_this_course%2Cincentives%2Cinstructor_links%2Clifetime_access_context%2Cmoney_back_guarantee%2Cprice_text%2Cpurchase_tabs_context%2Cpurchase%2Crecommendation%2Credeem_coupon%2Csidebar_container%2Cpurchase_body_container#overview
module_number: 1
short_link: <% tp.frontmatter["link"] %>
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] [[#What is React?]]
- [x] [[#Why would you use it?]]

```

## What is React?

```ad-example
title:

The official React [webpage](https://react.dev/) states that:

> React is a **library** for building user interfaces

Particularly, for single-page applications where the content is dynamically updated without requiring a full page reload. React allows developers to build reusable UI components and manage the state of their applications efficiently. It follows a component-based architecture, making it easier to develop and maintain complex user interfaces.

```

## Why would you use it?

```ad-info
title:

React is both a widely popular and efficient JavaScript library. If you look at a website like [Netflix](https://www.netflix.com/browse) which is built on React, you can see that interacting with the website is a very seamless experience. There's minimal loading screens (usually replaced with skeletons) and the responsiveness of the application makes it feel more like a mobile app.

When working with React you in the end write declarative code, which means you define a target UI state or states, not the steps needed to get there.

On the other hand, when writing vanilla JavaScript code you are writing imperative code, not declarative code which simply means you're not defining the goal but instead the steps needed to get there.

![[Pasted image 20240131114031.png | center]]

```

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
