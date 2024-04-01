UsbTest
=========

Test app to confirm whether or not app can get USB permission for UVC device with verious target SDK version.

## Background
As documents on [Android Developers](https://developer.android.com/reference/android/hardware/usb/UsbManager.html#requestPermission(android.hardware.usb.UsbDevice,%20android.app.PendingIntent)) shows, app that use USB WebCam(UVC device) needs `CAMERA permission` if it runs on Android 9 and later.
But even if app has `CAMERA permission`, app can't get USB permission to access UVC device on Android 10 if target SDK version is 28 and later.

### The result of my tests  

OK in following tables means app could get USB permission NG means app could't get permission.

* targe SDK version <= 27

 |   | UVC, has CAMERA permission | UVC, has no CAMERA permission | other USB device | 
 --- | :---: | :---: | :---:
 | Android <= 8 | OK | OK | OK |
 | Android 9 | OK | NG(expected) | OK |
 | Android 10 | OK | NG(expected) | OK |

* targe SDK version >= 28

 |   | UVC, has CAMERA permission | UVC, has no CAMERA permission | other USB device | 
 --- | :---: | :---: | :---:
 | Android < 8 | OK | OK | OK |
 | Android 9 | OK | NG(expected) | OK |
 | Android 10 | **NG (unexpected)** | NG(expected) | OK |


* Test devices:
   * Android 10:
      * Pixel3
      * Essential Phone PH-1
   * Android 9:
      * Moto g(6) plus
   * Android 8:
      * Moto Z Play
      * Moto Z2 Play
      * ASUS ZenPhone 4 Pro    


### Note:  
   When app request permission, or when user give permission from system permission dialog, Android output error message on logCat regardless app has `CAMERA permission` or not.  
   ```
   UsbUserSettingsManager: Camera permission required for USB video class devices
   ```

Adaptado de:
https://github.com/saki4510t/UVCPermissionTest
