---
layout: post
title:      "Sinatra Project - Museum Reviewer"
date:       2019-11-15 14:32:37 +0000
permalink:  sinatra_project_-_museum_reviewer
---


    For my Sinatra project, I decided to build a museum reviewer app.  This app allows the user to write a review of a museum, read all other reviews and comments and also comment on the reviews.  The app does not allow users to edit or delete reviews or comments they did not create.  Flash messages were very helpful to notify the user of anything that's gone wrong.

    I started with a different version of the app in my mind and on paper.  I was hoping to seed the database with a list of museums the user could then select from to write their own review.  This list would have consisted of radio buttons that would allow the user to select one museum at a time.  
		
		I was able to create a seed file and and the populate the database with the list as I imagined.  A review form was below the list and allowed the user to fill out some review information---date visited and their thoughts on the museum.  Everything seemed to work until I realized the musuem name was not being output with the review information.  I tried to find a solution, but everything I looked up seemed to only work for Rails applications.
		
		So I changed my project to allow users to write their own review including musuem name, location, date of visit and their thoughts on the musuem.  Then users could comment on their own reviews and others' reviews as well.
		
		The hardest part of the project was setting up the application so that the user could edit their own comment.  I ran into a lot of hurdles with this aspect.  It seemed I would get one piece working---editing the comment for example---but then another piece would not function correctly.  I had to figure out how to let the user that wrote the comment edit it but also not be able to save an empty field.
		
		I also wanted the original comment to carry over into the edit comment form.  This was tricky as well until I realized I had a tiny typo in my comment edit form html.  Once that was fixed, the original comment now displayed in the edit comment field.  This is much more user friendly than a blank field that would require the user to type an entire new comment.
		
		The empty comment field issue was solved by adding "&& !params["content"].empty?" to the"if @comment" line of my edit comments method.  I also made sure only the creator of the comment could edit it by adding this line of code:
		
		@comment.user_id = current_user.id
		
		to the edit comments get and patch routes.  If the currect user did not create the comment, they were not allowed to edit it.
		
		Overall, this project was very challenging.  I was not expecting it to go the way it did but I feel like I learned a lot about how RESTful routes work to create web applications.  I'm happy with the end result.
		
		

