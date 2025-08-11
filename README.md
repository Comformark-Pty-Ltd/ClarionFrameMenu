# Clarion for Windows Frame Background Menu

## Using the Frame Background in an MDI application

In a typical MDI application the Frame backgound is inaccessible to the developer and users. This is a demo application showing how a Window procedure can be STARTed from the main frame of an application and styled so it appears to be the frame background. After starting the procedure it can be disabled and resized if necessary, to match the background area of the frame.

This technique is useful for adding branding to an application, showing information to a user, adding more attractive styling to an application etc etc.

If user interaction with this background window is wanted, the window can be enabled and disabled using a simple Windows API command.

To implement this technique in an application the following steps can be used...

1. Add the following in your global map embed...

   ```
   MODULE('GWBFBW_Template')
           GWBDisableWindow(USHORT,SHORT Enabled=False),PASCAL,NAME('EnableWindow')
   END
   ```

3. Declare a global variable to hold the thread number of the window that will serve as the frame background
```
GWBFrameBackgroundThread  LONG
```
4. Create a Window procedure in your Clarion application that will serve as the Frame background. e.g. FrameBackground

5. In your Frame procedure START the procedure after opening the frame
```
  START(FrameBackground,25000)
```

7. In your backgound procedure assign the THREAD value to the global variable using an embed for ThisWIndow.init, BEFORE the window is opened...
```
  GWBFrameBackgroundThread = THREAD()
```

9. In your backgound procedure in an embed AFTER the window is openened call...
```    
  GWBDisableWindow(BackWindow{PROP:Handle})                ! Call the api to disable the window
```

The demo application shows how the background window can be enabled and disabled, if user interaction is required. Otherwise the window will remain disabled.

  



