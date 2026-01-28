# [28.01.26]

- add new link for the img as old wasn't working.
- learnt where I might need :first-child or :last-child
- learnt about <i>transitionend</i> , it returns the propertyName of the transition ended;
- how to toggle class.


### Problem I faced :

while I was writing translateY for the first and last child of panel class , I got stuck as CSS was not applying for last-child and when checked on CHATgpt I found the reason was a comma after a property.

CSS is read **top to bottom**, **character by character**.

When the browser sees:

```
.panel.open-active > *:first-child {transform: translateY(0);};
```

it expects this pattern:

```
selector { property: value; }
```

But it gets:

```
selector { property: value; } ;
                             ↑ unexpected token
```

That **extra ; has no meaning in CSS grammar**.

CSS parsers follow a rule called **error recovery**:

> “If something doesn’t make sense, skip until you can safely continue.”
> 

But here’s the twist:

- Inside a stylesheet, a stray token like ;
- **outside of any rule**
- gives the parser *no safe place to recover*

So it goes:

> “I don’t know what this is… I’ll ignore everything after this.”
>