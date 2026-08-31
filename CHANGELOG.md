# Changelog

## v2.3.9

### 📊 Command Statistics Improvements

Expanded the command statistics system with detailed usage statistics and historical graphs.

### Added

- Added a new command statistics function to display command usage data
  - Displays the total number of command executions per command
  - Displays the number of unique users executing each command
  - Supports selecting between the last 7 days and 30 days

- Added per-command execution graphs
  - Displays command executions over time
  - Supports viewing the last 7 days or 30 days
  - Shows the number of executions per day
  - Includes unique executions to show how many unique users used the command each day

### ⚙️ Interaction Router Improvements

Updated the interaction routers to improve error handling, scalability, and maintainability.

- Updated the button router to provide improved error handling
- Updated the select menu router to provide improved error handling
- Updated the modal router to provide improved error handling
- Changed the interaction routers to use Maps for better scalability
- Improved the overall structure and handling of interaction routes

### 📈 Server Count Improvements

Updated the server count system to reduce unnecessary API requests.

- Updated `serverCount.js`
- Removed unnecessary guild fetching

### 🌐 Apex API Improvements

Improved map rotation data handling in `apexApi.js`.

- Updated `fetchMapRotation`
- Invalid map rotation data is no longer cached
- Prevents invalid API responses from being stored and reused from the cache
- Improves the reliability and freshness of map rotation data

## v2.3.8

### 🔐 Authentication & Security

Removed unnecessary authentication data being passed throughout the bot.

- Removed `auth` from being passed as a parameter throughout the bot
- `auth` was not required for most functions
- Reduced unnecessary data exposure between functions
- Improved the overall security and maintainability of the code

### 💎 Entitlement Handling

Added automatic handling for newly created Discord entitlements.

- Added `entitlementCreate` handling
- Automatically saves entitlement information to the database
- Automatically updates the user's cache
- Keeps the user's premium status synchronized without requiring additional requests

### 🗳️ Vote Webhook System

Added automatic vote processing using a Cloudflare Worker and Discord webhook channel.

- Added webhook support for vote events
- Cloudflare Worker receives the vote webhook
- The Worker sends the vote information to a private Discord channel
- `messageCreate` processes the message and updates the database
- Automatically updates the user's cache after receiving a vote
- Keeps vote information synchronized between the database and cache

### ⚡ Interaction Handling

Improved the `interactionCreate` handler to reduce unnecessary database requests and improve response speed.

- Improved the overall interaction processing speed
- `userData` is now passed throughout the interaction handling process
- Prevents unnecessary repeated `getUserData` calls
- Reduces database requests during interactions

### 👤 User Data & `getUserData`

Improved how user data is retrieved and synchronized.

- `getUserData` now primarily relies on the database instead of fetching all user data from an API endpoint
- User data is automatically updated in the database when required
- User data is cached for up to one hour
- Reduced unnecessary API requests
- Improved reliability when retrieving user information

### 💾 Caching System

Improved the general caching system throughout the bot.

- Added caching for `userData`
- API response caching can now be configured per function
- Cache durations can be configured through `settings.json`
- Improved cache performance and reduced unnecessary API requests
- Improved synchronization between cached data and database data

### 🧩 Command Routers

Improved all command routers to use centralized user data instead of repeatedly calculating user status.

- Command routers now use `getUserData` to determine whether a user has voted
- Command routers now use `getUserData` to determine whether a user has premium
- Removed unnecessary repeated vote status calculations
- Removed unnecessary repeated premium status calculations
- Reduced database and API requests

### 📊 Server Count

Changed the server count update system to prevent unnecessary executions.

- Removed automatic `setGuildCount` execution from `guildCreate`
- Removed automatic `setGuildCount` execution from `guildDelete`
- `setGuildCount` is now only executed once per day
- Reduced unnecessary server count updates

### 🛠️ Crafting System

Improved the crafting system by removing unnecessary external requests.

- Crafting items are now hardcoded
- Removed API requests for crafting rotations
- Crafting rotations have remained unchanged for the last several seasons
- Improved reliability
- Reduced external API usage

