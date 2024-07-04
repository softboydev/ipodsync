# iPodSync
This is a collection of Apple Shortcuts to sync the Calendar, Reminders and Notes application with an iPod Classic.

The shortcuts will create a folder called iPodSync in your home folder.
You might need to set correct paths in some shortcuts, so look through all of them for red or greyed out variables before use.

The shortcuts will also HEAVILY invade your privacy settings.
You will need to enable handling of big data, execution of scripts and screen recording.

The collection consists of these 5 shortcuts, which can either be run reperately to only sync one app or all together.
calendarsToIpod https://www.icloud.com/shortcuts/7dca14cbcb9641e786d60d511b6e4425
remindersToIpod https://www.icloud.com/shortcuts/09a42ec4aa0a4992bc26619d3b286246
notesToIpod https://www.icloud.com/shortcuts/ce9353ba57674e9a8f6c66a96fab7db7
copyToIpod https://www.icloud.com/shortcuts/0e35a933089a4145a4e20292c321749e
syncIpod https://www.icloud.com/shortcuts/b5f2ec8885284f219e14d4ae16207cca

## calendarsToIpod
Contains some Apple Script UI magic to export all calendars to .ics files. It is necessary to create an ~/iPodSync/calendars folder manually once and use it for export, after that the Calendar app will remember.

~~~
on run
	tell application "Calendar"
		activate
	end tell
	tell application "System Events"
		tell process "Calendar"
			set frontmost to true
			set n to count rows of outline 1 of scroll area 1 of splitter group 1 of splitter group 1 of window 1
			repeat with i from 2 to n
				tell row i of outline 1 of scroll area 1 of splitter group 1 of splitter group 1 of window 1
					set selected to true
					delay 1
				end tell
				
				tell menu item 1 of menu of menu item "Export" of menu "File" of menu bar 1
					click
					delay 3
				end tell
				tell button 3 of sheet 1 of window 1
					click
					delay 1
				end tell
				if button "Replace" of sheet 1 of sheet 1 of window 1 exists then
					tell button "Replace" of sheet 1 of sheet 1 of window 1
						click
					end tell
					delay 1
				end if
			end repeat
		end tell
	end tell
end run
~~~

## remindersToIpod
Puts all your open reminders into a text file and the text file into a folder.

## notesToIpod
Iterates over all your notes, names them in a sensible way and puts them in yet another folder.

## copyToIpod
Uses shell to move the content of the folders created by the scripts above to the iPod.
!!! Change all paths to match the name of your device!!!

# syncIpod
Runs all 4 shortcuts in succession.
