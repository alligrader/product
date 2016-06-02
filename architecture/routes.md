# Motivation

I want to write up our routing documentation using the API Blueprint. That way we have a verifiable, human readable document specifying exactly what the shape of our API is. Using the API Blueprint spec, we can auto-generate documentation for our API. We can also auto-generate integration tests, using a continuous integration tool or command line tool like `Dredd`. My life just gets way easier once we have integration tests in place, because that's ultimately how I'll know if the backend works. Integration tests are in essence The One Truthof backend functionality. Having them in a format that JJ and Alyssa can read (not Golang) is justa  bonus.

# How?

Before I write up the API Blueprint, which is actually a heavy amount of code for me to write, I want to make sure I have my resources correct. This is documentation even higher level than the API Blueprint. The API Blueprint specifies what the request headers are, what the request payload is, what the response schema is, and gives examples of sample responses that should be expected. Before I get into that level of detail, I just want to make sure that the resources I specify are actually doing what I expect them to do, and that I'm not missing out on anything important.

At the time of writing, I haven't completed architecting all of the resources, so there **will** be resources left out of this document at the time of pushing. I want you, the reader, to say "Hey Robbie, you forgot this resource!". While I know that there are things missing, I still want you to tell when you notice something missing. That's kind of the point.

Below I've listed each route and what it's purpose is. If you disagree with what it should do, or think I've missed something, please please let me know.

## About

0. The prefix `/api` exists before all routes. The reason is that these are routes that only return JSON, and thus should be considered "private" in that users should never be linking to them or manually pinging them. They should only be pinged by the SPA application. Note that `/invite-link/<token>` is the sole exception.

0. AUTH requires to the JWT request header `X-AUTH-TOKEN` passed along with each request.

# Routes:

- `POST /api/organizations`
    Create a new organization, and a new user with the role "organization admin". This user is the owner of the organization.
- `GET /api/organizations`
    Requires AUTH.
    This route returns a list of organizations that the logged in user is a member of.
- `GET /api/organizations/<id>`
    Requires AUTH.
     This route returns the public information about a particular organization.
- `GET /api/users/<id>`
    Requires AUTH.
    Get the public information for the user.
- `POST /api/users`
    This route is used to create a new user in conjunction with an invite link. The invite link is generated elsewhere (see `POST /classes/<id>/users` and `POST /organizations/<id>/teachers`). The link includes a SHA value that must be passed along as part of the request body (not invite links are the only place where I explicitly mention elements of the request body; everywhere else, more details are withheld).
- `POST /api/classes/<id>/users`
    AUTH required
    While `POST /api/users` represents making a new student for the first time from an invite link to a class, this route represents adding an existing student to a class.
- `POST /api/classes`
    AUTH required
    This route represents creating a new class. Only teachers and organization admins are allowed to add classes.
- `GET /api/classes/<id>`
    AUTH required
    This route returns the data for a class including references to assignments and announcement text.
- `POST /api/organizations/<id>/teachers`
    AUTH required
    This route is used to generate and send invites out to the teachers, enumerated in the request. The request must be sent by someone with the `organization admin` role.
- `POST /api/organizations/<id>/billing`
    AUTH required
    This route adds new billing information.
- `GET /api/organizations/<id>/billing`
-   AUTH required
-   This route gets billing information (only the information provided by our 3rd party privder, e.g. BrainTree, Stripe, not like their full card number or anything like that). User token must have the org admin role.
- `DEL /api/organizations/<id>/billing`
    AUTH required
    Deletes billing information. User token must have the org admin role. You cannot edit billing information.
- `DEL /api/users/<id>`
    AUTH required
    Deletes the user account, and removes it from all organization and classes. The user toke must have "self" role on the deleted ID.
- `DEL /api/organizations/<id>`
    AUTH required
    Deletes the organization, removing all classes in that organization. Does not delete students. I don't know what the fuck happens to students in a deleted organization. It's late at night. User token must have `org admin` role.
- `DEL /api/organizations/<id>/classes/<id>`
    AUTH required
    Deletes a class. Teacher must be a member of the class to be able to delete it.
- `GET /invite-link/<token>`
    This route represents a request to join a particular class. Since this request is going to come in from someone clicking an email or following a link, it's going to hit the server before React can get to it. Thus, I have to define some kind of response for it since it's touching the backend. I think we should return React in a certain state (if possible, idk how this works). This route should give the user an HTML page for joining a class. The user has the option to either **Sign In with an existing account** and **add the class to that account**, or to **Create a new account**.
