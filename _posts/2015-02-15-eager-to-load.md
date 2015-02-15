---
layout: page
---

This week was not as productive for me as I'd hoped due to the fact that I got sick in the middle of the week. I stayed home on wednesday, thursday and friday and couldn't get that much work done. This led me to fall a bit out of the loop on how the other team members did the things they did, so I need to catch up on that next week. But it's not all bad. I think I made some progress in understanding how the parts of Rails that we need to work with are built, which brings me to this weeks topic, the feature we are implementing into Rails and our progress with it. 

### Eager loading

The task we got from Aaron Patterson at the code sprint was to implement an option to eager load view templates in production mode of Rails. Currently Rails compiles and caches a view template only when the first request for that particular view is made, which is called lazy loading. What we need to do is to cache all view templates when the server is started even if they are not necessarily needed, which is eager loading. This will make server start up a bit slower and might cause some unnecessary loading, but page requests will become faster. We don't want to implement this option for development mode as the views get changed and the server gets restarted a lot, so it would just slow things down. 

### Progress

At this point we have mostly figured out where and what the classes/methods related to view templates and their caching are. We have started the implementation of the feature and I'd estimate we are about 1/3 done, assuming most of what we have done so far is what they want and the correct way of doing it. What has consumed a lot of our time this week has been finding out the location where our code needs to go and how to get access to the right cache and the necessary attributes for finding and caching the view templates from that location on server startup. Our method currently looks like this (this is not all our code, only the main method).

    def cache_templates
        partial = false
        locals = []

        prefixes.each do |prefix|
            path_names(prefix).each do |name|
                locales.each do |locale|
                    pieces = name.split('.')
                    details, key = details_and_key(locale, name, pieces)
                    @controller._view_paths.find_all(pieces.first, prefix, partial, details, key, locals)
                end
            end
        end
    end

This method is called in an initializer (initializers are run on server startup) when an ActionController::Base class has been loaded. From this ActionController (@controller) we can get an instance of a PathSet class (called _view_paths here), which is responsible for storing and accessing view paths. PathSet has a method called find_all that looks for the templates with the given parameters and caches them if they are not yet found in the cache. From the attributes needed for find_all we still lack partial and locals, but finding those shouldn't take too much time. After that we need to find out how to compile the template, as I don't think our code does that just yet. We also need to make sure this feature can be turned off and that it is only used in production mode. And finally we need to test the feature, which I think the other team members already started a bit on friday as I saw a couple of testing related commits. So still at least a couple of weeks of work left.




