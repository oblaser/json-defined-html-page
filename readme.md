# JSON Defined HTML Page

Used to quickly create small and simple content pages. All the content is defined in the `index.json` file.
Since version 1.1.0 it's possible to define the content in `index.js`, so the page content data is loaded together with the html and not only after the page has been loaded.
For backwards compatibility the JSON file is loaded if the page data object is not defined or the JS file is not found.

## Examples
- [./web/examples](./web/examples)
- Live: <https://static.oblaser.ch/json-defined-html-page/examples>

## Common Source Code Modifications
- index.html head section: title and favicon

---

# index.js Specification

A const object has to be defined. The structure of it is the same as for the JSON file.

```
const pageData =
{
    content: [ /* ... */ ],
    footer: [ /* ... */ ]
};
```

# index.json Specification

The main object contains two arrays named `content` and `footer`, each containing content defining objects.

Optionally the `config` and/or the `defaultStyle` objects can be added.


## Content Defining Objects
Each object must provide the `type` key. Types are:


### titleX
Where X can be 1, 2, or 3.

|Key|Value Type|Description|
|---|---|---|
|`text`|string||
|`htmlStyle`|string|_optional_|


### text
|Key|Value Type|Description|
|---|---|---|
|`text`|string||
|`htmlStyle`|string|_optional_|


### link
|Key|Value Type|Description|
|---|---|---|
|`url`|string||
|`text`|string|_optional_ If not specified the display text will be the same as the url.|
|`download`|bool|_optional_|
|`newTab`|bool|_optional_|
|`htmlStyle`|string|_optional_|


### spacer
|Key|Value Type|Description|
|---|---|---|
|`value`|number||
|`htmlStyle`|string|_optional_|


### list
|Key|Value Type|Description|
|---|---|---|
|`items`|array of objects|Contains content defining objects|
|`htmlStyle`|string|_optional_|

List items are normal content defining objects, which can have additional optional keys:
|Key|Value Type|Description|
|---|---|---|
|`comment`|string|_optional_|
|`liHtmlStyle`|string|_optional_|


### html
|Key|Value Type|Description|
|---|---|---|
|`text`|string|The whole html element|


## Configuration

_object, optional_

|Key|Value Type|Default Value|Description|
|---|---|---|---|
|`maxWidth`|string|_not set_|_optional_ Max width of `#mainContainer`|
|`color1`|string|`#d3d3d3`|_optional_ Color scheme|
|`color2`|string|`#b3b3b3`|_optional_ Color scheme|
|`color3`|string|`#424242`|_optional_ Color scheme|
|`colorText`|string|`#424242`|_optional_ Color scheme|
|`colorHighlight`|string|`#4b84ff`|_optional_ Color scheme|
|`fontFamily`|string|`Helvetica, sans-serif`|_optional_|
|`center`|bool|_not set_|_optional_ Only relevant, if `maxWidth` is smaller than the window width|

## Default Styles

_array, optional_

The array contains the following objects:

|Key|Value Type|Description|
|---|---|---|
|`type`|string|One of the content defining objects `type`|
|`css`|string|The css style string|

An additional type is `listItem`, which affects each object in the `list.items` array.

Does neither affect childs of a list item nor the footer.
