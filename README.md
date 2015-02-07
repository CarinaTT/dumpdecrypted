# About

Dumps decrypted mach-o files from encrypted `iPhone applications` or `app extensions` to a file.    


# Usage
1) \# vim `dumpdecrypted.plist`   

```
{
	Filter = {
		Bundles = ("your.bundle.id");
	};
}
```

2) \# cp dumpdecrypted.plist  dumpdecrypted.dylib /Library/MobileSubstrate/DynamicLibraries/  

3) launch application or app extension

```
[+] detected 64bit ARM binary in memory.
[+] offset to cryptid found: @0x100020b68(from 0x100020000) = b68
[+] Found encrypted data at address 00004000 of length 294912 bytes - type 1.
[+] Opening /private/var/mobile/Containers/Bundle/Application/39B13E69-D80E-4F8B-9635-679607634DE6/xxxxx.app/PlugIns/xxxxxx.appex/xxxxxx for reading.
[+] Reading header
[+] Detecting header type
[+] Executable is a FAT image - searching for right architecture
[+] Correct arch is at offset 655360 in the file
[+] Opening /var/mobile/Containers/Data/PluginKitPlugin/3D7C83EE-B249-45C1-AC8E-DFE896A1F751/Library/Caches/xxxxx for writing.
[+] Copying the not encrypted start of the file
[+] Dumping the decrypted data into the file
[+] Copying the not encrypted remainder of the file
[+] Setting the LC_ENCRYPTION_INFO->cryptid to 0 at offset a0b68
[+] Closing original file
[+] Closing dump file
```

# Check
$ otool -l xxx.decrypted | grep crypt  

```
  cryptoff  16384
  cryptsize 294912
  cryptid   0
```

Optional: lipo if you'd like   
$ lipo -thin armv7 xxx.decrypted -output xxx_armv7.decrypted  
$ lipo -thin armv64 xxx.decrypted -output xxx_arm64.decrypted



# Credit

[Dumpdecrypted](https://github.com/stefanesser/dumpdecrypted) was orignally developed by [stefanesser](https://github.com/stefanesser). 
