# remove-MotW
A registry script to safely and conveniently remove Mark of the Web (MotW) from known files, which removes restrictions imposed by the MotW, by adding a powershell script to the context menu. 

## Mark of the Web
Read about it [here at wikipedia](https://en.wikipedia.org/wiki/Mark_of_the_Web).

## Use the registry script
Just double-click the registry script and click Yes and Yes. It should be done.

## To do it manually
1. Open registry editor via search or via Win+R -> type "regedit" -> OK.
2. Navigate to Computer\HKEY_CLASSES_ROOT\*\shell\
3. Add a new key with whatever name you desire "unblock" or "removemotw" or whatever but unique. I'll assume you named it "removeMotW"
4. Add a new String value under this with
       Value name: MUIVerb
       Value data: remove MoTW
   (this value data is also your choice)
5. Add another Key under removeMoTW key, and name it "command"
6. Double click the "(Default)" string add this 
      Value data: powershell.exe -Command "Unblock-File -LiteralPath '%L'"
7. Right click any "locked PDF" in your system to check if it works. (No restart required)
