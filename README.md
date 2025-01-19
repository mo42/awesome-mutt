# Awesome Mutt ![image](https://neomutt.org/images/mutt-48x48.png)

A curated list of resources for the mail user agents (MUA)
[Mutt](http://mutt.org/) and [NeoMutt](https://neomutt.org/) to help you get
started, customized, and master terminal-based emails.

## Why use Mutt in the 2020ies?

Mutt might seem like a relic of the past.
Looking more closely, it remains a practical and efficient tool.
Mutt let's you combine your favorite tools for emailing.
For example, you can write emails in [Vim](https://www.vim.org/), so you can leverage your text-editing skills.
- Customization: You can tailor it to fit your workflow, with options for custom keybindings, macros, hooks, and scripts.
- Modularity: Mutt is just a MUA. You can and should combine it with other components ([abook](https://abook.sourceforge.io/), [OfflineIMAP](https://www.offlineimap.org/), [GnuPG](https://gnupg.org)) to create the email experience you like.

## Getting Started

A very basic configuration looks like so:
```bash
# IMAP Settings
set imap_user = "your.email@example.com"
set imap_pass = "yourpassword"
set folder = "imaps://imap.example.com/"
set spoolfile = "+INBOX"

# SMTP Settings
set smtp_url = "smtp://your.email@example.com@smtp.example.com:587/"
set smtp_pass = "yourpassword"

# Default mail directory
set record = "+Sent"
set postponed = "+Drafts"
set header_cache = "~/.mutt/cache/headers"
set message_cachedir = "~/.mutt/cache/bodies"
set certificate_file = "~/.mutt/certificates"
```

As a next step, you can avoid storing your email password in plain text by
using the standard Unix password manager [pass](https://www.passwordstore.org/)
and changing muttrc to like so:
```sh
set imap_pass=`pass path/to/imap/password`
set smtp_pass=`pass path/to/smtp/password`
```

On starting Mutt, the shell runs the `pass` commands and GnuPG might ask you
for the passphrase.

## Customization

### Color Themes
- [Mutt colors solarized](https://github.com/altercation/mutt-colors-solarized)
- [Dracula Mutt theme](https://github.com/dracula/mutt)

To apply a theme, it is ideally stored in a separate file an loaded like so:
```sh
source ~/.config/mutt/themes/solarized-dark.muttrc
```
This way, you can swap themes easily.

Alternatively, one can skip a color theme and reuse the terminal colors. For
example, the author just uses the [terminal
colors](https://github.com/mo42/dotfiles).

### Some Useful Configuration Tricks

Threaded Email View: Keep your emails organized by conversation threads.
```sh
set sort = 'threads'
set sort_aux = 'reverse-last-date-received'
set auto_tag = yes
```

Keybindings for Quick Actions: Customize keybindings to speed up your workflow.

```sh
macro index,pager <space> "<toggle-flag>N" "Mark mail as read and go to next"
```

HTML Email Viewing: Mutt can render HTML emails using an external browser or a tool like w3m.

```sh
set mailcap_path = "~/.mutt/mailcap"
set implicit_autoview = yes
```

Example `~/.mutt/mailcap` entry:

```sh
text/html; w3m -dump %s; copiousoutput
```
