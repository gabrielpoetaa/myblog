---
layout: post
title: "The % Jingle: Unwrapping Rendering Surprises in My App for the Holidays"
feature_image: /assets/images/posts/2023-12-25-the-percentage-jingle/cover.png
categories: misc
---

The <a href="https://torontofoodbasket.com">torontoFoodBasket App</a> is an application that retrieves information from a backend I developed. Conversely, this backend is fueled by data collected through a web scraper I’ve also created. The web scraper saves details of 65 different food items in a MongoDB database. I process this data to render it in an API, from which my frontend extracts the information required for display. Operations that involve data manipulation, like calculating average price per 100g, are performed on the backend to prevent unnecessary calls and potential overloading of the frontend. However, a persistent issue arises when the frontend attempts to render information from items containing the special character ‘%’. This problem becomes apparent when the frontend generates a list of items for users to choose from based on the titles. My backend processes this list by sorting it alphabetically and removing duplicates, then handling the necessary data for each unique item.

The challenge emerges when the frontend fails to render information for items with ‘%’ in their title. For instance, items like “100% Pure Vegetable Oil” or “Quick 100% Whole Grain Oats” encounter rendering issues. Though I identified this problem some time ago, my recent holiday break allowed me the time to investigate further. Up until then, my Express API rendered documents with special characters flawlessly.

However, attempts by the frontend to retrieve information from such items failed, resulting in a console error with a status code of 400 (Bad Request) and a `‘SyntaxError: Unexpected token ‘<‘, “<!DOCTYPE “… is not valid JSON’ message. These errors suggested a potential issue with the endpoint the frontend was trying to reach.`

Exploring MongoDB documentation, I encountered the term ‘URL Encoding,’ a method used to represent special characters in a URL. For instance, spaces are represented as “%20,” and other characters have similar representations. To ensure proper formatting for safe web transmission like, URLs utilize this encoding. My investigation revealed that the correct encoding for an item with a title like ‘100% Pure Vegetable Oil’ should be something like ‘100%25%20Whole%20Wheat%20Bread.’ However, my frontend was attempting to access a different endpoint: ‘100%%20Whole%20Wheat%20Bread.’ The issue likely stemmed from the encoding of the ‘%’ character at the beginning of the title.
<br>
<br>  


<!-- ![Image of that displays the error within google devops tools](/assets/images/posts/2023-12-25-the-percentage-jingle/cover.png){: style="display: block; margin: 0 auto"} -->

![Image of that displays the error within google devops tools]({{site.url}}/myblog/assets/images/posts/2023-12-25-the-percentage-jingle/cover.png){: style="display: block; margin: 0 auto"}

<br>
This issue might not have occurred if I had generated the list of items using unique IDs. Unfortunately, when I initially developed the web scraper, I hadn’t assigned unique IDs to each item. By the time I realized the benefits of doing so, my web scraper had already been collecting data for almost a month. I subsequently implemented the schema with an ‘id’ field for each of the 65 items, but I haven’t had the time to rectify the data collected before this change.

Returning to the issue, suspecting a problem with the endpoint, I began trying to rectify my code. After several hours, I made progress in fixing items with ‘%’ in their title. However, this adversely affected my frontend rendering.
<br>
<br>

<!-- ![Image of first attemp to fix the issue](/assets/images/posts/2023-12-25-the-percentage-jingle/firstFix.png){: style="display: block; margin: 0 auto"} -->

![Image of first attemp to fix the issue]({{site.url}}/myblog/assets/images/posts/2023-12-25-the-percentage-jingle/firstFix.png){: style="display: block; margin: 0 auto"}


Although the information was now correctly retrieved from the backend, the frontend displayed poorly. Taking a break, I realized that I needed to rethink my approach. Instead of solely focusing on backend and frontend code modifications, I decided to explore adjustments to my web scraper.

After some thought I considered altering the titles in my database to circumvent the issue with special characters. Although I hadn’t read extensively about making permanent changes to documents in my database, I decided to give it a try. Referring back to MongoDB documentation, I crafted a code snippet to change the titles of specific items.
<br>
<br>

<!-- ![Image of first attemp to fix the issue](/assets/images/posts/2023-12-25-the-percentage-jingle/function.png){: style="display: block; margin: 0 auto"} -->

![Image of first attemp to fix the issue]({{site.url}}/myblog/assets/images/posts/2023-12-25-the-percentage-jingle/function.png){: style="display: block; margin: 0 auto"}

The result? It worked flawlessly!

I was elated to see those numbers on my screen. Solving these intricate problems and emerging with a functional solution is immensely satisfying. The new titles also looked cleaner. These recent days were truly exciting, and I’ve come to appreciate the incredible feeling of accomplishment from overcoming challenges. More often than not, I realize that with hard work and patience, there’s nothing I can’t achieve.

May you all have a blessed holiday season!

<br>
<br>

<!-- ![Emoji of Dwight, from The Office TV Show, celebrating Christmas](/assets/images/posts/2023-12-25-the-percentage-jingle/dwight-christmas.gif){: style="display: block; margin: 0 auto; width: 500px; height: 300px;"} -->


![Emoji of Dwight, from The Office TV Show, celebrating Christmas]({{site.url}}/assets/images/posts/2023-12-25-the-percentage-jingle/dwight-christmas.gif){: style="display: block; margin: 0 auto; width: 500px; height: 300px;"}



