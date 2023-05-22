# Frontend
- [Pseudo-classes and Pseudo-elements](#pseudo)


## Pseudo-classes and Pseudo-elements <a name="pseudo"></a>
- pseudo-classes - are used to change css when the element is in specyfic state:
``` css
/* mouse over link */
a:hover {
  color: #FF00FF;
}
```
- pseudo-elements - are used to style specified parts of an element:
``` css
/* insert some text after the content of each <p> element*/
p::after {
  content: " - Remember this";
}
``` 