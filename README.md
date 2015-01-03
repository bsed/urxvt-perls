A small collection of Perl extensions for the rxvt-unicode terminal emulator.

Installation
------------
Simply place the scripts you want to install in the /usr/lib/urxvt/perl/ folder
for system-wide availability. You can also put them in a folder of your
choice, but then you have to add this line to your .Xdefaults/.Xresources:

    URxvt.perl-lib: /your/folder/

See the following sections for information on how to enable the scripts or set
script-specific options and keyboard mappings in your .Xdefaults/.Xresources.


keyboard-select
---------------
Use keyboard shortcuts to select and copy text.

After installing, put the following lines in your .Xdefaults/.Xresources:

    URxvt.perl-ext-common: ...,keyboard-select
    URxvt.keysym.M-Escape: perl:keyboard-select:activate

The following line overwrites the default Meta-s binding and allows to activate
keyboard-select directly in backward search mode:

    URxvt.keysym.M-s: perl:keyboard-select:search

Use Meta-Escape to activate selection mode, then use the following keys:

    h/j/k/l:    Move cursor left/down/up/right (also with arrow keys)
    g/G/0/^/$/H/M/L/f/F/;/,/w/W/b/B/e/E: More vi-like cursor movement keys
    '/'/?:      Start forward/backward search
    n/N:        Repeat last search, N: in reverse direction
    Ctrl-f/b:   Scroll down/up one screen
    Ctrl-d/u:   Scroll down/up half a screen
    v/V/Ctrl-v: Toggle normal/linewise/blockwise selection
    y/Return:   Copy selection to primary buffer, Return: deactivate afterwards
    q/Escape:   Deactivate keyboard selection mode


url-select
----------
Use keyboard shortcuts to select URLs.

This should be used as a replacement for the default matcher extension, it also
makes URLs clickable with the middle mouse button.

After installing, put the following lines in your .Xdefaults/.Xresources:

    URxvt.perl-ext-common: ...,url-select
    URxvt.keysym.M-u: perl:url-select:select_next

Use Meta-u to activate URL selection mode, then use the following keys:

    j/k:      Select next downward/upward URL (also with arrow keys)
    g/G:      Select first/last URL (also with home/end key)
    o/Return: Open selected URL in browser, Return: deactivate afterwards
    y:        Copy (yank) selected URL and deactivate selection mode
    q/Escape: Deactivate URL selection mode

Options:

    URxvt.url-select.autocopy:  if set to true, selected URLs are automatically
                                copied to the PRIMARY buffer
    URxvt.url-select.button:    mouse button to click-open URLs (default: 2)
    URxvt.url-select.launcher:  browser/command to open selected URL with
    URxvt.url-select.underline: if set to true, all URLs get underlined

For compatibility reasons, url-select will also use any patterns defined for
the matcher extension by reading all `URxvt.matcher.pattern.[0-9]` resources.


clipboard
---------
Use keyboard shortcuts to copy the selection to the clipboard and to paste the
clipboard contents (optionally escaping all special characters).

After installing, put the following lines in your .Xdefaults/.Xresources:

    URxvt.perl-ext-common: ...,clipboard
    URxvt.keysym.M-c:   perl:clipboard:copy
    URxvt.keysym.M-v:   perl:clipboard:paste
    URxvt.keysym.M-C-v: perl:clipboard:paste_escaped

Options:

    URxvt.clipboard.autocopy: if set to true, the clipboard is automatically
                              updated whenever the PRIMARY selection changes

You can also overwrite the system commands to use for copying/pasting.
The default ones are:

    URxvt.clipboard.copycmd:  xsel -ib
    URxvt.clipboard.pastecmd: xsel -ob

If you prefer xclip, then put these lines in your .Xdefaults/.Xresources:

    URxvt.clipboard.copycmd:  xclip -i -selection clipboard
    URxvt.clipboard.pastecmd: xclip -o -selection clipboard

On Mac OS X, put these lines in your .Xdefaults/.Xresources:

    URxvt.clipboard.copycmd:  pbcopy
    URxvt.clipboard.pastecmd: pbpaste

The use of the functions should be self-explanatory!


rotate-colors
-------------
_This plugin is currently non-functional. It prints the escape sequence needed,
however, so you can use it as a hard coded command bound to a keysym._

    URxvt.keysym.C-M-l : command:\033]...

Rotate color definitions from a list of files.

Install:
    URxvt.perl-ext-common: ...,rotate-colors
    URxvt.keysym.M-n:   perl:rotate-colors:next
    URxvt.keysym.M-p:   perl:rotate-colors:prev

Options:

    URxvt.rotate-colors.files: A comma-delimited list of files containing color
                              definitions like URxvt.color0: #000000. Other
                              lines are ignored so listing entire config files
                              should be ok.


resize-font
-----------
Increase and decrease the font size.

Install:

    URxvt.perl-ext-common: ...,resize-font
    URxvt.keysym.C-M-plus:     perl:resize-font:bigger
    URxvt.keysym.C-M-minus:    perl:resize-font:smaller
    URxvt.keysym.C-M-equal:    perl:resize-font:reset
    URxvt.keysym.C-M-question: perl:resize-font:show

`perl:resize-font:reset` restores the original font size.

`perl:resize-font:show` displays the current font and size using the OSD.


tabbedex
--------

This plugin is huge and I don't use it. See the `tabbedex` file for an
explanation and then feel free to contribute to this section.

Install:

    URxvt.perl-ext-common: ...,tabbedex
    ...

Calls to be able to open tabs via scripts have been added.

This is an example script to start some tabs with commands in them, which can
be started either with 
$ ./startup_script.sh
or via
$ urxvt -e './startup_script.sh'

startup_script.sh:

    printf "\033]777;tabbedex;new_tab\007"
    sleep 0.1
    printf "\033]777;tabbedex;make_current;1\007"
    printf "\033]777;tabbedex;set_tab_name;MAIL\007"
    printf "\033]777;tabbedex;interactive_command;pine\007"
    printf "\033]777;tabbedex;interactive_key;i\007"

    printf "\033]777;tabbedex;new_tab;tmux\007"
    sleep 0.1
    printf "\033]777;tabbedex;make_current;2\007"
    printf "\033]777;tabbedex;set_tab_name;TMUX\007"
    
    printf "\033]777;tabbedex;new_tab\007"
    sleep 0.1
    printf "\033]777;tabbedex;make_current;3\007"
    printf "\033]777;tabbedex;set_tab_name;interactive\007"
    printf "\033]777;tabbedex;interactive_command;ls /; ls -R\007"
    
    printf "\033]777;tabbedex;new_tab\007"
    sleep 0.1
    printf "\033]777;tabbedex;make_current;4\007"
    printf "\033]777;tabbedex;set_tab_name;interactive\007"
    printf "\033]777;tabbedex;interactive_command;ls /; ls -R /\007"
    
    sleep 0.1;
