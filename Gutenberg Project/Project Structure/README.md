Project structural overview


- Tenant Apps (market repos which point to the `host` repo, having flexibility of overriding configurations)
    - Some repos:
        - SLI(Japan): [discovery-ltd/v1-tenant-25-flutter (github.com)](https://github.com/discovery-ltd/v1-tenant-25-flutter "https://github.com/discovery-ltd/v1-tenant-25-flutter")
        - PRT(Portugal): [discovery-ltd/v1-tenant-42-flutter (github.com)](https://github.com/discovery-ltd/v1-tenant-42-flutter "https://github.com/discovery-ltd/v1-tenant-42-flutter"), etc
    - (search for **tenant** in org. to get list of all tenant repos)
- [Central app](https://github.com/discovery-ltd/v1-gutenberg-central-app-flutter "https://github.com/discovery-ltd/v1-gutenberg-central-app-flutter") (`host` app which bundles all `modules` together)
- A Module repo can be a: 
    - **Journey module**
        - Standalone module with a collection of features constituting a user journey in the app.
        - Ex:- 
            - [Registration journey](https://github.com/discovery-ltd/v1-registration-journey-flutter "https://github.com/discovery-ltd/v1-registration-journey-flutter")
            - [Login Journey](https://github.com/discovery-ltd/v1-login-journey-flutter "https://github.com/discovery-ltd/v1-login-journey-flutter")
            - [Physical Activity Goals](https://github.com/discovery-ltd/v1-physical-activity-goals-flutter "https://github.com/discovery-ltd/v1-physical-activity-goals-flutter") journey
            - [Screenings & Vaccinations](https://github.com/discovery-ltd/v1-screenings-vaccinations-flutter "https://github.com/discovery-ltd/v1-screenings-vaccinations-flutter")
            - [Profile Settings](https://github.com/discovery-ltd/v1-profile-settings-flutter "https://github.com/discovery-ltd/v1-profile-settings-flutter"), etc
    - **Platform, common/shared module**
        - Packages which hold reusable and enforceable resources for all journey modules.
        - Includes core utilities like:
            - Design system [[discovery-ltd/v1-ui-lib-flutter (github.com)](https://github.com/discovery-ltd/v1-ui-lib-flutter "https://github.com/discovery-ltd/v1-ui-lib-flutter")]
                - theme, colors, typography
                - common components(widgets), etc
            - Base infrastructure 
                - Platform core(bundle of core dependencies) [[discovery-ltd/v1-platform-core-flutter (github.com)](https://github.com/discovery-ltd/v1-platform-core-flutter "https://github.com/discovery-ltd/v1-platform-core-flutter")]
                    - http-manager [[https://github.com/discovery-ltd/v1-http-manager-flutter](https://github.com/discovery-ltd/v1-http-manager-flutter "https://github.com/discovery-ltd/v1-http-manager-flutter")]
                    - session-manager
                    - storage & persistence
                    - common-utils
                    - resource-providers(localization, assets), etc
                - Framework-contracts(bundle of base interfaces) [[discovery-ltd/v1-framework-contracts-flutter (github.com)](https://github.com/discovery-ltd/v1-framework-contracts-flutter "https://github.com/discovery-ltd/v1-framework-contracts-flutter")]
    - **Wrapper service** 
        - Packages for external(rest mostly) API calls.
        - Code generated from the backend api-doc using JFrog, Freemarker Template (Yogesh's domain)
        - Example repos:
            - [https://github.com/discovery-ltd/v1-manage-assessments-micro-service-sdk-flutter](https://github.com/discovery-ltd/v1-manage-assessments-micro-service-sdk-flutter "https://github.com/discovery-ltd/v1-manage-assessments-micro-service-sdk-flutter")
            - [https://github.com/discovery-ltd/v2-manage-rewards-micro-service-sdk-flutter](https://github.com/discovery-ltd/v2-manage-rewards-micro-service-sdk-flutter "https://github.com/discovery-ltd/v2-manage-rewards-micro-service-sdk-flutter")


### TODO