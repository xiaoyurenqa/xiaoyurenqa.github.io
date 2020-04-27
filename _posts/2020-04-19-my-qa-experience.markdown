---
layout: posts
title:  "Software Testing: What I Have Learned in the Past 5 Years"
date:   2020-04-19 22:34:00 -0700
categories: personal
---
I recently quitted my job as a software test engineer of 5 years, while I am in self-quarantine and preparing for my new journey, it may be of some value to share and summarize my experience on software testing.

I was not equipped with any textbook software testing knowledge until my career as a QA engineer was launched off. Before that, software testing was nothing but some marginal tests right before submitting a school project, or a few prints, get times and simple gcc commands during a code debugging. Software testing is a much wider field than it seems, and it has been evolving quickly with the introduction of DevOps, Continuous Integration and more. 

How to become an excellent software tester, and how to remain competitive in the growingly fierce job market? Here are some of my takeaways as a 5-year software QA engineer.

### Testing comes first (vs. coding)

Here is a hard truth: coding tends to be more well-received and considered “cooler” than testing. While it is tempting to code up at every opportunity, testing, by the end of the day, is what matters. As a new QA engineer, it is time to take a break from programming books, and turn to resources on software testing. Software testing is a very practical field, but some theories summarized by our predecessors are still worth learning, they can save us a lot of time along the way. “Standing on giants’ shoulders”, so they say.  

There are different types of tests: black-box, gray-box and while-box testing. Usually a full-time QA engineer would be involved in black-box or gray-box testing. If the job involves performance testing, there will be a lot more to learn and practice. 

Besides testing theories, study the product is also very important. Know the technology, the logic behind the product. The better we know something, the easier we exploit it and find bugs. It’s kind of similar to the “know your enemy” theory, except that it is not an enemy, but something we help to make better. 

### Shift focuses when automating test cases

I understand how exciting it is to use our programming skills in test automation, that’s exactly how I felt. After years of automating test cases and building/maintaining continuous integration platforms, I realize, that coding for test cases is a lot different from coding for a project. 

I plan to write a separate article on this topic, but long story short, test cases need to be incredibly robust and comprehensive, while slightly compromising other parts such as design patterns and OOD. Don’t assume the bar is lowered just yet, it is a lot harder than it seems. Without careful design and thoughts, it can easily get buggy that would make the case meaningless.

To automate a good test case, coding skills are of course, very important. Other than that, knowing the test case is very crucial. It is best to manually try out every step of the case, observe its behaviors and side effects, make sure to cover them in the code. Sometimes it is best to manually go through them multiple times, and see if there are unexpected (but not a bug) reactions from the software. 

### Keep up with the technology 

Yes, being a QA engineer does not mean just show up in the office and report bugs. Software testing has been evolving rapidly in recent years. People are adopting various technologies to test software more rapidly, efficiently and accurately. The emerge of DevOps has also made an impact on the software testing field. It is no longer uncommon for a QA engineer to write production code to support an ecosystem of end-to-end software testing. Let alone the fact that many companies are attempting to use AI and data science to revolutionize how QA is done. 

With that background, it is crucial for every QA engineer to never stop learning. Some directions that can be of help in QA are: Linux, bash scripting, database, web design, AI, data science, and you can never go wrong with the basics of programming such as algorithms, operating systems, design patterns, etc. 

### Sharpen your soft skills 

While software testing sounds just as geeky as software development, QA engineers often need to communicate with the dev team, DevOps team and their managers. Do not be surprised if a developer tries to dodge your bug reports and mark them as FAD (function as designed), we all know how developers hate to fix bugs, since once upon a time, we were in their shoes. 

It is the QA engineer’s job to convince a developer to accept that it is indeed a bug and it needs a fix. Once you have learned all about the product, use the knowledge and social skills to professionally yet firmly sell your opinion that it is a valid bug that needs attention. When I say “social skills”, it is not just about talking to a developer one on one through email or face-to-face, but there are a lot more subtleties to it. For example, you need to know when to escalate the bug to the higher management team, when to follow up and push the progress of a bug being fixed, and how to handle things when you mistake a feature for a bug. 

### Enjoy the journey

QA engineer is not a dominant position in the IT field, but it has its fun in a unique way. Being a QA engineer means you get to learn all about a product, work with people from different backgrounds in the company, and explore state-of-the-art technologies that can be applied quickly in your job. Plus, while this may not happen very often, but the rewarded feeling when a multi-million business critical bug is discovered by you! What a great contribution it is!

