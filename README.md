# unit-analysis-json-schema
JSON Schema for algorithmic unit analysis

Encodes unit-analysis definitions based on the blog post
["Algorithmic Unit Analysis"](http://erikerlandson.github.io/blog/2019/05/03/algorithmic-unit-analysis/)

### examples
A unit analysis schema is an array of unit definitions.
The following example shows some `"base"` and `"derived"` unit definitions.
```json
[
  {"unit": "base", "name": "meter", "abbv": "m"},

  {"unit": "base", "name": "second", "abbv": "s"},

  {"unit": "derived", "name": "minute", "coef": 60, "expr": "second"},

  {"unit": "derived",
   "name": "liter", "abbv": "L",
   "coef": {"coef": "rational", "num": 1, "den": 1000},
   "expr": {"lhs": "meter", "op": "^", "rhs": 3}
  },

  {"unit": "derived",
   "name": "gravity", "abbv": "g",
   "coef": 9.8,
   "expr": {"lhs": "meter", "op": "/", "rhs": {"lhs": "second", "op": "^", "rhs": 2}}
  },

  {"unit": "derived", "name": "kilo", "coef": 1000, "expr": "unitless"}
]
```

Here is an Avro schema augmented with unit expressions:

```json
{
     "type": "record",
     "name": "demo_units",
     "fields": [
       { "name": "distance", "type": "number", "unit": "meter" },
       { "name": "velocity",
         "type": "number",
         "unit": {"lhs": "meter", "op": "/", "rhs": "second"} }
     ]
}
```
