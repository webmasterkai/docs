---
layout: api-command 
language: Python
permalink: api/python/with_fields/
command: with_fields
github_doc: https://github.com/rethinkdb/docs/edit/master/2-query-language/api/python/transformations/with_fields.md
---

{% apibody %}
sequence.with_selectors([selector1, selector2...]) → stream
array.with_selectors([selector1, selector2...]) → array
{% endapibody %}

Takes a sequence of objects and a list of fields. If any objects in the sequence don't
have all of the specified fields, they're dropped from the sequence. The remaining
objects have the specified fields plucked out. (This is identical to `has_fields`
followed by `pluck` on a sequence.)

__Example:__ Get a list of heroes and their nemeses, excluding any heroes that lack one.

```py
r.table('marvel').with_fields('id', 'nemesis')
```

__Example:__ Get a list of heroes and their nemeses, excluding any heroes whose nemesis isn't in an evil organization.

```py
r.table('marvel').with_fields('id', {'nemesis' : {'evil_organization' : True}})
```


__Example:__ The nested syntax can quickly become overly verbose so there's a shorthand.

```py
r.table('marvel').with_fields('id', {'nemesis' : 'evil_organization'})
```
