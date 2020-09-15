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
---


### Crowdsourced Data Labelling Platform for AI/ML Training Data

[GitHub Repo](https://github.com/siu-sing/labellr)
[Live Demo](http://labellr.herokuapp.com/)

Motivation
- Related to data
- Solve a real problem encountered at work
- Practice building a full stack application
- Design data model for a typical crowdsourcing and data tool

gifs for labelling flow
gifs for text upload flow
gifs for results download flow

Featured Features
- Users
    - Labeller sign up, login, label data (text/image)
    - Client upload data, download report view statistics
    - Admin full control of all assets
- Labelling Process
    - Text labelling for 1) Sentiment, 2) Topic
    - Image labelling binary labelling (yes, no, unsure)
    - Image anotation
    - Labelling process can be saved and continued later
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

