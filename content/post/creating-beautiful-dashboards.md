---
title: "Creating Beautiful Dashboards"
date: 2021-05-27
metaAlignment: center
coverMeta: out
categories:
  - Business Intelligence
tags:
  - dashboard
draft: false
---

As a data analyst, I often create dashboards as part of my analysis. When supporting multiple stakeholders it might become quite tricky to design a dashboard that will serve all of them. Unfortunately, there is no one-size-fits-all solution when creating dashboards for multiple stakeholders. In this post, I will introduce some of the methods I use when designing self-serve dashboards.

<!--more-->

Broadly speaking, there are three different types of dashboards: operational, analytical, and strategic. Let us first start discuss the purpose of these types of dashboards.

**Operational Dashboard**

The operational dashboard is a reporting tool that is used to track frequently changing business processes and key performance indicators (KPIs). This is a dashboard that people spend a lot of time on, constantly monitoring changes in real time or near real time. Not too many filters added to the operational dashboard because users don't have to worry about reconfiguring the chart to answer their questions. It would be a good idea to see the status of the metrics they are tracking and the business decisions they are going to make.

**Analytical Dashboard**

An analytical dashboard is a reporting tool that enables users to check trends, predict outcomes, and discover insights. This is the kind of dashboard where you go to visually play with the information. You will put on filtering capabilities and many knobs they can turn. If you don’t know what questions they are going to ask, please provide them with a button so they can turn and look at themselves.
If you are a data analyst/owner with a large amount of rich data but a fairly large number of non-technical users, you can use filters to group the data for non-technical users to ask questions about the data. You want to make it easier for them to explore the data with limited resources. As a data analyst, even though you know what the data is, you might not know what questions they might ask. You provide them with a sort of a mini-exploration tool so that they can use it to analyse the data themselves.

**Strategic Dashboard**

A strategic dashboard is a reporting tool commonly used by executives to track the top-line organization's key performance indicators (KPIs).

Executives want to see the health of the company. They come to it infrequently to once a week or a day to get a broad overview of status and to observe for anomalies. The questions you ask in the strategic dashboard are different from the ones that you ask in the operational dashboard because in strategic dashboards only covers the most important top level KPIs that help the executive assess with just a single glance.

An executive doesn’t want to spend a lot of time investigating things. They just want to look at the status of the business. For example, if they see a spike or a dip in revenue, they will highlight it and ask somebody to investigate it.

**Common Dashboard Questions**

When creating a dashboard, you may get questions along the line: hey, I want to see revenue by county or zip code level. In such cases, you add a widget to display the granularity at the county or zip code level. Then a week later, you might get another question asking you to make changes to the logic of data pipeline logic that feeds the dashboard. You don’t want to have a dashboard that is constantly changing to the point it ceases to serve its original purpose. This kind of communication might be prevalent in some organizations. In such scenarios, it makes sense to have a design document for the dashboard and properly document the suggested changes and their impacts.

Communicate this with those involved stakeholders to track requested changes without affecting your workflow. This might not be feasible in start-ups where the delivery time might be very short. In such a fast paced environment, it is always important to keep tabs of the changes you are making to your dashboard and when you made them. In some cases, what appears to be a simple UI change request you received might end up changing the data pipeline that creates the dashboard. If you are working with self-serving live dashboards, materializing your source tables regularly will help you tremendously, in case something goes wrong.

**Approaching Dashboard Design**

Dashboards are very important. They help you quickly gain insights into the key aspects of your data. As a dashboard creator, your primary role of creating dashboards should be user-centric. The purpose is to display information so that stakeholders can understand and make informed decisions.

The first question to ask yourself when structuring a dashboard is who your audience is and what questions they want to ask. How much domain knowledge do they have? In some cases the audience will come to your dashboard fully understanding all of the terms that you are using. As a data owner, you are mostly familiar with what the metrics mean and the assumptions you made when calculating? Compared to untrained users, you have a more detailed understanding of what the dimensions mean and what questions they are trying to answer.
Therefore, when you are asking what questions the user is trying to answer. Do you really understand what those questions are or are you simply building a dashboard because you are given data? You should not randomly toss metrics that seem interesting into the chart without thinking about what users are coming to your dashboard to answer.

Here are a few point to consider when creating a beautiful dashboard.

**1. Sketch Out a Logical Structure**

Below are some of the important things I follow when creating dashboards. When designing a dashboard, I start with a pencil and paper, then I

1. sketch out the organization of multiple charts and information flow.
2. enumerate the questions your dashboard is trying to answer.
3. put them in sub-categories (sections).
4. build an outline (head, card, charts within the sections, what question each one of those charts is trying to answer).
5. start building the dashboard in dev environment and do some data quality check.
6. finally launch the dashboard to prod if everything looks good.