### 🌍 `/loadout` Localization

Improved localization for the `/loadout` command.

- Added localized placeholders for select menus
- Select menu placeholders now use the user's selected language
- Improved the overall localization of `/loadout`

### 🔄 Shard Handling

Improved shard reconnect handling.

- Fixed an issue where `undefined` could be displayed for reconnecting shards
- Improved shard status handling
- Improved shard reconnect logging

### 🧰 Helper Functions

Improved and reorganized commonly used helper functionality.

- Added commonly reused functionality to helper functions
- Reduced duplicated functionality throughout the bot
- Improved code reusability
- Improved maintainability

### 🗄️ Data Configuration

Moved configuration data into `settings.json`.

- Moved links into `settings.json`
- Moved default user data into `settings.json`
- Moved other configurable information into `settings.json`
- Removed unnecessary hardcoded configuration
- Reduced the amount of configuration stored in `.env`

### ⏳ User Data TTL

Added automatic expiration for inactive user data.

- Added a 30-day TTL for user data
- User data is automatically deleted after 30 days of inactivity
- Premium users are excluded from automatic deletion
- Premium user data is stored indefinitely

### 🔒 User Data Hashing

Improved privacy by hashing stored user information.

- Added separate hashes for personal information and statistics
- User data stored in the cache is also hashed
- Improved protection of stored user information
- Reduced exposure of raw user data

### 🔥 Firebase Configuration Security

Improved the security of the Firebase configuration.

- Removed `firebaseConfig.json`
- Firebase configuration is now encoded and stored in `.env`
- Prevents the Firebase configuration from being stored as a separate file
- Improved protection of Firebase credentials

### 🧪 Import Validation

Added a script to detect broken relative imports.

- Added the `check-imports` script
- Checks relative import paths throughout the project
- Detects invalid or broken relative imports
- Makes it easier to identify import issues before deployment

### 🛡️ Error Handling

Improved general error handling throughout the bot.

- Improved handling of unexpected errors
- Reduced the chance of secondary errors during error handling
- Improved overall reliability

### 🐛 Bug Fixes

Fixed several issues throughout the bot.

- Fixed an issue with `/pickrate` where deleting the message before the component timeout could cause the timeout handler to crash
- Improved handling of deleted messages during component cleanup
- Removed unnecessary functions
- Improved general functionality and stability

### ⚙️ General Improvements

Made various improvements to the overall bot architecture.

- Removed unnecessary functionality
- Reduced duplicated code
- Reduced unnecessary API and database requests
- Improved data flow throughout the bot
- Improved caching and database synchronization
- Improved overall performance, security, reliability, and maintainability

## v2.3.7

### 📊 Command Statistics & Analytics

Added a new command statistics system to track command usage and provide more detailed insights into how commands are being used.

### Added

- Added a command usage logger that records command executions in the database
  - Tracks the total number of executions for each command
  - Tracks the number of unique users executing each command
  - Statistics are stored per day
  - Uses Firestore transactions to ensure execution and unique-user counts remain accurate

- Added privacy protection for unique-user tracking
  - Discord user IDs are hashed using SHA-256 before being stored
  - A server-side `COMMAND_STATS_HASH_SECRET` environment variable is used as a secret for the hashing process
  - Raw Discord user IDs are never stored in the command statistics data

- Added the ability to exclude specific users from command statistics
  - Excluded user IDs can be configured through `settings.json`
  - Excluded users are not counted in executions or unique-user statistics

### `/pickrate` Improvements

Updated the `/pickrate` command to use the centralized custom ID system.

- Updated `/pickrate` pagination buttons to use `customIds.json`
- Added three new pickrate custom IDs:
  - `prevPageButton`
  - `nextPageButton`
  - `indicator`

- Updated the pickrate button handling to use the new custom ID configuration
- Removed the unnecessary `return message` from the `/pickrate` command
- Removed the unnecessary returned message from the pickrate button handling
- Improved the organization and maintainability of the pickrate interaction system

### ⚙️ Performance & Stability

