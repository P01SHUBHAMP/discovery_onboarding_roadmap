Following article aims to cover certain development guidelines, *partly* within our agreed upon methodologies of code architecture, state management & flow choices, modularization and responsibility segregation for an enterprise application like Gutenberg. Its highly opinionated but, intended for good reasons.

### TODO


### Index
- Dart standards (language & grammar)
	- analyzer (effective dart)
	- iterable extension methods
	- null aware access
	- defined return types
	- immutable objects & class definitions
	- handling hardcoded values (constants, enums, static getters)
	- naming standards for anything and everything
	- late, late final, var, dynamic
- Flutter specifics (UI)
	- Un-intelligent (Logic unaware) widgets
	- widget class v/s widget function
	- immutable widgets
	- refactoring into smaller independent components
	- screen, view and component
	- theming & localization extension
	- common standard components
	- layout, visual flow and scaling
	- overlays
	- listener, builder, consumer, provider
- BLoc
	- Strict bloc pattern (masking)
	- Bloc object scope
	- immutable state
	- lean and non-bloated state
	- separation of concern (UI, Bloc, data)
	- delegation/offloading of common behaviors to BlocObservers/Dad-bloc
- Architecture & responsibility segregation guidelines
	- feature-first clean architecture
	- core and shared chunks/resources
	- Api(remote, storage, platform) penetration level
		- Data
			- interface based datasources
			- SRP
			- exceptions to meaningful error/failure objects
		- Domain/Business
			- entity: minimalist data class
			- interface based usecases (overkill)
		- Presentation
			- Bloc layer (cli based thought process)
			- state aware screen, ephemeral views, dumb and happy widgets
- Error handling guidelines
	- catch, evaluate and translate exceptions at early stage (data layer preferably)
	- don't let null values flow freely
	- 
- Code coverage practices
	- not just for the sake of compliance
- Dependency injection
	- singleton vs factory; when and what
	- module based approach