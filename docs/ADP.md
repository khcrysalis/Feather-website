---
hide:
  - toc
---

# Using an Apple Developer Account
This page will guide you through getting the proper files from your account associated with `ADP` (Apple Developer Program) that are required to use Feather. The instructions are slightly different depending on whether or not you're on macOS. You'll need to use a computer to do the initial set up (gather the certificates), but once you have that everything else can be done on-device.


??? "macOS"

    ## Gathering Files

    ### Obtaining the `.p12`

    1. Open `Keychain Access.app` on your macOS device

        * Find Certificate Assistant
        * Request a Certificate from a Certificate Authority

        Input a personal email address into the user email address section, enter a common name, and enter the email associated with your Apple Developer Account under the CA address section. Select `save to disk`, and then proceed.

    2. Go to the Apple Developer Portal, go to the Certificates section, select Apple Distribution, and then upload your certificate request (it should be a `.csr`, we generated this in the previous step)
        * Download your `.cer` file after this step

    3. Import the `.cer` file into keychain access (drag and drop works fine)

    4. You will now be able to select the certificate and export as a `.p12` file. (This step will have you create a password, **remember this for the end**)

    ### Obtaining the `.mobileprovision`

    1. Go back to your Apple Developer Program profile and under Identifiers, create a new App ID. Make this App ID explicit rather than wildcard, and enter your preferred reverse-domain name string (com.blank.yourshere for example), enable the following capabilites:

        * Associated Domains
        * Custom Network Protocol
        * MDM Managed Associated Domains
        * Network Extensions

        Feather needs these to properly sign and install `.ipa` files.
    2. If you haven't already, add your iOS device under the Devices section with your UDID.
        * Use iTunes to find your UDID
        * Or, use [udid.tech](https://udid.tech) to check what your UDID; this has to be downloaded on-device
    3. Under Profiles, register one under Adhoc distribution, select the App ID you created previously, and select your iOS device (only devices added under Devices will appear in this list)

        * Click continue and you will be able to download your `.mobileprovision`

    ### Obtaining the Feather `.ipa`

    1. Download the latest Feather `.ipa` from <https://github.com/khcrysalis/Feather/releases>

    ## Installation

    1. Go to [sign.ipasign.cc](https://sign.ipasign.cc) (this must be done **on your device**)
        * Upload all the neccessary files
            * `.p12`, `.mobileprovision` & the Feather `.ipa`
            * Enter your password (the one you chose earlier)
        * Press `Sign it now!`, and it will proceed to install. There will be prompts that pop up on-screen

    ## Usage 

    1. Make sure Feather has been installed and signed properly
    2. Open Feather and go to the settings tab in the bottom left corner, scroll down to signing, and add your files (`.p12` & `.mobileprovision`)
        * You will need to enter a password, this will be the one you chose earlier. If you don't remember this, you'll have to start all over

    **You're all good to go!**

??? "Any other OS"
    ## Gathering Files

    ### Obtaining the `.p12`

    We use `OpenSSL`, an open-source library with functions to replace that of Apple's proprietary `Keychain Access.app` on non-macOS operating systems. This is likely preinstalled depending on your OS, but if not, you will **need** to install it to generate the certificate files Feather needs.

    You'll run the following two commands to generate a .csr and .key file. You'll be prompted for information after running each one, and while some of it is optional, enter however much you can for best results.
    - `openssl genrsa -out csr.key 2048`
    - `openssl req -new -key csr.key -out csr.csr`

    3. Head over to the Apple Developer portal, go to the Certificates section, select Apple Distribution, and then upload your certificate request (the `.csr` file we generated in the previous step).
        * Download your `.cer` file here

    4. Run this command after changing the `.cer` path for your own; this converts the file into a different format required for the next step (`.pem`)
    `openssl x509 -in <path/to/cer.cer> -inform DER -out distribution.pem -outform PEM`

    5. Run this command after changing the `.key` path for your own, and the `.pem` path for your own (we've generated these files in previous steps)
    `openssl pkcs12 -export -inkey </path/to/key.key> -in <path/to/pem.pem> -out distribution.p12`

    **You need to enter a password when prompted. Remember this for later**.


    Now that you have your `.p12`, everything else can be done through the online Apple Development portal.

    ### Obtaining the `.mobileprovision`

    1. Go back to your Apple Developer Program profile and under Identifiers, create a new App ID. Make this App ID explicit rather than wildcard, and enter your preferred reverse-domain name string (com.blank.yourshere for example), enable the following capabilites:

        * Associated Domains
        * Custom Network Protocol
        * MDM Managed Associated Domains
        * Network Extensions

        Feather needs these to properly sign and install `.ipa` files.
    2. If you haven't already, add your iOS device under the Devices section with your UDID.
        * Use iTunes to find your UDID
        * Or, use [udid.tech](https://udid.tech) to check what your UDID; this has to be downloaded on-device
    3. Under Profiles, register one under Adhoc distribution, select the App ID you created previously, and select your iOS device (only devices added under Devices will appear in this list)

        * Click continue and you will be able to download your `.mobileprovision`

    ### Obtaining the Feather `.ipa`

    1. Download the latest Feather `.ipa` from <https://github.com/khcrysalis/Feather/releases>

    ## Installation

    1. Go to [sign.ipasign.cc](https://sign.ipasign.cc) (this must be done **on your device**)
        * Upload all the neccessary files
            * `.p12`, `.mobileprovision` & the Feather `.ipa`
            * Enter your password (the one you chose earlier)
        * Press `Sign it now!`, and it will proceed to install. There will be prompts that pop up on-screen

    ## Usage 

    1. Make sure Feather has been installed and signed properly
    2. Open Feather and go to the settings tab in the bottom left corner, scroll down to signing, and add your files (`.p12` & `.mobileprovision`)
        * You will need to enter a password, this will be the one you chose earlier. If you don't remember this, you'll have to start all over

    **You're all good to go!**

!!! Tip
    DNS methods to install and sign Feather are not covered in this guide, however if you're using one please do not blacklist `*.backloop.dev`. Doing so would interfere with Feather's functionality.