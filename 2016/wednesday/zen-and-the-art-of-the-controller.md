# Zen and the Art of the Controller

Caused by a misunderstanding of what resource an action is actually dealing with.

### Example: Social Ad SaaS Tool
- Ads need standard CRUD
  - **7 standard actions**
- Ads can be paused, activated or archived
  - Pause
  - Activate
  - Archive
- Users should be able to see ad performance
  - Preview?
  - Stats?
- What about statistics?
  - Audience
  - Dashboard

> Now we're up to **14 actions**

What to do about it? Break it up.

Maybe some of these don't actually deal with ads.

### Other possible types of controllers
1. Static or View Layer controllers
  - `AdPartialsController` - this could be just for views of a model.
2. Composite controllers
  - `AdJobsController` - a controller that works with ephermeral resources like Sessions or Jobs. In this case, we are actually working with Jobs like pause and activate
3. Aggregate controllers
  - `AdStatisticsController` - this is a view of ads in the aggregate, not taking actions on an ad resource itself.

## Why should we do it?
1. Easier debugging
2. Onboarding new developers
3. Localized/domain changes
  - so that you can do `before_action` or `before_filter` without selecting or excluding specific actions
4. Easier to coordinate large teams working on the same code, fewer conflicts in files

## Conclusion
 - Look at what your actions are actually working on
 - Break up your controllers to keep them lean.
 - Make the unmodified scaffolded controller the most complicated controller you have. Break it up if it gets any more complicated.
