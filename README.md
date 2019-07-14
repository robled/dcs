# DCS Stuff

## Branches

master is intended to hold scripts and other junk needed for easily distributing stuff in here.

Missions live in orphaned branches in their unzipped form. Create an orphaned branch with
`git checkout --orphan <branchname>`. Remember to clear out files from other branches after
creating an orphan branch.

## Making a .miz file

DCS requires the missions file to be zipped and have the **.miz** extension. It's easy enough to
create a zip folder natively in Windows, but be sure to create the zip folder from the files in
the root of the branch and not from a directory containing those files (an easy mistake to make
with the Windows UI). There should be a **mission** file at the root of the zip file.

Your **.miz** (zip) file should look like this:
```
mission-budahas.miz
├── l10n
│   └── DEFAULT
│       ├── dictionary
│       ├── mapResource
│       └── mist_4_3_74.lua
├── mission
├── options
└── warehouses
```

## Skin package management with skindle

skindle is a program that allows a community of DCS hotshots to see one
another's sweet liveries.  Basically, it grabs an agreed-upon list of skins
that everyone should have, and installs them automatically for each wannabe
pilot who runs it.

### How to use skindle

* Download the [standalone EXE file](https://github.com/DontCamp/dcs/releases)
  from the releases page.
* Ensure that you've installed [7-Zip 64-bit](https://7-zip.org/) to the
  default installation directory at **Program Files\7-Zip**
* Run skindle.

In theory, skindle can be configured to run automatically via Steam when you
start DCS via skindle's **batch mode**. The following in the Steam launch
options for DCS might do the trick:

```C:\Windows\System32\cmd.exe /c "C:\Users\me\skindle.exe -b" & %command%```

### Updating the shared skin list

Update [this YAML
file](https://github.com/DontCamp/dcs/blob/master/configs/skins.yml) with the
following:

* `name`: The name of the skin from the DCS files site
* `link`: The page on the DCS files site where the skin can be found
* `dl_url`: Direct link to download the skin file.  To find this direct link,
   press **F12** in your web browser to bring up the development tools, then
   switch to the **Network** tab, then press the **DOWNLOAD** button on the page.
   As the file downloads, the **Network** tab will reveal the direct download
   **Request URL**.
* `type`: The name DCS gives to the subdirectory where skins for this
   particular aircraft live.  Known aircraft types:
   
   ```
   A-10C
   AJS37
   AV8BNA
   f-14b
   F-5E-3
   FA-18C_hornet
   M-2000C
   MiG-21Bis
   uh-1h
   ```
   
* `sub_dir`: The subdirectory inside the skin archive provided by the skin
   author. This setting merely exists to prevent re-installation of skins you
   already have.  If a skin archive contains multiple subdirectories (skins), then
   listing just one of the subdirectories will be sufficient.

### Details for crazy people

skindle is written in Python 3.7.  Source code is
[here](https://github.com/DontCamp/dcs/tree/master/scripts/skindle).
Environment variables are available to override the default configuration
options.  Look at the source if you want to mess with these settings.

Development steps:

* ```pip install requirements.txt```
* ```pyinstaller.exe --onefile skindle.py```
* A standalone EXE file can be distributed from the **dist** subdirectory
  generated by **pyinstaller**

