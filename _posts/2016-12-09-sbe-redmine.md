---
ID: 3284
post_title: Redmine user manual
author: frinxadmin
post_date: 2016-12-09 15:24:40
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/sbe-redmine.html
published: true
sidebar:
  - ""
footer:
  - ""
header_title_bar:
  - ""
header_transparency:
  - ""
apost_date:
  - 'a:1:{i:0;s:19:"2016-11-16 12:51:40";}'
hheader_title_bar:
  - 'a:1:{i:0;s:17:"a:1:{i:0;s:0:"";}";}'
---
This is the Redmine manual for users to develop, track and manage tasks in the Secondary Build Environment. Redmine is a flexible project management Web application. Written using the Ruby on Rails framework, it is cross-platform and cross-database. Redmine is open source and released under the terms of the GNU General Public License v2 (GPL). It allows you to create multiple projects, assign multiple persons with the help of a local Wiki page and document storage place. Redmine can be used by managers, developers and reporters (support teams). It allows you to create a nice project hierarchy and to organize and track multiple bugs, features and support nice and smoothly.  
The translation of the Redmine guide is available in Japanese language here: http://redmine.jp/guide/

### 1 Sign Up

Go to the Register button.

**Figure 1 Redmine registration**

![Figure 1: Redmine registration][1]

Complete the registration form; all necessary fields are marked with a red star.

**Figure 2 Completion of registration form**

![Figure 2: Completion of registration form][2]

Activate and modify your account, change the password, choose the time zone and decide how comments will be displayed.

**Figure 3 Account modification**

![Figure 3: Account modification][3]

Your account is ready!

### 2 Adding new members to your project

Every new member must be signed up with his/her email address. Please read Section No. 1. When you are logged in, go to Settings and choose the Members tab.

Choose your colleague from the list and assign him/her a role of Manager, a Developer or a Reporter. Then submitt with Add button.

### 3 Creation of a project

Go to the Project tab on the top of blue screen and click on New project button.

**Figure 4 Adding a new project**

![Figure 4: Adding a new project][4]

Complete the project’s form according to the picture below. Use the project identifier you like, choose different types of modules/features and which type of issue you would like to track.

**Figure 5 Creation of a new project**

![Figure 5: Creating a new project][5]

Start 123 is an example of a project that will be shown many times in this documentation. Your project is ready to manage!

### 4 Creation of a new issue in the project: bug, feature or support

It’s very easy to create a new issue in Redmine. If you are in your project area, go to the New issue tab. The Type of issue can be: bug feature support

Choose the Priority for your issue: Low Normal High Urgent Immediate Assign the task to a certain person from the Assignee drop down menu. If you don’t have anybody listed, please add your colleagues to your project and repeat Section No. 2. There is a possibility to choose Parent task, Start date, Due date as Estimated time and % Done. Don’t forget to assign Watchers. A watcher should be a person responsible for the project, a person who wants to have a complete overview about the project.

**Figure 6 Creation of issue**

![Figure 6: Creation of issue][6]

For a better overview, you can even link a bug to your Redmine Wiki or your corporate Wikipage using the button Link to a wiki page.

**Figure 7 Issue linking to a wiki page**

![Figure 7: Issue linking to a wiki page][7]

### 5 Issue management

All issues are listed in the Issues tab under your Project. Searching of the concrete issues or a bunch of the issues from the same category has been never easier. You can use the Add filter drop down menu on the right side and choose the filter you need. On the other hand, you have a possibility choose the concrete state of the bug in the left corner. For more details please see the picture below.

**Figure 8 List of issues**

![Figure 8: List of issues][8]

You can see the project’s issues in multiple ways. Reporting and logical structure can be seen by clicking on the Summary link on the left side in Issue tab. It brings you a nice overview and the current state of your bugs, features and support issues.

**Figure 9 Issue categories on the left side**

![Figure 9: Redmine registration][9]

**Figure 10 Summary of the bugs, features and support issues**

![Figure 10: Redmine registration][10]

