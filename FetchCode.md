# FetchCode

Objective: learn how to use the FetchCode tool to identify hard-coded strings in the instance.

## Contents

- [Overview](#overview)
- [Where to Download](#where-to-download)
- [Finding Hard-coded Strings](#finding-hard-coded-strings)
- [Demo](#demo)

## Overview

FetchCode is an instance code search utility. This project on ServiceNow Share helps find code in your instance. You give it a search term, and it will show you all records in your instance that have that search term. It's a great tool that can save you a lot of time and effort from having to manually search every table and field for the search term you're looking for!

## Where to Download

[Download FetchCode here](https://developer.servicenow.com/connect.do#!/share/contents/1176688_fetchcode_an_instance_code_search_utility?v=2&t=PRODUCT_DETAILS)

## Finding Hard-coded Strings

One of the challenges with localizing your custom strings is identifying and converting all hard-coded strings to the appropriate Message API (`gs.getMessage()`, `getMessage()`, `${...}`). This task must be done if you need the strings in your scripts to be translated.

Here's how FetchCode can help with this challenge:

1. Scripts that contain the following APIs listed in this table are the most likely to have hard-coded strings, since they display some sort of message.
2. Enter each API as a search term in FetchCode to get all scripts that call these functions.
3. Review each script and check if any of the string inputs to the API are hard-coded.
4. If they are, the Localized Example column shows how you would want to change the hard-coded string so that it's able to be translated.

| API | Type | Localized Example |
| ----|------|-------|
| `addDecoration` | `g_form` | `g_form.addDecoration('caller_id', 'icon-star', getMessage('Mark as Favorite'), 'color-green');` |
| `addErrorMessage` | `gs` `g_form` | `gs.addErrorMessage(gs.getMessage('Error message'));` `g_form.addErrorMessage(getMessage('Error message'));`|
| `addFormMessage` | `g_form` | `g_form.addFormMessage(getMessage('info message'), 'info'));` |
| `addInfoMessage` | `gs` `g_form` `spUtil` | `gs.addInfoMessage(gs.getMessage('info message'))` `g_form.addInfoMessage(getMessage('info message'))` `spUtil.addInfoMessage(getMessage('info message'))` |
| `addTrivialMessage` | `spUtil` | `spUtil.addTrivialMessage(getMessage('Thanks for your order'));`|
| `alert` | `Client` | `alert(getMessage('alert message'));` |
| `confirm` | `Client` | `confirm(getMessage('confirm message'));` |
| `getEscapedMessage` | `gs` | `gs.getEscapedMessage(gs.getMessage('My message'));`|
| `prompt` | `Client` | `prompt(getMessage('prompt message'));` |
| `sendLiveMessage` | `spAriaUtil` | `spAriaUtil.sendLiveMessage(getMessage('live message'));` |
| `setError` | `GlideElement` | `current.field.setError(gs.getMessage('error message'));` |
| `setLabelOf` | `g_form` | `g_form.setLabelOf(field, getMessage('field label'));` |
| `showErrorBox` | `g_form` | `g_form.showErrorBox(field, getMessage('error box'));` |
| `showFieldMsg` | `g_form` | `g_form.showFieldMsg(field, getMessage('field msg'));` |

This list is as comprehensive as possible, but it probably doesn't cover everything. If anything, consider this a good starting point that should cover the most frequent / commonly used message APIs.

## Demo

This demo will show how to use FetchCode following the four steps outlined above.

![What FetchCode looks like when you first open it](/images/fetchcode-initial.png)

This is what FetchCode looks like when you first open it. Let's search for `confirm(` and see what happens.

After entering this search term, FetchCode shows all records with `confirm(` in it under the "Code Search Results" column. These results show you how many instances of the search term appear by table.

![FetchCode results](/images/fetchcode-results.png)

You're able to expand each of these headings to see which field on the table contains the search term.

![FetchCode results detail](/images/fetchcode-result-details.png)

This tells us that 39 Client Scripts have `confirm(` in the Script field, and that 15 Widgets have `confirm(` in the Client Controller and Link fields.

By expanding the headers even more, you will get a list of the actual records themselves. Clicking on the record will show you a preview of it on the right-hand column.

Let's preview one of the Client Script records.

![FetchCode Preview](/images/fetchcode-preview.png)

As the result shows, this script does have `confirm(` and we've found a hard-coded string that needs converting!

You want to repeat this process for each search term, and look over every result listed in the "Code Search Results" to find as many hard-coded strings as possible.
