## How to set Firefox new tab to a local file

This works on Windows 10/11 tested on Firefox 136

1. Find your Firefox install location. This would be ```C:\Program Files\Mozilla Firefox``` if Firefox was installed globally     and ```C:\Users\[User]\AppData\Local\Mozilla Firefox``` if Firefox was installed locally.
2. Create the file ```[FirefoxInstallLocation]\defaults\pref\enable-autoconfig.js``` with the code below:
    ```
    // enable autoconfig
    pref("general.config.sandbox_enabled", false);
    
    pref("general.config.filename", "autoconfig.cfg");
    pref("general.config.obscure_value", 0);
    ```
3. Create the file ```[FirefoxInstallLocation]\autoconfig.cfg``` with the code below:
    ```
    //
    var {classes:Cc,interfaces:Ci,utils:Cu} = Components;  
    
    /* set new tab page */  
    try {  
      ChromeUtils.defineESModuleGetters(this, {
        AboutNewTab: "resource:///modules/AboutNewTab.sys.mjs",
      }); 
      var newTabURL = "file:///PATH_TO_YOUR_FILE";  
      AboutNewTab.newTabURL = newTabURL;  
    } catch(e){Cu.reportError(e);} // report errors in the Browser Console
    ```
4. Edit it to point ```newTabURL``` to the file you want to use as your new tab page.\
_Make sure your link includes the ```file:///``` part._

\
Notes:
- Make sure both files use LF (Unix) even if you're on Windows.
- Make sure to make the first line of both files is a comment.
- If Firefox is installed in Program Files, you might need admin permissions to create the files.

\
<sup>Credit to https://www.reddit.com/r/firefox/comments/c8z0hx/help_set_new_tab_page_to_local_file/ and https://www.reddit.com/r/firefox/comments/1iiakze/firefox_136_broke_new_tab_overwrite_code_in/</sup>
