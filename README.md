# Lets do some hstore.

## Why?

We all get it.  Sometimes the relational thing is a drag.  You want to use documents at times.

But maybe jumping to Mongo or Couch isn't necessarily the best choice in your situation.

What if you could use your battle-tested postgres box for this?

## Oh. Oh!  How do we do it?

First, we assume you are running postgres 9.1.3 (because that is what I'm using).

Enable the extension:

```sql
CREATE EXTENSION hstore;
```

Create a table:

```sql
CREATE TABLE reports (id serial PRIMARY KEY, data hstore);
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
# => [{:id=>1, :token=>nil, :data=>{"foo"=>"bar"}}]
```
