---
layout: post
title:      "Mod 3 Project"
date:       2021-02-08 12:01:28 -0500
permalink:  mod_3_project
---


Time flies, I am now 6 months of the part-time curriculum and proud of myself for making it this far, coming from a background of zero coding experience has been rough but with hardwork and countless hours of practicing and studying I have continued to persevere! 

Having not struggled with the Sinatra section much I thought I would also find the transition to Rails easier, it was not... Rails is different from Sinatra in that it has many more and independent components(routes, controller actions etc.. all have their own file). However if you stick to conventions Rails pretty much decides eveything for you. For example `resources :controller_name`, by using this keyword Rails provides you with path helpers and action abilities needed to perform CRUD for a controller. If you follow naming conventions through your application the controller action will know what view to display as well. 

For my project I decided on a chocolate review application. Users can add chocolates, chocolates belong to a category so a user must select a category or create their own. If another user has already added that same chocolate brand and flavor they cannot add it to avoid having the same chocolate being posted multiple times. Users can also review other users chocolate. I have decided to let logged in users view each others posts but limited the update action to just the user who the chocolate belongs 
One of my biggest struggles for this project was creating a form for a nested resource route. I had two of them. A user created a review related to a chocolate and for a user to also be able to create a chocolate independently or nested in categories.
In order to create a form with nested resources, first nest your routes with resources, make sure to specify the actions if you are not going to use them all.
```
resources :chocolates do
         resources :review, shallow: true
end

resources :categories , only: [:index]
        resources: :chocolates, shallow: true
	end
```

you get paths like

```
'chocolates/:chocolate_id/reviews
'chocolates/:chocolate_id/reviews/new

'categories/:category_id/chocolates
'categories/:category_id/chocolates/new
```

forms get tricky with nested resources, to create a new review that is nested under chocolates you will need to provide two instance variables. The path needs the chocolate_id and a template of a new review. 

```
form_for [@chocolate, @review]
```

In your controller you will need to set a condition to check if that chocolate exists or if it is a nested route. You will also need to set the chocolate into an instance variable as well as the new review. I chose build over save because it provides a template/creates a new instance  within an active record association .

```
reviews_controller.rb

def new

if params[:chocolate_id] && !Chocolate.exists?(params[:chocolate_id])
      redirect_to chocolates_path, alert: "Chocolate not found."
    else
      @chocolate = Chocolate.find_by_id(params[:chocolate_id])
      @review = @chocolate.reviews.build
    end

end
```

I got stuck in the create action for 2 days, I had to figure out how to not only associate the review with the chocolate but also to be able to carry over that chocolate_id to the create function and also assign that review to a user as well as be able to render my two instance variable if it got rendered new again without loosing the chocolate_id. 
I had to find the chocolate and build the review to set that active record association, lastly assign that review a user. It helped that my create method had a chocolate and a reviw variable so loosing the chocolate_id was no longer a problem.

```
def create
    @chocolate = Chocolate.find_by_id(params[:chocolate_id])
    @review = @chocolate.reviews.build(review_params)
    @review.user = current_user
    if @review.save
      redirect_to chocolate_path(@review.chocolate)
    else
      render :new
    end
  end
```

Although stressfull with all the errors due to active storage and my nested routes, it was gratifying when I finally got everything working!  

