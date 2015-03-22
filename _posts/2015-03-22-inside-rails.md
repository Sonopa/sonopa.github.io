---
layout: page
---

Week 10 was a quiet week. Things are pretty much the same as at the end of last week. We made some progress on the locals issue, but the feature is still not merged. Matthew said that non trivial pull requests could take a while to be merged, so I guess we just need to wait. We haven't heard anything about Matthews and Aarons progress on the locals issue, so I'm guessing it's up to us to try and make it work somehow. The issue is quite complex, so progress is slower than usual. Matthew wrote the ideas he had about the locals and how to implement them last week, so we are now trying to do what he proposed. It involves stuff like looking at Ruby machine code and figuring things out from that. At first when I read Matthews ideas I thought that it may be a bit too hard a problem for us, but now that we have looked at it a bit, I think it may be possible. But it won't be easy.

In this post, I will give a brief overview of the overall architecture of the Ruby on Rails framework.

###Rails Internals

Like many other popular frameworks, Rails is organized using the MVC pattern. MVC divides an application into three layers: model, view and controller.

The model layer maps things to a table in a database and encapsulates business logic. The parts that handle the model layer in Rails are called Active Record and Active Model. Active Record connects classes to relational database tables and Active Model provides a known set of interfaces for usage in model classes.

The view layer is responsible for representing/presenting an applications data/resources. In Rails this is done by a package named Action View, which is a framework for handling view template lookup and rendering. This is the part on which we are mostly working on.

The controller layer is the part that takes HTTP requests and decides what to do with them. In Rails there are two packages that take care of this layer. The first one is Action Dispatch, which parses information about a web request, handles routing, and does processing related to HTTP. The second one is Action Controller, which loads and manipulates models and renders view templates to generate the HTTP response. So Action Dispatch routes a request to the right Action Controller, and the controller uses the model and view layers to handle the request.

Those are the packages that handle the MCV pattern in Rails. They are not all the packages though. Rails also has Active Support, Active Job, Action Mailer and Railties. Active Support is a collection of useful utility classes and standard library extensions for Rails. Active Job implements jobs into Rails, which makes it possible to divide work into smaller pieces and run them later and/or parallel. Action Mailer is a framework for making email services. And last but not least is Railties, the part that glues all the other frameworks together. All those packages mentioned are usable by themselves, and Ruby on Rails is just a collection of those smaller frameworks glued together by Railties.
