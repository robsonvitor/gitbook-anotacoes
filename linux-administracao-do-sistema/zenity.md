# Zenity

\#\# Manual

[https://help.gnome.org/users/zenity/stable/index.html.en](https://help.gnome.org/users/zenity/stable/index.html.en)

\| Exit Code \| Description \|

\|:-----------:\|-------------\|

\| 0 \| The user has pressed either OK or Close\|

\| 1 \| The user has either pressed Cancel, or used the window functions to close the dialog.\|

\| -1 \| An unexpected error has occurred.\|

\| 5 \| The dialog has been closed because the timeout has been reached.\|

All Zenity dialogs support the following general options:

\*\*Specifies the title of a dialog.\*\*

\`\`--title=title\`\`

\*\*Specifies the icon that is displayed in the window frame of the dialog. There are 4 stock icons also available by providing the following keywords - 'info', 'warning', 'question' and 'error'.\*\*

\`\`--window-icon=icon\_path\`\`

\*\*Specifies the width of the dialog.\*\*

\`\`--width=width\`\`

\*\*Specifies the height of the dialog.\*\* \`\`--height=height\`\`

\*\*Specifies the timeout in seconds after which the dialog is closed.\*\* \`\`--timeout=timeout\`\`

\# Exemplos

The calendar dialog supports the following options:

\`--text=text\`

Specifies the text that is displayed in the calendar dialog.

--day=day

Specifies the day that is selected in the calendar dialog. day must be a number between 1 and 31 inclusive.

--month=month

Specifies the month that is selected in the calendar dialog. month must be a number between 1 and 12 inclusive.

--year=year

Specifies the year that is selected in the calendar dialog.

--date-format=format

Specifies the format that is returned from the calendar dialog after date selection. The default format depends on your locale. Format must be a format that is acceptable to the strftime function, for example %A %d/%m/%y.

The following example script shows how to create a calendar dialog:

\`\`\`

zenity --calendar --title="Select a Date" --text="Click on a date to select that date."

--day=10 --month=8 --year=2004

then echo $? else echo "No date selected"

\`\`\`

\#\# Color Selection Dialog

Use the --color-selection option to create a color selection dialog.

The color selection dialog supports the following options:

--color=VALUE

Set the initial color.\(ex: \#FF0000\)

--show-palette

Show the palette.

The following example script shows how to create a color selection dialog:

\`\`\`bash

\#!/bin/bash

COLOR=\`zenity --color-selection --show-palette\`

case $? in

```text
     0\)

    echo "You selected $COLOR.";;

     1\)

            echo "No color selected.";;

    -1\)

            echo "An unexpected error has occurred.";;
```

esac

\`\`\`

\# File Selection Dialog

Use the --file-selection option to create a file selection dialog. Zenity returns the selected files or directories to standard output. The default mode of the file selection dialog is open.

The file selection dialog supports the following options:

--filename=filename

Specifies the file or directory that is selected in the file selection dialog when the dialog is first shown.

--multiple

Allows the selection of multiple filenames in the file selection dialog.

--directory

Allows only selection of directories in the file selection dialog.

--save

Set the file selection dialog into save mode.

--separator=separator

Specifies the string that is used to divide the returned list of filenames.

The following example script shows how to create a file selection dialog:

\`\`\`bash

\#!/bin/sh

FILE=\`zenity --file-selection --title="Select a File"\`

case $? in

```text
     0\)

            echo "\"$FILE\" selected.";;

     1\)

            echo "No file selected.";;

    -1\)

            echo "An unexpected error has occurred.";;
```

esac

\`\`\`

\# Forms Dialog

Use the --forms option to create a forms dialog.

The forms dialog supports the following options:

--add-entry=FieldName

Add a new Entry in forms dialog.

--add-password=FieldName

Add a new Password Entry in forms dialog. \(Hide text\)

--add-calendar=FieldName

Add a new Calendar in forms dialog.

--text=TEXT

Set the dialog text.

--separator=SEPARATOR

Set output separator character. \(Default: \| \)

--forms-date-format=PATTERN

Set the format for the returned date. The default format depends on your locale. format must be a Format that is acceptable to the strftime function, for example %A %d/%m/%y.

The following example script shows how to create a forms dialog:

\`\`\`

\#!/bin/sh

zenity --forms --title="Add Friend" \

```text
--text="Enter information about your friend." \

--separator="," \

--add-entry="First Name" \

--add-entry="Family Name" \

--add-entry="Email" \

--add-calendar="Birthday" &gt;&gt; addr.csv
```

case $? in

```text
0\)

    echo "Friend added.";;

1\)

    echo "No friend added."

;;

-1\)

    echo "An unexpected error has occurred."

;;
```

esac

\`\`\`

\# List Dialog

Use the --list option to create a list dialog. Zenity returns the entries in the first column of text of selected rows to standard output.

Data for the dialog must specified column by column, row by row. Data can be provided to the dialog through standard input. Each entry must be separated by a newline character.

If you use the --checklist or --radiolist options, each row must start with either 'TRUE' or 'FALSE'.

The list dialog supports the following options:

--column=column

Specifies the column headers that are displayed in the list dialog. You must specify a --column option for each column that you want to display in the dialog.

--checklist

Specifies that the first column in the list dialog contains check boxes.

--radiolist

Specifies that the first column in the list dialog contains radio boxes.

--editable

Allows the displayed items to be edited.

--separator=separator

Specifies what string is used when the list dialog returns the selected entries.

--print-column=column

Specifies what column should be printed out upon selection. The default column is '1'. 'ALL' can be used to print out all columns in the list.

The following example script shows how to create a list dialog:

\`\`\`

\#!/bin/sh

zenity --list \

--title="Choose the Bugs You Wish to View" \

--column="Bug Number" --column="Severity" --column="Description" \

```text
992383 Normal "GtkTreeView crashes on multiple selections" \

