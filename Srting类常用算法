## concat
public String concat(String str)
Concatenates the specified string to the end of this string.
If the length of the argument string is 0, then this String object is returned. Otherwise, a String object is returned that represents a character sequence that is the concatenation of the character sequence represented by this String object and the character sequence represented by the argument string.

Examples:

 "cares".concat("s") returns "caress"
 "to".concat("get").concat("her") returns "together"
 
Parameters:
str - the String that is concatenated to the end of this String.
Returns:
a string that represents the concatenation of this object's characters followed by the string argument's characters.


## trim
public String trim()
Returns a string whose value is this string, with any leading and trailing whitespace removed.
If this String object represents an empty character sequence, or the first and last characters of character sequence represented by this String object both have codes greater than '\u0020' (the space character), then a reference to this String object is returned.

Otherwise, if there is no character with a code greater than '\u0020' in the string, then a String object representing an empty string is returned.

Otherwise, let k be the index of the first character in the string whose code is greater than '\u0020', and let m be the index of the last character in the string whose code is greater than '\u0020'. A String object is returned, representing the substring of this string that begins with the character at index k and ends with the character at index m-that is, the result of this.substring(k, m + 1).

This method may be used to trim whitespace (as defined above) from the beginning and end of a string.

Returns:
A string whose value is this string, with any leading and trailing white space removed, or this string if it has no leading or trailing white space.

## split
public String[] split(String regex)
Splits this string around matches of the given regular expression.
This method works as if by invoking the two-argument split method with the given expression and a limit argument of zero. Trailing empty strings are therefore not included in the resulting array.

The string "boo:and:foo", for example, yields the following results with these expressions:

Regex	Result
:	{ "boo", "and", "foo" }
o	{ "b", "", ":and:f" }
Parameters:
regex - the delimiting regular expression
Returns:
the array of strings computed by splitting this string around matches of the given regular expression
Throws:
PatternSyntaxException - if the regular expression's syntax is invalid
Since:
1.4
See Also:
Pattern

## join
public static String join(CharSequence delimiter,
                          CharSequence... elements)
Returns a new String composed of copies of the CharSequence elements joined together with a copy of the specified delimiter.
For example,

     String message = String.join("-", "Java", "is", "cool");
     // message returned is: "Java-is-cool"
 
Note that if an element is null, then "null" is added.
Parameters:
delimiter - the delimiter that separates each element
elements - the elements to join together.
Returns:
a new String that is composed of the elements separated by the delimiter
Throws:
NullPointerException - If delimiter or elements is null
Since:
1.8
See Also:
StringJoiner

## toCharArray
public char[] toCharArray()
Converts this string to a new character array.
Returns:
a newly allocated character array whose length is the length of this string and whose contents are initialized to contain the character sequence represented by this string.

## matches
public boolean matches(String regex)
Tells whether or not this string matches the given regular expression.
An invocation of this method of the form str.matches(regex) yields exactly the same result as the expression

Pattern.matches(regex, str)
Parameters:
regex - the regular expression to which this string is to be matched
Returns:
true if, and only if, this string matches the given regular expression
Throws:
PatternSyntaxException - if the regular expression's syntax is invalid
Since:
1.4
See Also:
Pattern

## substring
public String substring(int beginIndex,
                        int endIndex)
Returns a string that is a substring of this string. The substring begins at the specified beginIndex and extends to the character at index endIndex - 1. Thus the length of the substring is endIndex-beginIndex.
Examples:

 "hamburger".substring(4, 8) returns "urge"
 "smiles".substring(1, 5) returns "mile"
 
Parameters:
beginIndex - the beginning index, inclusive.
endIndex - the ending index, exclusive.
Returns:
the specified substring.
Throws:
IndexOutOfBoundsException - if the beginIndex is negative, or endIndex is larger than the length of this String object, or beginIndex is larger than endIndex.
