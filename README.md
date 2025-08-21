_Valid for Deltamod, version 1.0_

# Deltamod Standard
This file includes information on how a Deltamod modpack should be structured.

## Basic rules of the format.
There should be 3 files (1 optional) dedicated to mod metadata and patching data.
- `_deltamodInfo.json` is a file dedicated to storing the mod's name, authors, version and mod type (full game or demo). (See _deltamodInfo.json section).
- `modding.xml` is the most important file in the modpack. It consists of <patch> tags, which have three fields: `patch`, `to` and `type`. (See modding.xml section)
- `_icon.png` is an optional icon the modder can include in their modpack. It must be a 1:1 image. It isn't included in this example folder.

## `_deltamodInfo.json`

```json
{
    "metadata": {
        "name": "example",
        "version": "1.0.0",
        "description": "Lorem ipsum",
        "author": ["Mod Developer 1", "Mod Developer 2"],
        "demoMod": true
    },
    "neededFiles": [
        {
            "file": "data.win",
            "checksum": "YOUR CHECKSUM HERE"
        }
    ]
}
```
This is an example on how a `_deltamodInfo.json` should be structured. Deltamod checks the file is valid before loading the mod. Missing or corrupted fields will be replaced by a placeholder. 

### `neededFiles`
The `neededFiles` parameter can help you define files needed for your mod to function, but also check if they're the same files you have on your computer.<br /> <br />
When specifying a needed file, you'll need to specify it's name (examples: `data.win`, `chapter1_windows/data.win` if it is in a subfolder) and its checksum, in SHA256 standard. <br /><br />
To calculate a checksum of a file you can simply open it [here](https://emn178.github.io/online-tools/sha256_checksum.html).
**If you specify a needed file, it is required to add a checksum along it.**

## `modding.xml`

```xml
<patch type="xdelta" patch="./example.xdelta" to="./chapter3_windows/data.win" />
<patch type="override" patch="./example.win" to="./chapter4_windows/data.win" />
```

This is an example on how a `modding.xml` should be correctly structured. There are currently 2 types of patch: xdelta (which inputs the file through GM3P in order to patch the requested file) and override (which simply replaces the file.)<br /><br />
Every patch tag has three necessary fields: `patch`, `to` and `type`. If there are any missing/invalid fields, the program will delete the mod from its database and notify the user that the modpack is corrupted.

## Packing in ZIP
Deltamod only supports .ZIP archives. They also must be packaged like so:
```
.
└── (root of ZIP file)/
    ├── _deltamodInfo.json
    ├── modding.xml
    ├── icon.png
    └── (any needed patch file)
```
## License
This standard is licensed under a modified version of the EUPL, _EUPL-1.2-DELTAMOD_. Read it [here](./LICENSE.txt)
