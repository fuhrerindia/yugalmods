# Yugalmods
This library is successor of Yugal's main module file, extra methods for styles and other miscellaneous functions are removed from built-in `yugal.js` file in `modules/` directory, hence to use them, you need to install this library.
## yugal.include(filepath);
Adds external JavaScript to `<body>` script added by this method can not undone. This can not be undone. Accepts one argument as JS path in string.
## yugal.files(arrayofpaths);
This function accepts array of paths of JS files which you want to add into the `<body>`. It is similar to `yugal.include` but can add multiple files at once.
## yugal.style(cssobject);
Accepts a JS object which contains CSS Style and converts it to valid CSS string.
Example
```js
    const css = {
    fontSize: 10,
    color: "#000000",
    background: "red"
    };
    console.log(yugal.style(css));
    //Returns "font-size:10px;color:#000000;background:red;"
```
_Property name in css object should be in camel casing_
## yugal.css(css_style, element);
This function accepts CSS Style in first parameter and the target element in second parameter. CSS Style can JS Object or CSS String both.
```js
const some_style = {
color:"red",
fontSize:20
};
yugal.css(some_style, "#thisdiv"); //#thisdiv is used to target an element with 'thisdiv' id. Its rule is same as CSS.
//ABOVE IS VALID STRING

const another_style = "color:red;font-size:20px";
yugal.css(another_style, "#thisdiv"); //THIS IS ALSO VALID
```
## yugal.StyleSheet
This is a set of functions related to styles.
### yugal.StyleSheet.create(object, target_type);
Accepts CSS object in first parameter. It should be collection of objects in one parent object with keys as target elements. Second parameted is optional, but accepts a string if provided then it will change target type among class, id and tags. This function returns CSS string, which can be furter used in `yugal.StyleSheet.inject` or equivalent functions.
```js
yugal.StyleSheet.create({
mydiv: {color:"#000", textDecoration: 'none'},
abc: {fontSize:30}
}, "#"); 
//This will apply respective css property to id mydiv and abc. Instead of
// '#' use '.' for class and leave blank for  tags. 
```
### yugal.StyleSheet.inject(css_string);
Accepts css design string and inject it to DOM.
```js
a = "h1{font-size:40px;}";
yugal.StyleSheet.inject(a);
```
### yugal.StyleSheet.import(css_file_path, id)
This function will accept first parameter as file path to external CSS file and second parameter as id to be parsed to the <link> tag generated. It also returns generated tags.
```js
a = yugal.StyleSheet.import('abc.css', 'thistag');
```
Above code will inject HTML below to `<head>`
```html
<link rel="stylesheet" type="text/css" href="abc.css" id="thistag" />
```
You can manipulate it as below
```js
a.setAttribute("href", "def.css");
a.remove();
// variable `a` is defined above 
```
When this function is called, whole `<head>` tag is rebuilt, resulting in loading `<head>` contents like loaded files again. So use of this function should be limited. Use this function wisely.