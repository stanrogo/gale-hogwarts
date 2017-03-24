# gale_hogwarts
Provides the code for an adaptable learning experience and Hogwarts School of Witchcraft and Wizardry

# Development Environment Set Up

After a painstaking process, I finally figured out how to actually set up a fully fledged (almost) dev environment in which we can collaboratively develop our application.

## Prerequisites
- GALE must be installed on your computer as per the instructions found on [canvas](https://canvas.tue.nl).
- Node version 6 + should be installed and can be downloaded on the [official site](https://nodejs.org/en/download/). We will use node to be able to compile SASS files to CSS and to run our file server with. After install check if you have access to 'npm' from the command line (reopen your command line windows before you do this). If not, you may have to do some environment variable tweaking.
- Git must be installed on your system with the ability to clone repos and run git commands. For information on how to do this consult the git [help documentation](https://help.github.com/articles/set-up-git/).

## First Steps
Now that you (hopefully) have all the prerequisites in place we can begin to deploy the application. As a first step, simply clone this repository to your local machine to whatever folder you like.

Next, navigate to the directory you just cloned using terminal/powershell. Now run: ```npm install```. If you're using a mac, you will have to execute this command as ```sudo npm install```. This will install all the necessary files that we will use. After this run the command ```npm start``` which will start a server running on port 8000, serving out the files in this directory.

Now launch the GALE server which should open on port 8080 by default. Use the methods discussed in the lecture slides.

You can now launch the gale application! Navigate to the URL that should look as follows: ```http://localhost:8080/gale/concept/http://localhost:8000/hogwarts/hogwarts```.

This should present you with the intro page which currently has no adaptation at all.

# Vendor Tools

In order to make development of such an application easier than it otherwise would be, we can use a multitude of 3rd party tools to speed up the development workflow. These tools are mentioned below:

- Zurb Foundation - a easy to use CSS framework that hasn't been overused and provides tonnes of customisation.
- SASS - an extension to CSS that allows you to have variables and functions within your CSS. If you want to know more then google it.

# Common Issues (and How to Fix Them)

While developing there are some things to watch out for:
- If you CRUD a concept, then the changes might not be reflected until you restart the GALE server. Do this step before wondering why it isn't working.
- A badly created concept will give a very not useful error message. This proves Paul De Bra's point that every new feature should be implemented slowly and not in one fowl swoop.
- When the files on the server are changed and you attempt to reload the page, this may take a while. I do not know why yet but will attempt to see if there is anything that can be done to speed this up. Right now it is very annoying!

# GAM Files

After struggling a lot to figure out the exact reason why things are, I have compiled a list of when to do what
which I hope will help to serve as a reference guide when using the GAM syntax.

-  <-(parent)hogwarts/basic {} means that the basic page of hogwarts is a child of the current concept
-  ->(parent)../school means that the current concept has a parent called school
( The ../ is a reference to where the parent is located in the *hierarchy* based on the child)

Now let's look at the code below:

```
    #[visited]:Integer `0`
    #layout.title `The title`

    #resource `[[=layout.xhtml]]`
    #resource =`~
        return "[[=layout.xhtml]]";
    `

    event +`
        ${#course-knowledge} = 2;
    `
    event +`${#course-knowledge} = 2;`
```

Note that we use **back ticks** when writing. This makes sure that we don't need to escape characters and keeps all the
code consistent with each other. So please, use back ticks everywhere.

The meaning of this is something along the following lines:

- Persistent attributes are denoted by #[attribute]:type `value` - this will initialise this attribute once and store
it on the server.
- Properties of attributes do not need to be assigned and are instead directly set without the need for an = sign.
- Attribute expressions can either be evaluated and assigned by use of #attribute =`code`, or for multiline, the ~ symbol
denotes that this attributes code will be evaluated over multiple lines.
- Events are denoted by event +`event code` - the event code is concatenated into a single string and then evaluated at
run time. This is why the presence of the + is needed here. As you can see, event code can be multi line or single line.

```
    <gale:for var="concept" expr="${#fragments}">
        <h2>
            <gale:variable expr="${%concept?title}"/>
        </h2>
        <gale:object name="%concept" />
    </gale:for>
```

In the code above, we see how we retrieve attributes of the current concept via ${#attribute}. We also see how the
variable name is accessed using ${%variable-name} and %variable-name. The latter evaluates it directly as a string or
whatever type it is. The former evaluates it in a gale expression, which if it is a concept identifier, will allow access
to its properties.

Other things:

- You are not allowed to declare local variables in gale expression code. Therefore the code
```String[] list = {"string1", "string2"}``` will not work and no error message will be given.
- You are allowed to declare local variables in event code.

## Global Variables:

By using a construct like: ```${_concept->(personal)``` to access the personal concept, this can be a store of
all persistent values that follow the user around. If you need something to be available for all concepts, declare it
in here, since this way the value will be global and not for each individual concept.

Always reference the personal concept like so (depending on the hierarchy): ```->(personal)../../_personal```.
This will allow you to use it in that particular scope.