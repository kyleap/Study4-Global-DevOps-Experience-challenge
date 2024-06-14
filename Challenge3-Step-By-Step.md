# Challenge 3 - Step by Step Solution:


## 1. Enabling GitHub Copilot
Install GithubCopilot into Visual Studio Code.

1. Open Visual Studio Code
2. Click on the Extensions icon on the left sidebar
3. Search for "GitHub Copilot" in the search bar (https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
4. Click on the Install button

5. Install the Copilot Chat extension
6. Search for "GitHub Copilot Chat" in the search bar (https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)
7. Click on the Install button

![Image ](Images/Challenge03-01.png)

## 2. Hackathon challenge:

### APIs are not restful
1. GitHub Copilot can help us make the `EventController.cs` in the `catalog` project restful. Open the `EventController.cs` file and then open GitHub Copilot Chat.

2. In the chat ask `I want to make the EventController.cs restful. Please provide an implementation for the existing operations in a restful manner`. Copilot will provide suggestions on how to make the controller restful. Copy the suggestions into the `EventController.cs` file over the existing code.

3. To fix the frontend project, open the `EventCatalogService.cs` file in the `frontend` project and then open GitHub Copilot Chat.

4. In the chat ask `I want to make the EventCatalogService.cs use the new restful API. Please provide an implementation that is compatible with the new restful API`. Copilot will provide suggestions on how to make the service compatible with the new restful API. Copy the suggestions into the `EventCatalogService.cs` file over the existing code.

### Lacking Unit tests
GitHub Copilot should also be able to help us write unit tests for the `EventController.cs` in the `catalog` project. 

1. First create a new .Net project called `catalog.tests` in the solution.

2. Open the `EventController.cs` file and then open GitHub Copilot Chat.

3. In the chat ask `I want to write unit tests for the EventController.cs. Please create a number of unit tests that test all scenarios of the controller.`. Copilot will provide suggestions on how to write unit tests for the controller. Copy the suggestions into a new file called `EventControllerTests.cs` in the `catalog.tests` project.

### Internal developer documentation
GitHub Copilot can help us add Swagger to the API to generate OpenAPI Specifications.

1. Open the `program.cs` file in the `catalog` project and then open GitHub Copilot Chat.

2. In the chat ask `I want to add Swagger to the API to generate OpenAPI Specifications. Please provide an implementation to add Swashbuckle to the program.cs file.`. Copilot will provide suggestions on how to add Swagger to the API. Copy the suggestions into the `program.cs` file.