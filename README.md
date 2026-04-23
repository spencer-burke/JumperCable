# JumperCable
This project is not yet complete, but I have been working on/researching/ideating it for a months now.
## Why Does This Exist?
Hotwire and MVC is an amazing combination for building applications that are maintainable, simple, and accessible.
There is one problem.
The presentation layer of your app is scattered across different controllers.
Since everything a resource, the login form can be sessions#new and the sign up form will signups#show.
As you can see, the "resourcefulness" can make the app harder to navigate.
Simply because the different pages are scattered between different actions.
It can be ambigous as to what action matches to which page.
As a result Hotwire applications can be very challenging to navigate.
An easy to way to fix this is create a new "page" resource.
That way every page in the application has a specific place.
As a result, getting a site of your applications simply means looking at the "pages" in the routing file.
This is where JumperCable comes in.
It serves to codify this pattern into a convention by creating a gem.
That way it's much easier to understand what is happening in application.
This is especially true given that Hotwire is excellent for placing turbo frames in different pages sent to the client.
Resource controller now function exclusively as an api for turbo frames, backend actions(jobs, emails), and redirects.
Most of the Rails conventions already support this one form or another.
They just need to be connected with JumperCables.
## Technical
The plan is to make the page route map to the page inside of the controller.
Simply codifying the convention.
## Planned Features
- Add generator for new page controllers
- Expand the routing dsl to add pages just like resource
- If needed, make it compatible with inertia rails
## DSL Plans
```ruby
page :login #automatically maps to the PageController/JumperCablePageController::LoginController
page :login, params: [:id, :search] # handling router parameters, params should be id and search
page "/login" to: "loginController#page"
page "/login", controller: "login"
```
Those are examples for the routing dsl.
## Controller Example
The controller should look like this:
```ruby
class LoginController < PageController
 	layout :unauthenticated_layout
	
	def page
		@data_that_could_be_fetched = Example.find(params[:you_get_the_point])
	end
end
```
## Generator Example
```bash
rails generate page Login
```
This creates the LoginController that extends the page controller.