- Added transactional command statistics updates to prevent inaccurate execution and unique-user counts
- Improved the `/pickrate` button system by centralizing custom IDs in `customIds.json`
- Reduced unnecessary return values from command and button handlers
- Improved the overall structure and maintainability of command statistics and pickrate interactions

## v2.3.6

### ⚙️ Command Improvements

Improved several commands to provide more reliable data handling, better navigation, and a cleaner user experience.

### Changed

- Updated `/settings edit` to include a random number in the interaction ID
  - Prevents Discord from caching previously displayed information
  - Fixed an issue where deleted settings could reappear after using `/settings delete`

- Updated `/loadout` to fix an issue with the Rampage weapon description exceeding Discord's 100-character limit
- Fully updated `/pickrate`:
  - Added pagination with a maximum of 10 legends per page
  - Page navigation buttons automatically deactivate after 60 seconds of inactivity
  - Updated the pickrate display format to present all data more clearly
  - Improved the overall readability of pickrate information

### Performance & Stability

- Improved `/settings` data handling to prevent stale information from being displayed
- Improved `/pickrate` usability and navigation for larger datasets
- Fixed the Rampage loadout description exceeding Discord's character limit

## v2.3.5

### 🔒 Privacy & Permission Improvements

Improved bot privacy, reduced unnecessary Discord permissions, and updated user data policies for better transparency.

### Changed

- Removed `GatewayIntentBits.GuildMembers` from the bot
- Disabled the use of privileged intents in the Discord Developer Portal
- Removed the `memberRemove` event as it was no longer used
- Updated the `/info` command:
  - Added a button linking to the bot's status page
  - Status page links now automatically redirect users to their selected language version

### Privacy Policy Update

Updated the privacy policy wording to better reflect how user data is handled.

Changed from:

> Data may be shared with or sold to third-party services, partners, or providers for analytics, hosting, service improvement, advertising, or operational purposes.

To:

> Data may be shared with trusted third-party service providers when necessary to operate and maintain the bot, such as hosting providers, database providers, or external APIs used to provide Apex Legends-related features. We do not sell user data to third parties.

### Performance & Stability

- Reduced required Discord permissions by removing unused privileged intents
- Improved transparency around third-party services and data usage
- Reduced unnecessary event handling

### 🛡️ Security Improvements

Improved the bot's security by updating dependencies and resolving known security issues.

- Resolved 12 security vulnerabilities
- Updated affected dependencies to improve overall security and stability
- Improved protection against known vulnerabilities in third-party packages

## v2.3.4

### 📈 Monitoring & Reliability Improvements

Expanded the bot's monitoring infrastructure and improved how background statistics are managed for greater reliability and reduced unnecessary requests.

### Added

- Added comprehensive Better Stack monitoring
- Added automatic notifications when the bot goes offline
- Added automatic error notifications
- Added automatic warning notifications
- Added heartbeat monitoring for the daily database update task to ensure it runs successfully
- Added heartbeat monitoring for uptime

### Changed

- Pickrate data is now refreshed once every 24 hours instead of every 12 hours
- Updated pickrate data freshness checks:
  - Warning is now displayed when data is older than 48 hours
  - Pickrate information is now hidden when data is older than 72 hours

### Performance & Stability

- Reduced background processing by decreasing pickrate update frequency
- Improved bot reliability through continuous uptime, cron job, and error monitoring

## v2.3.3

### 📊 Statistics & Data Tracking Expansion

Added new statistics features to improve tracking of Apex data and bot growth over time.

### Added

- Added new `/pickrate` command
- Added automatic pickrate fetching every 12 hours
- Pickrate data now includes:
  - Current pickrate for every character
  - Pickrate changes compared to the previous update
- Pickrate statistics are now stored in the database for faster command responses
- Added pickrate data freshness checks:
  - Warning displayed when data is older than 24 hours
  - Pickrate information hidden when data is older than 48 hours
- Added daily server count tracking
- Added automatic server count history storage
- Added server count graph that updates daily to display bot growth over time

### Performance & Stability

