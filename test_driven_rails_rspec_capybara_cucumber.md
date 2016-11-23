## rspec

### before, before(:all), before(:each)
before is equivalent to before :each, not before :all

### let(:variable_name)
let is lazy loaded and only load once

### working with transactions

http://pawelgoscicki.com/archives/2015/09/testing-database-transactions-explicitly-in-rspec/


https://www.relishapp.com/rspec/rspec-rails/docs/transactions

### profiling
```bash
rspec spec --fail-fast --profile
```

## factory girl
