<!-- Translated from PRIVACY.md -->
# Fidenne Privacy

This page says **what Fidenne keeps on your Mac, what it sends off it, and what it does not collect at all**.
Technical details such as file names and addresses are collected at the very end, under "Technical details".

Reference version: <!-- gen:version -->0.5.0<!-- /gen --> · last verified 2026-09-18

- Your audio is neither stored nor sent.
- Information about the song you are listening to leaves only when you use a feature such as lyrics, search, or an integration, and only to the places listed below.
- There is no analytics, advertising, or error-reporting tool in the app, and nothing is logged remotely.

---

## 1. Audio

Fidenne **does not store** the audio it receives and converts. The sound flows through your Mac's memory straight to your DAC and never becomes a file.
There is no recording feature and no "save the current song" feature. The app itself cannot look at the audio data, and it has no way to send audio over the internet (no streaming, upload, or cloud backup).

## 2. What stays on your Mac

All of this is files on your Mac and none of it is sent anywhere. Files the app creates can be read and written only by your account.
File names and locations are under "Technical details".

- **A record of what you listened to** — song title · artist · album · time · which service, plus the sound settings at the time (output mode · sample rate · filter · whether EQ etc. were on · the output device's product name · dropout count) and where you played it from (playlist · album · search, etc.).
  For local files in your library, only an unreadable fingerprint is kept instead of the path. You can turn it off in settings, and clear it with **Clear listening history** on the Listening History page.
- **Resume information** — the last list and song you played, and the position in the song. Turning off or clearing the history removes it too.
- **Remembered sample rate per song** — the rate an Apple Music song was played at, so the next play can start at that rate.
- **Album covers, kept temporarily** — shrunken covers of songs in your history, for quick display; removed after 30 days unused.
- **Headphone measurement · target curves** — copies of the public measurement curves your saved EQ uses.
- **Lyrics** — lyrics that were found are kept for 30 days. They are stored so that the folder listing alone does not reveal what you listened to.
- **Library** — the folders and playlists you added, and the paths · tags · length · album art of the music files in them; several spellings of a song's names and which songs in different services are the same song (including Apple Music · Spotify track numbers). No audio · listening times · accounts.
- **YouTube Music** — imported playlists (the picked CSV file's path and your account are not kept, and no request is made), and, while the browser-extension connection is on, songs played for 5 seconds or more in Chrome · Edge and the lists of playlist · library screens you opened.
  Album art · playback position · queue · volume · liked status stay in memory and are not written to a file. Your account and other pages you visit are not seen. Turning the connection off does not delete received lists; delete them in Library.
- **Settings, presets, ABX results** — filter · EQ · crossfeed · UI scale, presets you named, and the results of comparison tests (no songs or devices). You can reset them in the app.
- **A restore note** — before changing your DAC's sample rate, the app writes down the original value so the next launch can put it back even after a sudden quit. It is removed once restored.
- **The "Fidenne play queue" playlist in the Music app** — when you play an Apple Music list, it fills in the current song and the next ten. A notice asks once before first use, and other playlists are not touched.
  If iCloud library is on, Apple syncs it to your other devices. You can turn it off under Settings › Privacy › Apple Music.
- **Spotify connection information** — only if you connected, and in the macOS Keychain rather than app files. Disconnecting removes it.
- **Diagnostic data for problem reports** — numeric records such as queue latency · dropouts · rate · error codes. The distribution build asks once on the first-run screen as an optional item, and starts recording at launch only if you agreed (you can change it under Settings › Privacy).
  A **diagnostic bundle** is made only when you press "Create diagnostics for a problem report…". It holds numbers and true/false values and the list of songs you heard in that period (time · service · title · artist · album, up to the latest 200). It does not hold file paths · device names · accounts · system logs.

Deleting the matching file or folder on your Mac removes any of these, and the app recreates it when needed.

To find out the sample rate of an Apple Music song, while the app is running it reads only the sample-rate and format numbers from the lines the Music app leaves in the macOS log. The log lines themselves are neither written nor sent; only the numbers are kept, in the per-song memory and the listening history.
On a non-administrator account macOS blocks only the fast method, and this detection carries on by checking the song's information once a second.

## 3. What leaves your Mac

Audio does not leave. But **what you are listening to can.** Only when you use that feature, and only to the places below. Each place can be turned off separately in settings, and they are asked about together on one screen the first time you run the app.
With everything off, playback · sound processing · DAC output and local playback carry on as before; only the integration features that use that place turn off.

- **Lyrics** (LRCLIB) — when first needed, you are told what is sent and asked for consent; nothing is sent before that. If you decline, only a `.lrc` file you connected yourself is used.
  Only four things are sent: song title · artist · album · length (for local files too, never the file path or contents). A lookup happens only after you have listened to the same song for 5 seconds or more.
- **Apple Music** — if you have allowed Apple Music access, the song title and first artist name etc. go to Apple for reading the library and finding other spellings or the same song (with the user token Apple issued). Album name and length do not go.
- **Spotify** — only if you connected, search terms · track and device identifiers · sign-in information go to Spotify. The Client ID is your own developer-app key that you enter yourself, and the app contains no key or token. Without it only the Spotify features turn off and the app works normally.
  **Information received from Spotify is not sent to other services and is not used for song matching or listening statistics.**
- **Store search · recommendations · album art · headphone measurement lists** — at most search terms or the headphone name you chose go to that service; song information does not.
- **Update check** — only when you press "Check for Updates…", or when you turned on automatic checking (off by default, once a day), it reads a new-version notice file from GitHub. A new version is downloaded and installed only when you press, after its signature is verified.
  What goes out is the app version and your IP address; no song · device · settings or system information. The developer does not receive these requests.
- **Received on your Mac only** — there is a temporary doorway that receives the Spotify sign-in result in your browser, and one that receives YouTube Music song information from the Fidenne extension in Chrome · Edge. Neither leaves your Mac, and they are open only while you sign in, or while you have the extension connection on (off by default).
  Over the extension connection, album art is fetched and shrunk by your browser from the image servers the page already uses; the app makes no separate request to an image address.

If a server redirects to another address, it is followed only if that address is allowed and its switch is on; otherwise the request ends. A request to a place not in the list is treated as a defect and fixed.
External links inside the app open in your browser when clicked; they are not requests the app sends.

## 4. If you send a problem report

**The app does not send diagnostic bundles.** "Send by mail" only opens your mail app with the recipient and subject filled in and attaches no bundle, and "Open GitHub issue composer" only opens a new-post screen in your browser. Attaching and sending a bundle is entirely your own action.

1. A report sent by mail reaches only the developer. It is not made public and is not put in the source repository.
2. Before analysis, the sender's name · mail address · signature are removed. The remaining report and diagnostic bundle (which contains the title · artist · service of songs heard in that period) may be read with analysis tools, including AI tools (such as Anthropic's Claude).
3. A diagnostic bundle is deleted within 90 days after the problem is fixed. The mail itself stays in the mailbox because a reply is owed.
4. If you want it deleted sooner, tell us at fidenne.support@gmail.com by mail.

## 5. Permissions the app asks for

- **Audio capture** — to receive system sound and convert it to DSD.
- **Audio input (microphone)** — needed when receiving Fidenne Inlet or an input device you chose, because macOS treats virtual input devices like microphones. Only the chosen device is read; the built-in microphone is not opened separately.
- **Apple Events (automation)** — to show the current song of Apple Music · Spotify and control playback.
- **Apple Music library** — for reading the library and for finding other spellings of a played song and the same song in Apple Music (kept in memory; only the link saying they are the same song is kept). If not allowed, it reads through the Music app and does not look up other spellings.

## 6. What has not yet been verified

- A record of actually measuring, by observing the running app, that no audio file is created: `NOT_RUN` (not done yet).
- A record of checking the destination table below against actual network traffic capture: `NOT_RUN`. The current basis is an exhaustive search of the source code.

---

## Technical details

This part is for people who want to verify. The promises above are checked on every build by automated checks that scan the source (they do not directly measure behavior while the app runs).
In the audio path's code there are no calls that open a file or write bytes other than five recorded exceptions — the coefficient cache, the library index, and the output-rate restore record (writes; not samples), plus two reads of files you picked — and no sample buffers are handed to the app, only numbers and state.

### Files (`~/Library/Application Support/Fidenne/`, readable and writable only by the owner `0o600`)

| What | Where | Contents | How to turn off or delete |
|---|---|---|---|
| Listening history | `listening-history-v1.jsonl` | Title · artist · album · time · source of songs listened to; per song, sound information (output mode · rate · filter order · whether EQ etc. were on · the output device's product name · underrun count) and where it was played from. A local file is recorded as a **hash of its path**, not the path. No audio | Turn off in settings. **Clear listening history** on the Listening History page, or delete the file |
| Song covers | `~/Library/Caches/<app bundle id>/Artwork-v1/` | A temporary cache of the album cover (long side 600 px) of songs in the history. Removed after 30 days unused, or beyond 300 MB. No new destination | Clearing history · delete the folder |
| Received headphone measurement · target curves | `curves/` | Copies of the public measurement · target curves that a saved EQ points to (so they are not fetched again) | Delete the folder — fetched again when next chosen |
| Resume | `last-session-v1.json` · `last-started-v1.json` | The song list and position of the last list played, and the last song's title · artist · album · length · service · position. Local files by path hash | Delete the files. Turning off or clearing history also removes them |
| Remembered track rates | `music-track-rates-v1.json` | The sample rate each Apple Music song was played at (per song ID · album name, up to 5,000 songs · 1,000 albums) | Delete the file — it learns again |
| Diagnostic numbers · runs | `Diagnostics-v1/` · `Diagnostics-Runs/` | Numeric time series such as queue latency · underruns · rate · error codes. A device is a per-run alias number, not a UID. The distribution build asks once on the first-run screen as an [optional] item and opens a run at launch only if you agreed (change it in Settings › Privacy) | Delete the folders |
| Diagnostic bundles | `Support-Bundles/` | A folder created only when you press "Create diagnostics for a problem report…". Numbers and true/false values (queue · underruns · rate · error codes · USB numbers · device model code · buffer size · clock drift) and the list of songs heard in that period (`tracks.json`: time · service · title · artist · album, up to the latest 200). No file paths · device names · accounts · system logs | Delete the folder |
| Song identity · music links | The `song_…` tables in `library.sqlite` · `music-links-v1.json` (an old copy, no longer read) | Per song: ISRC · several spellings of title · artist · album, Apple Music · Spotify track IDs, length, and which songs match. No audio · listening times · accounts | Delete the file (re-scan the library) |
| Library | `local-library.json` · `library.sqlite` | Paths and playlists of folders the user added, and the paths · tags · length · album art of music files. No audio | Remove the folder in Library, or delete both files |
| YouTube Music imported playlists | `youtube-music-playlists-v1.json` · `library.sqlite` | Playlist names · song information from the Google Takeout CSV the user picked, and add/remove choices. The picked file's path and account are not kept, and no request is made | Library → Playlists → Delete…, or delete the file |
| Received through the YouTube Music extension | `library.sqlite` · `youtube-music-browser-library-v1.json` · `youtube-music-browser-playlists-v1.json` | With the extension connection on, songs played for 5 seconds or more in Chrome · Edge (video ID · title · artist · album · length), and the lists of playlist · library screens the user opened. Album art · position · queue · volume · liked status stay in memory only. No audio · account · other pages visited | Delete… in Library, or delete the files. Turning the connection off does not delete them |
| Extension connection file · extension copy | `NativeMessagingHosts/fidenne.browser_bridge.json` in Chrome · Edge · `BrowserExtension/` | The connection file holds the helper's location and one allowed extension ID — present only while the switch is on. The copy is the extension files copied by **Open extension folder** | Turn the switch off · delete the folder |
| Output restore record | `output-restore-record.txt` | The DAC's UID and original rate. Kept so the next launch can restore the original rate even after an abnormal exit; removed once restored | Delete the file |
| Lyrics cache | `Lyrics-v1/` | Lyrics found, with source and lookup time. File names are hashes of song information, so the folder listing alone does not show what you listened to. Removed after 30 days unused, after 1 year, or beyond 2,000 | Delete the folder |
| ABX results | `abx-results-v1.json` | The two settings compared and per-trial answers · results (latest 200). No songs · artists · devices | Delete the file |
| Settings · presets | `UserDefaults` | Filter · EQ · crossfeed · UI scale, and EQ · Ostrum preset names and values the user made. No songs · paths · devices | Reset in the app |
| The "Fidenne play queue" playlist in Music | The Music app's library (Apple syncs it to other devices if iCloud library is on) | When playing an Apple Music list, it fills in the current and next ten songs. Other playlists are not touched. A notice asks once before anything is written | Settings › Privacy › turn off Apple Music. Delete the list in Music |
| Spotify token | macOS **Keychain** | Only if the user connected. Not stored in app files | Disconnect, or delete in Keychain Access |

### Where data leaves your Mac (generated from the registry)

<!-- registry:destinations -->
Audio does not leave. But **what you are listening to does.** The 14 destinations below are all of them, and in every case a request is made only when the user uses that feature.

This table is not written by hand — it is generated from the destination registry in the app code, and if the committed copy differs from the regenerated one, an automatic check stops the build.

| Where to | What is sent | When | Default |
|---|---|---|---|
| `lrclib.net` | Song title · artist · album · duration (seconds). For local files in the Fidenne library, only these four too; the file path and file contents are not sent | When the lyrics panel is used, and once after the same song has played continuously for 5 seconds or more (for both streamed songs and local files) | Off — only after asking |
| `itunes.apple.com` | Search terms · region code | When Store search is used | On |
| `rss.applemarketingtools.com` | Nothing — it only downloads a public chart file | When the recommendations list is viewed | On |
| `*.mzstatic.com` | Nothing — it only downloads the image from an image address already received. No song information is carried | When drawing the album art of an Apple Music song on screen | On |
| `accounts.spotify.com` | The Client ID · authorization code · PKCE verifier the user entered themselves | When the user connects Spotify or refreshes the token | On |
| `api.spotify.com` | Search terms · track and device identifiers · user token (Authorization header) | When using Spotify features after connecting | On |
| `i.scdn.co` | Nothing — it only downloads the image from an image address already received | When drawing the album art of a Spotify song on screen | On |
| `mosaic.scdn.co` | Nothing — it only downloads the image from an image address already received | When drawing the album art of a Spotify song on screen | On |
| `*.spotifycdn.com` | Nothing — it only downloads the image from an image address already received | When drawing the album art of a Spotify song on screen | On |
| `*.squig.link` | Search terms are not sent. Fetching the list downloads only the public measurement list file, and when a headphone or target is chosen, the names of that measurement file · target file are carried in the request address | When the user presses fetch list (a fetched list is not fetched again for 30 days), and when a headphone or target is chosen | On |
| `squig.link` | Search terms are not sent. Fetching the list downloads only the public DB list · measurement list file, and when a headphone or target is chosen, the names of that measurement file · target file are carried in the request address | When the user presses fetch list (a fetched list is not fetched again for 30 days), and when a headphone or target on this host is chosen | On |
| `api.music.apple.com` | Reading the library: the app makes no requests of its own — MusicKit in macOS reads the library, and at that time the library lookup and the user token issued by Apple may go to Apple's servers. Looking up other spellings of a song's names: a request the app makes itself through MusicKit — the title and first artist name of the song played (the search term) or its ISRC, the catalogue song number, and a language code (e.g. en-US) go, together with the user token issued by Apple. The album name is not sent. Finding the catalogue recording: a request the app makes itself through MusicKit — the title and first artist name of the song played (Apple Music · Spotify · YouTube Music) go as the search term, together with the user token issued by Apple; for a Spotify song only the names the Spotify app reported are used. The answer is used in memory to find the same song in your Apple Music and link it, and only the link is kept. Album name and length are not sent | After allowing the Apple Music permission in macOS, when library search or finding streaming-song links reads the whole library. And, for an Apple Music song one of whose title · album · artist is written in Hangul, kana or Chinese characters, once for a song listened to for 5 seconds or more (not asked again for 30 days if nothing is found, 10 minutes if it fails). The catalogue recording lookup follows the same rule for every song listened to for 5 seconds or more | On |
| `github.com` | A User-Agent containing the app version, and the IP address (unavoidable in any request). No song · device · settings information and no system information (macOS version · model, etc.) is sent | When the user presses "Check for Updates…" (업데이트 확인…), and when they answer that they want the new version. Only if automatic checking is turned on in settings does it check once a day by itself (off by default) | On |
| `release-assets.githubusercontent.com` | A User-Agent containing the app version, and the IP address. Sent only when github.com redirects to this address | When github.com redirects the update-check request to this address (within the same single check) | On |

**Receiving side.** `127.0.0.1` — a loopback listener (port 53682) that receives the Spotify sign-in callback in the browser. It is open only while the user is starting the Spotify connection, and it closes when done. What goes out: nothing — it does not leave the device.

**Receiving side.** `fidenne-browser-bridge/bridge.sock` — a Unix socket (in the user's temporary folder, readable and writable only by the owner) that receives from the Fidenne extension in Chrome · Edge the YouTube Music song information (title · artist · album · duration), the lists of playlist and library screens the user opened, and small album art, and that returns playback controls. The extension, helper, and app exchange only nine fixed commands. It is open only while "Connect with the Chrome · Edge extension" under Settings › Privacy › YouTube Music is on (off by default); turning it off closes it and removes the connection file (NativeMessagingHosts). What goes out: nothing — it does not leave the device. Song information is kept only for songs played for 5 seconds, opened lists go to their own files, and album art stays in memory only. The app makes no request to an image address — the extension reads the image inside the browser, without cookies, from the image servers the page already uses (`lh3.googleusercontent.com` · `i.ytimg.com`), and shrinks it.

**Per-item switches.** Each destination can be turned off and on separately, and they are asked about together on one screen the first time you run the app. Even with everything off, capture, DSP, DSD conversion, DAC output, and local playback continue as before — only the integration features that use that destination are turned off. If destinations are added later, the same screen appears once more, showing only the added lines.
<!-- /registry -->

### Permission names

Audio capture `NSAudioCaptureUsageDescription` (Process Tap) · audio input `NSMicrophoneUsageDescription` · Apple Events `NSAppleEventsUsageDescription` · Apple Music library `NSAppleMusicUsageDescription` (MusicKit).
Per-song rates of Music are read from the decoder lines of `log stream`.
