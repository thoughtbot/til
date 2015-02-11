# Binding to 0.0.0.0 in Rails

On OS X, [boot2docker] is an installable VM host to run Docker locally (OS X
doesn't natively support Linux Containers). In combination with [fig], it's
pretty straightforward to get a Rails application running on [Docker].

[boot2docker]: http://boot2docker.io/
[fig]: http://www.fig.sh/
[docker]: https://www.docker.com/

To access the application, you'll visit `$(boot2docker ip):3000` (or
whatever port your Rails application is running on) and things should work
fine. However, I'd recently tried setting up Docker in a Rails app that was
running WEBrick and wasn't able to access the application at all when running
`rails server`. I'd previously used [Thin] (`thin start`) and hadn't run into
this problem.

[thin]: http://code.macournoyer.com/thin/

Trevor, one of my coworkers, pointed out the `--binding` flag for `rails
server`, which needs to be set in order for the server to accept requests from
any network interface: `rails server --binding 0.0.0.0 --port 3000`. Due to
how boot2docker/VirtualBox work with network interfaces, binding to 0.0.0.0
when running the server works, whereas binding to localhost (127.0.0.1) does
not.

For security reasons, be careful when binding to 0.0.0.0; anyone with
your network IP address and port of the Rails app could interact with the app
(say, over wi-fi at a coffee shop).
