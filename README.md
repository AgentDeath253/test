[View Summer Update](https://github.com/FalixNodes-Software/FalixNodes-Desktop/tree/directive-rewrite-of-v4)

![image](https://i.imgur.com/7yzQ8u1.png)

Simple and stylish to use! Access FalixNodes features such as your client and game panel, help center, phpMyAdmin, status, and more all from a centralized place.

[Download Now](https://falixnodes.net/desktop) <br>
[Direct Download](https://cdn.korbsstudio.com/files/downloads/falixnodes-desktop/FalixNodes-Desktop.exe)  

## FAQ 
Q: Why and what's the point of FalixNodes Desktop?

A: Originally, a member of the community developed the software to avoid having to use their web browser to access FalixNodes. Eventfully this 'community' software became official, and that member being Korbs. FalixNodes Desktop was designed to be a simple and quick method to access FalixNodes' services, and it still is. The software has improved greatly over the years and get better in each update.

<br/>

Q: Who are the developers behind FalixNodes Desktop?

A: FalixNodes Desktop is primarly developed and maintained by Korbs Studio. There are some contribors that have helped out in the past.

<br/>

Q: Can I use FalixNodes Desktop?

A: The software supports the following:
 - Windows 8.1/10/11
 - maccOS High Sierra and up
 - Linux (Debian/Fedora/Arch)

It is possible to run FalixNodes Desktop on other operating system like Windows 7 and ChromeOS, however we won't help you if the software is acting buggy on those operating system. As we don't officially support Windows 7 or ChromeOS, or anything else that isn't listed above. 

As for mobile, you can try out our mobile app, which is suppose to serve the same purpose as our desktop software.

<br/>

Q: Is this official software of FalixNodes?

A: Yes, FalixNodes Desktop is offical software and has been approved for FalixNodes since mid-2020.

<br/>

Q: If an update is available, how do I get it?

A: This is done automatically on Windows and Linux, with auto update. We recommend that you wait at the least 1 - 2 minutes for the update to download, or depending on your internet. This usually take about 10 - 30 seconds for decent internet(200mbps).

On macOS, however, each update must be installed manually by the user themself. No, you are not required to do this on a regular basis; nevertheless, updating FalixNodes Desktop is recommended if you want the most up-to-date version in general. It's difficult to support macOS for auto updating at the time being.

<br/>

Q: The CPU usage from FalixNodes Desktop is a bit high, what do I do?

A: FalixNodes Desktop does have a lot going on behind the scene when it's running. High CPU usage is mainly caused by ads loading in the background on the client area and servers panel, sometimes caused by the blur effect of the window. You can easily disable the blur affect in Customization, located in Settings. 

As for the ads, we can't do much about this. 

<br/>

## FAQ - For Developers
Q: Why is Font Awesome included offline? Just use a script instead.

A: Yeah, you're right. I could just use one line of code, linking the script to Font Awesome, and it'll do the trick. But I don't like that for an Electron application.

I keep Font Awesome locally on the software for offline usage. If the user is not connected to the internet, the icons won't load unless Font Awesome if provided locally.

<br/>

Q: Why Electron and what is it?

A.1 (Why): I, Korbs, am mostly comfortable and knowledgeable with web coding languages such as HTML, CSS, and JavaScript, along with APIs by ElectronJS. Using Electron was the right approach for me, and I've acquired a huge amount of experience with it over the last three and a half years. The process of doing cross-platform support was also shortened and easier for me to do. I've also gotten very attach to Electron and am also most comfortable using technology built specifically for the framework like Electron Builder, Glasstron, and more.

A.2 (What): Electron is an open-source software framework developed and maintained by GitHub. It allows for the development of desktop GUI applications using web technologie. It combines the Chromium rendering engine and the Node.js runtime. - [Wikipedia](https://en.wikipedia.org/wiki/Electron_(software_framework))

<br/>

Q: What's the difference between the official X11 package and Korbs Studio's fork of X11?

A: Nothing, literally nothing. The fork only removes a lot of `console.log` code, so it would stop spitting out annoying "Bad Atom" errors when using Glasstron. Korbs Studio, nor the developer of Glasstron, don't know why these errors are happening. 

But I got sick of seeing the error over and over.

___

## Development and Building
## Checklist
 - Using latest version of ElectronJS
 - Using latest version of Electron Builder
 - Using latest version of Glasstron
 - Update server is pointed to correct source
 - FalixNodes Desktop starts up with no errors on all platforms
   - Windows
   - macOS
   - Linux (Bad Atom error allowed)

### Preparing to Develop FalixNodes Desktop
#### Requirements
To run FalixNodes Desktop in development mode and later build it, you must have the following installed on your workstation:
 - NodeJS 14 or 16 (17 will cause a build issue)
 - Python 3.9 and up
 - g++ (Linux)
 - Visual Studio (Windows)
   - Development with C++
 - Visual C++ Redistributable (Windows)
 - At least 2GB of storage (macOS/Linux/Other)
 - At least 8GB of storage (Windows)

It's also a good idea to have a capable code editor and be familiar with the fundamentals of the ElectronJS framework.

### Building FalixNodes Desktop
#### Electron Builder Environment
You should probably adjust a few additional things for Electron Builder before building. 

First off, what is Electron Builder?

We can easily distribute FalixNodes Desktop cross-platform using Electron Builder, which has auto-update support out of the box. We can also distribute our software in other formats if we wanted to like Snap, MSI, PKG, etc.

<br/>

What needs to be changed?

We include assets with our setup files like banners, backgrounds, and licenes. If you're planning on building your software on top of a fork of FalixNodes Desktop, it's best you change these to not confuse users who will use your fork. 

Everything you need to change is located in the `/build` folder, also note that any files in this folder won't be distrbuted as part of the software itself. So if you were to set the software icon, and point to the icon file in the build folder, it won't work in production. The build folder is for Electron Builder only.

You need to change the following files as they may include the name "FalixNodes" or include screenshots of previous versions of FalixNodes Desktop:
 - `/build/background.png` - Background of the DMG installer (macOS)
 - `/build/installSidebar.bmp` - Sidebar banner of the NSIS installer (Windows)
 - `/build/license_*.txt` - All license files
 - `/build/icons`/ - Obviously the icon, the icon included is trademark of FalixNodes Limited

 A Figma file is included if you want to the same layout for the background and banner, Figma is a free tool to use.

#### Metadata
Another thing to change is the metadata of FalixNodes Desktop like the ID, name, versions, update server location, and more.

The following should be changed in <u>package.json</u>:
 - Name
 - Under build config:
    - url
      - This tells the software where to pull new updates from
    - maintainer
      - Example: <u>com.electron.app</u>
    - shortcutName
    - description

Also if you plan to leave the settings page mostly as is, make sure to update the version number manually in there.

#### Building
Now to build the actual software, this process has been made more simple over time during the development of FalixNodes Desktop, all thanks to GitHub Actions and Electron Builder. 

With Electron Builder, you can simply run:
```
npm run build
```

Then Electron builder will start building for your operating system.

If you desire to, or are required to, create the software for multiple operating systems, you may leverage GitHub Actions. Using GitHub Actions, you can write software on many operating systems without having to use them. You can build a DMG file for macOS, for example, without owning or having access to a Mac. Workflow files have been added and are ready to be deployed.

## Credits
 - Developer: [Korbs Studio](https://github.com/KorbsStudio/)
 - Framework: [Electron](https://electronjs.org/)
 - Blur Composition Effect: [Glasstron](https://github.com/NyaomiDEV/Glasstron/)
