# Debugging Gaia in Desktop B2G

Of course, all you probably care about is running the debugger; as you should!
Here's how you do it.

## The Dev Tools

Make sure you have [Firefox
Aurora](http://www.mozilla.org/en-US/firefox/aurora/) or [Firefox
Nightly](http://nightly.mozilla.org/) for the latest Dev Tools stuff. If you're
curious how to run Firefox stable and Firefox Aurora together, check out how to
[add and manage
profiles](https://developer.mozilla.org/en-US/docs/Mozilla/Multiple_Firefox_Profiles).
You can make a separate profile for each and opt to be prompted which profile
to open when Firefox starts. 

Once you have it installed, open `about:config` and change the
`devtools.debugger.remote-enabled` setting to true.

## Configuration

You need to build gaia with debugging enabled. Create a file in the `build`
directory called `custom-prefs.js`. Here's what
`/path/to/gaia/build/custom-prefs.js` should look contain:

```
user_pref("marionette.defaultPrefs.enabled", false);
user_pref("devtools.debugger.log", true);
user_pref("devtools.debugger.remote-enabled", true);
user_pref("devtools.debugger.force-local", false);
```

When you make gaia, specify you want debug mode. Do that with:

```
DEBUG=1 make
```

## Get your hands dirty

Fire up `b2g-bin` with your gaia profile. Once you've unlocked the screen in
B2G desktop, open up the `Settings` App. The remote debugging is burried in
`Settings > Device Information > More Information > Developer` and a toggle is
present for `Remote Debugging`. Enable it. 

In Firefox, connect to the B2G desktop application by choosing `Connect...` in
the `Tools > Web Developer` menu. Connect to `localhost` on port `6000` and
you're all set! If you don't see `Connect`, turn on remote debugging in Firefox
in `about:config` and toggle `devtools.debugger.remote-enabled` to true.

## Asides

If you need to change the port for some reason (you already are using a service
that requires that, albeit unlikely) you can change it in the
`build/custom-prefs.js` file with `user_pref("devtools.debugger.remote-port",
XXXX);` where XXXX is the port number. 