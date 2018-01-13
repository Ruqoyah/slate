# Errors

<aside class="notice">This error section is stored in a separate file in `includes/_errors.md`. Slate allows you to optionally separate out your docs into many files...just save them to the `includes` folder and add them to the top of your `index.md`'s frontmatter. Files are included in the order listed.</aside>

The Kittn API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks.
401 | Unauthorized -- Your token in wrong or you don't provide a token.
403 | Forbidden -- You tried to delete other people's recipe.
404 | Not Found -- The specified page could not be found.
409 | Conflict -- You used an information that already exist.
500 | Internal Server Error -- We had a problem with our server. Try again later.
