# gale_hogwarts
Provides the code for an adaptable learning experience and Hogwarts School of Witchcraft and Wizardry

# Development Environment Set Up

After a painstaking process, I finally figured out how to actually set up a fully fledged (almost) dev environment in which we can collaboratively develop our application.

## Prerequisites
- GALE must be installed on your computer as per the instructions found on [canvas](https://canvas.tue.nl).
- Python 3.6 should be installed and can be downloaded either on the [official site](https://www.python.org/downloads/) or using a [conda](https://www.continuum.io/downloads) installation (recommended if you intend to use python in the future and want to manage multiple python versions with applications running in different environments).
- Git must be installed on your system with the ability to clone repos and run git commands. For information on how to do this consult the git [help documentation](https://help.github.com/articles/set-up-git/).

## First Steps
Now that you (hopefully) have all the prerequisites in place we can begin to deploy the application. As a first step, simply clone this repository to your local machine to whatever folder you like.

Next, navigate to the directory you just cloned using terminal/powershell. Now run: ```python -m http.server 8000``` after which you will have a server running on port 8000, serving out the files in this directory. If that port happens to be taken for any reason, you can always try with another in the range 8xxx.

You can now launch the gale application! Navigate to the URL that should look as follows: ```http://localhost:8080/gale/concept/http://localhost:8000/testing```.

This should present you with the intro page which currently has no adaptation at all.

# Vendor Tools

In order to make development of such an application easier than it otherwise would be, we can use a multitude of 3rd party tools to speed up the development workflow. These tools are mentioned below:

- Zurb Foundation - a easy to use CSS framework that hasn't been overused and provides tonnes of customisation.

# Common Issues (and How to Fix Them)

While developing there are some things to watch out for:
- If you CRUD a concept, then the changes might not be reflected until you restart the GALE server. Do this step before wondering why it isn't working.
- A badly created concept will give a very not useful error message. This proves Paul De Bra's point that every new feature should be implemented slowly and not in one fowl swoop.
- When the files on the server are changed and you attempt to reload the page, this may take a while. I do not know why yet but will attempt to see if there is anything that can be done to speed this up. Right now it is very annoying!

# Future Plans
As an enhancement to the development process of this application, we can think about using SASS for clearer css writing (which then has to be compiled, for instance via a gulp build process). We can also think about integrating live reload in to our dev tools so that reloading the page when making changes can be a thing of the past.
