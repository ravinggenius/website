---
created_at: 2012-10-09 23:10:23 UTC
title: Triangle Ruby Brigade 2012 October
---

## Metaprogramming Ruby

Presented by Joseph Jaber and Michael Stalker

### Announcements

* http://railsrumble.com/


### What metaprogramming is

* "Metaprogramming is writing cod that manipulates language constructs at runtime"
* "[Much] of the metaprogramming I see is either wrong or has an equivalent that's less confusing" - Gregory Brown, Ruby Rogues podcast


### Why?

* Understand other people's code
* Solving more difficult problems
* Level up as a programmer
* Debugging


### Use Cases

#### Dynamic methods
  * `method_missing(missing_method, *args)` (hackish)
  * `define_method(method_name, &block)`
  * `send(method, *args)`
  * Use `<<` to define class-level methods
      class Person
        class << self
          # in the meta-class!
          def whatever
          end
        end
      end
      # Person.whatever

#### Patterns
  * Open class
    * problem: need to modify a class
    * solution: reopen the class, directly or via including a namespaced module
      * module shows up in Class.ancestors
    * don't overwrite methods that already exists
    * don't overwrite inherited methods (uninitentionally)
    * don't modify too many core library classes
  * Method missing
    * if Ruby cannot find a method, it researches the class heirarchy for method_missing
    * Kernel#method_missing raises NoMethodError
    * call `super` if you cannot handle the missing method
    * debugging can be difficult
    * a class higher up in the ancestor chain could define a method you want to catch with method_missing
  * Blank slate
    * remove all instance methods from inherited classes (`undef_method` or inherit from `BasicObject`)
  * Around alias
    * modify existing methods
    * `alias`, or better, `alias_method`
      * `class Whatever; alias_method :old_sentenceize, :sentenceize; def sentenceize; # stuffs... old_sentenceize; # more stuffs... end; end`
    * you could break stuff
    * cannot use `alias_method` more than once per method
  * Include and extend
    * poor implementation example: paper_trail


### Last Thoughts

* Comment your metaprogrammed code
* Carefully weigh options before resorting to metaprogramming
* Can be difficult to debug
