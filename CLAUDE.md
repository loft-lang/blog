# Working on the loft blog

This is Jurjen Stellingwerff's blog, in his voice. Read this before touching a post.

## Whose words these are

- **The author gives the subject, the reasoning and the word use.** A post says what he wants
  to say, argued the way he argues it, in words he would use speaking to someone.
- **An agent helps; it does not author.** Welcome help: language corrections, ordering,
  tightening, suggesting content or an example that supports his point, checking that a fact
  is true. Not welcome: a new argument, a new thesis, or prose that replaces his voice.
- **Nothing is published until he has approved it** — and possibly rewritten it into
  something he can see himself saying to others. A draft is a proposal, never a finished post.
- **Suggestions are offered, not applied.** Propose a change with the reason for it; apply it
  only when asked. Corrections he asked for (spelling, grammar) may be applied directly.
- **Keep facts few.** A post points readers at
  [loft-lang/loft](https://github.com/loft-lang/loft) for the detail instead of carrying
  numbers that go stale.

## How a post is made

The first post went this way, and it is the method:

1. **The author's notes.** He writes the subject and his reasoning as rough notes — what he
   wants to say, in his own terms, however unpolished.
2. **A proposal.** The agent turns the notes into a draft that keeps his points, his order of
   thought and his framing, and may suggest examples or structure that support them. It says
   which parts are its own additions, so they are easy to keep or cut.
3. **His corrections of substance.** He says where the draft misses what he meant — for the
   first post, what "inexperienced" really means and what his own role is — and the draft
   follows his meaning, not the agent's reading of it.
4. **His rewrite.** He rewrites the draft into words he would say himself. From here on the
   text is his.
5. **A review, not an edit.** The agent checks his version — spelling, grammar, a sentence
   that says something other than he means, a fact that is wrong — and lists each finding
   with a suggested fix. It changes nothing until he says which to apply.
6. **Approval, then publication.** Only the version he approved is committed to `_posts/`.

## Mechanics

- A post is `_posts/YYYY-MM-DD-title.md` with `layout: post` and `title:` front matter; the
  README has the template. GitHub Pages builds the site from `main`.
- Posts are CC BY 4.0 (`LICENSE`); code samples in posts are MIT.
- Planned subjects and their sources are in loft's
  [`doc/claude/BLOG.md`](https://github.com/loft-lang/loft/blob/main/doc/claude/BLOG.md).
