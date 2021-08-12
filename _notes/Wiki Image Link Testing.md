---
category: Development
---

# Wikilinks
Double bracketed links are converted to Jekyll-ingestible Markdown formatting by the `bidirectional_links_generator.rb` plugin. However, Obsidian's Wikilink setting also applies to a proprietary image embed format with double brackets. 

I'm working on another plugin to complement the bidirectional link generator and resolve Obsidian image embeds automatically. This page is for testing the efficacy of the script and the regex I'm using.

This is a useful reference for [Regex in Ruby](https://ruby-doc.org/core-3.0.1/doc/regexp_rdoc.html) and this is a good [Ruby Regex Tester](https://rubular.com/).

# Version 1
- Does not support `"title"` in Markdown links because I couldn't figure out the regex
	- Example:  `![Alt text](tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg "a title")`
	- If you use these, the image will break
- Fixed the problem with links rendering inside `[[code blocks]]`

```
But it doesn't work in this [[type of block]] because of the extra linebreaks and characters before the tick marks
```

~~~
Is this also a code block oh shit
~~~

# Version 2
I DID A GOOD REGEX!
- Code blocks can contain `[[brackets]]` without rendering links!
- Markdown images contain `title` now!
	- **Update:** Regex is faulty. When title exists, the asset path picks up the space before the `"`. Will fix later.

Edits:
- New plugin called `obsidian_images_generator.rb` with higher priority than the bidirectional links generator
- Edited bidirectional links generator to exclude codeblocks

For those of you who would like to know, this is the regex I added to the end of each section in the generator:
```(?!.*?[\r\n]+[`{3,}|~{3,}])```

## Helpful References
- https://github.com/github/cmark-gfm/blob/master/src/scanners.re
- https://github.com/jeffreytse/jekyll-spaceship/blob/master/lib/jekyll-spaceship/processors/element-processor.rb
- https://jekyllrb.com/docs/plugins/generators/
- https://stackoverflow.com/questions/45279912/select-all-code-in-md-codeblock

It works! Now you can drag and drop images to Obsidian editor and the asset path will automatically generate. Make sure to follow guidelines in [[Obsidian Setup]]

# Testing
![[tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg]]

This image is in a Markdown link to nowhere and also has a title
[![Image alt text](tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg "a title")](https://URL)

Using the note `title` variable: [[a note about cats]]. Using the note's filename: [[cats]]. Using the note's title, with a label: [[cats|link to the note about cats using the note title]]. Using the note's filename, with a label: [[cats|link to the note about cats using the note's filename]]. In all cases, if the double-bracket link does not point to a valid note, the double brackets will still be shown, like this: [[there is no note that matches this link]]. This is an Obsidian Image. ![[tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg]]. This is a Markdown image with alt text only. ![Alt text](tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg). This is a Markdown image without alt text but with a title. ![](tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg "a title"). This is an Obsidian image that links to the assets folder. ![[assets/images/tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg]]. And another with a slash. ![[/assets/images/tom-wheatley-HdIb-5gRv7U-unsplash 1.jpg]]