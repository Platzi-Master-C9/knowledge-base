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

**State Management Tool**  | **Specific Framework**
------------- | -------------
NGRX | Angular
NGXS | Angular
Context | React
Relay* | React
Hooks | React
React Query | React
Vuex | Vue
**Redux** | **No**
AKITA | No
Mobx | No

*In case we decide to use GraphQL, it is recommended to use Relay as State Management

# Adoption strategy
First of all, the technical necessity of the tool is evaluated, if the impact on the states of the components its difficult to implement, we need to use a complete solution such as Redux, Recoil, etc. In case it is not strictly necessary, other solutions will be approached taking into account the % of knowledge within the team and the ease of implementation, as in the case of the State Management that are specific to React. It is also worth that it is possible to make use of several solutions depending on the complexity of each component.The chosen tool can be implemented initially in the cases mentioned in Detailed design.

# How we teach this
In case the people who have not used any STATE MANAGEMENT are in the minority, resources (readings or Platzi courses) will be provided to acquire skills in this tool, making its adoption gradually, and in case it is accepted for the project, it should be coordinated with all the members. State Management will be used indiscriminately in many components of the application

# Unresolved questions
- Which C9 members have had experience using STATE MANAGEMENT tools and which ones?

- Who has no experience with the use of the tool?

- Could we use several tools for state management depending on the complexity of each component?

- Will the state management we choose only be used in places or in the whole application?

- How to teach it, does it apply only to state management or the context that comes with the framework used?
