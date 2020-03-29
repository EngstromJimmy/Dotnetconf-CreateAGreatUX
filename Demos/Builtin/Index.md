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







