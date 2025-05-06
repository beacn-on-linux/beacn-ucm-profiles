# ALSA UCM Support for Beacn Hardware

This repository primarily exists for manual installation of the profiles. The intent is to eventually
push these files upstream into the ALSA UCM project once complete and verified, for now manual installation
is required.

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
