# GAME COMPANION MANUAL (EN)

**V 1.4.2- Mar/2026**

The Game Companion application works as a personalized gaming environment manager that allows you to manage game libraries and automate the pre- and post-game environment. It was tested on Windows 10 and Windows 11.

Game Companion allows you to configure a library of utilities-such as opentrack, trackir, joystick gremlin, steering or joystick drivers, crewchief, SRS, dial exporters, etc.-as well as a library of local or Steam games. In the registration of utilities, it is possible to indicate whether the utility should be launched before (trackir, crewchief, etc.) or after the game is already running (e.g., OBS), as well as inform its closing method (graceful signal, kill task, or command with arguments) after the game ends.

# Who is this application for?

Lazy users like me, or those tired of using .bat or .cmd files to manage utilities (mainly players) who switch between different software (usually games), who use different applications to configure the environment before use and want the system "cleaned" automatically after use.

# Install

Just copy both GameCompanion.exe and runner.exe to a folder. Better not use it inside Program Files or other "monitored" Windows folders because Game Companion will create a cache folder and log files on this folder as well, and sometimes Windows may be block access to this on these specific monitored folders.

# Main Screen - Game Library

This is what your Game Companion may look like after you create your game library in it. 
On the main screen of Game Companion, you will find your game cards. To start a game, just click on a card. Game Companion will execute the entire utility start sequence, call your game, and at the end of it, execute the entire stop sequence defined on that card. To edit a card, click the edit button in the top right of the card. To change the order of the cards, use the side arrows on each card to make it move in the grid. The change of order can only be made in the ALL category, and the other categories inherit the order of this main category automatically. The buttons appear when you hover your mouse over the cards.

- Status Monitoring: The app monitors if the game is "Starting", "Playing" or if there was an error, displaying this information in a status bar.
- Conflict Prevention: App doesn't let you start a second game while one is still being monitored.
- Initialization Cancellation: If a game takes time to respond, you can cancel the launch process directly through the card.

