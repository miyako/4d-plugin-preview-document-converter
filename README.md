# 4d-plugin-preview-document-converter
Convert document to PDF with Preview.app

### Platform

| carbon | cocoa | win32 | win64 |
|:------:|:-----:|:---------:|:---------:|
|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|||

### Version

<img src="https://cloud.githubusercontent.com/assets/1725068/18940649/21945000-8645-11e6-86ed-4a0f800e5a73.png" width="32" height="32" /> <img src="https://cloud.githubusercontent.com/assets/1725068/18940648/2192ddba-8645-11e6-864d-6d5692d55717.png" width="32" height="32" />

---

## Syntax

```
PREVIEW DOCUMENT TO PDF (src;dst)
```

Parameter|Type|Description
------------|------------|----
src|TEXT|
dst|TEXT|

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
