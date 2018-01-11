# sinatra study notes

## Setup your debug environment
```ruby
group :development do
  gem 'racksh'
  gem 'awesome_print'
  gem 'pry'
end
```
You can use console debugger like this https://github.com/hlee/sinatra_debugger_example, but I prefer rubymine.
To fake some requests are easy using racksh
```
pry> $rack.get '/'
```

## Call your sinatra app instance methods
According to http://stackoverflow.com/questions/12072865/calling-a-sinatra-app-instance-method-from-testcase
Sinatra aliases the new method to new!, so
```
pry> app=MyApp.new!
```

## YAML file support inheritance!
It's always good to have the flexbility to config your app. So add some inheritance in your app.
```ymal
database: &default
  server:
    ip: 192.168.1.5
    port: 2000
  db_name: test
  user: 
    name: root
    password: root

foo_database:
  <<: *default
  server:
    port: 2001
  db_name: foo
  user:
    password: foo_root
```
