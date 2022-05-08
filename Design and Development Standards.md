# Design and Development Standards

Objective: learn design and development standards to make it easier to localize custom strings.

## Contents

- [Avoid Concatenated Strings](#avoid-concatenated-strings)
- [Don't use Display Values in Script Logic](#dont-use-display-values-in-script-logic)
- [Name gs.getMessage keys like Code Variables](#name-gsgetmessage-keys-like-code-variables)
- [Use gs.getMessageLang when executing as System or Background User](#use-gsgetmessagelang-when-executing-as-system-or-background-user)

## Avoid Concatenated Strings

String concatenation is adding multiple strings together into a single sentence. An example of string concatenation is:

```javascript
gs.getMessage('You have ' + numItems + ' active requests.');
```

While this sentence makes sense in English, it might not in other languages due to different grammatical structures and rules. Translators might need to change the word order of a sentence, but that would be hard to do if the sentence is split into multiple strings.

Rather than concatenating strings, the best thing to do would be to phrase your sentences so concatenation is not needed. It's best to have a logically, complete sentence since it's easier to translate and test, like so:

```javascript
gs.getMessage('Number of active requests: {0}', numItems);
```

## Don't use Display Values in Script Logic

Most fields have a Value and Display Value. Consider the Priority field on an Incident. The Display Value could be "3 - Moderate", which is what the user sees when viewing the field, but the underlying Value is "3".

```javascript
incidentGR.priority.getDisplayValue() // 3 - Moderate
incidentGR.priority.getValue() // 3
```

Script Logic shouldn't use Display Values when checking the value of a field, since the Display Value will be different depending on the language of the user.

A script like:

```javascript
// Incorrect
if (field.getDisplayValue() == 'Yes') {
    // do something
}
```

will only work in English. When a user has a language other than English set, this condition will fail since the Display Value will be a translated version of "Yes". The translated version of Yes != the English version of Yes.

Instead, use the Value of fields. The Value will always be the same regardless of the language.

```javascript
// Correct
if (field.getValue() == 'Yes') {
    // do something
}
```

## Name gs.getMessage keys like Code Variables

A better practice to using `gs.getMessage()` is to make your keys be something similar to code variables rather than the actual message you want to display.

```javascript
gs.getMessage('I have a MSG Prefix and a record in the Messages table'); // typical use case, making the key be the message you want to display
gs.getMessage('widget_message'); // better approach, make the key be a variable-like message
```

![gs.getMessage key example](/images/get-message-key-example.png)

When a `gs.getMessage` call can't find the Messages record with that key, it will just display the key and not the value that corresponds to that key.

By using a code variable-like structure as our keys, we can easily tell that the key "widget_message" is missing a corresponding Messages record. It would be harder to tell at first glance if the key "I have a MSG Prefix and a record in the Messages table" does actually have a Messages record, since the output we're seeing seems like something we actually want displayed to the user, unlike "widget_message".

Making your keys in this fashion will make it easier to see when you're missing a Messages record for that string, and will help you in the process of locating missing translations.

## Use gs.getMessageLang when executing as System or Background User

```javascript
gs.getMessageLang('message_key', 'language_id');
```

This is an undocumented method that is used to retrieve content on behalf of someone else. It is similar to `gs.getMessage()`, but the second parameter allows you to specify which language you want the message returned in.

This method is useful in situations when `gs.getMessage()` is not enough. `gs.getMessage()` only applies to the logged-in user. When a script is executing as the System or in the background, the English version is always returned, which is not ideal when you want a different language version of the text.

### Demo

This example will show the difference between `gs.getMessage` and `gs.getMessageLang` when the user's language is set as English and Dutch.

Here is the English language version of the Message:

![MSG Record example English](/images/msg-record-example.PNG)

Here is the Dutch language version of the Message:

![Msg Record example Dutch](/images/msg-record-dutch.png)

This script is run using the System Definition > Scripts - Background module as the System user:

```javascript
//execute one second after running this script
var gdt = new GlideDateTime();
gdt.addSeconds(1)
gs.info(gdt);

var script = "gs.info('Language setting is: ' + gs.getUser().getLanguage()); gs.info(gs.getMessage('I have a MSG Prefix and a record in the Messages table'));";

//create the sys_trigger record to be executed by the schedule worker thread
var sched = new ScheduleOnce();
sched.script = script;
sched.setTime(gdt);
sched.setLabel("run this as system");
sched.schedule();
```

No matter if the user's language is set as English or Dutch, the Log table shows that the output of the script is:

`Language setting is: en` and `I have a MSG Prefix and a record in the Messages table`.

Now try running this script, which uses `gs.getMessageLang()` to specify the Dutch language instead:

```javascript
//execute one second after running this script
var gdt = new GlideDateTime();
gdt.addSeconds(1)
gs.info(gdt);

var script = "gs.info('Language setting is: ' + gs.getUser().getLanguage()); gs.info(gs.getMessageLang('I have a MSG Prefix and a record in the Messages table', 'nl'));";

//create the sys_trigger record to be executed by the schedule worker thread
var sched = new ScheduleOnce();
sched.script = script;
sched.setTime(gdt);
sched.setLabel("run this as system");
sched.schedule();
```

The output shows:

`Language setting is: en` and `Dutch Translation here`!
