
|                 | RequestDispatcher                                                                  | sendRedirect                                                                                               |
| --------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| URL             | URL is the same                                                                    | URL is changed                                                                                             |
| Request/Respone | the caller servlet forwards the request and response objects to the called servlet | new request and response objects are created                                                               |
| use case        | can be used only on the same domain                                                | required for accessing a page on a different domain. Optional for accessing a page within the same domain. |
