 # Roccat Tyon Driver Patching
 _Decreasing profile autoswitch delay or changing ScanInterval constant_
 
 ### Prologue

After some years of using gaming mice **Logitech G300** for work I decided to upgrade my hand by new **Roccat Tyon**. (More buttons, bigger size, etc ...)

When I got it, and started using, there appeared one problem. **Logitech G300** was switching profiles according to the application rather quickly, 0.5-1 sec may be, while **Tyon** took 2 times more time — **2 sec**. During my work I actively use Alt+tab, and the 2-second delay is very annoying. So, I started to look for a solution.
***

 ### Searching and solving the problem

1. Googled it first http://roccat.sourceforge.net/general.html (Roccat hardware support for Linux) and learned about the constant:

    >**ScanInterval**
    
    >Sets the interval in seconds, the monitor scans for the active window to change profiles according to gamefile settings. **Windows driver uses fix 2 seconds**. You can change this value to 0 to switch off the monitor completely if you don't use gamefile settings. A value of 1 leads to more responsive profile changes. Setting a value greater 2 leads to more lagging profile changes and does not make much sense.
    >Valid values: integer >= 0
    >Default value: 2
    >Supported since roccat-tools version 1.0.0
    

2. Used [dotPeek](https://www.jetbrains.com/decompiler/) decompiler to find necessary lines of the code in *TyonMonitorW.exe* with `ScanInterval = 2000` or smth like that. There I found 2 lines with value 2000. So, I decided to change this value in the [HEX editor](https://hexed.it) because I would never rebuild this exe back from a decompile state.

3. Used  [Hexed.it](https://hexed.it). There I found two adreses with 2000 value:

   ![Screen 1](https://image.prntscr.com/image/a5d11ce86f2f4da1b7ef8f9c03b52d9a.jpg)
   ![Screen 2](https://image.prntscr.com/image/2ff14905c1b543bfb64458fa5a98f2fc.jpg)
   
   And maked 3 files with values 1000, 500 and 100 respectively. You can find them in the repository https://github.com/frantsmn/TyonDriver. (Just replace and rename like original.) Not sure that all of them work steadily (I use  with 1000ms delay), but profiles switch is now much faster. :)
