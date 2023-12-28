---
layout: post
title: "Code in the Cloud: Bringing FoodBasketApp to Life with Vercel Deployment"
feature_image: /assets/images/posts/2023-12-18-code-in-the-cloud/code-cloud-cover.gif
categories: misc
---

Sooooo,

last week I’ve finally finished the first version of my torontoFoodBasket App. For this first batch I wanted to at least implement the dropdown menu along with some of the information I’ve been scraping that I believe will be crucial for future functionalities (such as prices per 100g). One thing I can tell: it looked way easier when I came up with the designing in Figma . It took me at least three to four days to have the dropdown menu and to pull the necessary information from my database. When I’ve finished it felt like I’ve conquered the world!!! But wait, I still needed to deploy this bad boy.. and then came another crusade. In parallel, a job opportunity showed up and a friend was going to refer me. So well, I HAD to deploy my app. I feel really proud of the work I’ve been doing with this project and I wanted people to see it. I wasn’t too optimistic about the job, but I wanted to at least include this project in my application.

Deploying a static page is super simple, lots of alternatives out there. Personally for now I’ve been choosing Github pages. Even my personal portfolio website is hosted there. You don’t need more than a couple clicks to have any page up and running. The problem I had is that my app is not only a static page, it also has to communicate with my database, pulling information from it and manipulating such information. Well, then another chapter began.

Reading about deploying back-ends of applications I came around AWS services. They have the most robust service and infrastructure out there, I’ve always wanted to learn about it. Reality is, after a couple days I realized that there is a learning curve. AWS is a whole new world, and I’ll definitely get to grips with it, but now I needed to see my application working. So I found Vercel. Their platform is as intuitive as Github pages, but faster. Still, some changes needed to be done in my project in order to have it properly deployed.

Up until now, I had my front-end and back-end together at the same project.. It was just the way I’ve developed. And I couldn’t figure it out how I was going to deploy my back-end along with the front-end.. there might be a way but I didn’t find it yet (if there’s one, I’ll find). But then I realized I could simply have my back-end deployed as an Express API, given that all the information I was using from my database was feeding my application with JSON files. It’s been a while since I last built an API, so I came around this 6min tutorial from <a href="https://www.youtube.com/watch?v=B-T69_VP2Ls&embeds_referring_euri=https%3A%2F%2Fgabrielpoeta624025322.wordpress.com%2F&feature=emb_imp_woyt">Coding Gargen</a> .

Now I just had to adjust some routes on my Dropdown react component and redirect my Vercel front-end project to a custom domain I’ve bought. And Done. The first version of my torontoFoodBasket App is fully deployed. The backend of my app is now up, running, and feeding my my front end. It's so nice to see this project come to life, little by little. 

Lots to come 🚀🚀🚀
<br>

  ![Gif of the actor Tom from TV Show Vanderpump Rules celebrating]({{site.url}}/assets/images/posts/2023-12-18-code-in-the-cloud/giphy.gif){: style="display: block; margin: 0 auto"}
<br>
  <!-- ![Gif of the actor Tom from TV Show Vanderpump Rules celebrating](/assets/images/posts/2023-12-18-code-in-the-cloud/giphy.gif){: style="display: block; margin: 0 auto"} -->

