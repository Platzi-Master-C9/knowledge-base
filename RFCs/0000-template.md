- Start Date: 2022-02-22
- Members: Carlos Henao and Angel Vazquez
- RFC PR: ( )

# Summary

Choosing the appropriate tool for "state management" that allows managing the flow of information (reading, writing, editing and deleting) considering the following factors:
- App size.
- Library and/or framework used: React, Angular, Vue, Svelte…
- Knowledge of the team that will develop and maintain it.

# Basic example

  Redux flow

  ```mermaid
    graph TD;
        STORE-->PROVIDER;
        PROVIDER-->CONTAINERS;
        CONTAINERS-->COMPONENTS;
        COMPONENTS-->COMPUTER;
        COMPUTER-->ACTION;
        ACTION-->REDUCERS;
        REDUCERS-->STORE;
  ```

# Motivation

Evaluate the use of State Management transversally in the components that need this tool, which require huge complexity and use a specific technology and which could be solved from the elements offered by React (Hooks or context API)
Reach a consensus with the C9 team to see the feasibility of implementing a State Management and Which choose?

# Detailed design

Possible cases to State Management:

- Favorite accommodation.
Being able to show and remember the user's favorites ♥ in all possible lists that will display (search, map, full description).
- User notifications.
Show, remember and keep updated the notification counter of the user's Profile, throughout their navigation on the site.
- Search an accommodation.

# Drawbacks

Cases in which this functionality should not be used:
The complexity of the applications or the other functionalities that are added to the project can dispense with STATE MANAGEMENT either because the states do not require updating or because the component does not have much complexity and can be updated efficiently with the hooks.
In this case we will not be able to use the context API since it updates the entire application to change a state, generating delays
Add a lot of complexity to a simple task, reload the entire page to change a single state.

# Alternatives

State Management Tool  | Specific Framework
------------- | -------------
NGRX | Angular
NGXS | Angular
Context | React
Relay* | React
Hooks | React
Vuex | Vue
**Redux** | **No**
AKITA | No
Mobx | No

*In case we decide to use GraphQL, it is recommended to use Relay as State Management

# Adoption strategy



# How we teach this



# Unresolved questions

