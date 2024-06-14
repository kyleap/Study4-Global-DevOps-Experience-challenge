# Challenge 1 - Braindump 

Ok team, Jordan wants us to create a codespace for our repository so that we can onboard new development teams fast. I really think that we can benefit from this, so I've already done some research. Here are my first thoughts and the links to the documentation that I found:

### Codespace cofiguration:
- For setting up the codespace you can check [this link to Github](https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository). Make sure we can run c# code in the codespace.
- Jordan also mentioned some extensions that he wants to have installed. By browsing to the extensions tab you can install these plugins. I found [this quickstart](https://docs.github.com/en/codespaces/getting-started/quickstart) that briefly explains how it works to give you some ideas. It doesn't look too difficult. 
- Once you click 'Add to devcontainer.json' you get the opportunity to install additional features. 

### Debugging
We need to check if we can run and debug the application from our codespace. Just press F5 and make sure that all applications start. If not, you probably need to change the launch settings in VSCode. Please also check if the application works with breakpoints, we need to be able to debug our code!

### Port forwarding
There is some documentation about port forwarding in codespaces [right here](https://docs.github.com/en/codespaces/developing-in-a-codespace/forwarding-ports-in-your-codespace). That should get you started.  


### Finally
We need to make sure that the devcontainer.json file is complete and pushed to the main branch of the repository, otherwise others can not make use of it. 