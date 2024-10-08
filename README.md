<img alt="LessPass" src="LessPassword.png" width="210px"/>

🔑 **In browser password generator** inspired by _« [lesspass](https://github.com/lesspass/lesspass), a stateless password manager »_.

LessPass is an extremely simple offline solution based on a small HTML-CSS-JS file played in a recent web browser for the user interface and password génération.

_Managing a multitude of unique, long and complex passwords has never been easy, even with an internal or external password manager, especially when switching from one browser to another, from one computer to another and from one smartphone to another !_

> _As an astronaut friend of mine used to say : “Don't wait for this kind of mishap to happen before getting into LessPass !”_.



# Password generation

The service and the secret provided are combined and mixed using the PBKDF2 cryptographic function to produce a very large number.
This number is then used to select characters from a set set of 26 lower-case letters of the Latin alphabet (`abcdefghijklmnopqrstuvwxyz`), the 26 upper-case letters of the Latin alphabet (`ABCDEFGHIJKLMNOPQRSTUVWXYZ`), the 10 Arabic-Indian numerals (`0123456789`) and 25 special characters (`(.,;:!?)[=+-*/&|]{#$%@_~}`).

> _Some services do not allow the use of special characters in password : the service prefix `-` prevents their use._



# Service, prefix and secret

## Service

Service (and its possible prefix) is one of the two pieces of information to be provided and therefore remembered.
The service must be at least 3 characters long.

> _For best recall, it's best to choose simple, easy-to-remember forms : `gmail` and `yahoo`, for example, for the respective e-mail services, `pseudo1@gmail` and `pseudo2@gmail` to distinguish two Gmail accounts, etc…_


## Prefix

The prefix, which is optional and precedes the service, is used to influence password generation.
It must be separated from the service by at least one space and have the following form `^((\+|-)?[1-9]? +)?` (eg. at the beginning, possibly a plus or a minus, possibly followed by a digit between 1 and 9, the whole necessarily followed by at least one space).

A few commented examples of prefixed services are sometimes better than a long speech :
- `myservice`, `+ myservice`, `1 myservice` and `+1 myservice` (eg. no prefix, `+`, `1` and `+1`) target the same service `myservice` and will generate for this last one a _first full password_
- `- myservice` and `-1 myservice` (eg. `-` and `-1`) target the same service `myservice` and will generate for this last one a _first downgraded password_ without special characters (for example, in case this one doesn't allow their use)
- `2 myservice` or `+2 myservice` (eg. `2` or `+2`) target the same service `myservice` and will generate for this last one a _second full password_ (for example, if the previous first full password had to be changed for security reasons)
- `-3 myservice` (eg. `-3`) target the service `myservice` and will generate for this last one a _third downgraded password_ without special characters

> _The prefix must be separated from the service to distinguish `2 myservice` (second full password for the service `myservice`) from `2myservice` (first full password for the service `2myservice`)._


## Secret

Secret is one of the two pieces of information to be provided and therefore retained.
No complexity is required for the secret, which must be at least 3 characters long.

> _However, it is preferable to use a robust secret._



# Installation

## Computer

- Download `LessPass.html` HTML file to your computer
- Check the code
- Create a desktop shortcut that opens your favorite browser to the HTML file (the URL will look like `file:///home/me/path/to/LessPass.html`)

<img alt="Chromium" src="computer.chromium.png" width="310px"/><br/><img alt="Firefox" src="computer.firefox.png" width="310px"/>


## Smartphone

### Android

> _Direct use of the `file` schema (eg. `file:///sdcard/path/to/LessPass.html`) in the URL is made difficult by Android : it is therefore simpler to install a small web server._

- Install [Simple HTTP Server](https://play.google.com/store/apps/details?id=com.phlox.simpleserver)
- Set an empty folder as the `Root folder`
- Restrict network interfaces to `lo` (eg. `127.0.0.1`)
- Set `Autostart at boot`
- Download `LessPass.html` HTML file to the empty folder defined as `Root folder`
- Check the code
- Create a desktop shortcut that opens your favorite browser to the HTML file with `http://localhost:8080/LessPass.html` URL

<img alt="Android" src="android.simpleHTTPserver.png" height="390px"/> <img alt="Android" src="android.firefox.png" height="390px"/>


### iOS

> _TODO…_<br/>
> _no iOS system yet : help would be appreciated._



## Translation

- Open the HTML file with your favorite code editor
- In the `language` section of the `script` section, copy/paste or rename the existing `fr(){…}` function
- Rename the new function with the two letters of the desired language
- Translate the few `"character strings"` present in the new function
- Save changes
- Reload the HTML file from your favorite browser

```js
// language (use fr template to create a new language) ------------------------
// french
function fr() {
	document.documentElement.lang = "fr";
	document.head.querySelector('meta[name="description"]').content = "Générateur de mot de passe";
	…}
// deutsch
function de() {
	document.documentElement.lang = "de";
	document.head.querySelector('meta[name="description"]').content = "Passwortgenerator";
	…}
```

> _Your translation is welcome ;-)_
