# Custom Translations

Objective: learn how to translate custom strings in ServiceNow.

## Contents

- [Overview](#overview)
- [Demo](#demo)

## Overview

Out-of-box, the default language strings have records in the five translation tables. If a Language Pack plugin is installed, then each of these strings also have a record for that language in the translation tables. This isn't the case for custom strings not created by ServiceNow. Each custom string will need to have its own record created in the translation tables for the target language. Some of this work can be done by following the information discussed in [Debug Translations](/Debug%20Translations.md) and [Locate translatable strings](/Locate%20translatable%20strings.md).

## Demo

### MSG

![MSG Prefix Service Portal example](/images/msg-prefix-example.png)

This is what the `MSG` prefix looks like for a string displayed from a widget in the Service Portal. The Body HTML template of this widget is:

```text
${I have a MSG Prefix and a record in the Messages table}
```

This syntax of `${}` is looking up the Messages (`sys_ui_message`) table where the `Key` field matches `I have a MSG Prefix and a record in the Messages table`. The Body HTML template of the widget will display the `Message` field of this corresponding Message record, which is currently "I have a MSG Prefix and a record in the Messages table".

The Message record looks like:

![MSG Prefix Messages record example](/images/msg-record-example.PNG)

Since the `Key` field matches the `Message` field, the text from the widget shows "I have a MSG Prefix and a record in the Messages table". However, what happens if the `Message` field is updated? Let's change it to "I have changed the Message field".

![MSG Prefix Messages record changed example](/images/msg-record-changed.PNG)

Notice how the widget output has changed to the new `Message` field value as well, all without having to change the widget code itself!

![MSG Prefix Service Portal changed example](/images/msg-prefix-changed.PNG)

When a user switches their language preferences, this message record needs to have a record where the Language value is that target language so that ServiceNow can show the translation.

In this instance, Dutch is installed so that means that there needs to be a Message record where the Language is Dutch, key is "I have a MSG Prefix and a record in the Messages table", and the Message will be the Dutch translation.

![MSG Dutch example](/images/msg-record-dutch.png)

Let's switch our language to Dutch and revisit the Portal. See how the widget output is now showing the Message from the Dutch version of the message record?

![MSG Dutch example on Portal](/images/msg-record-dutch-example.png)

### TRF

![MSG Dutch example translation missing](/images/trf-dutch-translation-missing.png)

The [nl] in the button label comes from the "Translate and learn" system property. This property already created the translation record for us, we just need to update the Label (translate) field to have it show the desired translation when a user has the Dutch language set in their preferences.

![TRF Dutch translation record](/images/trf-dutch-translation-record.png)

In an actual translation process, you would want to change the Label (translate) field from Retry Event[nl] to the Dutch translation, but for this demo let's change it to "Retry Event Dutch Translation demo".

![TRF Dutch translation label change](/images/trf-dutch-translation-label-demo.png)

The button now shows what we entered in the Label (translate) field when our language is set as Dutch!

![TRF Dutch translation label in Dutch](/images/trf-dutch-translation-label-dutch.png)
