# Challenge 3 - Testdriving GitHub Copilot

Hey Team, Alex here, Emily finally approved the use of GitHub Copilot. Before we unleash this on everyone in the organization, we need to test it out ourselves as platform team.

We've done a survey with the engineers on developer productivity and developer happiness and there were a lot of things that needs improvement. So let's do a hackathon to see if GitHub Copilot can help us improve the top 3 complaints from the survey.

### Survey results:
1. APIs are not restful
2. Lacking Unit tests
3. Internal developer documentation

## 1. Enabling GitHub Copilot
To start first enable GitHub Copilot and install the plugins in vscode for code completion and chat. I think especially the chat will be really helpfull here.

## 2. Hackathon challenge:

### APIs are not restful
We have a number of APIs that are not restful. In this hackathon let's focus on the `EventController.cs` in the `catalog` project. Make this controller restful.

This API is also being used in the frontend code so this needs to be compatible with the new restful API. Change the `EventCatalogService.cs` in the `frontend` project to use the new restful API.

### Lacking Unit tests
This same `EventController.cs` in the `catalog` project is also lacking unit tests. Write unit tests for this controller.

Make sure that these Unit tests are also compatible with the new restful API and are being ran in the pipeline.

Store the unit tests in a new .Net project called `catalog.tests`. and call the test class `EventControllerTests.cs`.

### Internal developer documentation
The current catalog API does not have any OpenAPI Specifications. You could add swagger to the API to generate the OpenAPI Specifications. Please try to have Copilot generate this addition of Swashbuckle for you to `program.cs`.