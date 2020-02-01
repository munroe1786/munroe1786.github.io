---
layout: post
title:      "Museum Reviewer Rails Project"
date:       2020-02-01 02:15:49 +0000
permalink:  museum_reviewer_rails_project
---


For my Rails project, I decided to continue the Museum Review application I built for the Sinatra project.  Coming from an Art History background, museums and art are some of my favorite things in the world.  So I decided to focus on an application that allows the user to add museums and write reviews on either their own museums or museums that other users created.  User are also able to view all reviews on the application.

This project allowed me to really understand how powerful Rails is.

For example, here are the errors.html.erb and form.html.erb from the Museum views of my app:



<% if museum.errors.any? %>
<div id="error_explanation">
    <h2>
        <%= pluralize(museum.errors.count, "error") %>
        prohibited this museum from being saved:
    </h2>

    <ul>
        <% museum.errors.full_messages.each do |msg| %>
        <li><%= msg %></li>
        <% end %>
    </ul>
</div>
<% end %>

<%= form_for @museum do |f| %>
    <%= f.hidden_field :user_id %>
    <p>
    <%= f.label :name %>
    <%= f.text_field :name %>
    </p>
    <p>
    <%= f.label :location %>
    <%= f.text_field :location %>
    </p>
    <%= f.submit %>
<% end %>


Rails was able to render these with a line of code each:

<%= render partial: "errors", locals: {museum: @museum} %>
<h1>Create a New Museum</h1>
<%= render partial: "form", locals: {museum: @museum} %>

Pretty amazing!  I knew Rails was powerful, but it took me building an app to fully appreciate it.
