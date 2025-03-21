# This is not the original sharpkeys. This is a fork that aims to clean up certain aspects of the original application.
## Project Description
SharpKeys is a utility that manages a Registry key that allows Windows to remap one key to any other key. Included in the application is a list of common keyboard keys and a Type Key feature to automatically recognize most keyboard keys.

## Original Mission:
This is something that I've thrown together to help people out with their keyboard mappings. What's a keyboard mapping? How many times a day do you accidentally hit cAPS lOCK BY MISTAKE AND END UP HAVING TO GO BAck and retype stuff? For me it was at least once an hour - in fact, I used to pop off the Caps Lock key so I wouldn't hit it anymore, but I found something better in Windows XP, as well as 2000, Server 2003, Vista, Windows 7, Windows 8, and Windows 10. There's a little used registry hack that allows you to remap keys across a keyboard. For me, this meant that I told my computer to treat Caps Lock as if it was a shift key, which it now does. 

The more I started working with other keyboard, the more I wanted to have this ability to map other keys across my keyboard, but working with the Hex numbers and having too look up scan codes could be painful... hence SharpKeys. 

SharpKeys is not responsible for any of the keyboard remapping functionality - it simply exposes a Registry key that controls how Windows remaps keys and has been available to us since Windows 2000.  The list of keys that are included in the application are from most of the US-based keyboards that I've used over the years and is not guaranteed to be 100% complete for world keyboards.

## Install

### Manual via web or Microsoft Store

Click the [Releases](https://github.com/randyrants/sharpkeys/releases) button in the header above or get the same MSI.
Note: that while this fork does support ARM CPUs, Microsoft Store distribution is not supported.

## How do I use it?  Getting Started
* Launch SharpKeys, by selecting its icon from the Start menu. If there are any errors reported, please check the Troubleshooting section below 
* Add a new key mapping or edit an existing one
* Click "Write to registry" and wait for a confirmation that the registry was successfully updated
* Close SharpKeys and either log out (and back in) or reboot to enforce the new mappings

## Things that SharpKeys _will_ do:
* Map an entire key to any other key - e.g. you could remap Caps Lock to a Shift key
* Remap more than one key to one single key - e.g. you could remap every key on a keyboard to the letter Q
* Force you to look for the Left or Right ALT key in the list of available keys because Type Key cannot scan for ALT
* Allow you to swap two keys with each other - e.g. you can swap Left Windows with Left Control and vice versa

## Things that SharpKeys **_will not_** do:
* Map multiple key presses to one key - e.g. it will not support an attempt to remap Ctrl+C to the F5 key
* Map mouse clicks to any key
* Support certain hardware keys that never make it to Windows - e.g. Logitech’s volume buttons or most Fn keys
* Support multiple mappings for different users - the Windows key being tweaked is for an entire machine
* Protect you from yourself - if you disable your DEL key and can’t login because Ctrl+Alt+Del doesn’t work now, you’ll have to reformat

## Additional FAQ and answers ##
**Q: Does it run on Windows 11?**  
A: Yes!

**Q: Can I remap a combination of keys to one key?**  
A: Sadly, no. SharpKeys only remaps whole keys rather than a modified key. For example, you can remap Ctrl or C but you can't remap Ctrl+C to another key.  That said, the Microsoft PowerToys tool does offer this functionality - you can learn more about their tool here: [Microsoft PowerToys](https://github.com/microsoft/PowerToys/releases).

**Q: Can I remap the Copilot key with SharpKeys?** 
A: No.  The Copilot key's scancode is a combination of Ctrl + Windows + F23 and the Windows technology the SharpKeys exposes only supports remapping an entire key and not a modified combination of the key.

**Q: Can I remap a mouse click to a new key?**  
A: Sorry, but no. The remapping technology that Windows uses to remap your keys isn't aware of your mouse.

**Q: Why can't I remap my Fn key on my [notebook or Apple] keyboard?**  
A: Some keys simply just never get to Windows. In the case of most Fn keys, they are interpretted by the hardware and never get passed onto the OS, no matter how they appear to work... if Windows doesn't see the key, there's no way for the key to be remapped by Windows.

**Q: Type a Key shows 00_100 - can I remap this key?**  
A: 00_100 is a catch all code that Windows reports when a key is captured by hardware or some other driver so there's no way to successfully remap that key, especially since multiple keys can return the same 00_100 code.

**Q: Type a Key shows Unknown Key - can I remap this key?**  
A: Odds are this is just a key that has never been seen by SharpKeys before so it doesn't know what to do with it. Open an issue on this site for this project and someone from the Open Source community can look into adding it.

**Q: Type a Key shows a code that is E0_nnnn - can I remap this key?**  
**Q: Type a Key for AltGr shows a code that is E0_2038 - can I remap this key?**  
A: If a scancode has 6 characters, then it is what is known as a triple-byte scancode which is something that cannot be remapped by the Windows Registry.  To remap a key like this, you'll need an active remapper like Microsoft PowerToys or AutoHotKeys or the app that came with the keyboard (e.g. Logitech's Options) if available.

