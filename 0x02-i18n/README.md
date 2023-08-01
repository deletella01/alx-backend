##  i18n

The normal workflow when making an application available in multiple languages is to mark all the texts that need translations in the source code. After the texts are marked, Flask-Babel will scan all the files and extract those texts into a separate translation file using the gettext tool. Unfortunately this is a tedious task that needs to be done to enable translations.

The way texts are marked for translation is by wrapping them in a function call that as a convention is called _(), just an underscore. The simplest cases are those where literal strings appear in the source code.

The idea is that the _() function wraps the text in the base language (English in this case). This function will use the language selected by the get_locale() function to find the correct translation for a given client. The _() function then returns the translated text, which in this case will become the argument to flash().

Unfortunately not all cases are that simple. 

This text has a dynamic component that is inserted in the middle of the static text. The _() function has a syntax that supports this type of texts, but it is based on the older string substitution syntax.

There is an even harder case to handle. Some string literals are assigned outside of a request, usually when the application is starting up, so at the time these texts are evaluated there is no way to know what language to use. An example of this is the labels associated with form fields. The only solution to handle those texts is to find a way to delay the evaluation of the string until it is used, which is going to be under an actual request. Flask-Babel provides a lazy evaluation version of _() that is called lazy_gettext().

Here I'm importing this alternative translation function and renaming to to _l() so that it looks similar to the original _(). This new function wraps the text in a special object that triggers the translation to be performed later, when the string is used.

The Flask-Login extension flashes a message any time it redirects the user to the login page. This message is in English and comes from the extension itself. To make sure this message also gets translated, I'm going to override the default message and provide my own, wrapper with the _l() function for lazy processing.
