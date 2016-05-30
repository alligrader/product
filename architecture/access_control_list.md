# Access Control List Background

An access control list is how websites tell whether or not a user has permission to perform an action. Actions are most commonly "create", "read", "update", or "delete", but other actions are possible too. A permission consists of two things: an action and a status. Having a permission for action X and status Y means "this user can do X when in state Y". The status element represents the fact that a given account can be in one of many different states. For example, a user who fails to pay his monthly bill might have the status of "defaulted", while a normal user may have the status of "active".

A user doesn't directly have permissions, but instead she has a list of roles. Each role has permissions which allow her to perform the specified actions. For example, user 1 might have the `teacher` role, which gives her all the permissions a teacher has. However, if that user is also writing the checks every month to Alligrader, than she will also have the `billing` role, which allows her to change her billing information.

# What I Need

I need help double checking the access control list I came up with. There's a lot of assumed knowledge about how I think the app is going to run built into this list, so I want to make sure we're all on the same page.

I've listed each of the roles below and included a list of permissions, ignoring the status for now.

- **Admin**: Represents someone with an unlocked account, i.e. an Alligrader founder    
    - Can do everything
   
- **Billing** : This role represents someone who's paying for a particular school or university. They're organization owners. They can...
    - add new billing information
    - view billing information (just like, last 4 digits of their card, we don't actually store any of this ourselves)
	- delete billing information
	- update billing information

	- invite teachers to their organization
	- kick teachers from their organization
	- view all classes in their organization

- **Teacher**: Teachers can...
	- invite students (add)
	- kick students   (remove)
	- view all students in their organization

	- create assignments
	- view assigments
	- edit assignments
    - destroy assigments

	- create grades for submissions
	- view submissions including grades, for all students in classes they created
	- edit submission grades including grades, for all students in classes they created
	- delete submission grades including grades, for all students in classes they created

	- create classes
	- view classes that they created
	- edit classes
	- delete classes
	
- **Student**: Students can...
	
	- create submissions
	- delete submissions
	- can view submissions including grades

	- view all classes that they are in
	- view assigments for classes they're in

- **TA**: TAs can...

	- apply grades to submissions
	- view submissions
	- view classes they are in
	- view all students in classes they share
	
# Feedback

Please let me know if I should add anything, modify anything, or left anything out. I'd love to do this one and get it done with rather than having to come back to it and modify it again and again.
	
