## What is Regular Expression?

> Regular expression is a group of characters or symbols which is used to find a specific pattern from a text.

A regular expression is a pattern that is matched against a subject string from
left to right. Regular expression is used for replacing a text within a string, 
validating form, extract a substring from a string based upon a pattern match, 
and so much more. The word "Regular expression" is a mouthful, so you will usually
find the term abbreviated as "regex" or "regexp". 

Imagine you are writing an application and you want to set the rules for when a
user chooses their username. We want to allow the username to contain letters,
numbers, underscores and hyphens. We also want to limit the number of characters
in username so it does not look ugly. We use the following regular expression to
validate a username:

## 1. Basic Matchers

A regular expression is just a pattern of characters that we use to perform
search in a text.  For example, the regular expression `the` means: the letter
`t`, followed by the letter `h`, followed by the letter `e`.

<pre>
"the" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

The regular expression `123` matches the string `123`. The regular expression is
matched against an input string by comparing each character in the regular
expression to each character in the input string, one after another. Regular
expressions are normally case-sensitive so the regular expression `The` would
not match the string `the`.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
## 2. Meta Characters

Meta characters are the building blocks of the regular expressions.  Meta
characters do not stand for themselves but instead are interpreted in some
special way. Some meta characters have a special meaning and are written inside
square brackets. The meta characters are as follows:

|Meta character|Description|
|:----:|----|
|.|Period matches any single character except a line break.|
|[ ]|Character class. Matches any character contained between the square brackets.|
|[^ ]|Negated character class. Matches any character that is not contained between the square brackets|
|*|Matches 0 or more repetitions of the preceding symbol.|
|+|Matches 1 or more repetitions of the preceding symbol.|
|?|Makes the preceding symbol optional.|
|{n,m}|Braces. Matches at least "n" but not more than "m" repetitions of the preceding symbol.|
|(xyz)|Character group. Matches the characters xyz in that exact order.|
|&#124;|Alternation. Matches either the characters before or the characters after the symbol.|
|&#92;|Escapes the next character. This allows you to match reserved characters <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>|
|^|Matches the beginning of the input.|
|$|Matches the end of the input.|

## 2.1 Full stop

Full stop `.` is the simplest example of meta character. The meta character `.`
matches any single character. It will not match return or newline characters.
For example, the regular expression `.ar` means: any character, followed by the
letter `a`, followed by the letter `r`.

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

## 2.2 Character set

Character sets are also called character class. Square brackets are used to
specify character sets. Use a hyphen inside a character set to specify the
characters' range. The order of the character range inside square brackets
doesn't matter. For example, the regular expression `[Tt]he` means: an uppercase
`T` or lowercase `t`, followed by the letter `h`, followed by the letter `e`.

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

A period inside a character set, however, means a literal period. The regular
expression `ar[.]` means: a lowercase character `a`, followed by letter `r`,
followed by a period `.` character.

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

### 2.2.1 Negated character set

In general, the caret symbol represents the start of the string, but when it is
typed after the opening square bracket it negates the character set. For
example, the regular expression `[^c]ar` means: any character except `c`,
followed by the character `a`, followed by the letter `r`.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

## 2.3 Repetitions

Following meta characters `+`, `*` or `?` are used to specify how many times a
subpattern can occur. These meta characters act differently in different
situations.

### 2.3.1 The Star

The symbol `*` matches zero or more repetitions of the preceding matcher. The
regular expression `a*` means: zero or more repetitions of preceding lowercase
character `a`. But if it appears after a character set or class then it finds
the repetitions of the whole character set. For example, the regular expression
`[a-z]*` means: any number of lowercase letters in a row.

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

The `*` symbol can be used with the meta character `.` to match any string of
characters `.*`. The `*` symbol can be used with the whitespace character `\s`
to match a string of whitespace characters. For example, the expression
`\s*cat\s*` means: zero or more spaces, followed by lowercase character `c`,
followed by lowercase character `a`, followed by lowercase character `t`,
followed by zero or more spaces.

<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the con<a href="#learn-regex"><strong>cat</strong></a>enation.
</pre>

### 2.3.2 The Plus

The symbol `+` matches one or more repetitions of the preceding character. For
example, the regular expression `c.+t` means: lowercase letter `c`, followed by
at least one character, followed by the lowercase character `t`. It needs to be
clarified that `t` is the last `t` in the sentence.

<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

### 2.3.3 The Question Mark

In regular expression the meta character `?` makes the preceding character
optional. This symbol matches zero or one instance of the preceding character.
For example, the regular expression `[T]?he` means: Optional the uppercase
letter `T`, followed by the lowercase character `h`, followed by the lowercase
character `e`.

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

## 2.4 Braces

