| ARIA Attribute   | Purpose                                                                   | Example Usage                                             |
|------------------|---------------------------------------------------------------------------|-----------------------------------------------------------|
| aria-label       | Provides a string label when a visible label is not present               | `<button aria-label="Close"></button>`                    |
| aria-labelledby  | References another element that labels this element                       | `<div role="dialog" aria-labelledby="modal-title"></div>` |
| aria-describedby | References another element that provides descriptive text                 | `<input aria-describedby="email-help">`                   |
| aria-hidden      | Indicates that the element is not visible to assistive technologies       | `<div aria-hidden="true">Decorative</div>`                |
| aria-expanded    | Indicates if an element like a menu or accordion is expanded or collapsed | `<button aria-expanded="false">Show Menu</button>`        |
| role             | Defines the type of widget or landmark the element represents             | `<div role="alert">Error message</div>`                   |