- Reduced unnecessary API requests by storing regularly updated statistics in the database

## v2.3.2

### 🌍 Localization Expansion

Continued improvements to the bot's localization system, with additional commands now fully supporting multiple languages.

### Added

- Added wildcard support to `/map`
- Added new `/map battle_royale` subcommand
- Added new `/map ranked` subcommand
- `/stats` and `/me` now display how long a player has been in-game
- `/stats` and `/me` are now fully localized across supported languages

### Improved

- `/drop` now displays images correctly and more reliably
- `/info` now fully supports localization
- Updated `/map` images for improved visual quality
- `/map` now prioritizes local image assets with API fallback support
- Language system improvements to ensure newly added languages function correctly

### Changed

- Renamed `/map ltm` to `/map mixtape`
- Updated ESLint configuration to improve switch-case handling and code consistency

### Fixed

- Fixed image rendering issues in `/drop`
- Fixed localization issues affecting newly added languages

### Performance & Stability

- General code quality, maintainability, and stability improvements throughout the bot

## v2.3.1

### 🌍 Expanded Language Support

Added new translations to make Apex Bot accessible to even more users.

### Added

- French language support
- Spanish language support
- Italian language support
- Local emoji assets integrated directly into the bot application
- `/info` now supports localized content and interactive buttons

### Improved

- `/who` now uses locally stored images with API fallback support, improving reliability and response times
- Vote caching system redesigned to provide instant access to premium commands after voting
- Vote data is now cached until its expiration time, reducing unnecessary API requests
- Guild count updates are now only sent when the count actually changes
- `/settings edit` now preserves existing account data when Apex API requests fail (such as 404 responses)

### Fixed

- Fixed `/stats` throwing errors when a player cannot be found
- Prevented duplicate vote cache checks
- Improved handling of API failures across multiple commands

### Changed

- Migrated emoji assets from the legacy emoji server to Discord application emojis
- Removed dependency on externally hosted emoji resources
- General performance, stability, and code quality improvements throughout the bot

## v2.3.0

### 🌍 Multi-Language Support

Added a new `i18n.js` system to improve localization and language management across the Bot.

### Added

- German language support
- Improved translation handling
- Better structure for future language additions

### Security

- Updated packages and dependencies to improve security and stability
- Included multiple dependency and vulnerability fixes

### Changed

- Moved legal documents and policies from `/docs` to the separate `apex-bot-legal` repository
- General performance, structure, and quality improvements

## V2.2.9

### Recent fixes & features

Major update 216 files changed.

- Moved bot status timed job into events and added in-memory caching to reduce unnecessary Apex API calls; integrated `setMapData` into `src/events/timedEvents/botStatus.js` and removed the old utility.
- Added per-user `ephemeral` setting (stored in Firestore) and wired it through interaction helpers and commands so responses respect user preference.
- Implemented a context command `stats` to view other users’ Apex stats and re-enabled context command loading and routing.
- Fixed modal/select builder serialization and enforced Discord component limits; reduced “Unknown Interaction” issues by removing unnecessary pre-modal database reads.
- Added `src/utilities/scripts/export-topgg-commands.js` and generated `topgg-commands.json` for Top.gg command export.
- Various improvements to localization, validation, and helpers (command descriptions/localizations, reply flags, stats utilities).
- Added `/settings` with `edit` and `delete`, including a clean modal UI for viewing and updating user settings.
- Updated dependencies to the latest compatible versions.
- Improved logging and file management with updated handlers.
- Updated weapons and legends data to support new seasons.
- Ongoing work for additional language support and `/drop` updates.

## V2.2.8

### Update node

Updated Node V22.14.0 -> V22.13.1

### Update canvas

Updated Canvas V3.0.1 -> V3.1.0

### Update discord.js

Updated Discord.js V14.17.3 -> V14.18.0

### Update eslint

Updated Eslint V9.18.0 -> V9.22.0

### Update firebase

Updated Firebase V11.1.0 -> V11.4.0

## V2.2.7

### Update eslint

Updated Eslint V9.17.0 -> V9.18.0

### Update discord.js

