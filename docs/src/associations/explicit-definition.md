# Explicit definition

You can define associations explicitly. This can be handy especially when
[overriding attributes](overriding-attributes.md).

```ruby
factory :post do
  # ...
  association :author
end
```
