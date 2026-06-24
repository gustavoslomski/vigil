### Services

```
services/
  surveys/
    do_something.rb
    *.rb
```

```ruby
# services/surveys/do_something.rb

# frozen_string_literal: true

module Surveys
  class DoSomething
    def initilize(ids:)
      @ids = ids
    end

    def call
      @participants = Surveys::Participant.where...
    end
  end
end

# Surveys::DoSomething.new(ids: 123).call
```

### where the service is called?
[JOBS](./jobs.md)