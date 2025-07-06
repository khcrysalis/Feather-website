# Frequently Asked Questions

!!! abstract "Can't install apps?"
    If you're having issues signing, the first troubleshooting step should be to `update SSL certificates`. This option is in the Settings menu.

!!! abstract "One of my repositories just isn't working."
    If you're having issues with one specific repository, the odds are that there is something wrong either the link you've entered, or the repository itself, rather than Feather.

!!! abstract "I'm using idevice and nothing's working properly."
    Feather supports idevice configuration, but remember that you'll **need** to use a pairing file and VPN.

!!! abstract "I can't change the app icon for this app I just installed with Feather."
    Some apps let the user change the app icon manually, in-app. A limitation of this is that it requires the app to have the same bundle ID as the profile it's signed with. So, for most users that use a single certificate and profile to sign several apps, you will **not** be able to change the icons of those apps. This is not something Feather can control at the moment. Remember that you can only use a bundle ID once per device at a time, so you can't have multiple apps installed at once with the same ID. Also, note that changing the bundle ID of an installed app puts you at risk for losing **all** of the app's data.

!!! abstract "My links aren't opening in-app."
    Deep linking, ie opening an Instagram link in Safari to take you to the Instagram app, will likely **not** work if the app's bundle ID is changed. If you need this functionality, **don't** change the bundle ID of those specific apps. Alternatively you can write a Safari extension; but that's a bit more technical.

!!! success "I've tried all of this and I'm still stuck."
    Make an [issue](https://github.com/khcrysalis/Feather/issues/new/choose) on GitHub! 