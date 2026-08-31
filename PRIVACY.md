# Privacy Policy

## Usage of Data

The Bot stores and processes user data when necessary to provide its features, remember user preferences, handle premium entitlements, process votes, and improve the reliability and performance of the Bot.

Stored data is used for:

- Command handling
- User preferences
- Vote status
- Premium status
- Premium entitlement management
- Caching and performance improvements
- Anonymous usage analytics

Data may be shared with trusted third-party service providers when necessary to operate and maintain the Bot, such as hosting providers, database providers, or external APIs used to provide Apex Legends-related features. We do not sell user data to third parties.

## Stored Information

The Bot may store the following information:

- `discordId` — The Discord user ID, stored in a protected hashed form
- `platform` — Selected Apex Legends platform
- `username` — Apex Legends username
- `embedColor` — Custom embed color preference
- `language` — Selected bot language
- `visibility` — Response visibility preference
- `lastUpdatedAt` — The last time the user's stored data was updated or its retention timer was reset
- `voteExpiresAt` — The time until the user's current vote status expires
- `premium` — Whether the user currently has premium
- `premiumEntitlementId` — The Discord entitlement ID associated with the user's premium purchase, when applicable
- `premiumSkuId` — The Discord SKU ID associated with the user's premium purchase, when applicable
- `premiumSince` — The date and time when the user first received premium, when applicable

No other personal information is intentionally stored.

## Data Retention

For non-premium users, stored personal data is automatically deleted after 30 days for security and privacy reasons.

The 30-day retention timer is reset when:

- The user votes on Top.gg
- The user uses `/settings edit`
- The user uses `/settings delete`
- The user purchases premium
- The user uses any command when their `lastUpdatedAt` is at least 7 days old

Purchasing premium changes the user's data retention to indefinite. Premium-related data is still stored securely and is only retained for purposes related to providing and managing the premium service.

The user's Discord ID is hashed before being stored. Personal information uses a dedicated hash that is separate from the hash used for usage statistics.

## Command Usage Analytics

The Bot collects limited anonymous usage statistics to understand how commands are being used and to improve the Bot.

For each command, the Bot may store:

- The total number of times the command was executed on a given day
- The number of individual users who used the command on that day

To calculate unique users, a separate hashed user ID is stored. This hash is different from the hash used for personal information to provide an additional layer of security.

The hashed user IDs used for command analytics are retained for a maximum of 30 days and are not used to identify users.

## Cached Data

The Bot temporarily caches data locally and in other caching systems to improve performance and reduce unnecessary database and API requests.

Cached data may include:

- User data
- Vote status
- Premium status
- API responses
- Bought SKU information
- Other temporary information required for Bot functionality

Cache durations can vary depending on the type of data and may be configured separately for different types of information.

Cached data is temporary and is not intended for long-term storage. Cached information may remain available for 24 hours or longer depending on the configured cache duration.

## Automatic Data Deletion

The Bot uses Firestore's Time-to-Live (TTL) functionality to automatically remove data after its configured retention period.

The specified retention periods are minimum intended retention periods. Firestore does not necessarily delete a document immediately when its TTL expires. As a result, data may remain in the database for 24 hours or longer after its configured expiration time before Firestore permanently removes it.

## Data Security

The Bot uses multiple measures to protect stored information.

- Discord user IDs are hashed before being stored
- Personal information and analytics use separate hashing systems
- Cached user information is protected using hashing
- Sensitive Firebase configuration is not stored as a separate configuration file
- Data is automatically removed when it is no longer required, where applicable
- Premium data is retained indefinitely but remains protected using the same security measures

## Removal of Data

Users may delete their stored personal data at any time using the `/settings delete` command.

When `/settings delete` is used, all stored personal information and user preferences are deleted, with the exception of the following information:

- `lastUpdatedAt`
- `voteExpiresAt`
- `premium`
- `premiumEntitlementId`
- `premiumSkuId`
- `premiumSince`

These fields are retained because they are required to determine the user's premium status and to correctly handle votes, commands, and data retention.

If the user does not have premium, the remaining data will be automatically deleted after the 30-day TTL expires. The retained information is still subject to the applicable security and retention measures described in this Privacy Policy.

If the user has premium, the premium-related information is retained indefinitely because it is required to recognize and manage the user's premium entitlement.

## Contact

If you have questions regarding your data or privacy, please contact the bot developer.