293823 High "GNOME Dictionary does not handle proxy" \

393823 Critical "Menu editing does not work in GNOME 2.0"
```

\`\`\`

\# Message Dialog

Error Dialog

Use the --error option.

Info Dialog

Use the --info option.

Question Dialog

Use the --question option.

Warning Dialog

Use the --warning option.

\# Notification Icon

Use the --notification option to create a notification icon.

--text=text

Specifies the text that is displayed in the notification area.

--listen=icon: 'text', message: 'text', tooltip: 'text', visible: 'text',

Listens for commands at standard input. At least one command must be specified. Commands are comma separated. A command must be followed by a colon and a value.

The icon command also accepts four stock icon values such as error, info, question and warning.

The following example script shows how to create a notification icon:

\`\`\`

\#!/bin/sh

zenity --notification\

```text
--window-icon="info" \

--text="There are system updates necessary!"
```

\`\`\`

The following example script shows how to create a notification icon along with --listen:

\`\`\`

\#!/bin/sh

cat &lt;&lt;EOH\| zenity --notification --listen

message: this is the message text

EOH

\`\`\`

\# Password Dialog

Use the --password option to create a password entry dialog.

The password entry dialog supports the following options:

--username

Display the username field.

The following example script shows how to create a password entry dialog:

\`\`\`

\#!/bin/sh

ENTRY=\`zenity --password --username\`

case $? in

```text
     0\)

     echo "User Name: \`echo $ENTRY \| cut -d'\|' -f1\`"

     echo "Password : \`echo $ENTRY \| cut -d'\|' -f2\`"

    ;;

     1\)

            echo "Stop login.";;

    -1\)

            echo "An unexpected error has occurred.";;
```

esac

\`\`\`

\# Progress Dialog

Use the --progress option to create a progress dialog.

Zenity reads data from standard input line by line. If a line is prefixed with \#, the text is updated with the text on that line. If a line contains only a number, the percentage is updated with that number.

The progress dialog supports the following options:

--text=text

Specifies the text that is displayed in the progress dialog.

--percentage=percentage

Specifies the initial percentage that is set in the progress dialog.

--auto-close

Closes the progress dialog when 100% has been reached.

--pulsate

Specifies that the progress bar pulsates until an EOF character is read from standard input.

The following example script shows how to create a progress dialog:

\`\`\`

\#!/bin/sh

\(

echo "10" ; sleep 1

echo "\# Updating mail logs" ; sleep 1

echo "20" ; sleep 1

echo "\# Resetting cron jobs" ; sleep 1

echo "50" ; sleep 1

echo "This line will just be ignored" ; sleep 1

echo "75" ; sleep 1

echo "\# Rebooting system" ; sleep 1

echo "100" ; sleep 1

\) \|

zenity --progress \

--title="Update System Logs" \

--text="Scanning mail logs..." \

--percentage=0

if \[ "$?" = -1 \] ; then

```text
    zenity --error \

      --text="Update canceled."
```

fi

\`\`\`

\# Scale Dialog

Use the --scale option to create a scale dialog.

The scale dialog supports the following options:

--text=TEXT

Set the dialog text. \(Default: Adjust the scale value\)

--value=VALUE

Set initial value. \(Default: 0\) You must specify value between minimum value to maximum value.

--min-value=VALUE

Set minimum value. \(Default: 0\)

--max-value=VALUE

Set maximum value. \(Default: 100\)

--step=VALUE

Set step size. \(Default: 1\)

--print-partial

Print value to standard output, whenever a value is changed.

--hide-value

Hide value on dialog.

The following example script shows how to create a scale dialog:

\`\`\`

\#!/bin/sh

VALUE=\`zenity --scale --text="Select window transparency." --value=50\`

case $? in

```text
     0\)

    echo "You selected $VALUE%.";;

     1\)

            echo "No value selected.";;

    -1\)

            echo "An unexpected error has occurred.";;
```

esac

\`\`\`

\# Text Entry Dialog

Use the --entry option to create a text entry dialog. Zenity returns the contents of the text entry to standard output.

The text entry dialog supports the following options:

--text=text

Specifies the text that is displayed in the text entry dialog.

--entry-text=text

Specifies the text that is displayed in the entry field of the text entry dialog.

--hide-text

Hides the text in the entry field of the text entry dialog.

The following example script shows how to create a text entry dialog:

\`\`\`

\#!/bin/sh

if zenity --entry \

--title="Add new profile" \

--text="Enter name of new profile:" \

--entry-text "NewProfile"

then echo $?

else echo "No name entered"

fi

\`\`\`

\# Text Information Dialog

Use the --text-info option to create a text information dialog.

The text information dialog supports the following options:

--filename=filename

Specifies a file that is loaded in the text information dialog.

--editable

Allows the displayed text to be edited. The edited text is returned to standard output when the dialog is closed.

--font=FONT

Specifies the text font.

--checkbox=TEXT

Enable a checkbox for use like a 'I read and accept the terms.'

--html

Enable html support.

--url=URL

Sets an url instead of a file. Only works if you use --html option.

The following example script shows how to create a text information dialog:

\`\`\`

\#!/bin/sh

\# You must place file "COPYING" in same folder of this script.

FILE=\`dirname $0\`/COPYING

zenity --text-info \

```text
   --title="License" \

   --filename=$FILE \

   --checkbox="I read and accept the terms."
```

case $? in

```text
0\)

    echo "Start installation!"

\# next step

;;

1\)

    echo "Stop installation!"

;;

-1\)

    echo "An unexpected error has occurred."

;;
```

esac

\`\`\`

