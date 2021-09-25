Run BIOSExtracter as Admin, set 'custom' as size of your ram (Eg i had 16gigs to did 16k)
Backup the extracted .rom file

Next run UEFI tool and select your image file, Search (Ctril+F) in text section(Neither in Hex nor GUID) for Overclocking lock/CFG Lock. Double-click the result you got.
In the upper part , we need the the parent tree underwhich we found out overclocking lock(highlighted one).
Now left-click the parent tree and select 'extract as is' , this will save a ffs file

Next Open up IREFExtractor , and select the ffs we just saved , click Extract , this will save a txt file which we can read.

Open up the file, search for Overclocking lock and note its VarOffset name.
Also Note name of CFG lock.

Note the varstore/varstore Id of these two too (Would be same)
Now search for VarstoreID which has value same as you found in the CFG Lock and Overclocking lock. And Note its name (In My case its name as Setup)




Now We need to setup Our USB 
Format it with FAT32. Make Folder named 'EFI' in root , and make a folder name 'boot'.
Place the grupx64 file in the boot folder, and rename it to bootx64.

Now Reboot your system with usb plugged in , Disable secure boot in BIOS , boot in your usb. 


Now we'll check if the usb Works or Not.

type ' setup_var (Your Varstore name) (name of cfg lock or OC lock, any one)'
and it would return its current value , 
IN MY CASE  

setup_var Setup 0x659

Where 0x659 is my name of uoverclock lock , it will return 0x1 (As its enabled now and value of enable is 0x1)

so we need to set it yo 0x0 to disable it and get your UV back. So Type in

' setup_var (Your Varstore name) (name of Overclock lock) 0x0 '

And after that 

' setup_var (Your Varstore name) (name of cfg lock) 0x0 '

In My case 

' setup_var Setup 0x659 0x0 '
' setup_var Setup 0x5BD 0x0 '


Thats it YOUR DONE . 
Reboot, enable Secure Boot , and get into windows .
You'll Now be able to Undervolt again.
