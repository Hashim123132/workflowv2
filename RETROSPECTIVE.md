# Retrospective

When I started this track my main goal was to learn. I did not have a very big idea in mind. My original project was a simple summarizer that worked only locally. I wanted to understand how AI automation worked and build something that could actually be used.

As I worked on the project the idea changed. The final workflow became much more useful than my original plan. A user can now choose between a local file or a file from Google Drive. The workflow can process the file and produce either a summary or a quiz. It can also return the result as a PDF or DOCX file. This was a big change from the simple local summarizer I had originally imagined.

The most frustrating part was making the whole workflow work together. When the workflow became bigger I would fix one node and then another node would have a problem. In normal programming I find debugging easier because I can look directly at the code and understand where an error is coming from. With n8n I was a beginner and the process was different. I had to understand how the nodes passed data to each other and why one node was not getting what it expected. Getting every node satisfied and making the complete workflow run without errors was probably the hardest part of the project.

Working with AI was also a major part of this experience. I used AI as a buddy for brainstorming and for figuring out which nodes I might need. Sometimes it helped me a lot. Sometimes it gave me an incorrect answer or did not have enough context about my workflow. There were also times when the context became too large and I had to explain the situation again. I learned that giving AI more context is important but that context also needs to be relevant. I cannot just give it everything and expect the answer to always be correct. I still have to understand the problem and check what AI suggests.

The first major technical thing I learned was n8n itself. Before this internship I mostly worked with tools like LangChain and LangGraph and I was trying to avoid n8n. This project forced me to actually use it. I learned how nodes work and how they can be connected to create an AI workflow. I also learned how this graphical approach is different from building an AI agent directly with Python.

The second thing I learned was how to connect different nodes and services together. The workflow uses different APIs and tools and I had to understand how data moves from one part of the workflow to another. The third thing I learned was how to use APIs inside n8n and connect them with AI models and other services.

One of the best moments was when the complete workflow finally worked without the errors I had been dealing with. There were problems with prompts. There were problems with nodes. There were also times when AI gave me suggestions that did not work. When everything finally ran successfully I had a real feeling of accomplishment. I could look at the workflow and think that I had actually built this. AI helped me with brainstorming and ideas but I still had to test everything and solve the problems when the suggestions did not work.

If I had another week I would improve the file output part. I would add a feature that automatically uploads the generated summary or quiz back to Google Drive. Right now the generated file can be saved locally but having the workflow put the final result directly into Google Drive would make it more complete.

Compared with Week 1 I feel that I have opened up a completely new area for myself. I was not using n8n at the beginning and I was actively trying to avoid it. Now I understand the platform and I can see how graphical AI automation can be useful alongside the coding approaches I already know.

The internship also affected other parts of my work. I improved my portfolio website during the track. While working through the assignments I found bugs glitches and some vulnerabilities that I had not noticed before. Whenever an assignment gave me a reason to look at that part of my website I fixed those problems. So the internship did not only give me one workflow. It also made me more comfortable finding problems in my own work and improving things that I had already built.

The three most transferable things I learned are to understand the tool before trying to avoid it to give AI clear and relevant context and to be patient when debugging a system where many different parts depend on each other. These lessons will be useful whether I continue working with n8n or go back to building AI systems with code.