#### Figure 1 - Main screen
![Main](https://github.com/user-attachments/assets/a9012f5d-1618-47ae-886b-261950590b76)

# Utility Registration

The first step is the registration of utilities, done by the first button in the upper left corner (the one with a tools symbol). This takes us to the screen below, shown already populated with some utilities for the sake of exemplifying.
#### Figure 2- Utility Registration Screen
![Utilities](https://github.com/user-attachments/assets/bbab1904-2335-4d76-88b7-6e18d3723623)

Filling out this screen is simple: On the left side, there is a list of utilities already registered and an X button next to each name for deleting said utility. Clicking on the name of the utility enters the edit mode screen (on the right). To add a utility, when not editing one, just fill in the data on the right screen and press the SAVE button.

**Fields:**

- Name: (what you want to call this utility)
- ID: (leave blank or specify a different name to distinguish from another entry with the same utility name, if any)
- Executable Path: (indicate where the utility is on your disk)
- Arguments: (indicate any call arguments, separated by space)
- Post-launch wait (ms): time to wait until calling the next utility in line or the game
- Instant: (check if this utility closes itself after being called, and doesn't depend on Game Companion to be closed)
- Delay: (check if the utility should be called only after the game is already running)
- Run as Admin: if you need to run as admin just for a specific game, instead of marking the utility to run as admin on Windows, you can mark it here (you can even create two profiles for the same utility, with and without admin permissions)
- Stop Method: choose between 3 ways:
  - Signal: (Windows sends a close signal to the utility)
  - Kill: (Windows kills the utility task) <- guaranteed method
  - Command: (calls the utility again passing defined arguments)

NOTE: The most guaranteed method of closing, although the least elegant, is Force Kill. Test your utilities; if they accept the Signal method, give preference to this. If they have a method that uses arguments, give preference to Command. Use Force Kill as a last resort.

# Game Library Management

Game Companion allows you to centralize your games in a visual interface organized by "cards". To do this, after having registered some utilities, access the second button at the top right of the screen (the one with a game controller symbol). This will open the following screen: 
#### Figure 3- Game registration screen
![Games](https://github.com/user-attachments/assets/5e6079b5-0bf5-4ea1-a8b8-614d25b8471d)

For game registration, we have two methods:

### Via Steam

If your game is from Steam, or if you want to take advantage of a cool game image coming from the Steam library, start by typing the name of the game in the first field (Import from Steam). Select the game from the list that will appear, and the screen will be auto completed with the game's steam:// path and its image. If the game is already installed on your machine, the application will try to locate its most likely executable and fill the "Process Name" field.

Note that some games, such as ARMA 3 or AUTOMOBILISTA 2, have more than one possible executable, and the application may choose one that is not ideal. Always check to ensure that the process name is indeed what your game uses when executed. (e.g.: in ARMA 3, it is usually arma3_x64.exe, and in AMS2 it is usually AMS2AVX.exe).

Some games when launched using steam:// protocol, especially those based on Madness Engine, can present difficulties working with Opentrack or Trackir (or any software that injects something on the shared memory). This is a limitation that I wasn't able to overcome. If you encounter such cases, please make sure to register the game using "local installation method" (below) instead of "steam://" protocol.

### Via local installation

In case you want to register a game that is not from Steam, or if you just used Steam search as a way to quickly populate the image for the game card, fill in the other fields of name, path, and process with the appropriate information. Note: When you indicate a game that is not from Steam, the application seeks to extract the game icon to represent it on the card at the time of saving, unless you explicitly provide an image.  
Remember: the process is usually the game's executable filename. You \*must\* include the extension in it (usually .exe).

The timeout field determines how many seconds Game Companion should wait to detect the game process in memory before judging that the launch wasn't successful. Normally detection is done in less than a second after the game is started, but for cases where the game is triggered from a "launcher" (e.g.: ARMA 3, Assetto Corsa via Content Manager or DCS), you may want to put a longer time to allow the launcher to load, change something in it, and only then execute the game itself. Tip: if possible, if your game has a launcher, configure the launcher to remain in memory after calling the game; this way, you can indicate the launcher process to be monitored instead of the game itself. This is more interesting than monitoring the game directly, avoiding the case of closing the game and returning to the launcher just to configure another session and get the "game closing" process called, terminating all utilities that were opened before the game.

You also have a "wait" time (in ms!) which is the time Game Companion waits to call delayed utilities after the game starts. Default=0.

Games can be assigned to one or more categories. Categories are defined in the general options of Game Companion. More on this later.

### Launch Sequence and Stop Sequence

Here is where the magic happens. On the left we have the Start Sequence list, and on the right we have the Stop Sequence list. On the left side, you mark the utilities you want to execute before the game when you click on your game card. Note that they will appear in reverse order in the right list (in red), which is the order of execution for closing after the game has ended. You can alter the start and end orders by unchecking and marking again in the desired order on both lists. Leaving a utility unchecked in any list indicates to Game Companion that that utility should be ignored when processing said list. E.g.: if you have marked a utility to start by marking it blue on the left list, but do not want Game Companion to close it at the end of the game, you can mark this utility as "Instant" in its utility registration, or alternatively simply uncheck it from the right list (Stop Sequence) in the registration of a specific game. If it isn't marked red, it will be ignored during the close sequence.

**NOTE: Whenever you see a field with a symbol ⓘ next his label, hover the mouse over it to see a quick help.**

# Customization and Global Settings

The user can adjust the appearance and behavior of Game Companion using the third button at the top of the window (the one with a gear wheel symbol), which will open the following window:
#### Figure 4-Global settings screen
![Settings](https://github.com/user-attachments/assets/3372248e-9d25-4be0-be20-792bc5a8b4a2)

- Card Size: Allows adjusting the size of the game grid (small, medium, or large) for better visibility.
- Background Modes: Supports background with dynamic gradient or the use of personalized wallpaper. A default wallpaper accompanies Game Companion, but you can choose another if you prefer.
- Categories: Allows the creation of categories for classifying games. Each game can participate in more than one category. All games participate in the ALL category obligatorily.
- Default Tab: Defines which category should be displayed as soon as the application is opened.
- Auto Close: If checked, it will make Game Companion close after the game session is finished.
- Enable Debug: generates an app.log file in the same folder as Game Companion, where messages of activities performed by the application are stored for verification of its operation. At each new session, the log is overwritten.  
    You can read the log (if any) by pressing the "View Log" button.



# GENERAL NOTES ABOUT GAME COMPANION

**Game Companion was developed in Go + Wails. It uses some techniques that can cause false positives in the antivirus, such as registry and disk scans (to look for the location of Steam and Steam games) and calls to Windows libraries for icon extraction (when the user does not determine an image for the game). In addition, the various library calls to run and close (in 3 different forms!) apps and games often trigger false positives, especially when they're all packaged into such a small utility.**

**Cache and Performance System**

- Image Optimization: All cover images are resized and converted internally to ensure the interface remains fast and consumes little memory.
- Automatic Persistence: Any change in games, utilities, or settings is saved automatically in a config.json file in an atomic way to avoid data loss.
- Calls to utilities and games are done using a detached launcher which dies after the call, avoiding Windows classifying them as "childs" of Game Companion.
- Game Tracking: Done in a very light and efficient way, using Windows' own calls that do not burden the CPU.
- Image Cache: game images and wallpaper are kept and managed in the CACHE folder, inside the folder where Game Companion is installed. The resizing and copying techniques for these images are done to avoid their transfer through memory (stream), making RAM consumption as minimal as possible.

**Simplicity:**

- Game Companion stores all settings on a config.json file in the same folder where the app runs from. You can edit the file if you wish (for instance, if you want to delete a large chunk of games and/or utilities at once), but make sure you know what you're doing.

**Game Companion was designed to help the player with the minimum use of CPU, DISK, and RAM.**

## DISCLAIMER

The developer is not responsible for any damage, including, but not limited to: loss of data, hardware failure, spontaneous combustion, or accidental summoning of supernatural horrors.

If your PC starts to levitate or emit a slight smell of sulfur, consult a priest, not the GitHub issues page, which, by the way, doesn't even exist. On the bright side, this software has a guarantee of doing something. If this "something" is what you expected, or a complete digital meltdown, that is a matter entirely between you and your CPU. By using this software, you completely and irrevocably waive your right to complain, even if the application decides to identify as a toaster and refuses to function until you insert bread.

**Have fun. JoKeR_BR**

# Regarding possible false positives (AV)

If you submit GameCompanion or its runner.exe to VirusTotal or other analysis services, you'll find that a few AVs may cite it as suspicious.

Example of an analysis item made by Hybrid Analysis (<https://hybrid-analysis.com/>) that "scares" a lot of AVs out there:
![VT](https://github.com/user-attachments/assets/bd20bf7c-4b63-4be3-9835-ebbd8a4983e5)

This message is a **classic false positive** from static analysis tools (such as CrowdStrike or VirusTotal). Here's the technical explanation of why this happens:

1\. Where does Game Companion use "Encryption"?

Game Companion does NOT use encryption to obfuscate the code, but uses **advapi32.dll** for two legitimate and necessary reasons:

- **Windows registry:** The runner.exe, which is responsible for calling and closing apps and games in a way that is not tied to the main app, uses the registry package to find out where Steam is installed. On Windows, all registry access functions (such as RegOpenKeyEx) are inside the advapi32.dll.
- **Random Number Generation:** Wails (and packages like google/uuid that it uses) needs to generate unique IDs when a game is registered. In Go, this calls the crypto/rand package, which in Windows uses advapi32.dll functions (such as CryptGenRandom) to ensure that the numbers are actually random and safe.

2\. Why does the alert say "for obfuscation"?

Antiviruses use heuristics: they know that malware uses advapi32.dll to encrypt its own data and hide (obfuscation). Since Game Companion is an "unknown publisher" and uses this DLL, the antivirus bot assumes the "worst-case scenario" (use for obfuscation) rather than the "real scenario" (use to read the registry or generate an ID).

3\. What about "Microsoft.CognitiveServices.Speech.core.dll"?

There is a simple explanation: This DLL **is not part of Game Companion**. What happens is that the static antivirus analyzer has a database of "behavior signatures". He's saying, _"I've seen this pattern of advapi32.dll calls in your app, and this pattern is identical to what I've seen in an official Microsoft component (Speech Core)."_

That is, it is comparing the behavior of Game Companion with that of a Microsoft voice component to try to classify what Game Companion is doing. **It is a comparison, not a dependency.**

### Abstract

- **Use of Encryption:** No, Go uses the Windows security components (advapi32) only to read the Registry and generate random IDs.
- **Obfuscation:** There is none. It's just an assumption of the analyzer robot.
- **Risk:** Zero. It is a default behavior of any Go/Wails application that interacts with the system.

As mentioned in the manual's note, Game Companion performs several file and search operations that make it suspicious to code analyzers, but it does nothing but call and close applications and games. This is another reason why standalone apps in Go suffer from false positives: the Go runtime makes system calls that antivirus programs consider "too deep" for a simple app. If in doubt, just run it inside a sandbox and see for yourself.

Cheers,

JoKeR_BR
