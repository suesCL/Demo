# CatClicker Javascript Web Application 
## Overview:
CatClicker is a client side and interactive single page web application which uses HTML, CSS and Javascript.
It uses vanilla JavaScript such as event listeners and DOM manipulation to process and store user input and subsequently display new content to the user. 

## Challenges:
1. The user input from the form cannot update page content. For example, the admin feature could not change the cat name, image source or number 
of clicks. When clicking save button, the page will refresh to the default page. 
2. New content cannot remain retrievable/viewable after a screen refresh. The page will reset to the default content. 

## Implementatioin:
* Model view controller:
The javascript application is composed of three parts which are model, view and modelview controller(octopus). 
1. The model is made of a model object which contains application data
such as list of cats' information and current cat. 

2. The modelview controller is an object called octopus which contains methods
that initialize user interface views and methods that get and change model object. It also sets the model data of currentCat to be the
first cat arbitrarily.

3. The view is composed of three objects which correspond to three views that are displaying cat, showing the list of cats, and an admin feature respectively.

* User interfaces(Views):
1. Catview: 
Catview displays a cat image, cat's name and its corresponding number clicks. The image is added an click listener. When clicked, 
the modelview controller is called to increment the current cat's clicks. 

2. CatListView:
catListView object renders a list of buttons that correspond to each cat and adds a click listener on each button to render the
cat view.

3. AdminView:
The adminView implements a feature where user can click to open a form to update each cat display's information including its name, image source and 
number of clicks. The adminView object adds a click listener on admin button, adds a click a listener on cancel button
to hide the form and adds a click listener on submit button to update current cat's displayed information. 
