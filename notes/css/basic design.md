# Basic Design

## CSS

## Headings
Headings (h1 through h6 elements) are workhorse tags that help provide structure and labeling to your content. Screen readers can be set to read only the headings on a page so the user gets a summary. This means it is important for the heading tags in your markup to have semantic meaning and relate to each other, not be picked merely for their size values.

Semantic meaning means that the tag you use around content indicates the type of information it contains.

If you were writing a paper with an introduction, a body, and a conclusion, it wouldn't make much sense to put the conclusion as a subsection of the body in your outline. It should be its own section. Similarly, the heading tags in a webpage need to go in order and indicate the hierarchical relationships of your content.

Headings with equal (or higher) rank start new implied sections, headings with lower rank start subsections of the previous one.

As an example, a page with an h2 element followed by several subsections labeled with h4 tags would confuse a screen reader user. With six choices, it's tempting to use a tag because it looks better in a browser, but you can use CSS to edit the relative sizing.

One final point, each page should always have one (and only one) h1 element, which is the main subject of your content. This and the other headings are used in part by search engines to understand the topic of the page.

## Article Element
article is another one of the new HTML5 elements that adds semantic meaning to your markup. Article is a sectioning element, and is used to wrap independent, self-contained content. The tag works well with blog entries, forum posts, or news articles.

Determining whether content can stand alone is usually a judgement call, but there are a couple simple tests you can use. Ask yourself if you removed all surrounding context, would that content still make sense? Similarly for text, would the content hold up if it were in an RSS feed?

Remember that folks using assistive technologies rely on organized, semantically meaningful markup to better understand your work.

**Note about section and div**
The section element is also new with HTML5, and has a slightly different semantic meaning than article. An article is for standalone content, and a section is for grouping thematically related content. They can be used within each other, as needed. For example, if a book is the article, then each chapter is a section. When there's no relationship between groups of content, then use a div.

```h
<div> - groups content
<section> - groups related content
<article> - groups independent, self-contained content
```

### Article Example

```h
<h1>Deep Thoughts with Master Camper Cat</h1>
<main>
  <div>
    <h2>The Garfield Files: Lasagna as Training Fuel?</h2>
    <p>The internet is littered with varying opinions on nutritional paradigms, from catnip paleo to hairball cleanses. But let's turn our attention to an often overlooked fitness fuel, and examine the protein-carb-NOM trifecta that is lasagna...</p>
  </div>

  <img src="samuraiSwords.jpeg" alt="">

  <article>
    <h2>Defeating your Foe: the Red Dot is Ours!</h2>
    <p>Felines the world over have been waging war on the most persistent of foes. This red nemesis combines both cunning stealth and lightening speed. But chin up, fellow fighters, our time for victory may soon be near...</p>
  </article>

  <img src="samuraiSwords.jpeg" alt="">

  <article>
    <h2>Is Chuck Norris a Cat Person?</h2>
    <p>Chuck Norris is widely regarded as the premier martial artist on the planet, and it's a complete coincidence anyone who disagrees with this fact mysteriously disappears soon after. But the real question is, is he a cat person?...</p>
  </article>
</main>
```

## Header Element
The next HTML5 element that adds semantic meaning and improves accessibility is the header tag. It's used to wrap introductory information or navigation links for its parent tag, and works well around content that's repeated at the top on multiple pages.

header shares the embedded landmark feature you saw with main, allowing assistive technologies to quickly navigate to that content.

## Nav Element
The nav element is another HTML5 item with the embedded landmark feature for easy screen reader navigation. This tag is meant to wrap around the main navigation links in your page.

If there are repeated site links at the bottom of the page, it isn't necessary to markup those with a nav tag as well. Using a footer (covered in the next challenge) is sufficient.

## Footer Element
Similar to header and nav, the footer element has a built-in landmark feature that allows assistive devices to quickly navigate to it. It's primarily used to contain copyright information or links to related documents that usually sit at the bottom of a page.

## Audio Element
HTML5's audio element gives semantic meaning when it wraps sound or audio stream content in your markup. Audio content also needs a text alternative to be accessible to people who are deaf or hard of hearing. This can be done with nearby text on the page or a link to a transcript.

The audio tag supports the controls attribute. This shows the browser default play, pause, and other controls, and supports keyboard functionality. This is a boolean attribute, meaning it doesn't need a value, its presence on the tag turns the setting on.

**Example**
```h
<audio id="meowClip" controls>
  <source src="audio/meow.mp3" type="audio/mpeg" />
  <source src="audio/meow.ogg" type="audio/ogg" />
</audio>
```

## Figure Element
HTML5 introduced the figure element, along with the related figcaption. Used together, these items wrap a visual representation (like an image, diagram, or chart) along with its caption. This gives a two-fold accessibility boost by both semantically grouping related content, and providing a text alternative that explains the figure.

For data visualizations like charts, the caption can be used to briefly note the trends or conclusions for users with visual impairments. Another challenge covers how to move a table version of the chart's data off-screen (using CSS) for screen reader users.

Here's an example - note that the figcaption goes inside the figure tags and can be combined with other elements

**Example**
```h
<figure>
  <img src="roundhouseDestruction.jpeg" alt="Photo of Camper Cat executing a roundhouse kick">
  <br>
  <figcaption>
    Master Camper Cat demonstrates proper form of a roundhouse kick.
  </figcaption>
</figure>
```

## Form Element
Improving accessibility with semantic HTML markup applies to using both appropriate tag names as well as attributes. The next several challenges cover some important scenarios using attributes in forms.

The label tag wraps the text for a specific form control item, usually the name or label for a choice. This ties meaning to the item and makes the form more readable. The for attribute on a label tag explicitly associates that label with the form control and is used by screen readers.

You learned about radio buttons and their labels in a lesson in the Basic HTML section. In that lesson, we wrapped the radio button input element inside a label element along with the label text in order to make the text clickable. Another way to achieve this is by using the for attribute as explained in this lesson.

The value of the for attribute must be the same as the value of the id attribute of the form control. Here's an example:

**Example**
```h
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name">
</form>
```

