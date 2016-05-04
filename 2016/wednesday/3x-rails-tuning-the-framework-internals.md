# 3x Rails: Tuning the Framework Internals
A talk about speeding up the rails framework, not your application

## How do we measure speed?
`require 'benchmark/ips'`

## How can we make stuff faster?

### Is the Garbage Collector slow?
> Ruby is slow because Ruby GC is slow

`GC.stat`

The GC adds only about 10% overhead. You could stop it from running entirely, but that wouldn't do much to increase speed, and of course you'll run out of memory quick

### Is it slow because it isn't compiled?
> Ruby is slow because it's a scripting language

You can now opt-in to precompiling Ruby

### Profile to find what parts are slow
 - rb-lineprof
 - tracepoint

### Is ActionPack slow?
There is no slow middleware in the default stack

### Is ActionView slow?
Maybe we could speed up OptimizedResolver. Why not cache files read for views? (see more_optimized_resolver on github for this)
It's 18x faster :-P

#### Partials
Rendering Partials is slow, he is working on something that would just concatenate a partial if it is simple, kind of like PHP's `include 'other_view.php'`
`render_collection` could be parallelized: he tried, but it makes too many connections with ActiveRecord
`ljax_rails` will render partials through AJAX instead of serially on the server
The worst part is Encoding. But nobody writes a non-UTF8 view. So they should remove the code that handle encoding for ERB. He will propose this maybe for Rails 6
It is 1.5x faster, and also saves memory. Try `Hamlit` to get this now.

### Is ActiveRecord slow?
It builds so many Arel Objects. What if we direction compose an SQL statement, just like it was in ActiveRecord 1 and 2.
`Arenai` does this, less memory usage and object creation

Never call `model.present?`, it calls 85 methods
He suggested a patch, but it was turned down for a dumb reason of principle.

- `active-record-import`
- `bundle-squash`

### Is ActiveSupport slow?
`AS:TimeWithZone` is slow

## Conclusion
These is no one solution that will make every app faster
Rails is Omakase, but in some cases we want to customize it. 
