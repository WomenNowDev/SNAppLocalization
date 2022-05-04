# Locate Translatable Strings

Objective: learn how to locate translatable strings using the "Translate and Learn" (`glide.translate.learn`) System Property.

## Contents

- [Overview](#overview)
- [Enabling the Property](#enabling-the-property)
- [Demo](#demo)
- [Resources](#resources)

## Overview

ServiceNow does not translate custom strings. This means you need to create the translation records on the correct tables yourself. Refer to the [Custom Translations page](/Custom%20Translations.md) to learn more about this process.

The "Translate and Learn" System Property can help create the initial translation records for you. Whenever you come across a string that doesn't already have a translation record, this System Property will generate the missing record on the correct table, and fill in most of the data for you, leaving you to focus on providing the translation.

This System Property is useful and can ease the burden of needing to create 100s of records manually.

## Enabling the Property

To enable the "Translate and Learn" System Property, navigate to `System Properties > System Localization`. Check the box for the option `"Add the labels, messages, or choices to the appropriate table in English with an ending of the language code for newly added customizations that are missing translations. (Translate and Learn)"`.

To turn it off, uncheck the box.

## Demo

### Process

Here's the approach we took to make this System Property work for us:

1. Enable the property.
2. Switch your language preference to the target language.
3. Literally click through everything in your instance, especially focusing on what you know is customized like Scoped Applications. This means every List, Form and all its sections including choice dropdowns, Module in the Filter Navigator, Service Portal, Knowledge Base and Articles, Guided Tours, etc.

Note: it seems like this property will only create the stub translation records for strings on the Translated Name / Field table.

**It's important to click and open as many records as you can since this System Property will only generate the missing translation record if the form/record you clicked on has been opened at least once!**

### Example

Here is a button with text "Retry Event". Because of its prefix `TRF`, we know that this is a Translated Name / Field.

![Translate and Learn example button with text Retry Event](/images/translate-learn-example.png)

Before we enable the property, notice how there is no translation record for this string:

![Translate and Learn before stub record](/images/translate-learn-trf-before.png)

Once we enable the property and revisit the form this button is on, we see that a stub translation record has been made for us!

![Translate and Learn after stub record](/images/translate-learn-after.png)

This demonstrates the convenience of this system property. All we had to do was visit a form, and ServiceNow did the hard work for us in creating a record on the Translated Name / Field table with the Language and Value fields populated, leaving us to focus on updating the Label (translate) field to actually translate the text.

## Resources

- [Use the translate and learn property](https://docs.servicenow.com/bundle/sandiego-platform-administration/page/administer/localization/reference/r_UseTheTranslateAndLearnProperty.html)
