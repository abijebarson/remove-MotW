# remove-MotW
A registry script to safely and conveniently remove Mark of the Web (MotW) from known files, which removes restrictions imposed by the MotW, by adding a powershell script to the context menu. 

## Mark of the Web
Read about it [here at wikipedia](https://en.wikipedia.org/wiki/Mark_of_the_Web).

## Use the registry script
Just double-click the registry script and click Yes and Yes. It should be done.

## To do it manually
1. Open registry editor via search or via Win+R -> type "regedit" -> OK.
2. Navigate to Computer\HKEY_CLASSES_ROOT\\*\shell\
3. Add a new key with whatever name you desire "unblock" or "removemotw" or whatever but unique. I'll assume you named it "removeMotW"
4. Add a new String value under this with
       Value name: MUIVerb
       Value data: remove MoTW
   (this value data is also your choice)
5. Add another Key under removeMoTW key, and name it "command"
6. Double click the "(Default)" string add this 
      Value data: powershell.exe -Command "Unblock-File -LiteralPath '%L'"
7. Right click any "locked PDF" in your system to check if it works. (No restart required)

# Disable MotW completely from all newly downloaded files
WARNING: Don't do this, unless you know what you are doing. Stick to the solution above. Windows has MotW for a reason. Malware which were discovered and yet to be discovered, can leak through windows preview unless restricted in these ways. The above solution as a convienient measure. I'm giving the permanant solution here to provide completeness. 

## Manual Regedit way:
1. HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies
2. Right click Policies -> New -> Key -> name it Attachments
3. Inside Attachments, right click -> New -> DWORD (32-bit) Value → name it SaveZoneInformation → set its value to 1.

All newly downloaded files will no longer get the MotW tag.

## Group Policy (Windows Pro/Enterprise only)
1. Win + R, type gpedit.msc
2. Navigate:  User Configuration -> Administrative Templates -> Windows Components -> Attachment Manager
3. Open "Do not preserve zone information in file attachments" and set it to Enabled.
