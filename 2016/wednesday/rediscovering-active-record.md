# Rediscovering Active Record
1. Introspection
  - ActiveRecord looks at the database schema and caches it
2. Casting
  - Each field is casted to an *ActiveModel::Type::Value* like date, text, integer, etc.
  - This handles serializing and deserializing between the database and ruby.
3. Queries
  - ActiveRecord will look for a cached Arel::Node tree, or create one from scratch
  - *Arel::Node* is ActiveRecord's abstract representation of SQL (or other kinds) queries. These are expensive to create
  - If a cache is found, it will only have to turn that Arel::Node tree into a SQL statement, which is cheap.
4. Executing
  - Instantiate object(s) that the find method will return
  - Define the automatically generated attribute getter/setter methods for the model object
  - It tries to query for only what is necessary at the time
