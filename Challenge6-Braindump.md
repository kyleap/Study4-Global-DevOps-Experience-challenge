

# Challenge 6 - Braindump

Ok, so I created a new pull request where I had the India team update the frontend code. Please merge this in your `main` branch. You will find it that the `EventCatalogController`can now call a new method on our catalog API called `EventRecommendations`. This controller already has a constructor that creates the semantic kernel instance that you can use.

The only thing you need to do is implement the method `GetRecommendations` in the `EventRecommendations.cs` file in the catalog project. This method needs to query the events repository and get the events that are available in the next month.

You can use the [Basic InvokePromptAsync](https://learn.microsoft.com/en-us/semantic-kernel/prompts/your-first-prompt?tabs=Csharp) method for that. If you just get the events from the DB and provide these eventd as argument to your prompt.

These events are used to ask the Kernel to provide you recommendations. For this, you write a prompt that gives you the results back as a list of comma-separated event identifiers. These identifiers can be used to select the correct events from the list of events you retrieved, and then you return this as the result of the function.

In the same way as you did with the previous feature (Our AI Event Parser), you create a prompt that instructs the LLM to return this list of events that would match the customer's need based on the artist they provided as their favorite.

