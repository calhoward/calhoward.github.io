---
title: Seamless Function Key Switching for iTerm2 with Karabiner-Elements and Hammerspoon
date: 2024-09-08 13:54:00 +/-TTTT
image: https://calhoward.com/assets/img/2022/pexels-pixabay-207580-Cropped-min.jpg
---

![]({{ site.baseurl }}/assets/img/2022/pexels-pixabay-207580-Cropped-min.jpg)
*Photo credit - [Pixabay](https://www.pexels.com/@pixabay/)*

## Effortless Function Key Toggling for Terminal and System Tasks

Developers who spend a lot of time in the terminal, especially those working on macOS, know the importance of function keys. When you’re switching between system-level tasks like adjusting brightness and volume and terminal-based tasks like code debugging or managing server sessions, the ability to toggle function keys becomes essential. The challenge? Doing it seamlessly without manually switching profiles or using cumbersome shortcuts.

In this guide, we'll show you how to achieve an elegant, instant function key switch when using iTerm2. With the combined power of Karabiner-Elements and Hammerspoon, this solution will automatically switch your function keys to act as F1-F12 in iTerm2 and revert back to their default macOS functions when you switch to other apps. The result is a smooth, instant transition with no noticeable delay-- exactly what you need when toggling between terminal and non-terminal tasks.

## Why This Setup is a Game-Changer

Before we dive into the technical setup, let's appreciate the simplicity and beauty of this approach:

	- Instant Profile Switching: The beauty of this solution lies in how swiftly it switches between modes based on app focus. There's no lag. As soon as you enter iTerm2, your function keys behave as traditional F1-F12 keys. When you switch back to another app, they instantly revert to their default macOS behavior.
	- No Manual Toggle: Forget having to manually toggle function keys through a modifier or system preferences. Everything happens in the background as you work.
	- Terminal-Specific Functionality: For terminal power users, having easy access to function keys is vital for navigating through apps like Vim, tmux, or debugging sessions. With this setup, you can use the terminal without sacrificing the convenience of system-wide function key actions outside of iTerm2.

Now, let's get this up and running.

##  Install Karabiner-Elements

If you don't already have it, Karabiner-Elements is an essential tool for remapping keys on macOS. It's highly customizable and will allow us to create profiles for different applications.

Download and install Karabiner-Elements from [here](https://karabiner-elements.pqrs.org/).

If you have [homebrew](https://brew.sh/) installed, you can use:

``` bash
brew install karabiner-elements
```

## Install Hammerspoon

Hammerspoon is another powerful macOS automation tool that lets us script actions based on window focus, among many other things.

Download and install Hammerspoon from [here](https://www.hammerspoon.org/).

Homebrew users may use:

``` bash
brew install hammerspoon
```

## Configuring Karabiner-Elements

Karabiner-Elements allows us to create different profiles depending on the focused application, in this case, iTerm2.

Open the Karabiner-Elements configuration file by navigating to '~/.config/karabiner/karabiner.json'.

Replace the contents of 'karabiner.json' with the following:

''' json
{
    "profiles": [
        {
            "fn_function_keys": [
                {
                    "from": { "key_code": "f1" },
                    "to": [{ "key_code": "display_brightness_decrement" }]
                },
                {
                    "from": { "key_code": "f2" },
                    "to": [{ "key_code": "display_brightness_increment" }]
                },
                {
                    "from": { "key_code": "f3" },
                    "to": [{ "key_code": "mission_control" }]
                },
                {
                    "from": { "key_code": "f4" },
                    "to": [{ "key_code": "launchpad" }]
                },
                {
                    "from": { "key_code": "f5" },
                    "to": [{ "key_code": "illumination_decrement" }]
                },
                {
                    "from": { "key_code": "f6" },
                    "to": [{ "key_code": "illumination_increment" }]
                },
                {
                    "from": { "key_code": "f7" },
                    "to": [{ "key_code": "rewind" }]
                },
                {
                    "from": { "key_code": "f8" },
                    "to": [{ "key_code": "play_or_pause" }]
                },
                {
                    "from": { "key_code": "f9" },
                    "to": [{ "key_code": "fastforward" }]
                },
                {
                    "from": { "key_code": "f10" },
                    "to": [{ "key_code": "mute" }]
                },
                {
                    "from": { "key_code": "f11" },
                    "to": [{ "key_code": "volume_decrement" }]
                },
                {
                    "from": { "key_code": "f12" },
                    "to": [{ "key_code": "volume_increment" }]
                }
            ],
            "name": "Default profile",
            "selected": true
        },
        {
            "complex_modifications": {
                "rules": [
                    {
                        "description": "Map F1-F12 to function keys and allow modifiers in iTerm2",
                        "manipulators": [
                            {
                                "from": {
                                    "key_code": "f1",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f1" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f2",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f2" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f3",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f3" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f4",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f4" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f5",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f5" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f6",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f6" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f7",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f7" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f8",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f8" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f9",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f9" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f10",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f10" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f11",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f11" }],
                                "type": "basic"
                            },
                            {
                                "from": {
                                    "key_code": "f12",
                                    "modifiers": { "optional": ["any"] }
                                },
                                "to": [{ "key_code": "f12" }],
                                "type": "basic"
                            }
                        ]
                    }
                ]
            },
            "name": "iTerm2"
        }
    ]
}
'''

This setup creates two profiles: one for iTerm2 where the 'F1'-'F12' keys behave like traditional function keys, and a default profile where they retain their macOS function key behavior (brightness, volume, etc.).

The profiles in the JSON file are structured as follows:

'Default Profile': Assigns the usual system functions (e.g., brightness, volume) to the function keys.
'iTerm2 Profile': Remaps the function keys to behave as standard function keys ('F1'-'F12'), ideal for use in iTerm2.

## Setting up Hammerspoon

We'll use Hammerspoon to detect when iTerm2 is in focus and switch to the appropriate profile in Karabiner-Elements.

Open the Hammerspoon configuration file by navigating to '~/.hammerspoon/init.lua'.

Replace the contents of 'karabiner.json' with the following:

''' lua

'''
    
This script will automatically detect when iTerm2 becomes the active window and trigger the profile switch in Karabiner-Elements.

## Testing the Setup

After configuring both tools, restart Karabiner-Elements and reload the Hammerspoon configuration (click the Hammerspoon icon in the menu bar and choose "'Reload Config'").

Now, open iTerm2 and press any of the function keys ('F1'-'F12'). You should notice that they behave like traditional function keys, enabling functionality that's typically required in a terminal environment. Switch back to any other application, and your function keys will revert to their default macOS behavior-- controlling brightness, volume, and other system settings.

## Enjoy Seamless Switching

With everything set up, you can now enjoy the convenience of instantaneous profile switching. The moment iTerm2 comes into focus, your function keys will adjust accordingly, and they'll seamlessly switch back once you exit iTerm2. The best part is that this setup works quietly in the background-- no more manual toggling or hunting through system preferences to make function keys work as needed.

## Final Thoughts

This setup is a testament to how powerful macOS automation can be when you combine the right tools. By leveraging Karabiner-Elements' flexible key remapping and Hammerspoon's window management capabilities, you can streamline your workflow in a way that feels truly frictionless. Whether you're debugging code, managing servers, or switching between multiple terminal sessions, this configuration ensures that your function keys are always optimized for the task at hand.

In the world of development, these small improvements can make a huge difference. Once you experience the ease of this setup, you'll wonder how you ever lived without it!