### Database configuration

```yml

development:
	primary:
		<<: *default
		database: name_development
		host: postgres
		passoword: postgres
	surveys:
		<<: *default
		database: surveys_development
		host: postgres
		passoword: postgres
		migrations_paths: db/surveys_migrate

test:
	primary:
		<<: *default
		database: name_test
		host: postgres
		passoword: postgres
	surveys:
		<<: *default
		database: surveys_test
		host: postgres
		passoword: postgres
		migrations_paths: db/surveys_migrate

production:
	primary:
		<<: *default
		database: name_production
	surveys:
		adapter: postgresql
		encoding: unicode
		database: surveys_production
		host: <%= ENV['SURVEYS_DB_HOST'] %>
		port: <%= ENV['SURVEYS_DB_PORT'] %>
		username: <%= ENV['SURVEYS_DB_USERNAME'] %>
		password: <%= ENV['SURVEYS_DB_PASSWORD'] %>
		migrations_paths: db/surveys_migrate
		replica: true
```

### Replicate schemas


```
db/
	schema.rb
	surveys_schema.rb
```

### Use Rails tasks to create it in local


```
// you can use rails --t to show all tasks
rails db:create
rails db:schema:load:surveys
```

### How to use it in models?
[MODELS](./models.md)