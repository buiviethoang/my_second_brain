2025-08-30 09:53
Status: #baby
Tags: [[instruction]]
## Main

### Headings: 
```# The largest heading
## The h2 heading
###### The smallest heading
```

**This is bold**
__also bold__

*Italic*
_also italic_

~~Strike through~~
***All bold and italic***

> Quote text in .md file
> Also quote but in the next line
> Keep moving on

### Using backticks to `hightlight`

### Special form: markdown with backticks: (triple backticks and backticks within)
```markdown
Use `git status` to list all new or modified files that haven't yet been committed.
```

```
kfjdfjd
```

### Create inline link with bracket (must be followed by parenthesis)
This site was built using [GitHub Pages](https://pages.github.com/).


### Relative links
[Contribution guidelines for this project](docs/CONTRIBUTING.md)


### Images: Adding !
![This is an image](https://myoctocat.com/assets/images/base-octocat.svg)

### Specify the theme an image is shown to
Light Theme

![GitHub Dark](https://github.com/github-dark.png#gh-light-mode-only)

### Lists:
- 1
- 2
- 3

Or 
* 1
* 2
* 3

To order:
1. 1
2. 2
3. 3

### Task lists: 

- [x] #739
- [ ] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:

### Mentioning people and teams: @
@Bui

### Using emoji: 
:(name of emoji): 
@octocat :+1: This PR looks great - it's ready to merge! :shipit:

### Footnotes: 

Here is a simple footnote[^1].

A footnote can also have multiple lines[^2].  

You can also use words, to fit your writing style more closely[^note].

[^1]: My reference.
[^2]: Every new line should be prefixed with 2 spaces.  
  This allows you to have a footnote with multiple lines.
[^note]:
    Named footnotes will still render with numbers instead of the text but allow easier identification and linking.  
    This footnote also has been made with a different syntax using 4 spaces for new lines.
	
	
### Hiding contents with comment: 
<!-- This content will not appear in the rendered Markdown -->

### Ignoring Markdown formatting: \

### Create horizontal line: 
--- 
or 
***
or 
___
### Hightlight: 
==text==
### Reference Lists & Titles
**The quick brown [fox][1], jumped over the lazy [dog][2].**

[1]: https://en.wikipedia.org/wiki/Fox "Wikipedia: Fox"
[2]: https://en.wikipedia.org/wiki/Dog "Wikipedia: Dog"

### Escaping
\*literally\*

### Tables

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

*Cell widths can vary, as shown below. The rendered output will look the same.*

| Syntax | Description |
| --- | ----------- |
| Header | Title |
| Paragraph | Text |
#### Alignment
You can align text in the columns to the left, right, or center by adding a colon (`:`) to the left, right, or on both side of the hyphens within the header row.

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

### Subscript& superscript
This isn’t common, but some Markdown processors allow you to use _subscript_ to position one or more characters slightly below the normal line of type. To create a subscript, use one tilde symbol (`~`) before and after the characters

H~2~O

This isn’t common, but some Markdown processors allow you to use _superscript_ to position one or more characters slightly above the normal line of type. To create a superscript, use one caret symbol (`^`) before and after the characters.

X^2^

Let's rename \*our-new-project\* to \*our-old-project\*.

## References