Updated Discord.js V14.16.3 -> V14.17.3

### Update canvas

Updated Canvas V3.0.0 -> V3.0.1

### Update cron

Updated Cron V3.3.1 -> V3.5.0

## V2.2.6

### Update canvas

Updated Canvas V2.11.2 -> V3.0.0

## V2.2.5

### NEW Engine

Node V20.14.0 -> V22.12.0

### Update NPM

Updated npm V10.8.2 -> V11.0.0

### Update firebase

Updated Firebase V11.0.2 -> V11.1.0

### Update eslint

Updated Eslint V9.16.0 -> V9.17.0

### Update cron

Updated Cron V3.2.1 -> V3.3.1

## V2.2.4

### Update dotenv

Updated dotenv V16.4.5 -> V16.4.7

### Update eslint

Updated eslint V9.15.9 -> V9.16.0

## V2.2.3

### Update cron

Updated cron V3.1.9 -> V3.2.1

### Update eslint

Updated eslint V9.14.0 -> V9.15.0

### Update firebase

Updated firebase V11.0.1 -> V11.0.2

## V2.2.2

### Update eslint

Updated eslint V9.13.0 -> V9.14.0

## V2.2.1

### Fixed /craft

Added banner crafting image.

### Restructured files

Reorganised image files.

## V2.2.0

### Code stability update

Improved overall code.

## V2.1.9

### Small fix

Corrected files spelling mistakes.

### Updated /me and /stats

Improved command speed and layout.

### Update cron

Updated cron V2.4.4 -> V3.1.8

### Changed embed color picker

Now uses autofill and supports all know discord colors including hex.

## V2.1.8

### Bug fix

Removed DM permissions for the settings commands.

## V2.1.7

### Improved activity of the client

Better speeds.

### Improved the SKU's for premium users

Removed subscription based models.

### Overall better quality and readability of code

Made minor changes to code for better speeds and readability.

### Updated error handling

Improved error handling.

## V2.1.6

### Updated settings embed color

Added custom colors as well as new basic colors.

### Overall better quality and readability of code

Made minor changes to code for better speeds and readability.

### Fixed loadout.js

Added new weapons.

### Fixed invite.js

Fixed the outdated DM Permissions.

### Fixed info.js

Fixed the oudated DM permissions.

### Updated map.js

Improved code.

## V2.1.5

### Fix crash on DM

Fixed the issue.

### Update firebase

Updated firebase V10.14.1 -> V11.0.1

## V2.1.4

### Update firebase

Updated Firebase V10.14.0 -> V10.14.1

### Update eslint

Updated eslint V9.11.1 -> V9.13.0

### Update .setDMPermission() (outdated)

Updated all command to follow the new syntax.

### Added Team command

Added Team command to get a team to use.

### Updated Crafting command

Update with new season added the permanent item and removed the weekly/daily.

## V2.1.3

### Update discord.js

Updated Discord.js V14.16.2 -> V14.16.3

### Update firebase

Updated Firebase v10.13.2 -> V10.14.0

## V2.1.2

### Update discord.js

Updated Discord.js V14.16.1 -> V14.16.2

### Update eslint

Updated eslint V9.9.1 -> V9.11.1

### Update firebase

Updated firebase V10.13.1 -> V10.13.2

## V2.1.1

### Heatbeat error fix

Because the firebase package has had an update the heartbeat error is now fixed. Previously the package was downgraded to mitigate this issue.

### Update Discord.js

Updated Discord.js V14.15.3 -> V14.16.1

### Update Firebase

Updated Firebase V10.12.5 -> V10.13.1

## V2.1.0

### Changed Bot.js

Removed auto updating commands on every startup.

### Downgraded Firebase

Downgraded Firebase V10.13.0 -> V10.12.5
This is because a heartbeats console.log error. This will be removed in the next firebase update this thursday (29-08-2024).

### Updated Eslint

Updated Eslint V9.9.0 -> V9.9.1

### Update Firebase

Updated firebase V10.12.5 -> V10.13.0

## V2.0.9

### New Season

