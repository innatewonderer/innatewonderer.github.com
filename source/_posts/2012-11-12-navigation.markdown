---
layout: post
title: "navigation"
date: 2012-11-12 13:41
comments: true
categories: 
published: false 
---
1. applicaiton layout
2. controller layout
3. action layout

## in controller?
<% content_for :page_navigation do %>

## sub_layouts

<nav>
  
  <nav od="main-navigation" >
  </nav> 

  <nav id="page-navigation">
    <%= yeild :page_navigation %>
  </nav>
</nav>

Navigation tabs

views -> application -> _navigation.html.erb

<html>
<p> 
  <%= link_to "Issues", issues_url %> | 
  <%= link_to "Repositories", repos_url %> | 
  <%= link_to "New Repo", new_repo_url %>
</p> 

<hr/>
</html>

views -> layouts -> application.html.erb

<!DOCTYPE html>
<html>
<head>
  <title>Gitbo</title>
  <%= stylesheet_link_tag    "application", :media => "all" %>
  <%= javascript_include_tag "application" %>
  <%= csrf_meta_tags %>
</head>
<body>

<%= render 'navigation' %> 
<%= yield %>

</body>
</html>