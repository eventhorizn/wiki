- I need to get notes on codespaces
    - Can I mess around w/ them for free?
    - visual studio codespaces
    - container of active environment
- new terminal? Windows Terminal
- winget (new windows package manager)
    - replacing nuget?

# Codespaces

This is what's been most exciting for me:

https://code.visualstudio.com/docs/remote/codespaces


https://devblogs.microsoft.com/visualstudio/introducing-visual-studio-codespaces/

- The development environment is now containerized
    - Easy to get up and running for a developer
    - Good for orgs that build apps in different languages and environments
- Runs in Azure, so there is a cost for use
    - [Pricing](https://azure.microsoft.com/en-us/pricing/details/visual-studio-online/)
    - This is what vscode online has become
- How much do we spend on hardware? compare that to cost to use this
- can connect to a codespace on the desktop version of vscode (more powerful machine, etc)
- develop on ipad, shit laptops, home machines

# Windows Terminal

https://devblogs.microsoft.com/commandline/windows-terminal-1-0/

Panes for multiple terminals all w/i Windows Terminal

# Windows Package Manager

Doesn't seem to be a development package manager replacement (nuget)
- Instead, seems to be a way to install apps on a windows system

# Modern Web UI w/ Blazor WebAssembly

https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.1

Wednesday

blazor.net (online)

Blazor: single page apps w/ c# and .net w/o javascript

Looks like it's a .net core only thing

VS 2019, .net core sdk (3.1)

WebAssembly runs in the browser (doesn't hit server)
- There is an option for a Blazor server app

Client side routing

can debug c# code in browser debugger

- What about WCF?
    - How much do we use WCF?
    - Not supported in core
    - https://blog.tonysneed.com/2016/01/06/wcf-is-dead-long-live-mvc-6/
    - https://devblogs.microsoft.com/dotnet/custom-asp-net-core-middleware-example/

# Modernize Windows Server apps w/ Containers

you can take an existing WS app (w/o any changes), put it in a container, hook it up to CI/CD and then deploy to a k8s service

So, looks like you build an image of your app, deploy that image to a container registry service, hook it up to a CI/CD pipeline, and use that pipeline to deploy the image to a k8s service
- This can be in azure, but it doesn't need to be
- The k8s deploys many instances of the app, but the managed db is static

The tooling in azure to monitor apps (and errors) is very nice
- Just think how many separate apps we use to do everything, azure gives you a one stop shop experience

Ingress controllers manage shutting down a deployed image so traffic doesn't hit it
- push night automated sound nice?
- i.e you need to push a new version of an app. k8s service w/ ingress controller can systematically shut down images, and spin up new ones and manage traffic