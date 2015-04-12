---
layout: page
---

Last week was short due to us having the easter break, we only worked from Monday to Wednesday. We did make progress in those three days. We managed to fix the tests, so a large part of the locals problem is now fixed. Hopefully we will have it fully working within the next few days.

The easter vacation was a welcome break, and I spent most of it just slacking off. We also had a 2 day clojure hackathon with our Ruby on Rails team, although in the end the clojure coding part was quite short. I'm a bit sad the vacation is over now, but on the bright side it's only a month to go until summer vacation.

Today I will write a little bit about refactoring.

###Refactoring

As I have said earlier, Ruby on Rails does not accept pull requests that are just refactoring. However, refactoring is an important part of a development process, and Ruby on Rails also has to do it sometimes. Refactoring in Rails is usually combined with the implementation of a new feature, since sometimes those require that some part of Rails works in a different way. When these kind changes are done, Rails also gets its refactoring. Changes that improve performance are also ones that usually include refactoring.

An example of refactoring that we did for our feature (though it was us refactoring our own code, not someone elses) is [this file](https://github.com/nygrenh/rails/blob/8f6080b23f4c107e9d2aec4c868527a6b650c24c/actionview/lib/action_view/template_eager_loader.rb). The result is [here](https://github.com/nygrenh/rails/blob/30e9b8109115d68b88a0ef4c91a3bd67990138b4/actionview/lib/action_view/template_eager_loader.rb) and it's a easier to read than the original. In the original this was the main method that does everything.

    def eager_load
      prefixes.each do |prefix|
        path_names(prefix).each do |name|
          locales.each do |locale|
            pieces = name.split('.')
            details, key = details_and_key(locale, name, pieces)
            action = pieces.first
            partial, locals = partial_and_locals(action)
            action = action[1..-1] if action[0] == '_'
            @resolver.find_all(action, prefix, partial, details, key, locals)
          end
        end
      end
    end

Not very clear what it does, is it? In the refactored version the main method is

    def eager_load
      each_template(&:compile!)
    end

And the each_template method is like this:

    def each_template(&block)
      prefixes.each do |prefix|
        path_names(prefix).each do |name|
          locales.each do |locale|
            details, key, action, partial, locals = set_template_parameters(locale, name)
            locals.each do |locals_array|
              @resolver.find_all(action, prefix, partial, details, key, locals_array).each(&block)
            end
          end
        end
      end
    end

Now you immediately see that the feature takes each template and compiles them. And in the each_template method you can clearly see thanks to better naming of methods that first the template parameters are set, and then a template with those parameters is being searched.

So, refactoring is obviously often useful, but it can have negative effects as well. Otherwise Rails would allow refactoring pull requests, right? The danger with refactoring is that you can break something accidentally, and that is why you need tests. Having tests makes refactoring easier by letting you know when you've done something wrong and if your tests are well done, they also tell you where the mistake is. Fortunately when we refactored our feature we already had a lot of tests ready. It made things a lot easier.
