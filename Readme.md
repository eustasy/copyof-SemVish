SemVish [![License](http://www.wtfpl.net/wp-content/uploads/2012/12/wtfpl-badge-1.png)](http://www.wtfpl.net/)
===========

A versioning interpretter that can process multiple versioning schemes such as

- [SemVer](semver.org)
- `<Max>-<Min>`
- `<Max>-<Min>-<release>`
- `<Max>`
- `<Max>-<release>`
- `<release>`

Passes [843 tests](http://snag.gy/ENBzm.jpg) (mostly from node-semver)

### Motivation

[jsDelivr](http://jsdelivr.com) [needed a multi version comparitor scheme](https://github.com/jsdelivr/libgrabber/issues/24)

# API

Borrows directly from [`node-semver`'s](https://github.com/npm/node-semver) API

* `clean` process a SemVer-ish string to a SemVer compliant string

```js
clean("1.2") // => 1.2.0
clean("1.2.0") // => 1.2.0
clean("1.2.0-beta1") // => 1.2.0-beta1
clean("1.2.0beta1") // => 1.2.0-beta1
clean("1.2-alpha1") // => 1.2.0-alpha1
clean("1.2alpha1") // => 1.2.0-alpha1
clean("1") // => 1.0.0
clean("1-rc1") // => 1.0.0-rc1
clean("1rc1") // => 1.0.0-rc1
```

* `valid` is some string semverish?

* `gt(v1, v2)`: `v1 > v2`
* `gte(v1, v2)`: `v1 >= v2`
* `lt(v1, v2)`: `v1 < v2`
* `lte(v1, v2)`: `v1 <= v2`
* `eq(v1, v2)`: `v1 == v2` This is true if they're logically equivalent,
  even if they're not the exact same string.  You already know how to
  compare strings.
* `neq(v1, v2)`: `v1 != v2` The opposite of `eq`.
* `cmp(v1, comparator, v2)`: Pass in a comparison string, and it'll call
  the corresponding function above.  `"==="` and `"!=="` do simple
  string comparison, but are included for completeness.  Throws if an
  invalid comparison string is provided.
* `compare(v1, v2)`: Return `0` if `v1 == v2`, or `1` if `v1` is greater, or `-1` if
  `v2` is greater.  Sorts in ascending order if passed to `Array.sort()`.
* `rcompare(v1, v2)`: The reverse of compare.  Sorts an array of versions
  in descending order when passed to `Array.sort()`.