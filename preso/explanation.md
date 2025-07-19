# BrightSign Presentation File (.bpfx) Field Explanation

## Overview
This document explains the structure and fields of a BrightSign presentation file (simple-object.bpfx). This is an object detection demonstration presentation that switches between different video content based on detected objects (phone and cup).

## Root Structure

### `meta`
- **brightAuthorVersion**: "1.63.2" - Version of BrightAuthor used to create the presentation
- **buildType**: "Standard" - Type of build configuration

### `bsdm` (BrightSign Digital Media)
Main presentation configuration container

## Sign Properties (`bsdm.sign.properties`)

### Device Configuration
- **id**: Unique identifier for the presentation
- **version**: "1.3.10" - Presentation version
- **name**: "simple-object" - Presentation name
- **model**: "XT1145" - Target BrightSign player model

### Display Settings
- **videoMode**: "1920x1080x30p" - Resolution and refresh rate
- **size**: Object with width (1920) and height (1080) in pixels
- **monitorOrientation**: "Landscape" - Display orientation
- **monitorOverscan**: "NoOverscan" - Overscan compensation setting
- **videoConnector**: "HDMI" - Output connector type
- **forceResolution**: true - Forces the specified resolution
- **fullResGraphicsEnabled**: true - Enables full resolution graphics

### Display Enhancement Settings
- **tenBitColorEnabled**: false - 10-bit color depth support
- **dolbyVisionEnabled**: false - Dolby Vision HDR support
- **backgroundScreenColor**: RGBA color object for background (black: r:0, g:0, b:0, a:255)

### Audio Configuration
- **audioConfiguration**: "MixedAudioPCMOnly" - Audio output format
- **audioAutoLevel**: false - Automatic audio level adjustment

### Web and JavaScript Settings
- **htmlEnableJavascriptConsole**: false - JavaScript console access
- **htmlEnableChromiumVideoPlayback**: false - Chromium-based video playback
- **deviceWebPageDisplay**: "Standard" - Web page display mode

### Variable Management
- **alphabetizeVariableNames**: false - Sort variables alphabetically
- **autoCreateMediaCounterVariables**: false - Auto-create media counters
- **resetVariablesOnPresentationStart**: false - Reset variables on startup
- **networkedVariablesUpdateInterval**: 300 - Update interval in seconds

### Interaction Settings
- **inactivityTimeout**: false - Inactivity timeout feature
- **inactivityTime**: 30 - Timeout duration in seconds
- **touchCursorDisplayMode**: "Auto" - Touch cursor display behavior
- **flipCoordinates**: false - Coordinate system flip

### Network Configuration
- **udpDestinationAddressType**: "IPAddress" - UDP address type
- **udpDestinationAddress**: "255.255.255.255" - Broadcast address
- **udpDestinationPort**: 5000 - UDP destination port
- **udpReceiverPort**: 5000 - UDP receiver port

### System Settings
- **language**: "English" - System language
- **languageKey**: "eng" - Language code
- **gpsConfiguration**: "None" - GPS configuration
- **enableEnhancedSynchronization**: null - Enhanced sync feature
- **disableSettingsHandler**: false - Settings handler control
- **isMosaic**: false - Mosaic display mode
- **graphicsZOrder**: "Back" - Graphics layer ordering

## Hardware Configuration

### Serial Port Configuration (`serialPortConfigurations`)
Array of 8 serial port configurations (ports 0-7):
- **port**: Port number (0-7)
- **baudRate**: 115200 - Communication speed
- **dataBits**: 8 - Data bits per character
- **stopBits**: 1 - Stop bits
- **parity**: "N" - No parity checking
- **protocol**: "ASCII" - Communication protocol
- **sendEol**: "CR" - Send end-of-line character
- **receiveEol**: "CR" - Receive end-of-line character
- **invertSignals**: false - Signal inversion
- **connectedDevice**: "None" - Connected device type
- **gps**: false - GPS functionality

