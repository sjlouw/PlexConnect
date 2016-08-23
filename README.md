# PlexConnect
or: "Plex @ aTV - think different..."

<a href="https://github.com/iBaa/PlexConnect">
<img src="https://github.com/sjlouw/PlexConnect/raw/master/assets/icons/icon%401080.png" border="0">
</a>

This is a collection of files developed for the little project described in this [Plex Forum thread][].

For more information, like detailed Installation Guides, FAQs and similar, visit the [Wiki][].


## How does it work?
The basic idea is, to...
- re-use an already available app (like YouTube, Vimeo, ... in this case: Apple Trailers)
- re-route the request to your local Plex Media Server
- re-work the reply to fit into AppleTV's XML communication scheme
- let iOS do the rest


## Requirements
- Python 2.6.x with minor issues: ElementTree doesn't support tag indices.
- Python 2.7.x recommended.


## Installation
```sh
# Installation
git clone https://github.com/sjlouw/PlexConnect.git
# Updating
cd PlexConnect
git pull
```

- create HTTPS/SSL certificate
- install certificate to ```assets/certificate/```
- install certificate on aTV

See the [Wiki - Install Guide][] for additional documentation.


## Usage
```sh
# Run with root privileges
sudo ./PlexConnect.py
```
> Depending on your OS, you might only need ```PlexConnect.py```. Or ```python PlexConnect.py``` or ...

- set your AppleTV's DNS address to the computer running PlexConnect
- run the Trailer App

See the [Wiki - Advanced Settings][] for more details on configuration and advanced settings.


## Installing the custom Plex icon from assets/icons/*.png :

- First, if you use an Ethernet connection with your AppleTV,
disconnect it from the other end (not your ATV end).
- Next, connect the Ethernet cable to somewhere to go nowhere
(e.g. a laptop or desktop that is powered on but won't allow the
AppleTV to connect to the internet!). If you use a wireless connection
you should also do this, or you can disconnect your router from the
outside world (unplug your DSL cable or equivalent) but keep it powered
on so it hands out IP addresses!
- Next, reset your AppleTV to factory settings (Settings > General >
Reset > Reset All Settings).
- When your AppleTV has finished, follow through the setup, pressing
MENU when you reach the wireless setup screen so you don't connect to
the web. Afterwards you should only see the Computers and Settings
options, since it hasn't connected to the web and doesn't have any
additional options.
- Now go to Settings > General > Network and set your DNS settings as
per the PlexConnect installation guide. Once that's done reconnect your
router / ethernet lead and let your AppleTV loose on the web! It should
connect to Plex as well as modifying the Trailers icon to a Plex icon!


## More detailed Information about the files
* __PlexConnect.py__ - 
Main script file, invoking the DNSServer and WebServer into seperate processes.
* __PlexAPI.py__ - 
Collection of Plex Media Server/MyPlex "connector functions": Auto discovery of running PMSs: Good Day Mate! // XML interface to local PMSs // MyPlex integration
* __DNSServer.py__ - 
This is a small DNS server (hence the name) that is now called whenever aTV needs to resolve an internet address. To hijack the trailer App, we will intercept and re-route all queries to trailers.apple.com. Every other query will be forwarded to the next, your original DNS.
* __WebServer.py__ - 
This script provides the directory content of "assets" to aTV. Additionally it will forward aTV's directory requests to PMS and provide a aTV compatible XML back.
Every media (video, thumbnails...) is URL-wise connected to PMS, so aTV directly accesses the Plex database.
* __XMLConverter.py__ - 
This script contains the XML adaption from Plex Media Server's response to valid aTV XML files.
* __Settings.py__ - 
Basic settings collection. Creates ```Settings.cfg``` at first run - which may be modified externally.
* __ATVSettings.py__ - 
Handles the aTV settings like ViewModes or Transcoder options. Stores aTV settings in ```ATVSettings.cfg```.
* __Localize.py__ -
Holds a couple of utility functions for text translation purposes. Uses dictionaries from ```assets/locales/```.
* __Subtitle.py__ -
Subtitle parser functions for PlexConnect's own renderer, converts subs to JSON for easy transfer to aTV.
* __PILBackgrounds.py__ -
Modify and cache fanart images for use by aTV.


[Plex Forum thread]: http://forums.plex.tv/discussion/57831/plex-atv-think-different/p1
[Wiki]: https://github.com/iBaa/PlexConnect/wiki
[Wiki - Install Guide]: https://github.com/iBaa/PlexConnect/wiki/Install-Guide
[Wiki - Advanced Settings]: https://github.com/iBaa/PlexConnect/wiki/Settings-for-advanced-use-and-troubleshooting
