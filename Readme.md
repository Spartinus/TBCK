## Project Overview

TBCK doesn't document every toggle because everyone can Google what each setting really changes and most of them are self-explaining anyway or they getting changed/removed by Mozilla after some time.


* [Mozilla Thunderbird](https://www.thunderbird.net/en-US/): _60.7.0_ ([Changelog](https://www.thunderbird.net/en-US/thunderbird/60.7.0/releasenotes/)) + [67 Beta 3](https://www.thunderbird.net/en-US/thunderbird/67.0beta/releasenotes/)
* [Thunderbird via Microsoft Store](https://www.microsoft.com/en-us/p/thunderbird/9pcvbx66llqf?activetab=pivot%3Aoverviewtab) - **Partially supported**
* [Eudora](https://wiki.mozilla.org/Eudora_Releases) - **Not supported!** 

Please remember to backup your original `prefs.js` file before you add the modified user.js file into your profile folder! 

This repository contains a list of about:config settings that I have changed for both preferential reasons, and also privacy and security reasons.

### Windows & Linux

The user.js files are  usually identical. The only difference is that the windows version has
Windows friendly carriage returns which you need to change yourself if you like to use the configuration on your Linux OS. 

### Configuration usage

In Thunderbird, you can get into the `about:config` window by going to
`Edit -> Preferences`, then select the `Advanced` panel, and then select the
`General` tab. Now click `Config Editor`.

In short, you can either go to the url `about:config` and search for the configs
manually and set them, or you can move the user.js file to the
[profile folder](http://kb.mozillazine.org/Profile_folder) which differs across
operating systems.

### Extensions

`extensions.strictCompatibility` is set to `false`, since Thunderbird 60.0 Beta 8 all add-ons which aren't labeled as _Thunderbird 60 compatible_ otherwise won't load anymore.

I use the following extensions, so you might find extension specific flags in the _user.js_ file, even if you're not using them, it's not needed to remove them manually from the configuration since they getting ignored by Thunderbird.

* [Engimail](https://addons.mozilla.org/en-US/thunderbird/addon/enigmail/?src=cb-dl-mostpopular)
* [KeeBird](https://addons.mozilla.org/en-US/thunderbird/addon/keebird/?src=cb-dl-recentlyadded)
* [Great DANE](https://addons.mozilla.org/en-US/thunderbird/addon/great-dane-smime/?src=cb-dl-recentlyadded) - incompatible with TB 60+
* [Allow HTML Temp](https://addons.mozilla.org/en-US/thunderbird/addon/allow-html-temp/?src=cb-dl-users)
* [MinimizeToTray Reanimated](https://addons.thunderbird.net/en-US/thunderbird/addon/minimizetotray-reanimated/?src=ss)
* [MEGAbird](https://addons.mozilla.org/EN-US/thunderbird/addon/megabird/?src=cb-dl-users)
* [Encrypt if possible](https://addons.mozilla.org/EN-US/thunderbird/addon/encrypt-if-possible/?src=cb-dl-users) 
* [Secure Addressing](https://addons.mozilla.org/en-US/thunderbird/addon/secure-addressing/?src=cb-dl-created)
* [TorBirdy](https://addons.mozilla.org/en-US/thunderbird/addon/torbirdy/?src=cb-dl-created) 
* [ReloadPAC](https://addons.mozilla.org/en-US/thunderbird/addon/reloadpac/?src=cb-dl-created)
* [Copy Folder](https://addons.mozilla.org/en-US/thunderbird/addon/copy-folder/?src=cb-dl-popular)
* [Stego Block](https://addons.mozilla.org/en-US/thunderbird/addon/stego-block/?src=cb-dl-popular) - incompatible with TB 60+
* [Logout](https://addons.mozilla.org/en-US/thunderbird/addon/logout/?src=cb-dl-popular)
* [Sensitivity Header](https://addons.mozilla.org/en-US/thunderbird/addon/sensitivity-header/?src=cb-dl-popular)
* uBlock ([not officially Thunderbird ready](https://github.com/gorhill/uBlock/issues/3698))
* (optional) [ProtonMail Bridge](https://protonmail.com/bridge/)

### How to install uBlock Origin into Thunderbird?

The extension is not officially in the Thunderbird Store (AMO), however you can manually install the extension by downloading the `uBlock0_[version].thunderbird.xpi` from the official source and then drag & drop it into Thunderbird's Add-ons Manager pane.

## Warning for AntiVirus User

**DO NOT** enable the function to allow your AV to scan your inbox, disable this in your AV program **AND** in Thunderbird. 

The problem with this function is a possible security risk. This function not only allows the AV engine to scan the files it also _opens_ the emails to inspect it's content and attachment which might trigger certain things, like placing a cookie or to let the original transmitter know if you read it or in the worst case scenario (if it's really spam) to trigger an automatically subscription.

## Attacks against S/MIME and PGP

In the recently published ["Johnny-You-Are-Fired"](https://github.com/RUB-NDS/Johnny-You-Are-Fired) [(paper)](https://github.com/RUB-NDS/Johnny-You-Are-Fired/blob/master/paper/johnny-fired.pdf) publication we learned that the signature check can be bypassed. 

What can (currently) be abused?
* Exploiting the CMS (Cryptographic Message Syntax) flaws
* Performing GnuPG API injection attacks
* Constructing non-standard MIME trees
* Displaying valid ID on the email header with a false signature
* Mimicking valid signatures on the UI by using HTML and CSS

So how do we migrate this in order to protect ourselves? 

We disable/block HTML-Code in eMails and we disallow to download third-party content (both is already done via our hardened user.js). The rest must be fixed within the plugins because the mentioned attacks are not targeting the OpenPGP or S/MIME standard or underpinning cryptographic primitives they are basically abusing various flawed implementations.