Fixed commands to work for the new season.

### Edited files

Edited multiple files to be more compact.

### Season Bug Fix

Removed Image causing error.

### NPM Update

Upgraded from 9.8.1 -> 10.8.2

### Eslint Update

Upgraded from 9.5.0 -> 9.9.0

### Firebase Update

Upgraded from 10.12.2 -> 10.12.5

## V2.0.8

### Updated CRON

Updated to latest version.

### Removed package MS

removed it. Was not used.

### Change @types/node to dev

Changed to dev.

### Update firebase

Updated to latest firebase package for security reasons.

### Update ESLINT

New version.

### Bug Fix

On guildDelete there was a small error.

## V2.0.7

### Updated language

There was a small issue.

### Fix /news

Removed components and not change embed.

### Embed color green /link

From set color to green.

### Fixed /settings delete

Added auto delete message after 15sec of no interaction.

### Fixed images

Images got locked away not added a work around.

### Made Sucessfull embeds green

Embed like delete data are now green.

### Fixed /me and /stats

If person had rank "unranked" there would be not emoji and would state undefined. Now set to Rookie 4.

## V2.0.6

### Fixed glitch /me and /stats

Badges fix.

### Update News commands

From 3 pages to unlimited. Added a new button system. Auto removes buttons after 15sec of not using.

### Changed Privacy Policy

Check PRIVACY.md.

### Added visible messages

Choose if your message is visible or not.

### Added color embeds

Change the color of the embed.

### Moved some command to settings commands

Moved link, unlink, languages.

### Database resture

Restuctured database.

### New settings command

Added new settings command.

## V2.0.5

### Minor big fix

Removed tiny bugs.

### Moved some files

Moved guild files into guild folder.

### Improved Activity Type

Now added sleep of 500ms to fix an issue with API.

### New added Drop command

Random place to drop.

## V2.0.4

### Premium Vote glitch removed

When you voted you would not get access to the premium commands.

### Moved images

Moves images into image folder.

### Error handling improved

Added Lookup errors and overall beter handling.

### Minor Security Update

Made a token invisible. This token was not harmful but just to be safe.

## V2.0.3

### Added shard count for top.gg

Added shard count in the post request.

### Changed Activity Type

Custom activity. Removed Playing ...

### New added /invite

invite the bot to your server.

### Change /current -> /season

Change the name of the command.

### Multi languages Support

Added name localizations for Dutch.

## V2.0.2

### Updates to commands

Some minor bug fixes to some commands.

### New SUBSCRIPTIONS

Buy subscriptions for Apex Bot and get access to new features. Some commands need a subscriptions, some are free.
All premium command can be accessed for FREE if you vote on top.gg for Apex Bot. (This is not done to make money, I need to pay the host)

### New loadout command

New command

### Aplication name change

Ask discord dev to change the name of the app from "Apex" to "Apex Bot".

### Changed Banner and Profile Picture

Change bot's profile picture and banner.

### Updated ESLINT V9.3.0 -> V9.4.0

Updated Package

### Updated discord V14.15.1 -> V14.15.3

Updated package

## V2.0.1

### Added commands

Added: current, info

### Removed outdated commands

Removed: drop, heirloom, invite, loadout, rank (contex), shop, team, vote, help

### Updated commands

All commands got updated. Glitches got removed and overall better performance.

### Added Sharding

The new improved version support sharding.

### Updated outdated packages

Updated: firebase, node-fetch, cron, canvas

### Updated Discord.js to 14.14.1

Updated to the latest discord.js version.

### New NODE version 16.18.0 -> V20.14.0

New node version to support the new packages.

### Changed internalstructure of the bot

Put folders in commands. Data folder got created. src folder got created. Restructed the folders.

### Added eslint V9.3.0

From now we will be using a linter to keep our files organised.

### Added LICENCE and SECURITY.md

Here you can find the licence of the APEXBOT. SECURITY.md will show potential issues and what version of the ApexBot is supported.

### Added TOS and PRIVACY.md

Location changed to now be in the files of the ApexBot instead of external folders.
