# Keyboard packaging

To package the keyboard with Presage support, you need to get keyboard
layout described in QML and its configuration file.

If you have a favorite keyboard, pull its files from device at
`/usr/share/maliit/plugins/com/jolla/layouts` or similar location. In
this example, I used Estonian keyboard and pulled
`et.qml`. 

Configuration file may or may not exist as a separate entity together
with QML file. However, syntax is rather simple and its easy to write
a new one. 

As a first step, rename keyboard QML file into something unique. I
used `et-presage.qml`. If there is configuration file, rename it
accordingly or create one. In the case of Estonian keyboard,
configuration file is `et-presage.conf`.

Next, adjust the configuration file to be something like

```
[et-presage.qml]
name=Eesti (Presage)
languageCode=et_EE
handler=PresageInputHandler.qml
```

Notice that `[]` refers to QML configuration and you provide
user-visible _name_ and _language code_. The _name_ will be appear in the Settings menu, so you should suffix it with (Presage) for e.g. to make it distinguishable from the original layout. As for Presage support, you
specify the handler.

To package the new keyboard, you could use the script
`utils/keyboard/package-keyboard.sh`:

```
utils/keyboard/package-keyboard.sh Language langcode version keyboard.qml keyboard.conf
```

where 

* Language: Specify language in English starting with the capital letter, ex 'Estonian'
* langcode: Specify language four-letter code, ex 'et_EE'
* version: Version of the language package, ex '1.0.0'
* keyboard.qml: Keyboard QML file
* keyboard.conf: Keyboard Configuration file referencing the QML file

When finished, the keyboard support will be packaged into RPM in the
current directory. The script requires rpmbuild to be installed. Note
that rpmbuild can be installed on distributions that don't use RPM for
packaging.

In case of Estonian keyboard:

```
utils/keyboard/package-keyboard.sh Estonian et_EE 0.1.0 keyboards/et-presage.qml keyboards/et-presage.conf
```

