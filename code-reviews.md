# Code Reviews

Effective code reviews help improve code quality, share knowledge, and catch bugs early. 

The biggest mistake I see is doing a review that focuses solely on the diff2. Most of the highest-impact code review comments have very little to do with the diff at all, but instead come from your understanding of the rest of the system.

For instance, one of the most straightforwardly useful comments is “you don’t have to add this method here, since it already exists in this other place”. The diff itself won’t help you produce a comment like this. You have to already be familiar with other parts of the codebase that the diff author doesn’t know about.

Likewise, comments like “this code should probably live in this other file” are very helpful for maintaining the long-term quality of a codebase. The cardinal value when working in large codebases is consistency

Probably my most controversial belief about code review is that a good code review shouldn’t contain more than five or six comments. Most engineers leave too many comments. When you receive a review with a hundred comments, it’s very hard to engage with that review on anything other than a trivial level. Any really important comments get lost in the noise

If you want to block, leave a blocking review. Many engineers seem to think it’s rude to leave a blocking review even if they see big problems, so they instead just leave comments describing the problems. Don’t do this. It creates a culture where nobody is sure whether it’s okay to merge their change or not. An approval should mean “I’m happy for you to merge, even if you ignore my comments”. 

I should mention a caveat: this depends a lot on what kind of codebase we’re talking about. For instance, I think it’s fine if PRs against something like SQLite get mostly blocking reviews. But a standard SaaS codebase, where teams are actively developing new features, ought to have mostly approvals. 

In my experience, it’s a good idea to:

Consider what code isn’t being written in the PR instead of just reviewing the diff
Leave a small number of well-thought-out comments, instead of dashing off line comments as you go and ending up with a hundred of them
Review with a “will this work” filter, not with a “is this exactly how I would have done it” filter
If you don’t want the change to be merged, leave a blocking review
Unless there are very serious problems, approve the change

Here are the main things to focus on during a code review:

## 1. Correctness

- Does the code do what it’s supposed to?
- Are edge cases and error handling covered?
- Are there any potential bugs or logic errors?

## 2. Readability

- Is the code easy to read and understand?
- Are variable, function, and class names meaningful?
- Is complex logic explained with comments or broken into smaller functions?

## 3. Inconsistency (the main one)

- Ignoring the rest of the codebase and just implementing your feature in the most sensible way
- Check if there are some specific set of helpers, you should use that helper instead of writing your code (think of error, auth, etc)
- Does this or a part of this belong in another file?
- Never start a feature without first researching prior art in the codebase
- If you don’t follow existing patterns, you better have a very good reason for it

## 4. Simplicity

- Is the solution as simple as possible?
- Is there unnecessary complexity or duplication?
- Can any part be refactored or made more concise?

## 5. Tests

- Are there sufficient automated tests for new features or bug fixes?
- Do tests cover edge cases and potential failures?
- Do all tests pass?

## 6. Security

- Are there any obvious security issues?
- Is user input validated and sanitized?
- Are secrets and sensitive data handled correctly?

## 7. Documentation

- Is the code adequately documented (comments, docstrings)?
- Are public APIs or functions explained?
- Is usage clear for other developers?

## 8. Performance

- Are there any potential performance bottlenecks?
- Is resource usage reasonable (memory, CPU, network)?
- Would this code scale if needed?

## 9. Dependencies

- Are dependencies necessary and up-to-date?
- Is third-party code used appropriately?

---

**Tip:** Focus on constructive feedback and help the author learn and improve. Remember, code reviews are a collaborative process!
