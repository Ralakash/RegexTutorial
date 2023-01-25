# Using Regex to Match an HTML Tag a Tutorial

This tutorial will demonstrate how to match an HTML tag using Regex or Regular Expression.

## Summary

During this tutorial you will learn how to match an HTML tag using Regex. This tutorial will demonstrate this by using the following Regular Expression and break it down to show how to customize the expression to fit your needs.
The expression you will learn to break down is `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Final Breakdown](#final-breakdown)

## Regex Components

To begin first your Regex must be wrapped in slash characters (/). This is due to regex being a literal.

### Anchors

The next character in the sequence is the carrot or hat (^). This is an anchor and signifies that the matching string must begin with the characters that follow it. This is case sensitive. In our scenario this next character is a (<). This is due to the fact that all HTML tags are wrapped in (<>).
Another anchor that is seen in this example is the ($) anchor which is the second to last character in the sequence. This character works in a similar manner to the (^) but indicates that the ending character of the string must be the character or characters that follow the ($).

### Quantifiers

Quantifiers are an important part of a Regex expression as they allow you to indicate how many times a certain portion of the sequence should occur in the matching element. In our example we see a number of quantifiers.
The 10th element of the expression is (+) This indicates that the previous bracket ([a-z]) must occur 1 or more times. The 17th element is another (+) indicating that ([^<]) must occur at least once but can occur multiple times as well.
The 19th element of the expression is a (\*) This indicates that group before it should is optional but can occur multiple times. We can see that this indicates that the group of the expression (([^<]+)) is optional but can occur more than once as well.
The final quanifier we see in this expression is the 21st element (?). This would normally indicate that the prior group or character occurs once or not at all, but in this situation indicates that the group it occurs in in considered non-capturing. This will be explained in more detail later in the tutorial.
Our example does not include the another common quanifier ({}). Curly brackets can be used to identify a specific number of times an element will occur or a range of times. For example ({5}) would indicate that the character or group preceding this will be repeated exactly 5 times.

### Grouping Constructs

In Regex you can use parenthesis (()) to group constructs together. These constructs will look for exact matches unless told to do otherwise. We can see a number or groups used in our example.
our first group shows (([a-z]+)). This would be classified as group 1 (The entirety of the expression is group 0). This group indicates any number of letters a through z and any number of these characters but at least one.
Next in our example we see group 2 ([^<]+). This indicates that in our expression we will have more than 1 (^) or (<). However because this group is followed by a (_) it would indicate that this is optional or could occur multiple times.
Group 3 is (?:>(._)<\/\1>|\s+\/>). Group 3 is a big group but can be broken down into easy steps. this group starts with (?:) This sequence indicates that the group is non-capturing. That means that it will use the group to match search criteria but will ignore the group later. Effectively giving the final result two groups (plus group 0) instead of 3. The rest of this group will be broken down throughout the rest of the tutorial.
Group 4 is inside of group 3 and is ((.\*)). Because group 4 does not have (?:) inside of it it will be captured as a group unlike group 3.

### Bracket Expressions

We have seen bracket expressions indicated twice in our tutorial already. Brackets indicate a specific set of characters that should be searched for.
First we see ([a-z]) this indicates any lowercase letter a through z. The second Bracket expression is ([^<]) This indicates that we will see either a (^) or a (<) but nothing else.

### Character Classes

Character classes are a set of characters in regex that fufill a specific requirement. For example a (.) indicates a match with any character, a (/d) indicates a match with any arabic numeral digit (0-9), and a (/w) indicates any alphanumeric character. These character classes are case specific and capitalizing the letter will invert the search criteria.
In our example we see a character class used twice. These are both inside of group 3. Group 4 (inside group 3) is ((.\*)). This would indicate any number (or none) of any character. The next character class we see is (/s) This indicates any single whitespace character but because our example is followed by a (+) we know that it indicates any number of whitespace characters with at least one.

### The OR Operator

Inside of group three we see our first (|) This indicates the Or operator and breaks group three into two parts. (>(.\*)<\/\1>) or (\s+\/>).

### Flags

Our example does not include any flags but if it did it would come after our closing (/) The flags can add options that apply to your entire search such as searching for your results among multiple lines, making your search case insensitive, or making your search global.

### Character Escapes

The final factor in our tutorial that will allow us to solve this expression is knowing about escapes. Escapes will allow you to escape a character that would otherwise be interpreted literally. For example we know that (/) is used to end the search that means that to search for a string with (/) we need to first escape from interpreting it literally. We do this by using a backslash (\). This can be seen in group 3 where we can see it used to search for the forward slash that closes the HTML element. With this we are able to finally break down every part of our HTML tag using Regex.

### Final Breakdown

Our expression is `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`
We will use the following HTML tag to highlight the sections that are beingn searched for: <div class="city">This is a sentence</div>
We start our expression with (/) as this is required for Regex.
We then must start our search with a (<) as we see at the beginning of any HTML element.
Next we come to our first group wich captures any group of lowercase letters after the initial (<). There must be at least one letter in this group. This group captures "div"
Our next group is ([^<]+) which indicates any string starting after the initial (<) but after the first group. This is followed by (_) which makes the entire group optional or it can occur any number of times. This group would capture "class="city" because of where the next group starts but if group 3 was not there it would capture the rest of the string.
Our third group is the most complicated and starts by being non capturing meaning that it will not output when called. This is indicated by (?:).
After that we have the closing (>) on our initial <div> tag followed by group 4.
Group 4 is (._). This means any number of any character. This would be any text in between our HTML tags. In our example group 4 would capture "This is a sentence".
After group 4 we have the opening (<) of our closing HTML tag indicated by (\/) as need to escape the literal (/) or it would think our regex is closing.
Next we have (\1) This indicates to search for what we found in group 1. In our example this would be the closing "div".
This is followed by (>|\s+>) This means that there is either a closing (>) or any number of spaces and a closing (>). This is the final peice of group 3. After group 3 we have a ($) indicating that the search must end with group 3.
Our last character is our closing (/) indicating we are done with our regex.

## Author

I am a Coding Bootcamp student. My Github username is [Ralakash](https://ralakash.github.io/)
