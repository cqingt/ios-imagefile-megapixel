# Mega pixel image rendering library for iOS6 Safari

# 前端图片上传压缩

# twitter 图片上传逻辑：

//将canvas转为 blob 前端压缩图片上传
	function convertCanvasToBlob(canvas) {
			var format = "image/jpeg";
			var base64 = canvas.toDataURL(format);
			var code = window.atob(base64.split(",")[1]);
			var aBuffer = new window.ArrayBuffer(code.length);
			var uBuffer = new window.Uint8Array(aBuffer);
			for(var i = 0; i < code.length; i++){
				uBuffer[i] = code.charCodeAt(i);
			}
			var Builder = window.WebKitBlobBuilder || window.MozBlobBuilder;
			if(Builder){
				var builder = new Builder;
				builder.append(buffer);
				return builder.getBlob(format);
			} else {
				return new window.Blob([ buffer ], {type: format});
			}
		}

Fixes iOS6 Safari's image file rendering issue for large size image (over mega-pixel), which causes unexpected subsampling when drawing it in canvas.
By using this library, you can safely render the image with proper stretching.

About iOS Safari's resource limitation and subsampling, see following link:
[http://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariWebContent/CreatingContentforSafarioniPhone/CreatingContentforSafarioniPhone.html#//apple_ref/doc/uid/TP40006482-SW15](http://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariWebContent/CreatingContentforSafarioniPhone/CreatingContentforSafarioniPhone.html#//apple_ref/doc/uid/TP40006482-SW15)

Although it mainly focuses fixing iOS Safari related issues, it can be safely used in the envionments other than iOS6.


## Usage

See ./test directory.


## FAQ
Q. Photos from iPhone is rotated and not in correct orientation.  
A. Orientation of jpeg file is recorded in EXIF format. This library won't detect exif information automatically. To detect the information in JavaScript, use exif.js (https://github.com/jseidelin/exif-js).


## Note

This project is not actively maintained by the author, and finding someone can contribute as a maintainer. See https://github.com/stomita/ios-imagefile-megapixel/issues/34 .
