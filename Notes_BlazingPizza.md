Notes from working through [Blazing Pizza workshop](https://github.com/dotnet-presentations/blazor-workshop)

## 02
`EventCallback` has smarts around dispatching events and re-rendering the component hosting the handler/delegate
([ref](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/02-customize-a-pizza.md#component-events)).
If the object hosting the handler/delegate is not a component (e.g. AppState pattern) then the component that *hooked up*
the handler is used ([ref](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/04-refactor-state-management.md#exploring-state-changes)).

## 03
Keep links relative (no / at beginning) so can deploy to non-root contexts.  &lt;base href="/"> in index.html specifies prefix for relative links.

Blazor will attempt to nav to link and if not found then do full reload.  Only then will the not-found page appear.

[Details](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/03-show-order-status.md#adding-an-order-details-display)
of how routing works.  Router listens for navigation events from browser and intercepts default behaviour.

Blazor component instances are reused when, say, a URL parameter changes.  So `OnParametersSet()` is the best place to process parameters.

Dispose polling loops to avoid wasted resources (using IDisposable).  `CancellationTokenSource` is handy.

## 04
[AppState](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/04-refactor-state-management.md#a-solution)
pattern for retaining state during navigation.  State often needs to outlive components.

'Scoped' scope in DI means 'for the current unit of work'.  'Singleton' means 'for all users'.

[Good Recap](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/04-refactor-state-management.md#conclusion)
of AppState, event handling & rendering.

## 05
Annotations in model class are enforced by MVC Controller.

Use &lt;EditForm> to set up an `EditContext` in the client side to manage the editing process ([ref](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/05-checkout-with-validation.md#adding-client-side-validation)).  
&ltDataAnnotationsValidator> to implement validation dictated by annotations.  Or a different element if using other rules.

&lt;ValidationMessage For=...> and &lt;InputXxx> to make for fields user friendly.

&lt;button disabled="@.."> handy for preventing double-submit.

## 06
Good [summary](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/06-authentication-and-authorization.md#tracking-authentication-state)
of OpenID Connect process for webapps.  Entails delegating auth to identity provider which redirects back to webapps endpoints according to outcome.

Beginning of fully featured user management system (use built-in components for Blazor / ASP.NET)

Various steps needed to get authN going.  But still just JIT enforcement (no so convenient for user who isn't logged in).

Can easily restrict pages on client side and redirect to login (with returnUrl param) while explicitly restricting the page with `[Authorize]`
or content with `<AuthorizeView>`.

## 07
Can interact with browser apis & JS libraries with `IJSRuntime`.  Bundle libs in `wwwroot`.

`OnAfterRenderAsync()` lifecycle event for actions after component has rendered markup.

[OpenStreetMap](https://www.openstreetmap.org/) for free maps (open use).  
[LeafletJS](https://leafletjs.com/) for mobile-friendly interactive maps.

Import content from libraries via `_content` in header of `wwwroot/index.html`.  CSharp classes and static content for example.

`EventCallback` properties can be async, which will be awaited.

# 08
Razor component library: `dotnet new razorclasslib -o BlazingComponents`
> Appears significant differences with project file layout between .NET 3.1 and 5.0.  
> Ended up copying contents of the other component library .csproj file.

Templates can have `RenderFragment` parameters (with or without generic type).  If typed then
an `@@context` variable is available to contained content (which can have another name if necessary).