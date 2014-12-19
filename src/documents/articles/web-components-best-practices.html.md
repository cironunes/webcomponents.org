---
title: Web Components Best Practices
author: addy_osmani
date: 2013-11-15
image: web-components-best-practices.jpg
category: articles
layout: single
tags: ['Best Practices']
---

Web Components (WC) fall under a new platform feature that we'd like developers
to start embracing. The following is an initial list of best practices we
advocate component authors consider to ensure their elements are good citizens
in the WC ecosystem.

<!-- Read more -->

1. **Namespacing** Custom elements must have a dash in their name. The text
   before the dash is effectively a namespace. You want to keep it short but
   also unique. Try not to overlap on someone else's prefix if possible. Only
   use a prefix shorter than three characters if you already have lots of
   developer interest in your set of components.
2. **Mimic built-in elements as closely as possible** Your component should feel
   just like any other natively implemented element to developers (other than
   the import, of course). If in the future you're formally speccing your
   element's API, will you feel embarrassed by how different it feels?
3. **Failing silently is **golden** Components should act like native DOM
   elements, so avoid creating elements that throw JS errors from ordinary DOM
   interactions, for example: you can place a `<div>` inside a `<ul>`, and while
   it may not behave or render normally, it shouldn't throw errors either.
4. **Attributes for data in** Use attributes to pass configuration in. Use
   boolean attributes for boolean values. Ex: `<my-element selected>` instead of
   `<my-element selected="true">`.
5. **Events for data out** Use custom events to pass information out of
   components unless the information to pass is large or changes extremely
   often.
6. **Include Dependencies**. Include all dependencies your component needs.
   Don't worry if that means including redundant `<link rel="import" ...>`; as
   long as you set appropriate cache headers, these will only be fetched and
   loaded once. Using SPDY can reduce the cost of having multiple files, or you
   can concatenate and minify them into a single file when you deploy your app.
7. **Document your component** Document your component so that others know how
   to use it. Components have many aspects that count as part of their API,
   including things that you might not think of as part of the API.
    * Attributes can be described concisely with example markup.
    * If one component is designed to be nested inside another one, show it
      being used in that context.
    * List its JavaScript methods and properties.
    * List its events.
    * When using Shadow DOM, the `<content>` element and "select" attribute
      allow you to select which nodes to put where. If your component treats
      different elements specially in these selectors, document it!
    * If your component relates to a microdata format, document how to apply
      that microdata to your component.
14. **Don't put too much in Shadow DOM**. Shadow DOM allows you to stuff a bunch
    of complex junk out of sight. However, that's not an excuse to have as many
    DOM elements as you want in your shadow, as more elements will still lead to
    worse performance. In addition, try to keep your configuration and state
    visible by keeping anything semantic exposed in the logical DOM. Cruft goes
    in the Shadow; semantic stuff doesn't.
15. **Don't create more custom elements than you need** If you have two similar
    custom elements and the only difference between them is a different visual
    structure/display of the same data, consider consolidating them into one
    element and create two different templates to switch between.
16. **Harmonize your declarative and imperative APIs** Attributes form (part of)
    your declarative API; your prototype defines your imperative API. Try to
    keep the analogous parts linked whenever possible so a user can modify
    either with the same effect.
17. **Don't presume the context you'll operate in** If your component is
    successful, it will be used in contexts you never expected, and mixed in
    with components you've never heard of. Strive to be as encapsulated and
    flexible--don't rely on any external frameworks or structure wherever
    possible.

## As always, don't forget...

A successful web component will be used by many people in many different
contexts--meaning that following general web development best practices becomes
even more important.

1. **Accessibility** Make your component accessible by using appropriate ARIA
   roles—something that is much more important when we're creating new types of
   elements! In cases where inheritance from a semantic base element is for any
   reason impossible or infeasible, be sure to add a `role=""` attribute, if any
   apply.
2. **Performance** If you use a callback-based API for long-running operations,
   don't block the main thread excessively. Debounce methods and logic loops
   that affect rendering performance using requestAnimationFrame as a queue.
   Respond to being removed from the tree by suspending expensive operations
   like animation—and don't start expensive operations until you're actually
   inserted into the DOM.
3. **Script isn't always the answer** Many structure and style techniques that
   once required JavaScript can now be accomplished with pure CSS in the world
   of web components.
4. **Be Responsive** Where possible, and applicable, design your components so
   that they responsively adapt to their environment. Your users may use your
   component for things you never dreamed of.
