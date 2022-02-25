- Start Date: 2022-02-24
- Members: Adriana Lucia Ardila Ramirez, Julian Camilo Huertas Fandiño, Mauricio Perera
- RFC PR: (leave this empty)

# Summary

In this case we work with the favorites flow. The functionality its simple, when a logged in user sees a proprietary who like he can attach this to an existent list or create a new list to attach this.

The user can access and manage all your lists and check the properties in any one of theirs.

# Motivation

The users of this platform are searching its a solution to make a trip. With this lists they can get an accessible short list of their more relevant or interested properties and can use this to make a fast reservation on the property of your dreams.

It's important to let them make different lists for different situations (holidays, a fast travel, a work trip, etc).

This function facilitate the user experience and generate a extra value related with the user interests permitting there with the power and liberty of access to a filtered content based only on her decisions

# Detailed design

To these functions we consider the user is logged in and any information generated is related to there. We supposed the easiest in this case is to use the current user id or a similar value related directly only with this.

Important: Any other users can not be affected by the actions of the current user in this case.
We use a heart icon as a call to action. This icon has two states, in the first the icon shows only the borders and this it means property is not attached in any of the users list. In the other case the icon is fully colored and it means the property has attached to any current user favorite list.

## The flows of favorites list:

When the user pick in the user menu (corner upper right with her photo) the "Favorites List" option it redirects to a page where can see all lists created and actived in the past by him. When picked on any list its redirect to a page similar asear property results where are shown all properties on the list and the geoposition of theres on a map.

This view is a clone of the result of search with few changes. The first difference it's based on the properties to show, they are limited to only to all properties attached on the list. The second difference it's on the header. This view shows the list title and a button before the list of properties. If user click on the title can edit him, whith a second click on any other part of the page its exit the title editor mode and save the changes. The button it's a delete list button, when the user picks this it shows a confirmation message to validate if the user really likes to delete the full list. If user confirm him the list its deleted and redirect to Favorites list view. In case to cancel the delete user continue in the list view.

The last functionality difference is related to the heart icons. In the list all properties show a completed colored icon, if the user likes to remove any property only need take to pick in the heart icon of this. The property related to the icon picked continue showed in the list but the icon change to stroke state, and if the user like restore this can click in the heart icon one more time and the state is reverted. When the user refreshes the page the changes in the property list are applied definitely.

When the user searches in the full content of the site and finds an interesting property he can attach it to a list. To this he can click on the heart, this ation open a modal. The modal sho wthe option to create a new list, if the user pick this the option changes to an input text to write the list name, and a button to confirm the creation. Under this option in the modal show a list of "Favorites lists" previously created by the user. By default any user begins with a list called "Mis Favoritos”, this list is a speed option to save interested properties without need to create a new list or select a previou created.

After the user set where he like attach the property (in a new list, the default list, or other created list) a confirmation message its showed to confirm the action its completed an the user can continue using the platform.

# Drawbacks

Why should we _not_ do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Adoption strategy

In this case we suggest make this function as a module what we can turn on/off if it's required. The module contains the heart icon, the pop ups and the create list, lists, and list content view.

Any of this functions are related with the user id and property id, we can create a particular table to related a user with theres lists and the lists with there properties. All the rest of the data (property name, descriptions, photos, url, etc) we can take from the already existing data in the DB.

This function only need can read, write or update the table what relate the users lists and properties, read the property data by id and not need make any other change in the data.

# How we teach this

This its a regular and frequently used function. Terms as Favorite list, or wishes list are the most common in any ecommerce platform or similar.

This idea its a complement and continuation of a full idea of the platform. The functions to enable any user to preselect the contents most relevance to there and organize there in a lists its a basic functionality today.

The acceptance of these functions mean we need make a extra table in the db and a new user flow. This action need appears on the documentation of the product.

To the new devs on the project this is a part of the product related directly with the user and with some independence of the rest of the data.

To the old devs on the project this is a part of the product related directly with the user and with some independence of the rest of the data.

# Unresolved questions

- [ ] Users can share their list to others?
- [ ] The lists take a taxonomy to filter or similar?
- [ ] The owner of a property have any notification when their property is posted in any user list?
- [ ] The favorite can be deprecated or have an end time, the favorite will disappear after this?
- [ ] if owner user deleted a property there disappeared to the list? The users with this property as their favorite take any notification about this?
