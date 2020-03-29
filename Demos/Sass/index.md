# Sass demo

# Instructions Demo Built-in CSS Classes

In Blazor, there are a couple of helpful CSS functionalities.

## Navlink

One of them is the NavLink

### 1. In Shared \ MainLayout.razor

There you can see 

```` HTML
<NavMenu> 
````

This is the navmenu component that is the left menu of the page.


### 2. In Shared \ NavMenu.razor
This is the navmenu component,it is using the built-in navlink-component.

``` HTML
<div class="@NavMenuCssClass" @onclick="ToggleNavMenu">
    <ul class="nav flex-column">
        <li class="nav-item px-3">
            <NavLink class="nav-link" href="" Match="NavLinkMatch.All">
                <span class="oi oi-home" aria-hidden="true"></span> Home
            </NavLink>
        </li>
        <li class="nav-item px-3">
            <NavLink class="nav-link" href="counter">
                <span class="oi oi-plus" aria-hidden="true"></span> Counter
            </NavLink>
        </li>
        <li class="nav-item px-3">
            <NavLink class="nav-link" href="fetchdata">
                <span class="oi oi-list-rich" aria-hidden="true"></span> Fetch data
            </NavLink>
        </li>
    </ul>
</div>
```

if we take a look at one of the items

``` html
 <NavLink class="nav-link" href="fetchdata">
                    <span class="oi oi-list-rich" aria-hidden="true"></span> Fetch data
</NavLink>
```

This will generate the following link

```html

<a href="fetchdata" class="nav-link"><!--!-->
    <span class="oi oi-list-rich" aria-hidden="true"></span> Fetch data
</a>
```
When one of these links are clicked it will match the url and add an active class to the generated link.

``` html
<a href="fetchdata" class="nav-link active"><!--!-->
    <span class="oi oi-list-rich" aria-hidden="true"></span> Fetch data
</a>
```

1. Start the project an run debug tools (F12)
2. Inspect the link the selected link
3. Inspect a non selected (active) link.
   

## Forms

When it comes to forms, blazor has som built-in functionality.
There are X component used in this part

``` html
<EditForm/>
<DataAnnotationsValidator/>
<InputText/>
<ValidationMessage/>
```

In this demo we are not going into depth on how they work.  
**Editform** will create form tags for you form.  
**DataAnnotaionValidator** will validate your form based on the data annotations on you data class.  
**InputText** will add an input field and you will get som other benefits like the CSS classes.  
**ValidationMessage** will show any validation problems in the model.

### In Pages / Form.razor

This file contains all the parts for this demo including a data class.
Normally I would put this in a separate file so don't think this is the best practice in any way.

1. Take a look at the Person class in the code-section

``` csharp
public class Person
{
    [Required(ErrorMessage="Please provide a name",AllowEmptyStrings =false)]
    public string Name { get; set; }

    [Required(ErrorMessage = "Please provide an age")]
    public int Age { get; set; }

}
```

This class contains two properties, *Name* and *Age*.
The properties are decorated with DataAnnotations, in this case *Required*, and also an optional error message if the data is missing.

2. There is also an insstace of this class in the code-section

``` csharp
protected Person Item = new Person();
``` 

3. The edit form contains all the components described above

``` HTML
<EditForm Model="Item" OnValidSubmit="@HandleValidSubmit">
        <DataAnnotationsValidator />
        <div class="form-row">
            <div class="form-group">
                <label for="ItemName">Name</label>
                <InputText @bind-Value="Item.Name" id="ItemName"></InputText>
                <ValidationMessage For="@(() => Item.Name)" />
            </div>
        </div>
        <div class="form-row">
            <div class="form-group">
                <label for="ItemAge">Age</label>
                <InputNumber @bind-Value="Item.Age" id="ItemAge"></InputNumber>
                <ValidationMessage For="@(() => Item.Age)" />
            </div>
        </div>
        <button type="submit">Submit</button>
    </EditForm>
```

1. Run project
2. Run F12 to see the before state
3. Type anything into the field
If you enter any text into the name field it will turn green automatically.
The InputText will add a class called *.valid* and *modified*.

These are some of the build in functions when it comes to adding and removing CSS classes.



In this demo we are not going to write much code.
This is a demo of how we work with Sass (and CSS) and contains a couple of ideas on how you can create a better UX using Blazor.
It uses Sass, Components and Bootstrap.

## Bootstrap Setup

