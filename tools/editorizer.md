---
layout: page
title:  "Editorizer"
categories: [tools]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

The Editorizer is a free program written by Ben for making vehicles. Contributions: Tuusita (Comments, Structure, Connect To).

It's a fairly old and simple program. Note you can't use it to create a new vehicle from scratch, you need to manually create a _.truck_ file with a basic structure. The file must contain a section for nodes, beams, hydros, commands, shocks, and wheels. It can be blank to begin with or when saving but the heading must be there.

# Download and run on Windows

[Download here](https://repofiles.avrintech.net/repofiles-1st-batch/57ddb080d4ea83b7d40df778c916a66a379d4dd1_Editozer.zip) (ZIP archive)

Run as administrator! (only needed on the first run or if you move Editorizer's directory)

## Troubleshooting

If you don't run Editorizer as administrator for the first time, or you subsequently move it's directory, you may encounter this error:
![](/images/editorizer-error-comdlg32ocx.jpeg)

To resolve this, try running as administrator again, and if it doesn't help, try these steps:

-   Find comdlg32.ocx and mscomctl.ocx in Editorizer's directory.
-   On 32-bit Windows:
    -   Move comdlg32.ocx and mscomctl.ocx to _C:\\Windows\\system32_.
    -   Open a command line window and run following commands:
    
        ```
        regsvr32 c:\Windows\system32\comdlg32.ocx
        regsvr32 c:\Windows\system32\mscomctl.ocx
        ```
-   On 64bit Windows:
    -   Move comdlg32.ocx and mscomctl.ocx to _C:\\Windows\\SysWOW64_
    -   Open a command line window and run following commands:
    
        ```
        regsvr32 c:\Windows\SysWOW64\comdlg32.ocx
        regsvr32 c:\Windows\SysWOW64\mscomctl.ocx
        ```

# Download and run on MacOSX

[Download here](http://www.mediafire.com/download/ji2edf2ng4rcy9b/MAC%20RoR%20Editorizer.zip) (ZIP archive)

Requires MacOSX Snow Leopard or Higher.

The mac port is standalone with all the files needed built into the app, Huge thanks to MothBird.

Warning: the file is quite large (511.6MB) because of all of the required frameworks.




