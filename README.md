# unit-analysis-json-schema
JSON Schema for algorithmic unit analysis

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
