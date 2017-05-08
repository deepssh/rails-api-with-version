# This is a simple rails versioned API example


We have covered the following in this example,

 * Simple Api
 * Version control
    We have used the contrains to run version in the api
 * Mime Type
    Using MIME types initialisers and getting the desired json response


```constraints
  # add this initializers.mime_types.rb
  class ApiConstraint
    attr_reader :version

    def initialize(options)
      @version = options.fetch(:version)
    end

    def matches?(request)
      request
        .headers
        .fetch(:accept)
        .include?("version=#{version}")
    end
  end
```
Using this helps to change the url to
````
  # before
  curl http://localhost:3000/articles.json
  # after
  curl -H "accept: application/json; version=2" http://localhost:3000/articles

  **version=2** has been added and the curl was simple
````

```Mime Type
# add this initializers.mime_types.rb
  Mime::Type.register 'application/vnd.articles+json', :articles_json
```

Using this helps to change the url to
````
  # before
  curl -H "accept: application/json; version=2" http://localhost:3000/articles
  # after
  curl -H "accept: application/vnd.articles+json; version=1" http://localhost:3000/articles

  **vnd.articles+json** has been added and **json** removed
````
[Read More](http://blog.steveklabnik.com/posts/2011-07-03-nobody-understands-rest-or-http#i_want_my_api_to_be_versioned)
