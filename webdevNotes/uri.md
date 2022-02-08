createdAt: "2020-07-14T21:02:59.224Z"
updatedAt: "2020-07-31T16:11:21.544Z"
type: "MARKDOWN_NOTE"
folder: "b682d2d60df3a4241969"
title: "URI (Uniform Resource Indentifier)"
tags: [
  "uri"
]
content: '''
  # URI (Uniform Resource Indentifier)
  [Uniform Resource Identifier - Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Generic_syntax)
  ## Parts of URI
  ### scheme
  - Tells the client how to access the server.
  - Like: `http:`, `file:`, `mailto:`, ...
  - `:` goes after the scheme
  ### hostname
  - Tells the client which server to connect to.
  - Like: `//en.wikipedia.org`, `//localhost`, ...
  - `//` goes before the hostname
  - Not every URI has a hostname, mailto scheme for example doesn't have a hostname.
  
  ### path
  - Identifies a particular resource on the server.
  - If you  write your URI without path name the browser fills in the default path: `/`
  - the path: `/` is called the `root` (the root of the resources served by the server)
  
  ### fragment
  - `#` as in: https://en.wikipedia.org/wiki/Oxygen#Discovery
  - used to scroll an ID on the page
  - that part of the URI is not sent to the server
  
  ### query
  - `?` as in https://www.google.com/search?q=fish
  
  ### port number
  As IP addresses distinguish computers, port numbers distinguish programs on those computers.
  - default port for `http: 80`
  - default port for `https: 443`
  
  ## Connecting To a Server
  
  1. Determine Host Name from URI
  2. Get IP Address
  3. Connect to the right port number on that IP address
    
'''
linesHighlighted: [
  9
]
isStarred: false
isTrashed: false
