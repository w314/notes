createdAt: "2020-07-31T16:16:50.684Z"
updatedAt: "2020-08-05T21:37:50.783Z"
type: "MARKDOWN_NOTE"
folder: "b682d2d60df3a4241969"
title: "HTTP"
tags: [
  "http"
]
content: '''
  # HTTP
  
  Starting a python http webserver with `python -um http.server 8000` under any directory will serve up the content of that direcory if you access `localhost:8000` in your browser.
  
  ## HTTP Requests
  
  ### GET Request
  `GET /my_directory/my_file.txt HTTP1.1`
  - `GET` is the **method** or **HTTP verb**
  - `/my_directory/my_file.txt` is the **path** of the resource being requested
  - `HTTP1.1` is the **protocol** of the request
  
  
  ## HTTP Response
  
  ### HTTP Response Headers
  - Starts with keyword followed by : and value:
  `Conent-type: text/html; charset=utf-8`
  - Ends with a blank line
  #### Status Line
  `HTTP/1.1 200 OK`
  or
  `HTTP/1.1 301 Moved Permanently`
  ##### Status Codes
  - `1xx` - **Informational** the request is in progress or there is an other step to take
  - `2xx` - **Success** servers is sending the data the client asked for
  - `3xx` - **Redirection** different codes will refer to permanent or temporary redirection. A `Location` header usually contains the updated URI. Browsers automatically follow redirects.
  - `4xx` - **Client Error** the server didn't understand the client's request, or can't or won't fill it. Different codes tell if it was a bad URI, or permission problem or other sort of error
  - `5xx` - **Server Error** somthing went wrong on the server side
  
  ### HTTP Respons Body
  - Headers, blank line, after blank line it's the response body
  - In case of error, the error message shows up in the response body
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
