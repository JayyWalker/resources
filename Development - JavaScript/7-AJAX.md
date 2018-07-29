AJAX allows web pages to be updated without refreshing the whole page using XMLHttpRequest and JSON, a lightweight data-interchange format, which is easy to read and write.



JSON
JSON stands for 'JavaScript Object Notation', it is a transport language for Javascript.  All keys and strings are in double quotes ("")

Javascript to JSON

var person = {name: 'fred'};
var personJSON = JSON.stringify(person);
JSON to JavaScript

var personJSON = '{"name": "fred"}';
var person = JSON.parse(personJSON);


AJAX
AJAX stands for 'Asynchronous JavaScript and XML' and is a way to call a server to get data

Javascript syntax

var xmlhttp = new XMLHttpRequest();

xmlhttp.onreadystatechange = function() {
console.log('state changed', xmlhttp.readyState);
if (xmlhttp.readyState === XMLHttpRequest.DONE ) {
if (xmlhttp.status === 200) {
console.log('response: ', xmlhttp.responseText);
console.log('parsed: ', JSON.parse(xmlhttp.responseText));
}
 else if (xmlhttp.status === 404) {
alert('The resource was not found');
}
else {
alert('Error: Call to server failed with code: ' + xmlhttp.status);
}
}
};

xmlhttp.open("GET", "https://jsonplaceholder.typicode.com/users/1", true);
xmlhttp.send();
JQuery syntax

$.ajax({
method: 'GET',
context: document.body,
url: '//api.github.com/users/helencodes'
}).done(function(response){
console.log(response);
}).fail(function(error){
console.error(error);
}).always(function(){
console.info("ajax call made");
});
