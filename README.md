GmailSendLater is a [Google Apps
Script](http://code.google.com/googleapps/appsscript/) that lets you send a Gmail draft at a specified time in the future. If you're writing work emails at 2am but want to preserve the illusion of work-life balance, you can use this script to sleep in and have the emails automatically sent at 9am as if they were sent by a normal human.

## Installation

TODO

## Usage

1. Create a draft that you would like sent.
2. To have that draft sent at 9am tomorrow, add a new label to the thread containing the draft named "send at 9am tomorrow".
3. The draft will automatically be sent at 9am tomorrow by Google's servers. You don't have to be logged into Gmail or even have your computer on.

You can use natural language to express the time at which the email should be sent. Try out different expressions at the [SugarJS Dates site](http://sugarjs.com/dates). If GmailSendLater doesn't understand the time you typed, it will add the **GmailSendLater/error** label to the thread and the draft will **not** be sent.

GmailSendLater will automatically delete these labels after the drafts have been sent, to avoid cluttering your Gmail account.

## Features & Limitations

Features:
* The time at which a draft should be sent is specified via a label, so the formatting of the draft is not affected by GmailSendLater.
* You can easily send a bunch of drafts at a specific time, by labeling them all at once.
* Threading with drafts is preserved, just as if you hit the "send" button yourself.
* You can verify that GmailSendLater understands when you want a draft to be sent (see *Technical Details*).

Known limitations:
* If there are multiple drafts per thread, they will all be sent at the same time via GmailSendLater (since labels are per-thread, not per-message).

TODO

* none currently

## Technical Details

TODO: move to blog post

GmailSendLater runs, by default, every 15 minutes. Thus, drafts will generally be sent within 15 minutes of the precise sending time you specify.

Sending a draft is a 3-step process:
1. You label the draft with a label like "send at 2pm"
2. GmailSendLater runs, and replaces your label with a new label like *GmailSendLater/sending_at Thursday, February 13, 2014 2:00:00 PM GMT-0900*. This allows you to *verify* that GmailSendLater understands when to send the draft. If you remove this *GmailSendLater/sending_at* label, the draft will not be sent.
3. GmailSendLater sends any drafts that should be sent at the current time.

GmailSendLater keeps a log as a [Script Property](https://developers.google.com/apps-script/guides/properties). You can examine the log in the Google Apps Script editor via: the *File* menu: File->Project properties->"Project properties" tab->*log* property.

GmailSendLater interprets the sending time using the timezone of the draft email, as the script isn't necessarily running in the same timezone as the user. You can always specify a 

## Shout-outs

I was inspired to write this by the [Gmail Delay Send script](https://code.google.com/p/gmail-delay-send/) which offers similar functionality with a different UI. Check it out: maybe you'll like it better!

GmailSendLater uses the excellent [SugarJS library](http://sugarjs.com) from Andrew Plummer, which makes the code a lot cleaner.

GmailSendLater uses the Google Apps Script version of [QUnit](http://qunitjs.com/)