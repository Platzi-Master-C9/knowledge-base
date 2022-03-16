- Start Date: 2022-02-24
- Members: Adriana Lucia Ardila Ramirez, Julian Camilo Huertas Fandiño, Mauricio Perera
- RFC PR: (leave this empty)

# Summary

This feature will add the option to manage favorite places in the booking system, when a logged in user sees a place who like, he can add this place to an existent list or create a new list.
The user can see all of his lists, can access to the list and see all the liked places, can remove the liked places in a list and delete the list. the users will also be able to add a place from the search main page and create a list too.

# Motivation

The users of this platform are searching is a solution to make a trip. With this lists they can get an accessible short list of their more relevant or interested places and can use this to make a fast booking on the place of their dreams.
It's important to let them make different lists for different situations (holidays, a fast travel, a work trip, etc).
This feature ease the user experience and generate a extra value related with the user interests giving the freedom to access content based only on their decisions

# Detailed design

To these features we consider the user is logged in and any information generated is related to there. We supposed the easiest in this case is to use the current user id or a similar value related directly only with this.
Important: Any other users can not be affected by the actions of the current user in this case.

We use a heart icon as a call to action. This icon has two states, in the first the icon is unfilled and this it means the place is not added in any of the users list. In the other case the icon filled means the place has been added to any current user favorite list.

![image](https://user-images.githubusercontent.com/43361414/157812598-4ca3db91-50c6-44e5-a624-2a27cfb99cbd.png)

## Flows

### looking at my favorite lists:

When the user click on the photo (corner upper right )

![image](https://user-images.githubusercontent.com/43361414/157812631-c7c25ddf-5c2c-4234-8b2f-5ec02c35ab93.png)

it will be shown the menu, when the user click on "Favorites List" option it redirects to a page where can see all lists created.

![image](https://user-images.githubusercontent.com/43361414/157812740-292b6e2b-1dc4-4c84-bcc9-4f985021d25a.png)

When the user click on any list, the user will be redirect to a page listing the places that the user previously added to favorites.

![image](https://user-images.githubusercontent.com/43361414/157812761-e4b32614-2761-4624-9489-fd7996e63199.png)

This view is a clone of the result of search with few changes. The first difference it's based on the places to show, they are limited to only to all places added on the list. The second difference it's on the header. This view shows the list title of the list. If user click on the title can edit him, with a second click on any other part of the page its exit the title editor mode and save the changes.
If the user want to remove any places only need take to click on the heart icon of the place, the heart icon will change to an unfilled state this means that the place has been removed from the list. If the user want to restore this can click in the heart icon one more time and the place will be saved on the list again. the removed places only will disappear when the user leave the favorite list.

### Deleting a list:

To delete a whole list, the user need to access to his favorite list (read looking at my favorite lists). In this list there will be a delete button (trash)

![https://img.icons8.com/ios-glyphs/2x/trash.png](https://img.icons8.com/ios-glyphs/2x/trash.png)

when the user clicks that button, an alert will be shown to confirm the changes, if the user confirms the added favorites will be deleted with the list.

### Adding a place to a favorite list:

When the user search places to book and finds an interesting place he can add it to a list clicking on the heart, this action open a modal.

![image](https://user-images.githubusercontent.com/43361414/157812879-0437a2e0-3ff4-493c-b55e-1cdde847336c.png)

The user can add the favorite to an existing list or will have the option to create a a new list, if the user click on this, a modal to create a new list will be shown to the user. 

By default any user begins with a list called "Mis Favoritos”, this list is a speed option to save interested places without need to create a new list or select a previous created.
After the user set where he like to add the place (in a new list, the default list, or other created list) a confirmation message its showed to confirm the action its completed an the user can continue using the platform.

![image](https://user-images.githubusercontent.com/43361414/157812913-4a18e1ab-7c9a-4dc9-afa9-9c51f36dc4ec.png)

# Drawbacks

Why should we *not* do this? Please consider:

- Implementation cost, both in term of code size and complexity.
- Whether the proposed feature can be implemented in user space.
- The impact on teaching people React.
- Integration of this feature with other existing and planned features.
- Cost of migrating existing React applications (is it a breaking change?).

There are trade offs to choosing any path. Attempt to identify them here.

# Adoption strategy

In this case we suggest make this function as a module what we can turn on/off if it's required. The module contains the heart icon, the alerts and the create list, lists, and list content view.
Any of this functions are related with the user id and place id, we can create a particular table to related a user with their lists and the lists with their places. All the rest of the data (place name, descriptions, photos, url, etc) we can take from the already existing data in the DB.
This feature only need can read, write or update the table what relate the users lists and places, read the place data by id and not need make any other change in the data.

# How we teach this

- This its a regular and frequently used function. Terms as Favorite list, or wishes list are the most common in any ecommerce platform or similar.
- This idea its a complement and continuation of a full idea of the platform. The functions to enable any user to preselect the contents most relevance to there and organize there in a lists its a basic functionality today.
- The acceptance of these functions mean we need make a extra table in the db and a new user flow. This action need appears on the documentation of the product.
- To the new devs on the project this is a part of the product related directly with the user and with some independence of the rest of the data.
- To the old devs on the project this is a part of the product related directly with the user and with some independence of the rest of the data.

## Technical skills

- Javascript
- React Js
- Css
- Next.JS

# Unresolved questions

- [ ]  Users can share their list to others?
- [ ]  The lists take a taxonomy to filter or similar?
- [ ]  The owner of a place have any notification when their place is posted in any user list?
- [ ]  The favorite can be deprecated or have an end time, the favorite will disappear after this?
- [ ]  if owner user deleted a place there disappeared to the list? The users with this place as their favorite take any notification about this?
