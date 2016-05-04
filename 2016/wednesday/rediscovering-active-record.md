# Rediscovering Active Record
1. Introspection
  - ActiveRecord looks at the database schema and caches it
2. Casting
  - Each field is casted to an ActiveModel::Type::Value like date, text, integer, etc.
  - This handles serializing and deserializing between the database and ruby.
3. Queries
  - ActiveRecord will look for a cached query first
  - what the heck is Arel::Node?
  - It will create a statement if there isn't one already
4. Executing
  - Instantiate object(s) that the find method will return
  - Define the automatically generated attribute getter/setter methods for the model object
  - It tries to query for only what is necessary at the time
