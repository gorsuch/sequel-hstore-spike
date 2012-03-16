Lets do some hstore.

First, we assume you are running postgres 9.1.3 (because that is what I'm using).

Enable the extension:

```sql
CREATE EXTENSION hstore;
```

Create a table:

```sql
CREATE TABLE reports (id serial PRIMARY KEY, token varchar, data hstore);
```

Bundle:

```bash
bundle install
```

Open up your irb session:

```bash
bundle exec irb -r sequel -r sequel/extensions/pg_hstore
```

Connect to a database:

```ruby
DB = Sequel.connect('postgres://localhost/mydb')
```

Insert some hstore data:

```ruby
DB[:reports].insert(data: { foo: 'bar' }.hstore)
```

Fetch your data:

```ruby
DB[:reports].all
```
