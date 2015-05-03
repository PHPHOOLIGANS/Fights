
One of the gripes I have, is with people that think Frontend/Backend is synonymous to Client-side/Server-side.

It is not.

It is perfectly acceptable to have Front-End logic happen on the Server:

                           System Boundry
                                 +
                                 |
                                 V
    +-------------------------+     +--------------+
    |        Front End        | +-> |   Back End   |
    +-------------------------+     +--------------+

    +----+     +--------------+     +--------------+
    | UI | +-> |     Logic    | +-> |  Application |
    +----+     +--------------+     +--------------+

    +--------------+     +-------------------------+
    |    Browser   | +-> |          Server         |
    +--------------+     +-------------------------+
    
                      Ʌ
                      |
                      +
                Server Boundry

The main reason why I have a gripe with this is that the front-end is just a delivery mechanism (exelently explained by Robert Martin at Ruby Midwest 2011
 http://www.youtube.com/watch?v=WpkDN78P884)
 
 If this delivery mechanism is incorporated in the application and I want to use another means of connecting to the user (like the command line) this means I now have to _first_ separate the original code before implementing another connector.
 
 -- EOF --
 
 

