# Customising Remarkable Tablet splash screens and templates

Brief notes on the how to set custom images as splash screens and templates on the [Remarkable Tablet](https://remarkable.com/) using Windows OS. Similar approaches exist for Mac and Linux.

This is not officially endorsed by the device manufacture. Misuse of this method could break the software on your device so proceed with caution and at your own risk. 

# Making PNGs of the correct dimensions

Remarkable table splash screens and templates need to be PNG images of the correct dimensions for the device. 

There are many tools for generating/resizing PNG images. The target dimensions you're aiming for are 1872 x 1404 px.

226 DPI

If using MS Office programs (Powerpoint or Word):

- Set page size to letter or 21.039 cm x 15.778cm
- 'Save As' PDF or PNG rather than using print to pdf functionality.


# Connecting to your remarkable to update splash screen and templates with WinSCP

Use WinSCP login to remarkable from Windows machines. Download and install from: https://winscp.net/

**Do not modify/move/delete/rename any other files on your remarkable.**

Since this method provides full access to the files on your device, you could break functionality or brick your device if you mess around with files you're not supposed to. Proceed at your own risk.

Information from [tips:templates [reMarkableWiki]](https://remarkablewiki.com/tips/templates) and [Connect to your reMarkable from a Windows PC – reMarkable Tablet User](https://remarkabletabletuser.com/2018/01/02/connect-to-your-remarkable-from-a-windows-pc/)

On reMarkable, find the connection address and password under Settings > About > Copyright notices > GPLv3 Compliance. You'll need your root password and the last listed IP address

File protocol: SFTP
Host name: <IP address you gathered in settings help >
Port number: 22
User name: root
Password: <Password you gathered in settings help>

'Warning: Continue connecting to an unknown server...' - disregard this warning and login anyway, assuming you've connected to an IP address from your remarkable (and not some random IP address on the internet).

Once you've updated any files on your remarkable, you'll likely have to restart the device to see the updates (eg new splashscreen/template).

# Splash screens

In WinSCP, the left hand panel shows the folder structure of your computer and the right hand side shows the internal folder structure of your remarkable.
    
![image](https://user-images.githubusercontent.com/17323155/136550100-a2456153-69f3-4c68-84e0-7eefcfe27bde.png)
    
In WinSCP navigate to the folder on the remarkable (Remote menu > Go to > Open Directory): /usr/share/remarkable

There should be a number of .PNG files in this folder, such as starting.png, suspended.png. You should be able to download them from the remarkable to a folder on your local computer to open them and see which name corresponds to each screen. 

To add your own image as a splash screen, copy it to that folder in the remarkable and change the file name so it matches the name of the screen you're trying to replace. Because you can't have two files with the same name, you'll need to rename the original splash screen file (I just add an underscore to the end of the name). 

Since this folder will get wiped everytime remarkable deliver a software update, it's a good idea to keep a copy of your custom splash screens in a folder on your computer so that next time you want to readd them after a software update, it's a simple copy and paste job. 

# Templates

In WinSCP navigate to the folder on the remarkable (Remote menu > Go to > Open Directory): /usr/share/remarkable/templates

Copy and paste your .png templates into the templates folder on the remarkable.

So that the remarkable knows to look for your new templates, you'll need to update a text file in the templates folder called `templates.json` on your remarkable device. Locate and open the file using WinSCP. It'll probably open by default in a text editor such as Notepad.

Explanation of JSON [Good introduction here](https://attacomsian.com/blog/what-is-json)..., lists of items. Items in {curly brackets} ('objects') consist of `"key": "value",`, items in [square brackets] are unnamed lists ('arrays'). You can change the values inside double quotes to be whatever you want. Spaces, tabs and newlines outside of quotation marks don't matter but capitalisation and all other punctuation is important.

For each new template you're copying across, you need to add an item to the list in templates.json that looks something like this:


    {
      "name": "Checklist double",
      "filename": "LS Checklist double",
      "iconCode": "\ue9aa",
      "landscape": true,
      "categories": [
        "Life/organize"
      ]
    },
    

Where "name" is the name of the template that gets displayed on the remarkable device, "filename" is the filename of your new PNG file without the extension. "iconCode" must be from the list [here](https://remarkablewiki.com/tips/templates). Include the line `"landscape": true,` if your template is landscape. Copy and paste this text back into templates.json, making sure to include the curly brackets and the comma. Easiest is to paste them at the top of the list, after `"templates": [`.

Save the templates.json file with your updates. Disconnect and restart your remarkable. 

Since this folder will get wiped every time remarkable deliver a software update, it's a good idea to keep a copy of your custom templates, and the text you copy for templates.json, in a folder on your computer so that next time you want to add them after a software update, it's a simple copy and paste job. Eg, here's the snippet for the two templates I use:

    {
      "name": "5yr Diary",
      "filename": "5yr Diary",
      "iconCode": "\ue977",
      "categories": [
        "Life/organize"
      ]
    },
    {
      "name": "Weekly",
      "filename": "Weekly",
      "iconCode": "\ue9da",
      "categories": [
        "Life/organize"
      ]
    },

