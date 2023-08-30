# README

This is a vanilla Rails app that demonstrates `ViewComponent` breaking `rails stats`.

Steps to reproduce this error:

1. `rails new error-demo`
2. `cd error-demo`
3. `bundle add view_component`
4. `rails stats`

This yields the result:

```
rails aborted!
TypeError: no implicit conversion of nil into String

Tasks: TOP => stats
(See full trace by running task with --trace)
```

After some digging, I found the issue stems from [this line](https://github.com/ViewComponent/view_component/blob/main/lib/view_component/rails/tasks/view_component.rake#L10).

At this point, `ViewComponent::Base.view_component_path` resolves to `nil`.