# Super Awesome Epic Tutorial for Regex (Dummie Edition)

So, you're probably wondering what Regex is. Great me too! We're going to learn together and we're doing it the dummie edition. The dummie edition meaning for absolute beginners, like no experience what so ever. Or for those who are genuinely curious, welcome!

## Summary

So what is a Regex? Well according to MDN web docs, they are regular expression that match character combinations in strings! Okay lots of fancy words, so basically you're describing patterns with characters. It's like going into Google and using the control/command + f feature and searching for very specific words or characters. For example, `/r[aeiou]+/g`, this example looks for specific words that have the letter r and a vowel. 

Regular expressions needs:
* A set of characters that can be used in the language, called the alphabet.
* A Concatenation: `ab` means "the character `a` followed by the character `b`".
* A Union: `a|b` means "either `a` or `b`".
* A Kleene star: `a*` means "zero or more `a` characters".

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

There are several parts of regex. We're learning a language. So there are pieces to form a sentence like a noun, verb, adjective, commas, periods, etc like in english. In Regex, we have anchors, bracket expressions, quantifiers, grouping constructs, OR Operators, character escapes, character classes, and flags. All of thsese componenents are able to form our "regex sentence."

### Anchors

Anchors are limiters. `^`, for example, lets the reader know that this is the begginning. `^The` searches for "The" or "The person." The "T" versus "t" are different in the anchor's perspective. `$` lets the reader know that the `$` is the end of the line. It's like the end of the sentence.

### Quantifiers

Regex quantifiers are special characters or sequences in regular expressions that specify how many times the preceding element should be matched.
* `*` - Matches the pattern zero or more times
* `+` - Matches the pattern one or more times
* `?` - Matches the pattern zero or one time
* `{}` - Curly brackets can provide three different ways to set limits for a match:
  - `{ n }` - Matches the pattern exactly n number of times
  - `{ n, }` - Matches the pattern at least `n` number of times
  - `{ n, x }` - Matches the pattern from a minimum of `n` number of times to a maximum of `x` number of times
  
 `/^[a-z0-9_-]{3,16}$/`
This regex is looking for any string between 3 and 16 characters that starts and ends with a combination of lowercase characters, the numbers 0–9, and the special characters of an underscore and a hyphen.

### OR Operator

`|` The OR operator is literally something the reader must pick, it can't be both. It does not require the string to meet the all the requirements in the pattern. 

`(a|b|c):(x|y|z)`

Now, both of the strings `"abc:xyz"` and `"acb:xyz"` would match, as well as `"a:z"`, but `"xyz:abc"` would not.

### Character Classes

Character classes regex defines a set of character. Any one can occur to fulfill the match. 

Common character classes:
* `.` - Matches any character except the newline character (`\n`)
* `\d` - Matches any Arabic numeral digit. This class is equivalent to the bracket expression `[0-9]`
* `\w` - Matches any alphanumeric character from the basic Latin alphabet, including the underscore (`_`). This class is equivalent to the bracket expression `[A-Za-z0-9_]`.
* `\s` - Matches a single whitespace character, including tabs and line breaks

### Flags

Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits for the regex. 
* `g` - Global search: the regex should be tested against all possible matches in a string.
* `i` - Case-insensitive search: case should be ignored while attempting a match in a string.
* `m` - Multi-line search: a multi-line input string should be treated as multiple lines.

### Grouping and Capturing

A capturing group groups a subpattern allowing you to repeat atoms (or veriables) to the entrie group or random alternatives.

MDN Example => Matching the date `YYYY-MM-DD`
```
function parseDate(input) {
  const parts = /^(\d{4})-(\d{2})-(\d{2})$/.exec(input);
  if (!parts) {
    return null;
  }
  return parts.slice(1).map((p) => parseInt(p, 10));
}

parseDate("2019-01-01"); // [2019, 1, 1]
parseDate("2019-06-19"); // [2019, 6, 19]
```

### Bracket Expressions

We could put anything in the square brackets `[]` to represent a range of characters that we want to match. For example, `[abc]` will look for a string that includes `a` or `b` or `c`, regardless of the length of the "regex sentence." As long there is an inclusion of the letter, the related 'word' will appear like "court" where the `c` is in the world. If the reader is searching for "Court", where the `C` is capital, the word will not appear. Gotta be very specific. To do that, try `[abcABC]`. Then "Court" will appear.

### Greedy and Lazy Match

`Greedy` means match longest possible string. Greedy: Keep searching until condition is not satisfied.

`Lazy` means match shortest possible string. Lazy: Stop searching once condition is satisfied.

### Boundaries

There are two boundaries, input and word.
Input checks if the current position in the string is an input. The boundaries are usually at the start or the end of the string.

MDN `Input` Example => Matching file extensions

```
function isImage(filename) {
  return /\.(?:png|jpe?g|webp|avif|gif)$/i.test(filename);
}

isImage("image.png"); // true
isImage("image.jpg"); // true
isImage("image.pdf"); // false
```

A word boundary is where the next character is a word character and the previous character is not a word character, or vice versa.

MDN `Word` Example => Detecting Words

```
function hasThanks(str) {
  return /\b(thanks|thank you)\b/i.test(str);
}

hasThanks("Thanks! You helped me a lot."); // true
hasThanks("Just want to say thank you for all your work."); // true
hasThanks("Thanksgiving is around the corner."); // false
```

### Back-references

These refer to the capturing group and can reuse the text captured by a capturing group within the same regex pattern. Writing code is time consuming and hard to remember every single detail. So what's a saving grace? Copy and paste.

MDN Example => Matching Duplicate Words

```
function findDuplicates(text) {
  return text.match(/\b(\w+)\s+\1\b/i)?.[1];
}

findDuplicates("foo foo bar"); // 'foo'
findDuplicates("foo bar foo"); // undefined
findDuplicates("Hello hello"); // 'Hello'
findDuplicates("Hello hellos"); // undefined
```

### Look-ahead and Look-behind

There are four groups: Look ahead positive `(?=)`, Look ahead negative `(?!)`, Look behind positive `(?<=)`, and Look behind negative `(?<!)`.

+ ahead => `x` if followed by `y` => `x(?=y)`
- ahead => `x` if not followed by `y` => `x(?!y)`
+ behind => `x` if after `y` => `(?<=y)x`
- behind => `x` if not after `y` => `(?<!y)x`

## Author
Written by GitHub User: Kibarke => `https://github.com/kibarke`

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)

## Sources 
- Boot-Camp => `https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial`
- MDN WebDocs => `https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Regular_expressions`
- ChatGPT
- Wikipedia => `https://en.wikipedia.org/wiki/Regular_expression`
- Medium => `https://medium.com/@NALSengineering/regex-for-dummies-part-4-capturing-groups-and-backreferences-50c338a3b6f6#:~:text=Backreferences%20are%20a%20feature%20that,within%20the%20same%20regex%20pattern.`