### 6 Issues in Calendar view

The next level of information is provided by the calendar feature. By clicking on the Calendar tab under your project you can see the calendar filled with all issues that can give you a nice overview with respect to planning. Please see the picture below.

**Figure 11 Calendar view**

![Figure 11: Redmine registration][11]

### 7 Gantt chart

Visibility of all issues with regard to planning is provided in the Gantt tab under your project. The Gantt chart shows you a very detailed progress overview with the percentage of completion and the possibility to view issues from many different point of views by using filters. For more info please see the picture below.

**Figure 12 Gantt chart**

![Figure 12: Gantt chart][12]

### 8 Sharing the news with your team

If you would like to share the newest information with your team and you don’t want to spam everybody, you can use News tab under your project. News will allow you to share very important information in a creative way and what is important, visible to everybody. Your colleagues can comment the article and reply to you immediately after publishing.

**Figure 13 Adding news**

![Figure 13: Adding news][13]

**Figure 14 List of news**

![Figure 14: List of news][14]

### 9 Documentation

Redmine allows you to create two different types of documentation. Creation of User documentation and Technical documentation is available under your project in Documents tab. After creation of documents, you can find a list of documents in logical order with the option to sort by category, date, title and author.

**Figure 15 View of Documents**

![Figure 15: View of Documents][15]

### 10 Project’s Wiki page

Redmine allows you to create your own project’s wiki page. Wiki articles can be paired with created bugs, features or supports. More about linking to bugs can be found in Section No. 4. Output can be seen in pdf, html and txt form.

**Figure 16 Wiki**

![Figure 16: Wiki][16]

### 11 Files

Share the files with your team. The Files tab under your project will allow you to share different files up to 100 MB organized by date and size.

**Figure 17 Adding multiple files**

![Figure 17: Adding multiple files][17]

### 12 Settings

You are allowed to change the design of your Redmine, set up new modules, organize the members group, use, categorize the issues and use forums for further discussions. What can be modified: **Information** The basic information of your project and type of issues (bugs, features and support) **Modules** Many different types of modules/tabs taht will be used in your project for instance Time tracking, Wiki etc **Members** Add a new member or modigy the gropups and editing the existing members **Issue categories** Create an issue category as you wish and use it for issue management **Wiki** Change the name of your wiki page **Forums** Create and manage a forum for your colleagues **Activities (time tracking)** Choose a method for how Design and Development will be tracked

### 13 Useful to know

**Table 1 Useful links**  
[Redmine overview][18]  
[List of features][18]  
[Installation, administration, user & developer guide][19]  
[Translated guide to Japanese language][20] [Recomended literature][21]

 [1]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig1.jpg "Figure 1: Redmine registration"
 [2]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig2.jpg "Figure 2: Completion of registration form"
 [3]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig3.jpg "Figure 3: Account modification"
 [4]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig4.jpg "Figure 4: Adding a new project"
 [5]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig5.jpg "Figure 5 Creating a new project"
 [6]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig6.jpg "Figure 6: Creation of issue"
 [7]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig7.png "Figure 7: Issue linking to a wiki page"
 [8]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig8.jpg "Figure 8: List of issues"
 [9]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig9.jpg "Figure 9: Redmine registration"
 [10]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig10.jpg "Figure 10: Redmine registration"
 [11]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig11.jpg "Figure 11: Redmine registration"
 [12]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig12.jpg "Figure 12: Gantt chart"
 [13]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig13.jpg "Figure 13: Adding news"
 [14]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig14.jpg "Figure 14: List of news"
 [15]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig15.jpg "Figure 15: View of Documents"
 [16]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig16.jpg "Figure 16: Wiki"
 [17]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/redmine!fig17.jpg "Figure 17: Adding multiple files"
 [18]: http://www.redmine.org/
 [19]: http://www.redmine.org/projects/redmine/wiki/Guide
 [20]: http://redmine.jp/guide/
 [21]: https://www.packtpub.com/application-development/mastering-redmine