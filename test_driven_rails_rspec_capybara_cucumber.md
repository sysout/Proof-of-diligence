## rspec

### rubymine shortcut for jumping to/from a test to its test subject: ⇧⌘T
https://www.jetbrains.com/help/ruby/8.0/navigating-between-test-and-test-subject.html

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
