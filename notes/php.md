# PHP Notes
- [PHP Notes](#php-notes)
  - [Bypass filters](#bypass-filters)
    - [on parameters containing `_`](#on-parameters-containing-_)
  - [on parameters containing `[]` (arrays)](#on-parameters-containing--arrays)

## Bypass filters
In many cases HTTP QUERY parameters are filtered on edge servers (such as nginx). The following is a small list of tricks that can be used under certain circumstances.

### on parameters containing `_`
In such cases where a parameter that is filtered contains  `_` (ie `test_param`) we may be able bypass the filter by replacing the `_` with a dot (`.`), eg `test.param`. This will be converted back to `_` by php (`test.param`=>`test_param`).

## on parameters containing `[]` (arrays)
In such cases where a parameter is filtered for specific array variables (eg `user[id]=test`), we may be able to bypass the filter by appending some junk at the end of our array variable.
This will be removed by PHP and will be converted back to its normal form (eg `user[id]random=test` => `user[id]random=test`)
