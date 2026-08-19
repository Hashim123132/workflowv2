# AI Study Material Automation Workflow


## Overview


This project is an automated study-material workflow built with **n8n**.


It allows a student to provide a lecture file and choose what type of study material they want. The workflow processes the file using AI and other services and produces the requested study material as a **PDF or DOCX**.


The main goal is to reduce the manual work involved in turning lecture material into useful study resources.


### Who is it for?


This workflow is mainly designed for:


- University students
- Students who have lecture PDFs or DOCX files
- Students who want quick summaries or quizzes from their study material
- Anyone interested in learning how AI agents and automation can work together


---


# What It Does


The workflow supports two file sources:


1. **Local file**
2. **Google Drive**


It supports two study-material types:


- **Summary**
- **Quiz**


It supports two output formats:


- **PDF**
- **DOCX**


### Basic workflow


```text
Student
   |
   v
n8n Form
   |
   +----------------------+
   |                      |
   v                      v
Local File           Google Drive
   |                      |
   |                File Finder Agent
   |                      |
   +----------+-----------+
              |
              v
        Download / Read File
              |
              v
          AI Processing
              |
              v
       Summary or Quiz
              |
              v
      PDF / DOCX Output
Main Workflow

The workflow starts with an n8n form.

The user provides:

Lecture file or Google Drive file name
File source
Study material type
Output format

The workflow then selects the correct path.

Local File

If the user selects a local file, the workflow works with the uploaded file directly.

Google Drive

If the user selects Google Drive, an AI agent searches Google Drive for the requested file.

The Google Drive agent was designed to:

Search Google Drive.
Find the requested lecture file.
Return the exact Google Drive file ID.
Pass the file ID to the download step.

The agent is instructed not to download or process the file itself. Its job is only to find the correct file.

AI Processing

The workflow uses AI to process the lecture material and generate the requested output.

The main AI model used in the workflow is:

GPT-OSS 120B

It was used through the OpenAI node / Grok API setup in n8n.

The workflow also uses other APIs and services for processing and document generation.

These include:

OpenAI-compatible AI model access
Grok API
Google Drive tools
PDFShift
Nutrient
n8n built-in nodes and tools

The exact services used depend on which part of the workflow is being executed.

Output

The workflow produces the requested study material in one of these formats:

Summary

Creates simplified study material from the lecture content.

Quiz

Creates a quiz based on the lecture material.

The final result can be:

PDF

or

DOCX
Requirements

A person reproducing this project will need:

Docker
n8n
An OpenAI/Grok API key
Google Drive credentials/API access if using Google Drive
PDFShift API credentials
Nutrient API credentials
The workflow JSON from this repository
A local folder for files if using local-file processing

Some services may require creating an account and generating API credentials.

Docker / n8n Setup

The workflow was developed using a self-hosted n8n instance running through Docker.

Confirmed Docker setup

The development environment uses:

Docker image: docker.n8n.io/n8nio/n8n:latest
Container: n8n-n8n-1
n8n port: 5678
n8n URL: http://localhost:5678

The container can be checked with:

docker ps

The expected setup includes:

docker.n8n.io/n8nio/n8n:latest

and:

0.0.0.0:5678->5678/tcp
Local file folder

The development machine uses:

/home/ameera/Downloads/Assignment

This folder is mounted into the Docker container as:

/files

The mapping is:

/home/ameera/Downloads/Assignment
              |
              v
           /files

This allows n8n running inside Docker to access files from the local assignment folder.

Important

The path:

/home/ameera/Downloads/Assignment

belongs to the original development machine.

If you are reproducing this project on another computer, replace it with your own folder path and configure the Docker bind mount accordingly.

n8n persistent data

The n8n configuration and persistent data use the Docker volume:

n8n_n8n_data

The container stores this at:

/home/node/.n8n

The Docker volume can be inspected with:

docker inspect n8n-n8n-1 --format='{{json .Mounts}}'
Starting n8n

After Docker and the required configuration are set up, n8n should be available at:

http://localhost:5678

Open that address in a browser.

The workflow JSON included in this repository can then be imported into n8n.

Importing the Workflow

The workflow JSON is included in this GitHub repository.

In n8n:

Open n8n.
Create or open a project.
Import the workflow JSON.
Configure the required credentials.
Check the file paths.
Check the API credentials.
Save the workflow.
Test the workflow using a lecture file.
API and Credential Setup

The workflow uses external services, so API credentials need to be configured before running it.

AI / Grok

The workflow uses GPT-OSS 120B through the AI/API configuration.

Add the required API credential in n8n and connect it to the AI node.

The API key should not be placed directly inside the workflow JSON or committed to GitHub.

Use n8n's credential system instead.

Google Drive

Google Drive is used when the user chooses Google Drive as the lecture source.

Google Drive credentials need to be configured in n8n.

The workflow uses Google Drive tools to search for the requested file and download it.

The Google Drive search agent receives the file name/search text from the form and returns the matching file ID.

PDFShift

PDFShift is used for document/PDF-related processing.

A PDFShift API credential is required.

Configure the credential inside n8n rather than putting the API key directly into the workflow.

Nutrient

Nutrient is also used as part of the document processing/conversion workflow.

A Nutrient API credential is required for the relevant nodes.

Again, credentials should be stored securely in n8n.

Security

Do not commit API keys, passwords, OAuth tokens, or other secrets to GitHub.

Use n8n credentials for:

AI/API keys
Google Drive authentication
PDFShift
Nutrient
Other external services

If a credential is accidentally exposed, revoke or rotate it immediately.

Example Usage
Example 1 — Local lecture file

A student selects:

File Source: Local File
File: AI-234 Data Structures - Lec 12.pdf
Study Material: Summary
Output Format: PDF

The workflow processes the lecture and produces a summary PDF.

Example 2 — Google Drive lecture

A student selects:

File Source: Google Drive
File: lec 12.pdf
Study Material: Quiz
Output Format: DOCX

The Google Drive agent searches for:

lec 12.pdf

It returns the matching Google Drive file ID.

The workflow downloads the file, processes its content, generates the quiz, and produces the requested DOCX output.

Architecture

A simplified architecture of the workflow is:

                    +----------------+
                    |   n8n Form     |
                    +-------+--------+
                            |
                            v
                  +-------------------+
                  | Source Selection  |
                  +---------+---------+
                            |
                 +----------+----------+
                 |                     |
                 v                     v
          +------------+       +----------------+
          | Local File |       | Google Drive   |
          +------+-----+       +-------+--------+
                 |                     |
                 |             +-------v--------+
                 |             | File Finder    |
                 |             | AI Agent       |
                 |             +-------+--------+
                 |                     |
                 |             +-------v--------+
                 |             | Download File  |
                 |             +-------+--------+
                 |                     |
                 +----------+----------+
                            |
                            v
                   +------------------+
                   | Extract Content  |
                   +--------+---------+
                            |
                            v
                   +------------------+
                   | AI Processing    |
                   | GPT-OSS 120B     |
                   +--------+---------+
                            |
                            v
                 +---------------------+
                 | Summary / Quiz      |
                 +----------+----------+
                            |
                            v
                 +---------------------+
                 | PDF / DOCX Output  |
                 +---------------------+
Important Design Decisions
1. Separate file-finding from file-processing

For Google Drive, the AI agent is responsible only for finding the requested file and returning its file ID.

It does not download or process the file.

This makes the agent's responsibility simple and reduces unnecessary work.

2. Support multiple file sources

The workflow supports both local files and Google Drive files.

This makes the workflow more useful because students may store their lecture material in different places.

3. Let the user choose the output

The user can choose between:

Summary
Quiz

and:

PDF
DOCX

This allows the same workflow to handle different study needs.

V2 Evaluation
V2 Evaluation: No formal quantitative metric was measured.

Version 1 was an initial MVP focused mainly on validating the basic workflow and tool integration.

V2 expanded the workflow into a more complete end-to-end automation with multiple file sources, study-material types, AI processing, and document output.

However, a formal quantitative V2 evaluation metric was not conducted.

This is documented honestly rather than presenting an invented metric.

Limitations

The workflow has several limitations.

1. External API dependency

The workflow depends on external services such as AI APIs, Google Drive, PDFShift, and Nutrient.

If one of these services is unavailable or incorrectly configured, part of the workflow may fail.

2. API credentials are required

Users need to configure their own API credentials and Google Drive authentication.

3. Local Docker setup

The local file path and Docker configuration may need to be changed when running the project on another computer.

4. AI can make mistakes

The generated summaries and quizzes are AI-generated.

The AI may misunderstand lecture content or produce an incorrect question or explanation.

The generated material should therefore be reviewed by the student.

5. No formal V2 benchmark

A formal quantitative benchmark was not created for V2.

The project was evaluated mainly through practical end-to-end testing.

6. Internet connection

The workflow depends on external APIs, so an internet connection is required for the relevant services.

AI Transparency

AI was used during the development of this project.

I used AI as a brainstorming and development partner. I asked AI questions such as:

What n8n nodes should I use?
How should the workflow be structured?
What should a particular node do?
How can I connect different parts of the workflow?
How can I debug workflow errors?

AI also helped me develop parts of the workflow automation.

However, AI was not always correct. Sometimes it gave me incorrect suggestions, so I had to provide more context, test the suggestion, identify the problem, and correct it.

In other situations, AI was very helpful and saved significant development time. There were also times when debugging with AI became tiring or inefficient.

I therefore treated AI as a development partner rather than blindly accepting its answers. I tested the workflow myself and made the final decisions about the implementation.

What I Built

The main work in this project was:

Designing the n8n workflow
Connecting the different workflow branches
Creating the Google Drive file-finding agent
Configuring AI processing
Connecting external APIs
Handling local and Google Drive file sources
Creating Summary and Quiz paths
Supporting PDF and DOCX outputs
Testing and debugging the complete workflow
Fixing problems when AI-generated suggestions were incorrect

AI helped with brainstorming, technical suggestions, debugging, and workflow design, but the workflow was tested and assembled into a working system by me.

Demo

A 3–5 minute live demonstration of the workflow is available here:

Demo Video https://drive.google.com/file/d/1FCoOCuIuGlkJWdRrBiQ4OWd1q-ObIF27/view?usp=sharing

The demo shows:

The real n8n workflow
A live end-to-end run
File selection
AI processing
The generated study material
A design decision
One limitation of the system
Repository Structure

The workflow JSON is included in this repository.

A simple structure is:

.
├── README.md
├── workflow.json
└── ...

The exact filenames may vary depending on the exported workflow.

Reproducibility Checklist

Before running the workflow, make sure you have:

 Docker installed
 n8n running
 Workflow JSON imported
 AI/Grok credentials configured
 Google Drive credentials configured if using Google Drive
 PDFShift credentials configured
 Nutrient credentials configured
 Local file folder configured if using local files
 Required n8n credentials connected to the correct nodes
 A test lecture PDF or DOCX
 Internet access
Project Status

Status: Completed workflow and demo.

The project successfully demonstrates an end-to-end AI study-material automation workflow using n8n, AI models, Google Drive, document-processing services, and PDF/DOCX output.

NOTE: ME AND AI GO AS BUDDY IN THIS PROJECT INITIALLY TILL THE END WE BRAINSTORM AND MADE NODES STEP BY STEP ONLY IN VERY LAST SOME NODES WERE NOT SATISFYING THEN I ASKED AI TO MAKE ME FULL JSON FROM THE CURRENT ONE WITHOUT ERRORS THEN I TOOK THE SPECIFIC NODES FROM AI THE GIVEN WORKFLOW AND PUT THEM IN MY WORKFLOW TO KILL THE ERROR 