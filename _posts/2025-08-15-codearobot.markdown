---
layout: post
title:  "How I Created Code-A-Robot"
date:   2025-08-15 21:37:26 -0500
image: https://jacobkaiserman.com/logoShadow.png
---
<h1>How I Created Code-A-Robot</h1>


In my freshman year of high school, I decided to join my school’s robotics team. At that time, I already had some coding knowledge. I had taught myself JavaScript, HTML/CSS, Python, and a bit of PHP. Going into the club, I quickly realized that all the previous programmers had graduated, leaving me as the only one on the team. As a freshman, I did all the programming, learning Java as I went along. That year, our team did not perform very well. We were mostly freshmen and had no idea what we were doing. We ranked last in our league, but we learned a lot.

Sophomore year was much better. I had become almost fluent in Java from robotics and taking AP CSA. However, I was still the only programmer on the team. I became co-captain and spent a lot of time working on the robot. That year, we were consistently in the top 10 teams in our league. While we did not make it to state, we were satisfied with what we had accomplished.

I knew that for this year (my junior year), we needed more programmers. Coding and debugging the robot is not a one-person job. However, there are not many beginner-friendly resources. Existing Java courses were great, but none of them tied Java directly to robotics. Sure, there was Learn Java for FTC, but few people want to spend hours reading through a PDF. This was the problem my team faced when I was a sophomore. There were plenty of people who wanted to learn to code robots, but there were no simple and engaging resources to help them.

This summer, I decided that I wanted to make a website with lessons on the bare basics of programming for FTC. Something that would help new programmers and rookie teams get started without overwhelming them. That is when I started working on Code-A-Robot. The goal of this project was to teach teams the necessary skills to get a robot up and running, in manageable lessons.

---

## Creating the Bones of the Site

Before creating the site, I had made a few basic static sites using HTML, CSS, and JavaScript. These sites were basic and hosted on GitHub Pages, with domains from Google Domains (RIP). I had also created a website with PHP for businesses to get rid of unneeded pallets. Being into woodworking, I had seen videos of people transforming pallet wood into furniture. I myself went dumpster diving to find pallets, and had built a few things with them. I created a site for businesses to list pallets they no longer needed so that woodworkers could use them. 

This, however, was not the greatest idea for a website. I think that I just wanted to create a site, and I did not think much of the idea. I mean, why wouldn’t businesses just use Facebook Marketplace or Craigslist? And how many businesses would take the time to photograph their pallets and create a listing instead of just throwing them in the dumpster? Although this site was a flop and no longer exists, I learned a ton about backend development through it. I created the site the “old-fashioned” way using PHP and a MySQL database hosted on a shared VPS.

For this new site, I wanted a more modern stack. After some research, I found Next.js, which was perfect. It looked great and was cheaper to run than a standard PHP site.  

My tech stack ended up being:
- Next.js (App Router) for the front end, middleware, and backend  
- React for UI components  
- Tailwind CSS for styling  
- Supabase for authentication, progress tracking, and lesson storage (PostgreSQL)  
- Vercel for hosting  
- NameCheap for DNS  
- CheerpJ for the web-based editor  
- AceEditor for syntax highlighting  

The one issue was that I did not know React or Next.js. I looked through the Next.js docs and was able to understand the basics of it. To be honest, I still do not consider myself to know React or Next.js well, even though I built an entire site with them. I was able to build the site by creating a “shell” of a site by modifying a template and with the help of my amazing assistant, ChatGPT. Yes, some of the site was “vibe coded”, but I mostly know what I’m doing ;)  

The bare-bones version of the site handled user authentication, lesson management, and user settings. The authentication and settings were “borrowed” from a Supabase + Next.js starter template. I did not want my auth system to be held together by vibes and rocket emojis.  

---

## Writing the Lessons

My main goal of the site was to create informative, easy to follow lessons for beginners. I spent a lot of time experimenting with different writing styles for my lessons. In the end, I created what I believe are well-structured lessons that cover all the needed topics. The curriculum I designed is a mix of the AP CSA and Learn Java for FTC curriculums. 

Before writing any lessons, I created an outline of all the sections and their lessons. In total, I had come up with 88 lessons. This was a lot, and I knew it would be the most challenging and laborious part of building the site. For each lesson, I wrote my main points, then used ChatGPT to generate a detailed outline. I filled in the gaps to create meaningful lessons that covered all the content I wanted. This process also made things faster, letting me write about three lessons a day. ChatGPT often suggested ideas I had not considered, which improved the course.  

I believe that this is the appropriate use of generative AI: using it to assist you, but not to think and do everything for you.  

---

## Creating the Editor

Creating the editor was a long, painful process. I knew that I needed one to make the site more engaging and meaningful for its users, but it was a ton of work. I spent days researching ways of executing code in the browser. I then came across Judge0, an open source API that allows you to run code on the web.  

The only catch: it needs backend hosting. I was tired of searching for something so I decided to go with Judge0. I set it up through Docker on a DigitalOcean Droplet running Debian. After struggling to configure it, I got it working with questionable security. Then, I created an editor component for my site that called the API I had hosted on DigitalOcean. The editor worked perfectly, and I decided to continue on with the site.  

I created the quizzes and dragging activities after most lessons. By this point, I felt pretty good with how the site was coming together. Until I checked the billing on DigitalOcean. After only testing the editor maybe fifty times, my bill was about $6. This was not good. If I wanted the site to support many users, it would end up costing me way too much. I wanted to keep the site entirely free, but did not want to have to pay too much out of my pocket for it. I tried optimizing my Judge0 instance, but it was just not worth it.  

I decided that the best way to move forward would be to take a different approach. I went back to researching, and came across CheerpJ. CheerpJ claimed to convert Java into bytecode, enabling it to run completely in the browser. This was perfect for my site! It is completely free for personal projects and educational uses like mine.  

But setting it up was a completely different challenge. Since it is a newer, more experimental technology, there is not much documentation on it. However, there was a sandbox editor made using it. This project is open source, so I downloaded it and began reverse engineering. I figured out how it worked and made my own, less complex version called [SimpleJavaRunner](https://github.com/jpkaiser2/SimpleJavaRunner). I integrated this editor into the existing one on my site, eliminating the use of the Judge0 API. Finally, I had a functioning web-based Java editor that did not cost me a dime.  

---

## Final Thoughts

Creating Code-A-Robot has been one of the most rewarding projects I have ever worked on. It began as a simple idea: make programming for FTC robots more accessible and engaging for beginners. What started as a summer project grew into a fully functioning platform with lessons, quizzes, and an in-browser Java editor. Along the way, I learned more than I ever expected, not just about programming and web development, but about problem solving, resourcefulness, and perseverance.  

This project taught me that no tool or technology is truly out of reach if you are willing to learn and experiment. I had to adapt constantly, whether it was changing my tech stack, finding alternatives to expensive hosting solutions, or reverse engineering poorly documented software. Many parts of the process were frustrating, but every obstacle pushed me to think creatively and find a better solution.  

Code-A-Robot is still growing, and I hope it helps new FTC programmers gain the skills and confidence they need to succeed. My goal has always been to create something I wish I had when I first started, something that makes learning to code robots less intimidating and more exciting. If this project helps even one new programmer feel more confident, then all the late nights and problem-solving sessions were worth it.  

Visit the site at [www.codearobot.org](https://www.codearobot.org)
