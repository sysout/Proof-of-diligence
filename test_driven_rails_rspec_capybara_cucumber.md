## rspec

### before, before(:all), before(:each)
before is equivalent to before :each, not before :all

### let(:variable_name)
let is lazy loaded and only load once

### working with transactions

http://pawelgoscicki.com/archives/2015/09/testing-database-transactions-explicitly-in-rspec/


https://www.relishapp.com/rspec/rspec-rails/docs/transactions

### stub

```
allow(controller).to receive(:current_user) { user }
```
Some contradictory posts:
https://github.com/plataformatec/devise/wiki/How-To:-Stub-authentication-in-controller-specs
http://johnnyji.me/rspec/2015/06/18/stubbing-controller-instance-methods-in-rspec.html

### strong params
https://makandracards.com/makandra/27527-rails-3-mass-assignment-protection-and-create_with

## factory girl
