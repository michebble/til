# Print SQL query

When composing an active record query, `.to_sql` can be used show the generated query.
```ruby
User.where(email: 'foo@example.com').to_sql
=> "SELECT \"users\".* FROM \"users\" WHERE \"users\".\"email\" = 'foo@example.com'"
```
However the output contains quotation marks escaped with backslashes. If we want to use the SQL query directly, we need to remove the backslashes. 
This can be done using `puts`
```ruby
puts User.where(email: 'foo@example.com').to_sql
SELECT "users".* FROM "users" WHERE "users"."email" = 'foo@example.com'
=> nil

```
