---
layout: post
title: "Labellr"
excerpt_separator:  <!--more-->
categories: 
    - Projects
tags:
    - Node.js
    - Express
    - MongoDB
slug: labellr
---


### Crowdsourced Data Labelling Platform for AI/ML Training Data
Build with Node.js, Express, MongoDB

<a id="github-link" class="icon" title="Github" aria-label="Github Project" href="https://github.com/siu-sing/labellr"
	target="_blank">
	<i class="fab fa-github"></i> GitHub Repo
</a>
&nbsp;|&nbsp;
<a id="github-link" class="icon" title="LiveDemo" aria-label="Live Demo" href="https://labellr.herokuapp.com"
	target="_blank">
	<i class="fas fa-desktop"></i> Live Demo
</a>

<details>
	<summary>Login credentials for Demo</summary>
	<br>
	<table>
		<tr>
			<th>User Type</th>
			<th>Email</th>
			<th>Password</th>
		</tr>
		<tr>
			<td>Admin</td>
			<td>admin@admin.com</td>
			<td>admin</td>
		</tr>
		<tr>
            <td>Client</td>
            <td>client1@client.com</td>
            <td>client1</td>
        </tr>
		<tr>
            <td>Labeller</td>
            <td>john@john.com</td>
            <td>john</td>
        </tr>
	</table>
</details>

### Introduction

Having just learnt the basics of building full-stack web applications, we were given one week to develop and deploy an app using the technologies we were taught. Namely, Node.js, Express, MongoDB in the backend, with [EJS](https://ejs.co/) as the templating language for client views.

We were also given free rein on the type of application to build, as long as there were login capabilities and usage of a database.

Initially, I brainstormed several ideas which revolved around the common web app use cases like E-Commerce, Forums/Boards, Calendar/To-Do lists, etc. However, these use cases were pretty overused and would be trivial to replicate since there were many examples floating around. 

Instead of thinking about the common types of web applications, I then decided to consider real business problems that I have encountered, and attempt an MVP that addresses a simplified version of the problem.

<!--more-->

### Motivation

I landed on Labellr, a data labelling platform to help data scientists crowdsource manual labels for their AI/ML training data.
One of the many bottlenecks faced by data scientists is obtaining sufficient and accurate labelled training data as input into their models. 

Even though there are pre-labelled data readily available online, these labels may not be suited for the specific context in which the data scientists are trying to model. (e.g. “this vacuum cleaner sucks” - would this be a positive or negative sentiment?)

Labellr aims to provide a platform for crowdsourcing labellers to not only help label training data, but allow for users/data scientists to select different demographics to help label the data in specific contexts.

I was excited about this since it was a data-related problem that I have encountered and attemped to solve (hackily) before. 

It was also a good opportunity to design a system and data model for a typical crowdsourcing platform which could transfer easily to other types of similar business problems.

<div class="project__screenshots">
    <img class="app__screenshots__desktop" src="{{site.baseurl}}/assets/labellr/labellrLanding.png "
        alt="labellrLanding" />
</div>


### Key Features

Here are some of the key defining features of Labellr.

#### User Types
- Labellers
    - Users who can sign up, login and take on any available workflows that are available
- Clients
    - Data Scientists or ML Engineers who have training data that needs to be manually labelled by humans
    - Clients can create labelling workflows, bulk upload training data to be labelled, view labelling stats and download results in a csv
- Admin
    - Superuser with admin privileges to create, update, delete workflows and users
    - View overall stats of the Labellr instance

#### Labelling Process

Labellr allows clients to upload text based data and request for either Sentiment or Topic labelling. 
<div class="project__screenshots">
    <img class="app__screenshots__desktop" src="{{site.baseurl}}/assets/labellr/labellrLabellingPage.png "
        alt="labellrLabellingPage" />
</div>
Sentiment labels range from `1` (very negative) to `5` (very positive), with `3` being neutral. 
<div class="project__screenshots">
    <img class="app__screenshots__desktop" src="{{site.baseurl}}/assets/labellr/labellrLabellingTopic.png "
        alt="labellrLabellingTopic" />
</div>
Topic labels are predefined by the client at the creation of the workflow. The labels `Not Sure` and `Not Applicable` are automatically included as topic labels for users to select if the text content is unclear or irrelevant to the existing options.

During the labelling process, the text is shown one at a time (instead of a list), to enable the labeller to focus on the text data on hand, and not be distracted or affected by other text content.

Labellers can exit the workflow anytime and return to it later. Their progress will be automatically saved.

#### Labelling Results
- Labelling results
    - Overall statistics
    - Labelling statistics
    - Download of labelling results

Data Model

Screen Captures

Post Mortem Thoughts
Sprint Planning
Design
- Relational DB instead of Document Store
- More responsive front end
Data Labelling Strategy
- More intelligent way of selecting data points for labelling (only those with insufficient labels, or not useful labels)

Additional Work
- Image labelling
- APIs for uploading, downloading data, connecting to DBs

