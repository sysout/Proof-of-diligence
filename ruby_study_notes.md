## class instance variable
http://www.railstips.org/blog/archives/2006/11/18/class-and-instance-variables-in-ruby/


## private and protected methods
If a method is private in Ruby, then it cannot be called by an explicit receiver (object). It can only be call implicitly. It can be called implicitly by the class in which it has been described in as well as by the subclasses of this class.

If a method is protected in Ruby, then it can be called implicitly by both the defining class and its subclasses. Additionally they can also be called by an explicit receiver as long as the receiver is self or of same class as that of self

http://stackoverflow.com/questions/3534449/why-does-ruby-have-both-private-and-protected-methods


## block
http://mixandgo.com/blog/mastering-ruby-blocks-in-less-than-5-minutes

## update gem
```
gem list '^rails$' --remote --all
bundle update rails
```
