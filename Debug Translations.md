# Debug Translations

Objective: learn how to debug translations with the "Display translation prefix on translatable strings" `(glide.ui.i18n_test)` System Property.

## Contents

- [Overview](#overview)
- [Enabling the Property](#enabling-the-property)
- [Demo](#demo)
- [Resources](#resources)

## Overview

This System Property is a useful tool for identifying translation gaps in the application. It will display a prefix before each string which identifies the translation table the string comes from:

| Prefix | Table|
|--------| -----|
| `MSG`| Messages (`sys_ui_message`)|
|`CHC`| Choice (`sys_choice`)|
|`GMLD` | Field Label (`sys_documentation`)|
|`TRF`| Translated Name / Fields (`sys_translated`)|
|`TRT`| Translated Text (`sys_translated_text`)|

This is helpful because if there is something unexpected with the translation of the string, you have an idea of which table you need to look at in order to debug the translation.

Another thing this system property will help you identify is hard-coded strings. If you come across a string in your instance that doesn't have any of the five prefixes, that means the system was unable to locate a translation record for that string, meaning it's hard-coded!

## Enabling the Property

To enable the "Display translation prefix on translatable strings" System Property, navigate to `System Localization > Enable I18N Debugging`. When you enable this property, notice that there are now prefixes attached to the strings in your instance, if they aren't hard-coded.

To turn it off, use `System Localization > Disable I18N Debugging`.

## Demo

This demo will show examples of the different prefixes and how they work.

### MSG

The `MSG` prefix represents any string that is wrapped in the appropriate Message API (`getMessage()`, `gs.getMessage()`, `${...}`) in client or server scripts, including Service Portal widgets.

![MSG Prefix example](/images/msg-prefix-example.png)

### CHC

The `CHC` prefix represents all text that is displayed as a choice list. For example, the "State" field choice list on Incidents showing "New", "In Progress", "On Hold" and so on.

![CHC Prefix example](/images/chc-prefix-example.PNG)

### GMLD

The `GMLD` prefix represents all field labels on lists and forms.

### TRF

### TRT

### Hard-coded String

## Resources

- [Debug translations](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/localization/task/t_DisplayATranslationPrefix.html)
- [How to enable/disable prefixes on field labels for the current user session?](https://support.servicenow.com/kb?id=kb_article_view&sysparm_article=KB0749217)
