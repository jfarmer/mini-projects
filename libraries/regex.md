# Regex

We're going to write a miniature [regular expression parser](https://en.wikipedia.org/wiki/Regular_expression).  This is a fun project and a common interview question.

We will build it up by adding support for one regex construct at a time.

## Iterations

## v0.1 - any character `.`

Our first iteration will support the `.` character, which matches any character.  Let's call our regex function `isMatch`.  We want:

```javascript
isMatch('.ello', 'hello') === true
isMatch('.ello', 'jello') === true
isMatch('.ello', 'orange') === false

isMatch('.ello', 'hella') === false
isMatch('.ell.', 'hella') === true
```

## v0.2 - zero or more characters `*`

Now add support for the `*` character, which matches zero or more of the character that preceedes it.

```javascript
isMatch('a*', 'apple') === true
isMatch('a*', 'apples') === true

isMatch('a*s', 'apple') === false
isMatch('a*s', 'apples') === true

// Remember, * means "zero or more times"
isMatch('c*a*b', 'aab') === true

// .* should match anything, even the empty string
isMatch('.*', '') === true
isMatch('.*', 'anything') === true
```

## v0.2 - one or more characters `+`

Now add support for the `+` character, which means one or more of the character that preceeds it.

```javascript
// At least one 'c followed by at least one 'a' followed by a 'b'
isMatch('c+a+b', 'caab') === true
isMatch('c+a+b', 'ccaab') === true
isMatch('c+a+b', 'aab') === false

// .+ will match any non-empty string because + requires the preceeding character appear at least once
isMatch('.+', '') === false
isMatch('.+', 'anything') === true
```

### v1.0 - one or zero characters `?`

Add support for the `?` character, which means zero or one of the characters that preceeds it.

```javascript
// This matches the string "apple" followed by zero or one 's'
isMatch('apples?', 'apples') === true
isMatch('apples?', 'apple') === true

// We have two 's' characters at the end, so no match
isMatch('apples?', 'appless') === true
```
