
# Rack Questions
#### What is Rack?
The Rack interface sits between our chosen web servers and Ruby apps to give us complete flexibility in switching between what technologies we want to use in our stack.

Benefits of Rack:

— Easily switch web servers

— Easily switch Ruby frameworks

#### Explain the Rack application interface.

From Wikipedia -> By wrapping HTTP requests and responses it unifies the API for web servers, web frameworks, and software in between (called middleware) into a single method call.

#### Write a simple Rack application.

The below link covers how to write a simple rack application. 
https://www.leighhalliday.com/what-is-rack

A Rack application is any object that responds to the call method. The call method is passed an env variable, and is expected to respond with an array that consists of 3 items. - HTTP status code(200, 400, etc...) - A Hash of headers - The body of the response... an object that responds to each(an Array for example)

Here is an example of a simple Rack application:
```
# config.ru
require 'rack'

class HelloApp
  def self.call(env)
    [200, {'Content-Type' => 'text/html'}, ["Hello there."]]
  end
end

run HelloApp
```

#### How does Rack middleware works?

Middleware in Rack is something that allows you to chain a series of calls together, which can modify or halt request data before reaching the ultimate end of the Rack application.

We can use middleware to add headers to the HTTP response (how long the request took to process, how many more calls before the person is rate-limited), we can modify the body of the response (replacing images with another image, injecting something into our HTML), etc…

In the Rack GitHub repository there is a great list of available middleware for you to use. They cover everything from rate limiting to injecting data into your HTML response (ie. a Google Analytics tag or information on how long the request took).




