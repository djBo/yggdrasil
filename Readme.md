# A Journey into Minimal.db

With the LambdaMOO server comes a tiny database called *minimal.db*. It is just enough to boot-strap a new core. On closer inspection, it also becomes clear that the initial structure doesn't match LambdaCore as their Wizard is actually object #2 and not #3.

Let's take a crack at it anyways, and see where it might lead. The remainder of the document expects you to setup your own LambdaMOO server using the minimal.db as a starting point. It's also advised to do this locally, and wait with exposing your new MOO to the outside world until player management and `do_login_command` has been properly implemented.

1. [Bootstrapping](docs/01.%20Bootstrap.md)
2. [Server Options](docs/02.%20Server%20Options.md)

[LambdaMOO-1.8.1.tar.gz](http://ftp.lambda.moo.mud.org/pub/MOO/LambdaMOO-1.8.1.tar.gz)  
[LambdaCore-latest.db](http://ftp.lambda.moo.mud.org/pub/MOO/LambdaCore-latest.db)  
Programmers Manual [large](http://ftp.lambda.moo.mud.org/pub/MOO/ProgrammersManual.html) [small](http://ftp.lambda.moo.mud.org/pub/MOO/html/ProgrammersManual_toc.html)