In regular expression braces that are also called quantifiers are used to
specify the number of times that a character or a group of characters can be
repeated. For example, the regular expression `[0-9]{2,3}` means: Match at least
2 digits but not more than 3 ( characters in the range of 0 to 9).

<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

We can leave out the second number. For example, the regular expression
`[0-9]{2,}` means: Match 2 or more digits. If we also remove the comma the
regular expression `[0-9]{3}` means: Match exactly 3 digits.

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

<pre>
"[0-9]{3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to 10.0.
</pre>

## 2.5 Capturing Group

A capturing group is a group of sub-patterns that is written inside Parentheses 
`(...)`. Like as we discussed before that in regular expression if we put a quantifier 
after a character then it will repeat the preceding character. But if we put quantifier
after a capturing group then it repeats the whole capturing group. For example,
the regular expression `(ab)*` matches zero or more repetitions of the character
"ab". We can also use the alternation `|` meta character inside capturing group.
For example, the regular expression `(c|g|p)ar` means: lowercase character `c`,
`g` or `p`, followed by character `a`, followed by character `r`.

<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

Note that capturing groups do not only match but also capture the characters for use in 
the parent language. The parent language could be python or javascript or virtually any
language that implements regular expressions in a function definition.

### 2.5.1 Non-capturing group

A non-capturing group is a capturing group that only matches the characters, but 
does not capture the group. A non-capturing group is denoted by a `?` followed by a `:` 
within parenthesis `(...)`. For example, the regular expression `(?:c|g|p)ar` is similar to 
`(c|g|p)ar` in that it matches the same characters but will not create a capture group.

<pre>
"(?:c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

Non-capturing groups can come in handy when used in find-and-replace functionality or 
when mixed with capturing groups to keep the overview when producing any other kind of output. 
See also [4. Lookaround](#4-lookaround).

## 2.6 Alternation

In a regular expression, the vertical bar `|` is used to define alternation.
Alternation is like an OR statement between multiple expressions. Now, you may be
thinking that character set and alternation works the same way. But the big
difference between character set and alternation is that character set works on
character level but alternation works on expression level. For example, the
regular expression `(T|t)he|car` means: either (uppercase character `T` or lowercase
`t`, followed by lowercase character `h`, followed by lowercase character `e`) OR
(lowercase character `c`, followed by lowercase character `a`, followed by
lowercase character `r`). Note that I put the parentheses for clarity, to show that either expression
in parentheses can be met and it will match.

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

## 2.7 Escaping special character

Backslash `\` is used in regular expression to escape the next character. This
allows us to specify a symbol as a matching character including reserved
characters `{ } [ ] / \ + * . $ ^ | ?`. To use a special character as a matching
character prepend `\` before it.

For example, the regular expression `.` is used to match any character except
newline. Now to match `.` in an input string the regular expression
`(f|c|m)at\.?` means: lowercase letter `f`, `c` or `m`, followed by lowercase
character `a`, followed by lowercase letter `t`, followed by optional `.`
character.

<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

## 2.8 Anchors

In regular expressions, we use anchors to check if the matching symbol is the
starting symbol or ending symbol of the input string. Anchors are of two types:
First type is Caret `^` that check if the matching character is the start
character of the input and the second type is Dollar `$` that checks if matching
character is the last character of the input string.

### 2.8.1 Caret

Caret `^` symbol is used to check if matching character is the first character
of the input string. If we apply the following regular expression `^a` (if a is
the starting symbol) to input string `abc` it matches `a`. But if we apply
regular expression `^b` on above input string it does not match anything.
Because in input string `abc` "b" is not the starting symbol. Let's take a look
at another regular expression `^(T|t)he` which means: uppercase character `T` or
lowercase character `t` is the start symbol of the input string, followed by
lowercase character `h`, followed by lowercase character `e`.

<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

### 2.8.2 Dollar

Dollar `$` symbol is used to check if matching character is the last character
of the input string. For example, regular expression `(at\.)$` means: a
lowercase character `a`, followed by lowercase character `t`, followed by a `.`
character and the matcher must be end of the string.

<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>


##  3. Shorthand Character Sets

Regular expression provides shorthands for the commonly used character sets,
which offer convenient shorthands for commonly used regular expressions. The
shorthand character sets are as follows:

|Shorthand|Description|
|:----:|----|
|.|Any character except new line|
|\w|Matches alphanumeric characters: `[a-zA-Z0-9_]`|
|\W|Matches non-alphanumeric characters: `[^\w]`|
|\d|Matches digit: `[0-9]`|
|\D|Matches non-digit: `[^\d]`|
|\s|Matches whitespace character: `[\t\n\f\r\p{Z}]`|
|\S|Matches non-whitespace character: `[^\s]`|

## License
Original source: https://github.com/ziishaned/learn-regex
MIT &copy; [Zeeshan Ahmad](https://twitter.com/ziishaned)
