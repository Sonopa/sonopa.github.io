---
layout: page
---

After all the waiting of the last couple of weeks, this week we got a lot done and finally got some answers from the mentors! Juho, Qian and Henrik made tests
for the part of the eager loading feature that we have ready. Juho found a spot with a fixme tag in a Rails test, fixed it and got it merged into rails. Henrik
also found an issue that he fixed and got merged into rails. I worked on an issue about implementing a new rake dev:cache task into rails that would make
toggling development mode caching on and off easier. I got it done and made a pull request, but it hasn't been merged yet because some of the rails contributors are not sure if it's the right way to implement it (the way I did it was proposed by dhh, the creator of rails), so now I'm just waiting for them to figure it out.

On Thursday Eileen answered our help request email, but she wasn't able to help since she wasn't familiar with our task. Luckily our email exchange with
Eileen got the attention of Matthew, who answered us on Friday. His answer had the information we need to continue, so next week we will have a lot to do.
Since we are now half way through the course, in this weeks post I shall recap what we've done so far.

### Recap

We started the course by learning about Rails and how it's built for the first couple of weeks. At the code sprint we were given a task to implement eager
loading of view templates. After the code sprint we started working on the task and made progress for the first week and a half. Then we got a little
bit stuck due to a lack of feedback and help. Our problems were getting access to some attributes in the place we needed them and understanding the compilation
part of our feature (if/how/what we need to compile). We were stuck in that phase for a week or two, but meanwhile we managed to do other stuff as well, like
the tests and the couple of issues I mentioned earlier. Juhos was a [bug fix](https://github.com/rails/rails/pull/19074), Henriks issue was also a [bug
fix](https://github.com/rails/rails/pull/19076) and mine was a new [feature](https://github.com/rails/rails/pull/19091). While we were working on those issues, Qian was working on tests. This is where we are right now. Ready to start finishing our current task.

### The second half

Since we now have what we need to finish our task, that will be our priority probably at least for the first couple of weeks of the second half of the course.
After that I hope we will get another feature to implement that's as interesting as the current one. I'm not sure how likely that is though, they probably
don't have that many smallish features waiting to be implemented. If we don't get another one, I guess the options will be to fix issues or to try to come up
with a feature to implement ourselves, which could be fun but challenging. In any case, I still hope to learn more about the internals of Ruby on Rails so
I can continue to contribute even after the course is over.
