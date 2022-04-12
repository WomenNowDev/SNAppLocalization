# Debug Translations

Objective: learn how to debug translations with the "Display translation prefix on translatable strings" `(glide.ui.i18n_test)` System Property.

## Contents

- [Overview](#overview)
- [Enabling the Property](#enabling-the-property)
- [Demo](#demo)
- [Multiple Prefixes](#multiple-prefixes)
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

The `MSG` prefix represents any string that is wrapped in the appropriate Message API (`getMessage()`, `gs.getMessage()`, `${...}`) in Client or Server Scripts, including Service Portal widgets.

![MSG Prefix example](/images/msg-prefix-example.png)

### CHC

The `CHC` prefix represents all text that is displayed as a choice list. For example, the "State" field choice list on Incidents showing "New", "In Progress", "On Hold" and so on.

![CHC Prefix example](/images/chc-prefix-example.PNG)

### GMLD

The `GMLD` prefix represents all field labels on lists and forms. Here's the list view for Incidents showing that the field labels for "Number", "Opened", "Short description" and "Caller" have the `GMLD` prefix:

![GMLD Prefix List example](/images/gmld-prefix-list-example.png)

Opening up an Incident and viewing the form, the prefix is also displayed on the field labels there as well:

![GMLD Prefix Form example](/images/gmld-prefix-form-example.png)

### TRF

The `TRF` prefix represents texts from fields where that field type is `translated_field` in its Dictionary. To see which fields those are in your instance, search this query on the `Dictionary Entries` table: `internal_type=translated_field`. In general, these are fields like Titles, Names or Short descriptions.

The `Title` field of a Catalog is an example of the `TRF` prefix:

![TRF Prefix example](/images/trf-prefix-example.png)

### TRT

The `TRT` prefix is similar to the `TRF` prefix in that its based on the field type in its Dictionary. But instead of `translated_field`, the `TRT` prefix is based on the types `translated_text` and `translated_html`. To see which fields those are in your instance, search this query on the `Dictionary Entries` table: `internal_type=translated_html^ORinternal_type=translated_text`. In general, these are fields like Descriptions.

The `Short description` and `Description` fields of a Record Producer are examples of the `TRT` prefix:

![TRT Prefix example](/images/trt-prefix-example.png)

### Hard-coded String

If there's a string that doesn't have any prefix attached to it, that means it's hard-coded in your script! This lets you know what text needs to be converted with the Messages API so ServiceNow knows to translate it.

The first message has the `MSG` prefix since it was created using this syntax `${I have a MSG Prefix and a record in the Messages table}`. However, the string below has no prefix at all since it was hard-coded to be `"I am hard-coded and have no prefix attached"`.

![No Prefix example](/images/no-prefix-example.png)

## Multiple Prefixes

As you explore your instance with this System Property enabled, you may come across a string that has multiple prefixes on it.

Consider the `Resolution code` on Incidents. The "None" option looks like `MSG: CHC: -- None --`.

![Multiple Prefixes example](/images/multiple-prefixes-example.png)

What does this mean and how would you know which table to look at? The `CHC` prefix is telling us that the "None" option is a choice to select as a Resolution code. However, the actual text of "-- None --" is stored as a Message, which is what the `MSG` prefix indicates. If you look at the choices for the Resolution code, "-- None --" doesn't appear as a record:

![Incident Resolution code choices](/images/multiple-prefixes-choices.png)

But, "-- None --" does appear as a record on the Messages table, which is what the prefix told us!

![None Messages record](/images/multiple-prefixes-msg.png)

Based on this, we recommend looking at the outermost prefix first to try and identify which table a string is from.

## Resources

- [Debug translations](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/localization/task/t_DisplayATranslationPrefix.html)
- [How to enable/disable prefixes on field labels for the current user session?](https://support.servicenow.com/kb?id=kb_article_view&sysparm_article=KB0749217)
- [Translation tables](https://docs.servicenow.com/bundle/sandiego-platform-administration/page/administer/localization/reference/r_TranslationTables.html)
