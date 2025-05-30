# ALSA UCM Support for Beacn Hardware

These files have been merged into `alsa-ucm-conf`, and will be included in alsa-lib 1.2.15. This 
repository is being maintained until it's a commonly distributed version.

## ALSA UCM Files for Beacn hardware
This repository is for manual installation of the UCM profiles for Beacn devices. It will correctly
split and present channels as they are on Windows, including the Beacn Link channels if we are USB2.

## Installation

1. Create `/usr/share/alsa/ucm2/USB-Audio/Beacn/`
2. Extract the contents of this repository into that folder
3. Open `/usr/share/alsa/ucm2/USB-Audio/USB-Audio.conf`
4. Locate the `If.goxlr` block, after it, insert:

```
If.beacn-mic {
	Condition {
		Type String
		Haystack "${CardComponents}"
		Needle "USB33ae:0001"
	}
	True.Define.ProfileName "Beacn/Beacn-Mic"
}

If.beacn-studio {
	Condition {
		Type RegexMatch
		String "${CardComponents}"
		Regex "USB33ae:[04]003"
	}
	True.Define.ProfileName "Beacn/Beacn-Studio"
}
```

Then restart your PC, and your Beacn device should appear correctly.


## Notes:
The Beacn Studio comes with two profiles, 'Basic', 'Link'.

The basic profile contains just the headphones and microphone, and the 'Link' profile contains
all the PC2 Link Channels. This is so if you're not using them, you can disable them easily.
