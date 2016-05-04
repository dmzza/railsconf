# Multi-table full-text-search with Postgres

The most simple way is to use ILIKE in SQL

If you create a VIEW in Postgres, you can create a custom model class for it and access it just like any other model.

You can create VIEW's in migrations

Use the Scenic gem to put those VIEW's into your schema.rb

Use Textacular for full-text-search of all fields in a model (which could be a VIEW for multiple tables)