### GPIO Configuration (`gpio`)
Array of 8 GPIO pins, all configured as "input"

### Button Panel Configuration (`buttonPanels`)
Configuration for BP900 and BP200 button panels:
- **configureAutomatically**: true - Auto-configuration enabled
- **configuration**: 0 - Configuration index

### IR Remote Configuration (`irRemote`)
- **irInConfiguration**: IR input source configuration
- **irOutConfiguration**: IR output destination
- **irRemoteControl**: Detailed remote control mapping
  - **id**: "RC-1002" - Remote control model
  - **encoding**: "NEC" - IR encoding protocol
  - **manufacturerCode**: 28560 - Manufacturer identifier
  - **buttons**: Object mapping button codes to descriptions

### Audio Signal Configuration (`audioSignPropertyMap`)
Volume ranges (0-100) for various audio inputs:
- analog1-3, hdmi1-4, spdif, various USB ports

## Media and Presentation Logic

### Zones (`zones`)
Display regions configuration:
- **zonesById**: Zone definitions by unique ID
- **allZones**: Array of all zone IDs
- **zoneLayersById**: Layer configuration for graphics, audio, and video
- **zoneSequence**: Ordering of zones in layers

#### Zone Properties
- **viewMode**: "Letterboxed and Centered" - Content scaling
- **videoVolume**: 100 - Video audio level
- **maxContentResolution**: "HD" - Maximum content quality
- **audioOutput**: "Analog" - Audio output type
- **audioMapping**: Channel mapping configuration

### Media States (`mediaStates`)
Defines the three video files used in the presentation:
1. **meet-brightsign.mp4** - Default/fallback video
2. **galaxy-flip-phone.mp4** - Displayed when phone detected
3. **starbucks.mp4** - Displayed when cup detected

Each media state includes:
- **contentItem**: Video file properties
- **volume**: Audio level (100)
- **videoDisplayMode**: "2D" - Display mode
- **automaticallyLoop**: true - Continuous playback

### Events (`events`)
Trigger conditions for content switching:
- **UDP Event**: Listens for external detection signals
- **MediaEnd Events**: Handle video completion

### Transitions (`transitions`)
Logic for switching between content based on detection:
- **faces_attending**: Two conditional transitions
  - If `cup > 0`: Switch to starbucks.mp4
  - If `phone > 0`: Switch to galaxy-flip-phone.mp4
- **Return transitions**: Go back to default video when other videos end

### User Variables (`userVariables`)
Variables for object detection state:
- **faces_attending**: Number of faces detected (shared access)
- **timestamp**: Detection timestamp (shared access)
- **cup**: Cup detection count (private access)
- **phone**: Phone detection count (private access)

## Asset Management

### Asset Map (`assetMap`)
Maps asset IDs to actual media files:
- File paths, sizes, modification dates
- Reference counts for each asset
- Media type classification

### Thumbnail
Base64-encoded JPEG thumbnail (200x112 pixels) representing the presentation

## User Interface State

### Selection (`selection`)
Current UI selection state in BrightAuthor

### Interactive Canvas (`interactiveCanvas`)
Visual layout information:
- State positions on the canvas
- Event display configuration
- View transforms and zoom levels

### Screen Layout (`screenLayoutSettings`)
Display configuration:
- **selectedLayoutId**: "Landscape1x1" - Single landscape screen
- **screenCount**: 1 - Number of displays
- Layout boundary and snap settings

## Object Detection Flow

This presentation implements a simple object detection system:

1. **Default State**: Plays meet-brightsign.mp4
2. **Detection Input**: Receives UDP messages with object detection data
3. **Content Switching**: 
   - When cup detected (`cup > 0`): Shows starbucks.mp4
   - When phone detected (`phone > 0`): Shows galaxy-flip-phone.mp4
4. **Return to Default**: When specific content ends, returns to default video

The system uses user variables to track detection state and conditional transitions to implement the switching logic.