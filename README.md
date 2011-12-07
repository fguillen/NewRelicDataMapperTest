# NewRelic DataMapper test

## Setup

    git clone NewRelicDataMapperTest git://github.com/fguillen/NewRelicDataMapperTest.git
    cd NewRelicDataMapperTest
    bundle install
    rake db:setup
    script/rails server

## Issue

Normally calling to `/people` show in the log something like this:

    Started GET "/people" for 127.0.0.1 at 2011-12-07 15:30:12 +0100
      Processing by PeopleController#index as HTML
      SQL (0.496ms)  SELECT "id", "name" FROM "people" ORDER BY "id"
    Rendered people/index.html.erb within layouts/application (15.7ms)
    Completed 200 OK in 60ms (Views: 58.7ms | Models: 0.496ms)
    
But if we turn `monitor_mode: true` in `newrelic.yml` we obtain this log in the same request:

    Started GET "/people" for 127.0.0.1 at 2011-12-07 15:32:42 +0100
      Processing by PeopleController#index as HTML
    Rendered people/index.html.erb within layouts/application (17.1ms)
    Completed 200 OK in 61ms (Views: 60.2ms | Models: 0.000ms)

See that I miss the **SQL** log and also the **Models** benchmark.
