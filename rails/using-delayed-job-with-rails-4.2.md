# Using Delayed::Job with Rails 4.2

[Delayed::Job][dj] is a reliable way to manage tasks which need to be run
asynchronously, like processing large files or sending emails. Prior to Rails
4.2, the common pattern to deliver emails asynchronously with Delayed::Job was
by calling `.delay` prior to the method on the mailer:

```ruby
# synchronous
ScoreMailer.congratulate_user_for_high_score(user, high_score).deliver

# asynchronous
ScoreMailer.delay.congratulate_user_for_high_score(user, high_score)
```

In Rails 4.2, it becomes more natural with [ActiveJob]:

```ruby
# synchronous
ScoreMailer.congratulate_user_for_high_score(user, high_score).deliver_now

# asynchronous
ScoreMailer.congratulate_user_for_high_score(user, high_score).deliver_later
```

When upgrading Rails to 4.2 or introducing Delayed::Job on a 4.2 app, don't
forget to set the ActiveJob's queueing backend correctly when using
`#deliver_later`:

```ruby
# config/application.rb
module AppName
  class Application < Rails::Application
    # ...
    config.active_job.queue_adapter = :delayed_job
  end
end
```

[activejob]: http://guides.rubyonrails.org/active_job_basics.html
[dj]: https://github.com/collectiveidea/delayed_job
