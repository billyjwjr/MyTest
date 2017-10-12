# Platform Unification Details

## Established Details
1. .NET Core to be used for new solution development.
2. Single project creation that centralizes the four endpoint entries using the existing /services.ashx entry point for backwards compatibility to third party providers.

## Task List
1. DC API documentation to be provided to DTV team.
2. Lower DC environment test environment details to be provided:
	- Endpoint address
	- Credentials
	- Testing and log viewing tools
3. Epic for mapping request/response flow:
	- Map DTV request to DC request
	- Map DC response to DTV response
4. Developers to determine .NET Core required installations and configurations for TeamCity build compatibility.
5. TechOps .NET Core required installations and configurations for TeamCity build compatibility.
6. Determine name for the application.
7. Create Github Repo for source code. 
8. Create new solution to contain DTV shim application
	- Stripped down PartnerGateway Project for the 4 endpoints
9. TeamCity build project
	- Automated branch builds
	- Automated PR builds
10. Octopus Deployment Project Creation
	- Lower environments
	- Production environments
	
## Outstanding Questions:	
1. Configuration/Suppression Details: How does DC handle phone package, product, beams, and other exclusions?
2. VisitID tracking: Generation in new translation tool and does DC require an additional field or have an area flexible enough to contain it.
3. Due to the automation testing using selenium and being based on OP, will this be invalidated?
	
## Technology Discussion Items:
1. TC may need upgraded and/or at the very least the associated build agent machines will need to be updated to be able to build .NET Core. Development team should provide a list of items needed to install on build agent machines. **This should be a priority for TechOps.**
2. Developer machines need to be capable of .NET Core development
	- Priyanka's machine specifically needs to be updated as Eric's was recently
	- New laptop hardware for the developers still remains outstanding

## Action Items:
1. Schedule recurring meetings in order to keep all DTV team members up to date on progress of implementation and development tasks. **(Rich Reed)**
