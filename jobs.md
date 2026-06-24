### Jobs

```
jobs/
  management/
    metrics/
      do_something_job.rb
      *.rb
```

```ruby
# jobs/management/metrics/do_something_job.rb

# frozen_string_literal: true

class Management::Metrics::DoSomethingJob < ApplicationJob
  queue_as :management

  def perform
    ids = ...
    Surveys::DoSomething.new(ids: ids).call
  end
end
```

### sidekiq-cron

```yml
Management::Metrics::DoSomething:
  cron: ...
  class: ...
  status: enabled
  ...
```