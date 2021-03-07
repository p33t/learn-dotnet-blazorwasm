# Read Me for Blazor Learning Project

Can use anonymous lambda methods / expressions to avoid needing to 'unregister' an action-listener/event-delegate ([ref](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-5.0#component-disposal-with-idisposable)).
But is only safe if object lifetime is understood/known. 

Use `CancellationTokenSource` to cancel/abort long-running operations ([ref](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-5.0#component-disposal-with-idisposable))

See also `app/Pages/razorfundamentals`.

See also [Notes from Blazing Pizza Workshop](Notes_BlazingPizza.md)