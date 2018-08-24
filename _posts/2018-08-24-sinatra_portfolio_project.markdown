---
layout: post
title:      "Sinatra Portfolio Project"
date:       2018-08-24 14:37:24 +0000
permalink:  sinatra_portfolio_project
---






So going through the sinatra project and the sinatra section entirely I realized that i have some weak spots.One: im in big trouble if I was in an interview and I had to explain concepts in my projects. Two: There is concept that I really don’t really know that well. I feel it will help to write it down so it can translate well verbally. A few key things I need to explain is: 



 What is rendering? 
- How do you render a view in Sinatra?
- What is redirection? 
- How do you redirect in Sinatra?
- Are  variables still accessable on a view if they are declared in the controller action   that will render a view? 
- Are you able to access variables set in a controller action after redirecting to another controller action? 


With That being said WHAT IS RENDERING?

Render (erb method for sinatra.) tells Rails which view or asset to show a user, without losing access to any variables defined in the controller action.

Redirect is different. The redirect_to method tells your browser to send a request to another URL. Since the request is completely different, the view to which you redirect will NOT have access to any variables defined in the controller.


```
 get '/tasks/:id/edit' do
    @task = Task.find_by_id(params[:id])
    if @task = current_user.tasks.find_by_id(params[:id])
      erb :'/tasks/edit'
    else
      redirect to 'tasks'
    end
  end
```

Lets dig deep an gather some example of this. If we look at out if statment we created a validations. It checking if the the task list belongs to the user. If the `@task = current_user.tasks.find_by_id(params[:id])` returns true then it will render a view that contains a form that alows a user to edit their tasks. If the statement returns false then sinatra will redirect to 'tasks'. Well let look at what is actualy happening.

```
get '/tasks' do
    redirect_if_not_logged_in
    @user = current_user
    @lists = @user.lists
    erb :'tasks/show'
  end
```

As perviously stated redirecting is telling your browser to send a request to another URL. If you notice if you try to access a task or list that does not belong to the current logged in user you are sent back to the show page. If we look at the code above notice the first line. `get '/task' do` Looks familiar right? this is the URL we redirected to in our edit method.  So after the if statment return false you are sent to a new URL request. 

Now you're working with Rendering/Redirecting.







