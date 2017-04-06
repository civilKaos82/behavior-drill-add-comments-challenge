# Behavior Drill: Add Comments


## Summary
We have a webpage that displays an article and a few user comments.  We want users to be able to add new comments, and we're going to write the JavaScript to implement this feature.  The finished product should behave like the page seen in Figure 1.

![adding comments](readme-assets/add-comments.gif)  
*Figure 1*.  Demonstration of adding comments behaviors.

*Note:* Normally, when users submit comments, we want to persist the data in a database. We're going to bypass that feature in order to focus on handling events and updating the DOM.


### Helpful jQuery Resources
This is one of the more complex behavior drills.  There are a few different moving parts we need to coordinate.  We'll rely on a JavaScript library to help us.  The library is [jQuery][].

These links should be useful in helping to complete this challenge.

- [jQuery Event Basics][]
- [Handling Events][] (e.g., a form `"submit"` event)
- [event.preventDefault()][] (e.g., to prevent the default form submission behavior)
- [.appendTo()][] / [.append()][]
- [.val()][]


## Releases
### Release 0: Implement Adding Comments
We'll do the vast majority of our work in the JavaScript file `application.js`.  HTML is provided in the file `index.html`; don't modify anything inside the `<body>` tag. CSS is also provided, and should not be modified.  Implement the behavior in Figure 1:

- When the user clicks the *New Comment* button,
  - the button is hidden.
  - the comment form appears.
- When the user submits the form,
  - the data from the form should be added as a comment to the end of the comment list.
  - the form fields should be reset, so that the next comment can be added.
  - the form should be hidden.
  - the *New Comment* button should reappear.

Be sure to follow the specifications and remember to take it slow.  Test the code frequently, make small iterations, and write elegant code.

_Note:_ Don't worry about deleting comments until Release 2.

### Release 1: Handle Empty Form Fields
What happens if a user submits the form without adding any data in the form fields?  We just add empty comments to the comment list.  Let's update the comment-adding behavior to control for missing content:

- Prevent empty comments from appearing in the comment list.  When a user submits the form, only append the new comment if the user has entered some text into the form's text area.
- Allow anonymous comments.  If a user submits the form without providing a name, attribute the comment to *Anonymous*.

### Release 2: Deleting Comments

The "Delete Comment" button is currently not functional. It'll be up to you to make it work.

When a "Delete Comment" button is clicked, that comment should be removed from the DOM (thus removing it from the page).

The "Delete Comment" button needs to work both for the existing comments, as well as any comments we add via our comment form in the future. Be sure to test both.

You may want to revist the jQuery page about [Handling Events][], including the section on binding elements that will be rendered in the future.

### Release 3: Sanitizing input

Whoo! Your comment section works and is ready for real users. But now you get a report from your boss that she can't add a comment with the text "I think this article is <awesome>"

What happens when you try this in your application? Why do you think this is? Now, what happens if you try to insert this string as a comment into your article?
  
```<script type="text/javascript">$(document.body).html("In your article, deleting your posts")</script>```

This is another example of an injection attack. It's very similar to the SQL injection attack you learned about in phase 1. If you remember, your SQL code looked something like `SELECT * from Users where id = #{user_id}`. By using string interpolation, the database didn't know the difference between the sql command and the data from the user.

Similarly, for javascript, when you have code that looks like this:
```
var comment = $('#comment_text').val();
$('#new_comment_form').html("<li class='comment'><article><p>" + comment + "</p></article>");
```

The pattern is similar. We are taking user input (in this case stored as comment), using string interpolation, and then passing that to the [$.html()](https://api.jquery.com/html/) function. One way to solve this is to use the [$.text()](https://api.jquery.com/text/) method. When you use .text it is saying to treat whatever is passed in as plain text, not html.

To pass this release, modify your code to prevent HTML injection attacks.

## Conclusion
Handling events and manipulating the DOM are crucial JavaScript skills.  Are we confident in our understanding of how to listen for events?  What about how to handle events?  How to pull data from the DOM?  How to update the DOM?  Get clarity around these issues.


[.append()]: http://api.jquery.com/append/
[.appendTo()]: http://api.jquery.com/appendTo/
[.val()]: http://api.jquery.com/val/
[event.preventDefault()]: http://api.jquery.com/event.preventDefault/
[Handling Events]: http://learn.jquery.com/events/handling-events/
[jquery]: https://jquery.com/
[jQuery Event Basics]: http://learn.jquery.com/events/event-basics/
