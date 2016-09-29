---
layout:  post
title: "NYC's Taxi Flow"
comments:  true
published:  false
author: "Yeedle"
date: "2016-09-11 09:50:00 EDT"
categories: [NYC, taxi, R, ggplot2, ggmap, dplyr]
output:
  html_document:
    mathjax:  default
    fig_caption:  true
excerpt: "Visualizing the flow of travel in NYC, through the prism of the yellow taxi system."
---



This past summer, I've had the incredible experience of attending the [Data Science Summer School](https://ds3.research.microsoft.com/) (DS3), by Microsoft Research NYC. As part of DS3, I got to research some interesting questions using [TLC trip data](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). 

If that sounds boring, think again. The open[^1] dataset we worked with hold the records of every single trip that has taken place in NYC in extreme detail. The precise location where it was hailed, its destination, the price that was paid, the mode of payment, the amout of tip paid, the total number of passengers, the duration of the trip, distance traveled... Just about any piece of information you can possibly think of. This is an incredible dataset with lots to be discovered if only it is analyzed and explored. And indeed, many people have done some awesome analysis using this data, including our team at DS3.


[^1]: Open data is data that is "freely available to everyone to use and republish as they wish, without restrictions from copyright, patents or other mechanisms of control", as per [Wikipedia](https://en.wikipedia.org/wiki/Open_data)

But in this post I want to focus on one particular question we explored. We asked: Is there a way to measure, quantify, and visualize the daily flow of taxis in New York City? It's a simple question

