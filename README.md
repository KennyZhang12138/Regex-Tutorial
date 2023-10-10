# Regex-Tutorial

# What Is a Regex?

A regex, which is short for regular expression, is a sequence of characters that defines a specific search pattern. When included in code or search algorithms, regular expressions can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input.

For example, the following regular expression can be used to verify that user input is a valid email address:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

## Summary

This is a regular expression (regex) used to validate email addresses. The regex will check if an email address conforms to the typical format, including username, "@" symbol, domain name, and top-level domain (TLD).

Regex Pattern:

```
^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```

Explanation:
The components of this regex and how it works to validate email addresses. The regex pattern ensures that the email address contains a valid username, "@" symbol, valid domain name, and TLD.

This a regular expression (regex) for matching URLs. The regex will cover a broad range of URLs, including those with and without the "http://" or "https://" protocol, domain names, and optional paths.

Regex Pattern:

```
^(https?://)?([a-zA-Z0-9.-]+)(:[0-9]+)?(/[^?#]*)?(\?[^#]*)?(#.*)?$
```

Explanation:
The different parts of this regex pattern and how it can be used to match URLs with various components, such as the protocol, domain, port, path, query parameters, and fragments.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Anchors in regular expressions are special characters or assertions that allow you to specify the position within a string where a match should occur. They don't consume any characters; instead, they only represent a position in the string. There are two primary types of anchors: the caret **'^'** and the dollar sign **'$'**.

1. **'^'** (caret) - Start of Line Anchor:
    * The **'^'** anchor asserts that the match must occur at the beginning of a line or string.
    * It does not consume any characters; it only checks the position at the start.

Example:

    The regex '^Hello' will match "Hello" at the beginning of a line or string, but not "World Hello."

2. **'$'** (dollar sign) - End of Line Anchor:

    * The **'$'** anchor asserts that the match must occur at the end of a line or string.
    * like **'^'**, it does not consume any characters; it only checks the position at the end.

Example:

    The regex world$ will match "world" at the end of a line or string, but not "Hello world."

These anchors are useful for enforcing specific rules about where a pattern should start or end within a given input string. They are often used for tasks like validating email addresses (with **'^'** at the start and **'$'** at the end) or ensuring that a password meets specific criteria (e.g., starts with a letter and ends with a digit).

### Quantifiers

Quantifiers in regular expressions are used to specify how many times a particular character or group of characters should appear in the input text. They allow you to control the repetition of patterns within the regular expression. Here are some common quantifiers:

1. **'*'** (Asterisk) - Zero or More:

    * The **'*'** quantifier matches zero or more occurrences of the preceding element.

Example: 

    'a*' matches "aaa," "a," and an empty string.

2. **'+'** (Plus) - One or More:

    * The **'+'** quantifier matches one or more occurrences of the preceding element.

Example:

    'a+' matches "aaa" but not an empty string.

3. **'?'** (Question Mark) - Zero or One:

    * The **'?'** quantifier matches zero or one occurrence of the preceding element.

Example:

    'colou?r' matches "color" and "colour."

4. **'{n}'** - Exactly n Times:

    * The **'{n}'** quantifier specifies exactly n occurrences of the preceding element.

Example:

    'a{3}' matches "aaa."

5. **'{n,}'** - n or More Times:

    * The **'{n,}'** quantifier specifies at least n occurrences of the preceding element.

Example:

    'a{2,}' matches "aa" and "aaa."

6. **'{n,m}'** - Between n and m Times:

    * The **'{n,m}'** quantifier specifies a range of occurrences between n and m for the preceding element.

Example:

    'a{2,4}' matches "aa," "aaa," and "aaaa."

7. **'*?', '+?', '??', '{n,m}?'** (Lazy Quantifiers):

    * By adding a **'?'** after a quantifier, you make it "lazy" or non-greedy. It matches the shortest possible sequence instead of the longest.

Example:

    'a*?' in the string "aaa" will match just one "a."

Quantifiers are powerful tools for specifying the number of repetitions in your regular expressions, making it easier to match patterns that repeat multiple times in a given text. They are essential for tasks like validating dates, extracting phone numbers, or parsing structured data.

### Grouping Constructs

Grouping constructs in regular expressions allow you to create subpatterns within your regular expression. They serve several purposes, including capturing substrings, applying quantifiers to multiple characters, and creating alternations. There are two main types of grouping constructs: capturing groups and non-capturing groups.

