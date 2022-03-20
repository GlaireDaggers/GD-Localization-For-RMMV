# GD-Localization-For-RMMV
Super simple localization plugin for RPG Maker MV

## Plugin Parameters
* **Directory for language files** - this is the directory where language files should be stored, relative to your game's base directory. The default is to put files in /data/lang
* **Directory to search for per-map language files** - this is the directory where per-map language files should be stored. They should be named the same as the map's name (NOT its display name) with ".csv" appended (for example, if your map is MAP001, the associated language file would be MAP001.csv and would be put in this directory). The default is to put per-map files in /data/lang/maps
* **Default files to load for localization** - A list of default localization files which are loaded immediately on game startup
* **List of supported language codes** - A list of language codes which are supported by the game. This is used by the options screen to show a list of languages to choose from.
* **Default language code** - The default language to set. The default is "en-us"
* **Key column name** - The name of the column to look for localization keys. The default is "Key"
* **Localize image & sound resources** - If true, allows images, videos, & sound files to be redirected depending on the current language. The default is "true"
* **Strict error mode** - When strict mode is enabled, if any key cannot be located in currently loaded localization files an error will be displayed. Otherwise, the error will be silently logged to the console. The default is "false"

## Usage
Anywhere you'd put text which would be displayed to the player (actor names, nicknames, profiles, item names & descriptions, skill messages, event show text, system terms, etc), you can simply put in a token of the form {{PUT_KEY_HERE}}. The localization plugin will search all currently loaded localization data for a row with a key column value of PUT_KEY_HERE, and will substitute that token with the value of the current language column. If the key could not be found, or there is no language column for the current language, it will simply paste in the text PUT_KEY_HERE unless strict mode is enabled (in which case an error will be displayed and the game halted).

For image, video, & sound resources, instead of defining an arbitrary key you will put the original path to the resource in the Key column, and put a redirected path in the language column. For example:

| Key                     | Description | Comment   | en-us                   | fr                          |
| -----------             | ----------- | --------- | ----------------------- | --------------------------- |
| img/system/GameOver.png |             |           | img/system/GameOver.png | img/system/GameOver_fr.png  |

At runtime, calls to load these resources will automatically be redirected to the correct path depending on the selected language.

## Script calls
These can be called either from event script calls, or from other plugins
```
L18NManager.getLanguage(langCode)       // get the current language code
L18NManager.setLanguage(langCode)       // set the current language code
L18NManager.getLanguageList()           // get the list of supported languages
L18NManager.loadLanguageFile(langFile)  // load translations from the given localization file
L18NManager.localizeText(text)          // replace special tokens of the form {{KEY}} in the given text with translations fetched from all loaded localization files
L18NManager.localizeResource(url)       // return the path to the localized version of the given resource url, or the original url if that resource is not localized or resource localization is disabled
```
