# Ruby on Rails Questions

#### What is ActiveJob? When should we use it?

ActiveJob is responsible for declaring jobs (code scheduled to run at certain times) and works with a variety of queuing backends. These jobs can involve scheduled billing, email and cleanups. Rails by default will keep jobs in RAM, which means if the process crashes all outstanding jobs will be lost. A third party library can be used like Sidekiq, Resque, Delayed Job in order to make the job storage persistent. 

#### What is Asset Pipeline?
From Rails guide

> The asset pipeline provides a framework to concatenate and minify or compress JavaScript and CSS assets. It also adds the ability to write these assets in other languages and pre-processors such as CoffeeScript, Sass and ERB. It allows assets in your application to be automatically combined with assets from other gems. 

> The asset pipeline is implemented by the sprockets-rails gem, and is enabled by default. You can disable it while creating a new application by passing the --skip-sprockets option.

Concatenating assets reduces the number of requests a browser makes to render a web page, web pages are limited in the number of requests they can make in parallel so this can mean faster application loading. 

All javascript is concatenating into one master .js and all css into one master .css file. 
Fingerprinting is also used (where the filename is unique and based on its content) by sprockets as part of a process called cache busting, ensuring the user always has the most up to date version of the asset. 

#### Explain the difference between Page, Action, Fragment, Low-Level, SQL caching types.
From rails guide.

- Page caching: A Rails mechanism which allows the request for a generated page to be fulfilled by the webserver (i.e. Apache or NGINX) without having to go through the entire Rails stack. While this is super fast it can't be applied to every situation (such as pages that need authentication). Also, because the webserver is serving a file directly from the filesystem you will need to implement cache expiration.

- Action caching: Page Caching cannot be used for actions that have before filters - for example, pages that require authentication. This is where Action Caching comes in. Action Caching works like Page Caching except the incoming web request hits the Rails stack so that before filters can be run on it before the cache is served. This allows authentication and other restrictions to be run while still serving the result of the output from a cached copy. This has been replaced since rails 4. 

- Fragment Caching: Dynamic web applications usually build pages with a variety of components not all of which have the same caching characteristics. When different parts of the page need to be cached and expired separately you can use Fragment Caching.

Fragment Caching allows a fragment of view logic to be wrapped in a cache block and served out of the cache store when the next request comes in.

- Low-level caching: Sometimes you need to cache a particular value or query result instead of caching view fragments. Rails' caching mechanism works great for storing any kind of information.
The most efficient way to implement low-level caching is using the Rails.cache.fetch method. This method does both reading and writing to the cache. When passed only a single argument, the key is fetched and value from the cache is returned. If a block is passed, that block will be executed in the event of a cache miss. The return value of the block will be written to the cache under the given cache key, and that return value will be returned. In case of cache hit, the cached value will be returned without executing the block.

- SQL caching: Query caching is a Rails feature that caches the result set returned by each query. If Rails encounters the same query again for that request, it will use the cached result set as opposed to running the query against the database again. However, it's important to note that query caches are created at the start of an action and destroyed at the end of that action and thus persist only for the duration of the action


#### What is a Rails engine?

A rails engine allows you to wrap up a rails application in a way that makes it easy to share with other applications. 
