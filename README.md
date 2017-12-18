# 4d-plugin-preview-document-converter
Convert document to PDF with Preview.app

### Platform

| carbon | cocoa | win32 | win64 |
|:------:|:-----:|:---------:|:---------:|
|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|||

### Version

<img src="https://cloud.githubusercontent.com/assets/1725068/18940649/21945000-8645-11e6-86ed-4a0f800e5a73.png" width="32" height="32" /> <img src="https://cloud.githubusercontent.com/assets/1725068/18940648/2192ddba-8645-11e6-864d-6d5692d55717.png" width="32" height="32" />

### Remarks

Preview creates an empty PDF the rendering/conversion is incomplete (the display is asynchronous).

**TODO**: ~~Hold ``close`` and repeat while the result document is empty..?~~ retry for ``120`` seconds while file size is < ``1000`` (empty PDF is ``920`` bytes). 

---

## Syntax

```
PREVIEW DOCUMENT TO PDF (src;dst)
```

Parameter|Type|Description
------------|------------|----
src|TEXT|path (HFS)
dst|TEXT|path (HFS)

Effectively the same operation as the ``AppleScript`` code below:

```applescript
on convert_to_pdf(src_path, dst_path)
	tell application "Preview"
		set d to open (POSIX file src_path as alias)
		save d as "com.adobe.pdf" in POSIX file dst_path
		close d saving no
	end tell
end convert_to_pdf

convert_to_pdf("/Users/miyako/Desktop/test.pptx", "/Users/miyako/Desktop/test.pdf")
```

## Examples

```
  //to prepare the app for scripting bridge
  //-g: Do not bring the application to the foreground
  //-j: Launches the app hidden
  //-F: Opens the application fresh, without restoring windows
  //-b: bundle_indentifier

LAUNCH EXTERNAL PROCESS("/usr/bin/open -g -j -F -b com.apple.preview")

$src:=System folder(Desktop)+"test.pptx"
$dst:=System folder(Desktop)+"test.pdf"

PREVIEW DOCUMENT TO PDF ($src;$dst)
```

### Discussion

Preview has the capability to display various document types, including the following. It can also save them as ``PDF``.

```
public.jpeg
public.png
public.tiff
public.fax
public.camera-raw-image
public.xbitmap-image
public.jpeg-2000
public.radiance
public.mpo-image
com.adobe.pdf
com.adobe.postscript
com.adobe.encapsulated-postscript
com.adobe.illustrator.ai-image
com.adobe.photoshop-image
com.ilm.openexr-image
com.compuserve.gif
com.truevision.tga-image
com.sgi.sgi-image
com.kodak.flashpix-imagecom.apple.icns
com.microsoft.ico
com.microsoft.bmp
com.microsoft.word.doc
com.microsoft.word.dot
com.microsoft.word.stationery
com.microsoft.excel.xls
com.microsoft.excel.xlt
com.microsoft.powerpoint.ppt
com.microsoft.powerpoint.pot
com.microsoft.powerpoint.pps
com.apple.quicktime-image
com.apple.pict
com.apple.rjpeg
com.apple.macpaint-image
com.apple.iwork.numbers.numbers
com.apple.iwork.numbers.sffnumbers
com.apple.iwork.pages.pages
com.apple.iwork.pages.sffpages
com.apple.iwork.keynote.key
com.apple.keynote.key
com.apple.iwork.keynote.sffkey
org.openxmlformats.wordprocessingml.document
org.openxmlformats.wordprocessingml.template
org.openxmlformats.wordprocessingml.document.macroenabled
org.openxmlformats.wordprocessingml.template.macroenabled
org.openxmlformats.spreadsheetml.template.macroenabled
org.openxmlformats.spreadsheetml.sheet
org.openxmlformats.spreadsheetml.template
org.openxmlformats.spreadsheetml.sheet.macroenabled
org.openxmlformats.presentationml.presentation
org.openxmlformats.presentationml.template.macroenabled
org.openxmlformats.presentationml.template
org.openxmlformats.presentationml.presentation.macroenabled
org.openxmlformats.presentationml.slideshow
org.openxmlformats.presentationml.slideshow.macroenabled
```
