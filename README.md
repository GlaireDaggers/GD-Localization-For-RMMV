# GD-Localization-For-RMMV
Localization plugin for RPG Maker MV

## Script calls

```
L18NManager.setLanguage(langCode) // set the current language code
L18NManager.loadLanguageFile(langFile) // load translations from the given localization file
L18NManager.localizeText(text) // replace special tokens of the form {{KEY}} in the given text with translations fetched from all loaded localization files
```
