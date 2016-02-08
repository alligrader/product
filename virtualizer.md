# Motivation

Our architecture is very complicated. We have a backend, plus a front end that's served independently of the backend (except in production). Then there's a message bus and a worker that pulls down messages and spins off a Docker container. And there's a database.

If we're going to have a team of seven people working on this, a virtualization method could really help reduce bugs between platforms, as well as simplify the development process.

I want to use Otto to manage virtualized environments.
However, I'm worried Otto isn't ready. So, I've come up with a list of requirements necessary for us to be able to commit to using Otto in development.

If there's an alternative virtualizer to Otto (like Vagrant, for example) that meets the below requirements, it may be adviced that we use that instead.

# Must Have

- [ ] the ability to use VMWare instead of just Virtualbox (avoids the SendFile bug)
- [ ] access to the private IP address of other virtualized machines
- [ ] reasonable fast loading time

# Should Have
- [ ] concise specification of a machine, preferably in a single file
- [ ] the ability to use multiple kinds of images concurrently (Docker images, VMWare images, ...)
- [ ] OS and platform customization

# Nice to Have
