- Start Date: 2022-02-24
- Members: Adriana Lucia Ardila Ramirez, Julian Camilo Huertas Fandiño, Mauricio Perera
- RFC PR: (leave this empty)

# Summary

In this case, we work with the flow of favorites. The functionality is simple: when a logged-in user does a search and sees a property they like, they can either attach it to an existing listing or create a new listing to attach it to.

The user can access and manage all their lists and consult the properties in any of them.

# Motivation

Users of this platform are looking for a solution to make a trip. This enables users to have a small group of properties organized in different lists by a common characteristic that they can use to make a quick reservation at the property of their dreams.

It's important to let them make different lists for different situations (vacation, quick trip, work trip, etc.).

This feature simplifies the user experience and generates extra value related to the user's interests by allowing them to have the power and freedom to access filtered content based solely on their decisions.

# Detailed design

For these functions, we consider the user to be logged in and any information generated is related to them. We suppose the easiest thing in this case is to use the current user id or a similar value.

Important: Any other users can not be affected by the actions of the current user in this case.

We use the heart icon as a call to action. This icon has two states. In the first, the icon shows only the borders, which means property is not attached in any of the users' lists. In the other case, the icon is fully colored and means the property has been attached to any current user favorite list.

## The flows of favorites list:

When the user picks in the user menu (corner upper right with her photo) the "Favorites List" option, it redirects to a page where he can see all the lists created and active in the past by him. When the user picks any list, it redirects to a page similar to the property results where all properties on the list are shown with their geoposition on a map.

This view is a clone of the result of the search with few changes. The first difference is based on the properties to be shown. They are limited to only the properties attached to the list. The second difference is in the header. This view shows the list title and a button to edit the list of properties. If a user clicks on the title, they can edit it. With a second click on any other part of the page, they exit the title editor mode and save the changes. The button is a "delete list" button. When the user picks this, it shows a confirmation message to validate if the user really wants to delete the full list. If the user confirms the list, it is deleted and the user is redirected to the Favorites list view. 

The last functionality difference is related to the heart icons. In the list, all properties show a completed colored icon. If the user wants to remove any property, the user only needs to pick up the heart icon. The property related to the icon picked continues to show in the list, but the icon changes to a stroke state, and if the user likes to restore this, they can click on the heart icon one more time and the state is reverted. When the user refreshes the page, the changes in the property list are applied immediately.

When the user searches through the full content of the site and finds an interesting property, he can attach it to a list. For this, he can click on the heart. This action opens a modal. The modal shows the option to create a new list. If the user picks this, the option changes to an input text to write the list name, and a button to confirm the creation. Under this option, the modal shows a list of "favorite lists" previously created by the user. By default, any user begins with a list called "Mis Favoritos". This list is a speed option to save interested properties without the need to create a new list or select a previously created one.

After the user sets where he likes to attach the property (in a new list, the default list, or other created list), a confirmation message is shown to confirm the action is completed and the user can continue using the platform.

# Drawbacks

Why should we _not_ do this? Please consider:

- Implementation cost, both in term of code size and complexity
- Whether the proposed feature can be implemented in user space
- The impact on teaching people React
- Integration of this feature with other existing and planned features
- Cost of migrating existing React applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Adoption strategy

In this case, we suggest making this function as a module that we can turn on/off if it's required. The module contains the heart icon, the pop-ups, and the ability to create lists and list content views.

Any of this functions are related with the user id and property id, we can create a particular table to related a user with theres lists and the lists with there properties. All the rest of the data (property names, descriptions, photos, urls, etc) can be taken from the already existing data in the DB.

This function only needs to read, write, or update the table that relates to the users' lists and properties, read the property data by id, and does not need to make any other changes in the data.

# How we teach this

This is a regular and frequently used function. Favorite lists or wish lists are the most common in any ecommerce platform or similar.

This idea is a complement and continuation of the full idea of the platform. The functions to enable any user to preselect the contents most relevance to there and organize there in a lists its a basic functionality today.

The acceptance of these functions means we need to create an extra table in the database and a new user flow. This action needs to appear in the product documentation.

To the new devs on the project, this is a part of the product related directly to the user and with some independence from the rest of the data.

To the old devs on the project, this is a part of the product related directly to the user and with some independence from the rest of the data.

# Unresolved questions

- [ ] Users can share their list to others?
- [ ] The lists take a taxonomy to filter or similar?
- [ ] The owner of a property have any notification when their property is posted in any user list?
- [ ] The favorite can be deprecated or have an end time, the favorite will disappear after this?
- [ ] if owner user deleted a property there disappeared to the list? The users with this property as their favorite take any notification about this?