The first thing we want to do is to add SASS.
Bootstrap are distributing their CSS as SASS files which works great for us.
1. Head over to [Bootstrap](https://getbootstrap.com/docs/4.4/getting-started/download/#source-files) and download the source files.
2. In the root of the project, create a folder called "Style".
3. Extract Bootstrap to that folder
4. In the style folder create a file called *site.scss*
5. Add Bootstrap the file

```` css
@import "bootstrap-4.4.1/scss/bootstrap";
````

6. Right click on that file and select "Web Compiler" and "Compile File".  
This will create a file called compilerconfig.json in the root of the project.  
7. In the root folder open compilerconfig.json
8. Change the output of the file to *wwwroot/css/site.css*
```
[
  {
    "outputFile": "wwwroot/CSS/Site.css",
    "inputFile": "Styles/Site.scss"
  }
]
```
Now we are all setup, everytime we save the scss this will generate the css file.


## Navigation

Next up we are going to change the navigation

> [!IMPORTANT]
> Show Presentation here


### In the file Shared / MainLayout

Replace the content with this:
```` html
[!INCLUDE [AddAnimationStyles](~\End\Shared\MainLayout.razor)]
````



We have removed som divs and replaced some with a  ```<main>```-tag instead.
We still have a div tag but you might be able to change this to a Article tag or section instead, but for now we keep one div tag.

### in the shared / NavMenu-file
Replace the content with 

```` html
[!INCLUDE [AddAnimationStyles](~\End\Shared\NavMenu.razor)]
````

Alot have happend here, we have removed almost all classes and cleaned up the html quite a lot, it now describes the actual hierarchy of the document better.

### In the Style / navigation.scss
Add the following code

```` css
[!INCLUDE [AddAnimationStyles](~\End\Styles\navigation.scss)]
````

> [!IMPORTANT]
> Continue here after CodeSurfer

In this case we are assuming there is only going to be one nav object (this might not be true for all apps, if not you can always make it more specific by adding html>body>).
The first style nav is importing all the styles from Bootstrap, so we no longer have to add them to the class attribute. 
The same goes for the rest of the styles, we make sure all we extend the html-tag with the styles from bootstrap.
This will make the html a lot cleaner, I don´t have to know the classes while I´m developing I only need to describe the data.
Sure this might not be the best solution for many, but for us, for us this world perfectly.

Now the menu supplied with the default template in blazor is a Bootstrap menu, without most of the unnecessary styles and div tags.

1. Start the site
2. Click around

## Forms

1. In the Pages folder create a file called form.razor
2. Add the following code

```` html
[!INCLUDE [formrazor](~\end\pages\form.razor)]
````

```` csharp
@code {
    protected Person Item = new Person();

    public class Person
    {
        [Required(ErrorMessage="Please provide a name",AllowEmptyStrings =false)]
        public string Name { get; set; }
        [Required(ErrorMessage = "Please provide an age")]
        public int Age { get; set; }
    }

    protected async Task HandleValidSubmit()
    {

    }
}

````

This is a typical simple form, notice the ````[Required]```` tag. This will tell the validation that we need data in these fields.
By adding ```` <DataAnnotationsValidator />```` and ````<ValidationMessage For="@(() => Item.Name)" />```` the error message supplied will be shown beneath each textbox.

1. Run the project see the styles.
   This looks the same as the project we sa in the first demo.
2. In Styles \ Site.scss add
````css
[!INCLUDE [AddForm](~/Snippets/AddFormsStyles.md)]
````
We can make this a bit better.

### In the Styles / forms.scss file
Add the following code

```` css
[!INCLUDE [formsscss](~/End/Styles/Forms.scss)]
````

Blazor is adding *.valid*, *.modified*, and *.invalid* to the textboxes upon validation, to get a better UX we can add the Bootstrap views to those tags by adding *.is-valid* and *.was-validated* and so on.
So without adding a single line of code (everything controlled from CSS) we can get the bootstrap look to these fields.

What we have done is that we have created a component that adds the validation message, a success message (remember the positive effects of positive feedback) and it reads data from the attributes on the data class (Displayname for example).
This means that every time we use a particular data model we will get the same text as a label. (override is available).  
We wont have to figure out what that text is, and we only need to change it in one place if we need to change it further along.

## Progress
The last demo I will show is how you can add some of those neurotransmitters and hormones.
There were a couple of returning things "Positive words", "progress", and "Gamification".
I have created a couple of components that will help with that.
The first one is *Azmtextinput* it will show a ordinary textbox, it will also show a label taken from the DisplayName attribute.
You can add watermarks, instructions and perhaps most importantly a success message.
Tell the user they did something good.
It has all the Bootstrap styling.

The second one is *ProgressSummary*.
This component uses Validation summary to figure out how far along our user are.
This is a kind of progress and gamification.
1. Start the project and type in you name
2. Notice "nice to meet you"
3. Notice the percentage is changing.

To create the progress I used styles and html I found in the internet and just changed some values to get it to work with Blazor.
One of the best parts with Blazor is that it is regular HTML and CSS in the end.

## Animation
For this demo I have added a small delay to the loading of the weather.
I have also increased the amount of items to 50.
1. Start the project and navigate to /Fetch.
Notice that you won´t see any data and the data just pops up.
2. In the styles / site.scss
Add    
[!INCLUDE [AddAnimationStyles](~\Snippets\AddSpinkitstyles.md)]
3. Run the projects again.
I have already added Spinkit to my project.
If you want to learn how to make a Spinkit-component check out Ed Charbenaues session later today.
4. In the styles / site.scss
Add    
[!INCLUDE [AddAnimationStyles](~\Snippets\AddAnimationStyles.md)]




