``` razor
<BlazorScopedCss.ScopedStyle EmbeddedStylePath="FetchData.razor.css"
                             Parent="this"
                             AfterInit="StateHasChanged"
                             @ref="scopedStyle" />
```