**2. Have a Layout Template**

You may own multiple dashboards. To use similar templates would make it easier for the audience to follow a certain style and would speed up creating your dashboard and make it look a lot nicer.
There should be a common visual representation you use:

- Major section
- Subsection
- Charts

You will spend time from designing a new layout every time towards prototyping that allows you to rapidly create dashboards with similar layout.
Dashboard real-estate: Do you understand the circumstances under which you would like users to use this dashboard? Are they using a big presentation screen, a 27 inch monitor or a 13 inch laptop? With these factors in mind, you can design your dashboard to accommodate for different usability and accordingly plan for how you can place certain charts in the dashboard. Anyone who visits the team's dashboard knows intuitively how to navigate through the dashboard.
Having a basic structure makes it easier for users to go through the dashboard with little assistance as they were already accustomed to similar layouts in the past.

**3. Improve Your Dashboard**

Two things that will help you improve your dashboard are accuracy and clarity. Obviously, the information displayed in a dashboard must be accurate, otherwise it is going to be worthless or even misleading. For example, suppose a certain metric needs to be displayed to two decimal points, however, if you round this metric to an integer, it will no longer be accurate. So, you need to double-check before such cases lead to unintentional errors.

Dashboard is all about visual storytelling. You can have various charts glued together in a dashboard, but it becomes very difficult for the user to go through them.

Poor organization and data layout, slumming a bunch of charts together and hoping it will make sense to the user isn’t a good dashboard design. This will make it difficult for the user to find the information they are looking for. They will spend more time connecting the dots between two charts and try to understand if there is logical flow between the charts. It is not obvious where anything really is. This would force them to do some heavy lifting to find the information they are looking for.

**4. One Question per Chart**

Create a chart to answer one question, just one question. I can’t stress this enough. If you need more, then add more charts. Decide what the most important question is, then add other charts for the relevant questions and place them in one section. This will help you better organize your charts and the information they convey to the user. In most cases, the users won’t know what information to take from a chart. Let’s say you are designing an executive dashboard, it would be imperative not to make them think hard on what the chart is supposed to answer. Executives spend only a few seconds to scan the top level metrics and answer specific questions they may have. If they notice something odd they delegate questions to other people to investigate. Sometimes it can be helpful to include a question statement or explanatory text about that particular card that you are presenting in a dashboard.

**5. Use Simple Visualization**

This is closely related to the above point. Not surprisingly, most people are not good at reading charts. Make your visualization easier by using simple charts. For example, using a double axis is more likely to confuse people as it makes them think hard by invoking different questions they had in their head. Therefore, it will be great if you avoid those using double axis unless it is a request from someone who is knowledgeable about data visualization and is sure they won’t be confused by your presentation.

Avoid obscure chart types, like tree charts, sunburst, network charts… etc. This doesn’t mean you shouldn’t use a chart type that suits the data, which, of course, defeats the purpose of a dashboard. Complexity is wreaking havoc on organization. Analysts or dashboard creators sometimes unwittingly over complicate analytics. You can focus on business enablement to effectively balance between risk and reward. If we use a simple chart, we are effectively providing decision-makers with the information they need to do their job quickly. It will get your point across easier and is a very important feature of self-serve dashboards. It is imperative for the dashboard author not to impose cognitive load to the user while creating charts.

**6. Consistency**

While creating a chart, consistency is important. You want to use the same colors, visualization type for all types of that chart. For example, let’s say you use bar charts to show revenue growth over time, if you want to show revenue growth of a department or product in another section of the dashboard, again use bar charts. If you prefer a line chart, then use a line chart. Just make sure you stick with it, because if you are using a bar chart in one section and line chart in another section, the user would think there might be some reason that the dashboard author used different visualization types to display the same type information.

**7. Default Settings**

Be wary of default settings in any BI tool you use. If you are using the default setting with most BI tools, you are likely going to make unintended errors with your dashboards. Think of default settings as boilerplate for your data visualization. Let’s say you create a chart with default settings, the different colors you are seeing may not make sense, because you wanted to have a shade of one color to represent the different levels of your metric. Also, they might not be in order. You may want to increase the text size from its default to make accommodations for the screen size it will be viewed on. Maybe you want to rotate the axes-labels so that they don’t overlap. As a dashboard owner, you have to change the default settings and the layout of this default dashboard to show the relevant information for the team. Therefore, when creating dashboards, it is always good to be mindful of the default settings and should customize them as needed.

**Conclusion**

In conclusion, we saw different techniques to design beautiful dashboards. Telling a story visually is very important in communicating your findings. To achieve that you should consider applying the points discussed above as needed. Happy storytelling and reporting!
