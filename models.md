### Models

```
models/
  application_record.rb
  task.rb
  *.rb
  surveys/
    survey_application_record.rb
    participant.rb
    *.rb
```

```ruby
# models/surveys/survey_application_record.rb

# frozen_string_literal: true

module Surveys
  class SurveyApplicationRecord < ApplicationRecord
    self.abstract_class = true

    connects_to database: { writing: :surveys, reading: :surveys }

    # Rails call this method internaly
    # Prevents writes in staging/production even if replica: true is not set
    def readonly?
        readonly_environment?
    end

    private

    def readonly_environment?
      %w[staging production].include? Rails.env.to_s
    end
  end
end
```

```ruby
# models/surveys/participant.rb

# frozen_string_literal: true

module Surveys
  class Participant < SurveyApplicationRecord
  end
end
```

### How to use it in services
[SERVICES](./services.md)