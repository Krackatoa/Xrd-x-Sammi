# Guilty Gear Xrd x SAMMI

A Bridge Extension for [SAMMI](https://sammi.solutions). It allows you to receive data from [ggxrd-mod](https://github.com/super-continent/ggxrd-mod) in the form of a button that fills with data at 60Hz, and Extension Triggers for individual, one-off events. It's currently separated into these two mechanisms for performance reasons. The data stream to the button may become an Extension Trigger of it's own at a later date.

## Quick Start Guide

Step 1: Download [SAMMI](https://sammi.solutions).

Step 2: Follow the various [SAMMI Onboarding Tutorials](https://sammi.solutions/docs/getting-started/step-by-step).

Step 3: Install Guilty Gear Xrd x SAMMI as a [SAMMI Bridge](https://sammi.solutions/docs/bridge) Extension.

Step 4: Boot up Guilty Gear Xrd while SAMMI and SAMMI Bridge are open to automatically connect.

Step 5: Access the Xrd_Data button for gamestate info, and make use of the various Extension Triggers generated by Xrd to drive stream gimmicks!

## Using the Mod
### Accessing the per-frame update
After installing, you can access the live datastream by referencing it directly in your commands. A reference to datastream Variables will look like:

| Example | Description |
| --- | --- |
| `Xrd_data.data.data.player_1.character` | Retrieves the current character in P1 slot. |
| `Xrd_data.data.data.current_frame` | Retrieves the current frame. |
| `Xrd_Data.data.data.player_2.steam_id` | Retrieves the Steam ID for the P2 slot. Netplay Only. Outside of netplay it always returns `0`. |

### Triggering Buttons via the per-frame update
Some buttons want to run logic on every frame of gameplay. Because we currently use a workaround to support the full 60FPS data stream, there is no Extension Trigger that can perform this.

Inside the button of ID `Xrd_Triggers`, insert the `Trigger Button` command in the appropriate field, with the variable set to whatever button you would like to trigger in time with the incoming data stream.

### Accessing Events via Extension Triggers
The following Extension Triggers are available for use. Add them to buttons via a button's Trigger menu. They all contain extremely relevant data within that can be accessed via the `Trigger Pull Button` command.

| Extension Trigger | Description |
| --- | --- |
| `ggxrd_hitEvent` | Occurs on Hit or Block. Contains relevant data. |
| `ggxrd_objectCreatedEvent` | Triggers on Object Generation. These can be logic objects, projectiles or special effects. |
| `ggxrd_roundStartEvent` | Triggers on Round Start. |
| `ggxrd_roundEndEvent` | Triggers on Round End. |
| `ggxrd_comboEndEvent` | Combo Summary! Corrals all the data from the last combo. |
| `ggxrd_gamestateDeinitialized` | Triggers when you leave a match or the application closes mid-match. |

### Example of Detecting Level 3 Mist Finer.
This is in the Commands screen of a button set up with the `ggxrd_hitEvent` Extension Trigger. The ggxrd_hitEvent trigger sends along it's own data object, separate from the one in the `Xrd_Data` button.

![image](https://github.com/user-attachments/assets/50741a4c-6f03-4601-b677-6ed87b04acd5)

### Example of Detecting if a character is Blitzing on a given frame.

This is in the Commands screen of a button with no Extension Trigger. If you look closely, the commands reference the current character state in the data stream via `Xrd_Data.data.data.player_1.state`

Adding the variable `is_blitzing` to the Init Variables:

![image](https://github.com/user-attachments/assets/4f4bf3c1-f059-419d-89ea-a1559de68cb3)

![image](https://github.com/user-attachments/assets/59d644c5-f61e-42b3-b396-d8c25eb0db8c)

Adding the button logic to detect a valid Blitz state on P1 side:

![image](https://github.com/user-attachments/assets/aa377c0c-05eb-4fb9-ae33-a5a051509703)

In order for this button to run on every frame, we need to add it to the `Xrd_Triggers` button provided in the Extension deck.

The `Xrd_Triggers` Button:

![image](https://github.com/user-attachments/assets/a47944e4-2734-4fd9-8c75-557c19401a15)

Inside the `Xrd_Triggers` Button:

![image](https://github.com/user-attachments/assets/82af8219-add4-47f0-b71b-e56a967d55a5)

## More Information

Check out [the Xrd Websocket mod](https://github.com/super-continent/ggxrd-mod) for more information.
