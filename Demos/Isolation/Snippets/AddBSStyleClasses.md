``` razor
@if (scopedStyle?.IsComplete ?? false)
{
    <h1 class="@scopedStyle.CssScopedClasses(scopedCssClasses: "myFirstScopedComponent")">Weather forecast</h1>

    <p class="@scopedStyle.CssClassesMixed(nonScopedCssClasses: "display-1", scopedCssClasses: "mySecondScopedComponent")">This component demonstrates fetching data from a service.</p>
}
```
