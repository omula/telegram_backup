# Telegram_Backup
Copyright 2017 Fabian Schlenz  
Licensed under GPLv3

## Description
This is a small Java app that allows you to download all your history from
Telegram's servers and keep a local copy of them.

## Download
You can find the whole app packed into one fat jar file under
[releases](https://github.com/fabianonline/telegram_backup/releases).

## Features
* You can use multiple accounts with this tool.
* Messages are saved in a SQLite database; media (documents, photos, videos,
  stickers, geolocations, audios) are downloaded and saved as files.
* A GUI is planned for later; at the moment this is a command line tool
  only.
* Incremental backups - if you run the tool at a later time, it will only
  download new messages / media.
* You will be able to use an HTML exporter to create static HTML files
  containing your chats. This feature is still in the works.

## Limitations
This tool relies on Telegram's API. They started rate limiting the calls
made by this tool some time ago. As of february 2017, downloading messages
is limited to 400 messages every 30 seconds, resulting in 48,000 messages
per hour. Media download is not throttled right now, so it should be a lot
quicker.

But since this tool is designed to be able to continue it's work at any
time, you can just abort the download and continue it later - that way,
you'll be moving step by step towards a complete archive of your telegram
messages and media files.

## Usage
You need to have at least Java 1.7 installed on your machine. Download the
jar file, and run it on the console like this: `java -jar telegram_backup.jar`.

Append `--help` to get a list of all available commands.

Basically, you have to call it with `--login` first to login to your telegram account and then
call it again with `--account <phone>` to use this account and download all
it's history. If you have just one account, you can omit this parameter.

## Donations
I've put quite some time into this tool. If you want to donate a small
amount, you can send it via Bitcoin to *1CofYzS88iEngxMu4NqQeohWDBUHv9CNDJ* or via PayPal to
[mail@fabianonline.de](https://paypal.me/fabianonline).

Alternatively use [this link](http://www.amazon.com/?_encoding=UTF8&camp=1638&creative=6742&linkCode=ur2&site-redirect=de&tag=telegrambackup-21) the next time you shop at
amazon.com or [this
link](https://www.amazon.de/ref=as_li_ss_tl?ie=UTF8&linkCode=ll2&tag=telegrambackup-21&linkId=c54d9fe7c560128c6f018dd24e80d486) for amazon.de. You won't
pay any more, but I will get a few percent of your purchase's worth from
amazon.

## Frequently asked questions
### Why do I see error messages?
The library I'm using to access Telegram has some small bugs. One of those
is the display of meaningless (because they are being acted accordingly upon)
error messages. Those include:
* Something containing `AUTH_ERROR`
You can just ignore these messages.

Basically, if the tool is continuing to run after error messages are shown,
you can just ignore the messages.
Either way, even if Telegram_Backup would "miss" some files or messages,
this will be detected at the next run of this program and then tried again.

### Where do you save the files?
The files are being saved in your User directory in a folder named
`telegram_backup`. Under windows, this would typically be under
`C:\Users\<username>\telegram_backup`. Linux users should look unter
`/home/<username>/telegram_backup`.

You can change this directory by supplying `--target <dir>` when calling
Telegram_Backup.

### What are those files and folders?
In the folder `telegram_backup` is one folder named `stickers`, which will
hold all sticker images you've received. Then there is a folder for each
account, named after the phone number associated with that account.

In these folders you will find `auth.dat` and `dc.dat`, which contain
authentication data. There is `database.sqlite` which is a SQLite3 database
containing all your messages and other data. The folder `files` contains all
media files, named after the ID of the message they belong to. Last but not
least the folder `export` contains exported data.


## Attribution
This tool uses libraries from other developers which are covered by other licenses,
which are:
* [Kotlogram](https://github.com/badoualy/kotlogram) by Yannick Badoual, licensed
  under MIT License.
* [SQLite JDBC](https://bitbucket.org/xerial/sqlite-jdbc) by Taro L. Saito,
  licensed under Apache License version 2.0.
* [Mustache.java](https://github.com/spullara/mustache.java) by RightTime,
  Inc., licensed under Apache License version 2.0.
* [Logback](http://logback.qos.ch) by QOS.ch, licensed unter LGPL version 2.1.
* [SLF4J](http://www.slf4j.org) by QOS.ch, licensed under MIT license.
