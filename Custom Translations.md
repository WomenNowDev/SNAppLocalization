# Custom Translations

Objective: learn how to translate custom strings in ServiceNow.

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