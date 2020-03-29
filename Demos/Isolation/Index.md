# CSS Isolation

Vue, Angular and React (using a plugin) has a way to isolate CSS.  
Personally I don´t see the beauty of it, instead of sharing CSS between all components, Isolated CSS rewrites the CSS rules so only that particular component are using the CSS.
But from what I have seen people are very passionate about this so I wanted to see if there was any ways to get this working in Blazor.  
There are actually a couple of ways of doing this, IMHO the best solution right now is a project called [BlazorScopedCss](https://github.com/alexandrereyes/BlazorScopedCss) by Alexander Reyes.  
The syntax differs a bit from what we are used to in other frameworks.

For these frameworks to work we either need to use Webpack or similar to package the CSS and rewrite it.
One of the thing I like with Blazor is the fact that I don´t need to transpile javascript or package CSS so I really don´t want to have to add that to my Blazor project.
Blazor scoped CSS lets you write CSS in normal CSS files (os SASS/LESS if you prefer) and then serve them rewritten to the web browser.

## BlazorScopedCSS

### Setup

1. Open Package manager and type

    ``` Powershell
    Install-Package BlazorScopedCss
    ```

    This will install the package into you project
2. In **setup.cs** and the *ConfigureServices*-method add
[!INCLUDE [AddBSCSSService](Snippets/AddBSCSSService.md)]

3. In _host.cshtml inside of the HEAD-tag add
[!INCLUDE [AddBSCSSStyle](Snippets/AddBSCSSStyle.md)]

4. In _host.cshtml toward the bottom (just after the blazor.server.js) of the page add
[!INCLUDE [AddBSCSSScript](Snippets/AddBSCSSScript.md)]

### Creating CSS

1. In the Pages folder create a file called *FetchData.razor.css*.  
This will keep the file just beside the FetchData.razor file.

2. Select your newly created file and make sure Build action is set to Embedded resource.

3. Add the following code to *FetchData.razor.css*
[!INCLUDE [AddBSCssContent](Snippets/AddBSCssContent.md)]

The important part here is the *-scopedId* that phrase is going to be replaced by the components id.

4. In the file pages / FetchData.razor in side of the @code-section add a variable.

[!INCLUDE [AddBSVariable](Snippets/AddBSVariable.md)]

5. At the top of the page att the BlazorScopedCss.ScopedStyle style component

[!INCLUDE [AddBSStyleComponent](Snippets/AddBSStyleComponent.md)]
Notice that it is referring to the scoped style variable we created in step 4.

6. Add the following code
[!INCLUDE [AddBSStyleClasses](Snippets/AddBSStyleClasses.md)]


Run the project ant take a look at the  \<style id="scopedCss"\>-tag.