1. Capturing Groups (Regular Parentheses):

    * Capturing groups are created by enclosing a part of the regular expression within parentheses **'('** and **')'**.
    * They capture and remember the text matched by the enclosed subpattern, making it available for later use.
    * Captured text can be referred to using backreferences, like **'\1'**, **'\2'**, etc.

Example:

    '(\d{2})-(\d{2})-(\d{4})' matches a date in the format "dd-mm-yyyy." The three sets of parentheses create three capturing groups, capturing the day, month, and year separately.

2. Non-Capturing Groups (?:...):

    * Non-capturing groups are also enclosed within parentheses, but they start with **'?:'** (e.g., (?:...)).
    * They are used when you want to group expressions for the purpose of applying quantifiers or alternations but don't need to capture the matched text.
    * Non-capturing groups are helpful for optimizing the regular expression when you don't need to store the matched text.

Example:

    '(?:https?|ftp)://' matches URLs starting with "http://," "https://," or "ftp://," but it doesn't capture the protocol.

3. Backreferences to Capturing Groups:

    * Captured text from capturing groups can be referenced later in the regular expression using backreferences.
    * A backreference uses a backslash followed by the group number (e.g., **'\1'** refers to the first capturing group).

Example:

    '(\d{2})-(\d{2})-(\d{4}) \1-\2-\3' matches a date in the "dd-mm-yyyy" format, followed by the same date (e.g., "15-10-2023 15-10-2023").

Grouping constructs are powerful tools in regular expressions because they allow you to structure and organize complex patterns, capture specific information, and create more efficient and readable expressions. They are commonly used when working with text data to extract or manipulate specific parts of a string.

### Bracket Expressions

Bracket expressions in regular expressions, often referred to as character classes, are used to specify a set of characters that can match a single character at a particular position in a string. They allow you to define a range or a list of characters that you want to match. Bracket expressions are enclosed within square brackets **'['**, **']'**.

Here are the basic elements and usage of bracket expressions:

1. **Single Character Matches:** Inside the square brackets, you can list individual characters that you want to match exactly.

Example:

    '[abc]' matches any single character that is either "a," "b," or "c."

2. **Ranges:** You can specify a range of characters using a hyphen - between the start and end characters.

Example:

    '[0-9]' matches any single digit from 0 to 9.
    '[a-z]' matches any lowercase letter from 'a' to 'z'.
    '[A-Z]' matches any uppercase letter from 'A' to 'Z'.
    '[0-9a-fA-F]' matches a hexadecimal digit (0-9, a-f, A-F).

3. **Negation:** You can use a caret **'^'** as the first character inside the square brackets to indicate negation, meaning it matches any character that is not in the specified set.

Example:

    '[^0-9]' matches any character that is not a digit.

4. **Combining Characters:** You can combine individual characters, ranges, and negation within a single bracket expression.

Example:

    '[aeiou]' matches any vowel (a, e, i, o, or u).
    '[^aeiou]' matches any consonant (a character that is not a vowel).

5. **Escaping Characters:** Certain characters inside a bracket expression have special meanings (e.g., -, ], ^). If you want to match these characters literally, you need to escape them using a backslash.

Example:

    '[a-z-]' matches lowercase letters and the hyphen character.

Bracket expressions are particularly useful for matching specific sets of characters or ranges of characters within text. They are commonly used for tasks like extracting valid email addresses, phone numbers, or finding specific patterns within a larger dataset.

### Character Classes

Character classes in regular expressions are predefined shorthand notations that represent commonly used sets of characters. They allow you to match characters based on their common characteristics, simplifying the regular expression pattern. Here are some commonly used character classes:

1. **\d** - Digit:

    * Matches any digit from 0 to 9.
    * Equivalent to **'[0-9]'**.

2. **\D** - Non-Digit:

    * Matches any character that is not a digit.
    * Equivalent to **'[^0-9]'**.

3. **\w** - Word Character:

    * Matches any word character, which includes letters (both uppercase and lowercase), digits, and underscore **'_'**.
    * Equivalent to **'[a-zA-Z0-9_]'**.

4. **\W** - Non-Word Character:

    * Matches any character that is not a word character.
    * Equivalent to **'[^a-zA-Z0-9_]'**.

5. **\s** - Whitespace Character:

    * Matches any whitespace character, such as space, tab, or newline.
    * Equivalent to **'[ \t\n\r\f\v]'**.

6. **\S**  - Non-Whitespace Character:

    * Matches any character that is not a whitespace character.
    * Equivalent to **'[^ \t\n\r\f\v]'**.

7. **.** (Period) - Any Character (except newline):

    * Matches any character except a newline character.
    * Equivalent to **'[^\n]'** in most regex engines.

