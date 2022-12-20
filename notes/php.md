# PHP Notes
- [PHP Notes](#php-notes)
  - [Bypass filters](#bypass-filters)
    - [on parameters containing `_`](#on-parameters-containing-_)
  - [on parameters containing `[]` (arrays)](#on-parameters-containing--arrays)
  - [on php 7.4.11 and up the cookie names are no longer url-decoded](#on-php-7411-and-up-the-cookie-names-are-no-longer-url-decoded)

## Bypass filters
In many cases HTTP QUERY parameters are filtered on edge servers (such as nginx). The following is a small list of tricks that can be used under certain circumstances.

### on parameters containing `_`
In such cases where a parameter that is filtered contains  `_` (ie `test_param`) we may be able bypass the filter by replacing the `_` with a dot (`.`), eg `test.param`. This will be converted back to `_` by php (`test.param`=>`test_param`).

## on parameters containing `[]` (arrays)
In such cases where a parameter is filtered for specific array variables (eg `user[id]=test`), we may be able to bypass the filter by appending some junk at the end of our array variable.
This will be removed by PHP and will be converted back to its normal form (eg `user[id]random=test` => `user[id]random=test`)

## on php 7.4.11 and up the cookie names are no longer url-decoded
As of PHP 7.4.11, the names of incoming cookies are no longer url-decoded for security reasons.

So a cookie name like this: `%41%42%43` was passed as `ABC` to php before and now is getting passed as is.