**Q: I have a new Microsoft keyboard with dedicated keys for Office and Emoji - can I remap those?**  
A: Not with SharpKeys, as these are both triple-byte codes, but the Microsoft offers keyboard software that can change the function of these keys.  Specifically for the Office key, there is also this additional workaround via [HowToGeek](https://www.howtogeek.com/445318/how-to-remap-the-office-key-on-your-keyboard/).

**Q: What's all this stuff about "scan codes"?**  
A: Whenever you press a key on your keyboard, it sends a binary code to the keyboard controller in you PC. That code is passed on into Windows (in most cases) and Windows interprets it as "they pressed code 0x3A so that's Caps Lock - turn that on!" What modern versions of Windows also does is it checks a registry key when the machine boots. What that registry key does is tell windows "even though they pressed 0x3A, treat it as 0x2A" (which is left shift). What SharpKeys does is edits this registry key using a simple UI and sidestepping the registry editor.

**Q: I have a new PC that has a hang up button I want to remap - can I remap this key?**  
A: A lot of people ask for E0_1F65 but as the above question calls out, triple byte scancodes cannot be remapped with the Windows Registry.  This applies to Lenovo, HP, Dell, and any other PC maker's laptop or desktop.

**Q: Type a Key doesn't recognize the Alt key when I type it - how do I remap this key?**  
A: The Alt key scancode doesn't make it through the system, to get to the Type a Key window.  Basically, when you type Alt, Windows sends it to the system menu and activate it, rather than sending the scancode to the window.  You can still remap this key, but you'll see to select it from the list manually; you'll find it in the grouping of keys marked as "Special".

**Q: What is the craziest remapping you've ever done?**  
A: I think it's my active remapping on Surface products, where some of the cursor navigation keys share space with F9-F12. Since I use F1-F8 for a lot for Office or Visual Studio, I don't want to have to remember to hit Fn but I also don't want to leave Fn-Lock on because I also need Home, End, PgUp, and PgDn as well.  Soooooo, I leave Fn-Lock on and then remapped F9-F12 to Home/End/PgUp/PgDn and then Home/End/PgUp/PgDn to F9-F12.  I also disabled Caps Lock and remapped the Right Alt to Left Windows because that's just happy for a laptop.  Since other people might make use of this, I put [the SKL file in the depot here](https://github.com/randyrants/sharpkeys/blob/master/HandyRemapForSurfaceKeyboard.skl).

**Q: What is an "Unknown" key?**  
A: There's no way I could get a lab of keyboards to test, especially when almost every modern keyboard comes with extra keys or language specific keys - some companies are even making keyboards with special buttons for their own software or product line up. Consequently, when you use Type Key and it hit a key that SharpKeys may not know about, it can still be mapped, even if the label says unknown. If there's a key that you have on your keyboard that is listed as Unknown but you have a used for it, email me and I'll see about adding a better label for it.

**Q: What happens if I use your utility and I add a bunch of key mapping and I can't use my computer anymore?**  
A: Well, more or less, you're screwed. I've tested this application a good deal, and there's very little risk in modifying this Registry entry, but if you turn off a key you need for your password, you're mostly out of luck.  One option is to **try using the onscreen keyboard that's available via Accessibility** options, as that wouldn't be impacted by remapping settings for Windows.  You can also try to plug in a USB keyboard if you're on a laptop or you can boot into Safe Mode and remove the Scancode Map Registry key, but you'll be on your own. Having said this, please be careful and you're using SharpKeys at your own risk!

**Q: I have to have combo key support or triple-byte enabled keys support! Why won't you make this change?!**  
A: There is absolutely nothing I can do about it: Windows is remapping the keys and this app is just a UX for the Registry key that controls the remapping.  In fact, I think I answered this already in the FAQ.  That said, if you want a deeper level of remapping support please check out [Microsoft PowerToys](https://github.com/microsoft/PowerToys/releases).

**Q: I have accidentally remapped a key I need to sign in with but I can reboot to safe mode or WinPE and get to a CMD prompt. Can I reset the mappings?**
A: If you can get to a CMD window. you should be able to open regedit, which will prompt for Administrator rights.  Navigate to `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout`, delete the `Scancode Map` value; likewise, if you have an admin CMD prompt open already, you can remove the Registry value by running: 
`reg delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout" /v "Scancode Map"` 
Reboot after resetting the Registry value.

On some PE systems, the registry editor will show the registry settings for the PE session. If this happens, click `HKEY_LOCAL_MACHINE` -> `File` -> `Load Hive` -> go to your original drive, `C:\Windows\System32\Config` and find a file named either SYSTEM, give it a random name, and delete the key as you would.

## Page for donations:
Not my project, but you should still go donate to the orignal author. [someone asked me to pop the link here](https://github.com/randyrants/sharpkeys/issues/387).  If you're interested, you can get more information [on my blog](https://www.randyrants.com/donate/).