8. **\b** - Word Boundary:

    * Matches a word boundary, which is the position between a word character (e.g., a letter or digit) and a non-word character (e.g., whitespace or punctuation).

9. **\B**  - Non-Word Boundary:

    * Matches a position that is not a word boundary.

These character classes provide a convenient way to match common categories of characters without having to explicitly specify each character or character range. They are often used in regex patterns for tasks like validating input, extracting specific information, or searching for patterns in text data.

### The OR Operator

In regular expressions, the OR operator, often represented by the pipe symbol |, allows you to specify multiple alternatives for a pattern. It functions as a logical OR, meaning that it matches any one of the alternatives. Here's how it works:

* The | operator is used to separate different alternatives within a regular expression.
* It will match the first alternative it encounters from left to right, and if none of them match, it continues checking the subsequent alternatives.

Example:

    The regular expression apple|banana matches either "apple" or "banana."
    In the string "I like apples and bananas," it would match "apple" and "banana."

* You can use parentheses to group patterns when you need to use the OR operator with more complex expressions. 

For example:

    '(apple|banana) pie' matches "apple pie" or "banana pie."
    'apple|banana pie' matches "apple" or "banana pie."

The OR operator is valuable when you want to find any of a list of alternatives in your text or when you need to specify multiple variations of a pattern without creating separate regular expressions for each one. It is a versatile tool for creating more flexible and powerful regex patterns.

### Flags

In regular expressions, flags are modifiers that you can add to the end of a regular expression pattern to control how the pattern matching should be performed. These flags alter the default behavior of the regex engine and can be used to fine-tune the way a regular expression is applied to text. Different programming languages and regex libraries may have slightly different flag options, but some of the common flags include:

1. **Case Insensitive (i):**

    * The **'i'** flag makes the regex pattern match characters regardless of their case. 

Example:

    '/apple/i' would match "apple," "Apple," and "aPpLe."

2. **Global (g):**

    * The g flag allows the regex engine to find all matches in the input string, not just the first match.

3. **Multiline (m):**

    * The **'m'** flag changes the behavior of the **'^'** and **'$'** anchors to match the start and end of each line within the input string rather than just the start and end of the whole string.

4. **Dot All (s):**

    * The **'s'** flag changes the behavior of the **'.'** metacharacter to match any character, including newline characters. By default, **'.'** does not match newline characters.

5. **Sticky (y):**

    * The **"y'** flag is used in some regex engines to perform a "sticky" match. It matches only at the current position within the string and does not advance.

6. **Unicode (u):**

    * The **'u'** flag is used to enable full Unicode matching. It allows the regex to handle Unicode characters and properties correctly.

7. **Verbose (x):**

    * The **'x'** flag allows you to add whitespace and comments within the regex pattern to make it more readable. This flag is particularly useful for complex regex patterns.

8. **Single Line (s):**

    * The **'s'** flag makes the **'.'** metacharacter match any character, including newline characters. It's similar to the **'s'** flag in some regex engines.

9. **Free Spacing (x):**

    * The **'x'** flag (also called "free spacing" or "ignore whitespace") allows you to use whitespace and comments within the regex pattern to improve its readability.

The usage of flags depends on the programming language or regex library you are using. For example, in JavaScript, you would use flags like **'/pattern/i'** to create a case-insensitive regex, while in Python, you can use the **'re.IGNORECASE'** flag with the **'re.compile'** function.

Flags are useful for customizing regular expressions to meet specific matching requirements and to control how patterns are applied to text.

### Character Escapes

Character escapes in regular expressions are special sequences that begin with a backslash \ followed by a character. They serve to match specific characters or character classes, some of which have special meanings in regular expressions. Using character escapes, you can match characters that might otherwise be interpreted as metacharacters or achieve other specific matching needs. Here are some common character escapes:

1. **\t - Tab:**

    * Matches a tab character.

2. **\n - Newline:**

    * Matches a newline character.

3. **\r - Carriage Return:**

    * Matches a carriage return character.

4. **\f - Form Feed:**

    * Matches a form feed character.

5. **\v - Vertical Tab:**

    * Matches a vertical tab character.

Using character escapes allows you to match specific characters without confusion or misinterpretation. It's especially useful when you need to match characters that are metacharacters or have special meanings in regular expressions. 

For example: 

    '\.' matches a literal period (dot), and '\\' matches a literal backslash.

## Author
:octocat: [Kenny Zhang](https://github.com/KennyZhang12138)