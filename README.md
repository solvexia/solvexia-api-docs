# SolveXia API Docs

This is an official repository for the SolveXia Public API documentation. Please follow this repository to see the changes over time.

For bug reports or change proposals for APIs please use issues, or create pull requests.

## Gettings started

In order to get started using SolveXia Public API you need to create an application in SolveXia API portal.

### Register SolveXia Application

Any application that is intended to access SolveXia Public API must have authorization credentials that identify the application to SolveXia authorization server.

Create authorization credentials for you app:

1. Navigate to SolveXia API portal from the user dropdown menu.
2. Click "Create new application".
3. Specify the name and callback URL. Click "Create application".
4. If the creation is successful you will see Client Id and Client Secret credentials generated.
5. Copy credentials and store them safely. You will not be able to see Client Secret again unless you generate a new one.


## OAuth

The following pages detail the OAuth API's that govern OAuth authorization flows, in order to be able to generate tokens to use SolveXia APIs.

[OAuth APIs](./oauth/authentication-oauth2.0.md)  

## Solvexia APIs

The following pages detail the Solvexia API's to manage client resources in SolveXia automation system.

[Process APIs](./processes/processes.md)  
[Process Run APIs](./process_runs/process_runs.md)  
[Data Step APIs](./steps/datasteps.md)  
[Table APIs](./tables/tables.md)   
[File APIs](./file/file.md)   
[User APIs](./users/users.md)   
[User Group APIs](./user_groups/user_groups.md)
