# The Solari Republic Discord Bot

A discord.js v14 government simulation bot. It creates/reconciles seven institutional categories, emoji-prefixed channels, colored roles, channel-by-channel permissions, a citizenship onboarding area, the Republic Police role, court/election workspaces, a provisional launch timetable, citizenship applications, party applications with screenshot evidence, on-demand elections, and audit logs. It intentionally does not create or post a constitution.

## Requirements
- Node.js 18.17 or newer
- A Discord application and bot
- A Discord server you own

## 1. Create the bot
1. Open https://discord.com/developers/applications and create an application.
2. Open **Bot**, create/reset the bot token, and copy it.
3. Under **Bot > Privileged Gateway Intents**, enable **Server Members Intent** and **Message Content Intent**. Message Content is used to detect screenshot attachments in party application channels.
4. Under **OAuth2 > URL Generator**, select `bot` and `applications.commands`.
5. Select these bot permissions: Manage Channels, Manage Roles, View Channels, Send Messages, Send Messages in Threads, Embed Links, Attach Files, Read Message History, Manage Messages, Moderate Members, View Audit Log, and Manage Guild. Administrator is easiest for initial setup but grants broad access; only use it if you trust the bot and keep the token private.
6. Invite the bot. Move the bot's role above every role it needs to create, assign, rename, or edit.

The bot cannot create a brand-new Discord server from nothing. Create a server first and invite the bot. Once installed with Manage Guild, `/setup` renames it **The Solari Republic**.

## 2. Install
Extract the ZIP, open a terminal in the `solari-republic-bot` folder, and run:

```bash
npm install
```

Copy `.env.example` to `.env` and fill in:

```env
DISCORD_TOKEN=your_bot_token
CLIENT_ID=your_application_id
GUILD_ID=your_server_id
LOG_CHANNEL_ID=
BOT_ADMIN_IDS=
```

To get IDs, enable Developer Mode in Discord, then right-click the application/server and choose **Copy ID**. Never share your bot token.

## 3. Deploy and run

```bash
npm run deploy
npm start
```

Run `/setup` as the server owner or an authorized administrator. It reconciles the seven categories, all defined channels and overwrites, colored roles, the Republic Police role, onboarding notices, and launch timetable. Run it again if you need to reapply the intended permission layout.

## Roles created
- **Founding Father** — Administrator; assigned to the server owner during setup. An existing “Founding President” role is renamed to “Founding Father.”
- **Vice President** — Administrator, as explicitly requested.
- **President** — executive role; no Administrator permission.
- **Chief Justice**, **Supreme Court Justice**, and **Court Clerk** — judiciary roles.
- **Assembly Speaker**, **Assembly Member**, and **National Assembly** — legislature roles.
- **Electoral Commissioner** and **Deputy Electoral Commissioner** — election administration.
- **Cabinet Minister**, **Government Official**, and **Government Staff** — executive and operational roles.
- **Republic Police** — renamed from an existing Moderator/Server Moderator role when possible; can timeout, kick, ban, manage messages, and view the Discord audit log. This role does not receive Administrator.
- **Internal Affairs**, **Audit Officer**, **Citizenship Officer**, **Party Registrar**, and **Technical Administrator** — oversight and administration roles.
- **Citizen**, **Candidate**, **Applicant**, **Unregistered**, **Party Leader**, **Deputy Party Leader**, **Party Member**, and **Bot** — member and party roles.

Role colors are configured in the source. The bot creates any missing roles and updates the names, colors, display settings, and permissions of roles it manages.

## Channel access and onboarding
- The seven categories have per-channel overwrites rather than relying on category defaults.
- Courts, Electoral Commission operations, Assembly private work, staff, application review, police, and logs have restricted access.
- `🚪・unregistered`, `🪪・citizenship-help`, `📢・citizenship-announcements`, and public notices are visible to unregistered members as appropriate.
- The **Unregistered** role is explicitly denied **Read Message History** in every channel it can access. It cannot send in public notice channels; it can ask questions in `🪪・citizenship-help` and use the public party application instructions. New members can use `/register` to submit the form.
- On application submission, the bot adds **Applicant**. Approval grants **Citizen** and removes **Unregistered** and **Applicant**. Rejection removes **Applicant** but leaves the member unregistered.
- The bot tries to rename an existing `Moderator`, `Server Moderator`, or `Server Moderator Team` role to **Republic Police** and sets its moderation permissions. Review any legacy roles manually after setup.

## Main commands
- `/setup` — create/reconcile the server structure, roles, and permissions.
- `/register` — apply for citizenship.
- `/application-review application_id decision reason` — approve or reject a citizenship application.
- `/party create name ideology leader` — creates a private party application channel.
- `/party approve application_id` — creates party roles and private channels after screenshot evidence is uploaded.
- `/party reject application_id reason` — rejects a party application.
- `/election start office candidates duration_hours` — starts an election on demand; candidate input must be at least two Discord user mentions or IDs separated by commas.
- `/election end election_id` — closes an election early and publishes results.
- `/election status election_id` — checks election status.
- `/launch-timetable` — publishes the provisional launch timetable.
- `/log action details` — records an official action.
- `/government` — command guide.

## Important behavior and limits
- Elections can be started by the server owner, Founding Father, President, Vice President (which has Administrator permission), or Electoral Commission. Voting is recorded per account; users may change their vote while an election is open. Results are tallied automatically; a tie is reported for the administration to resolve.
- Party applicants must upload screenshots showing people expressing interest in joining. The bot records image attachments but cannot prove a screenshot is authentic; authorized staff should inspect evidence manually.
- The bot records many visible Discord events and bot-managed government actions, including messages, edits/deletions, membership and role changes, channel changes, elections, applications, and moderation. Discord does not expose every possible event to bots in every circumstance, and logging can fail if the bot loses access. Keep Discord's native Audit Log enabled.
- State is stored in `data/state.json`. Back up the `data` folder and keep the bot running for interactions and timed election closure.
- **Administrator is highly powerful.** Founding Father and Vice President receive it as configured. Only assign the Vice President role to someone you trust with full server control. The constitution is intentionally not created or posted by this bot.


### Role hierarchy update

The setup command creates missing roles including Deputy Speaker, Assembly Whip, Assembly Clerk, Assembly Observer, Chief of Staff, Deputy Chief of Staff, Director of Government Operations, Department Director, Government Secretary, Government Intern, and Election Staff. It then attempts to position all managed roles in the defined order, from Founding Father at the top through Unregistered near the bottom. Before running `/setup`, move Solaria's bot role above the government roles in Server Settings → Roles; Discord does not let a bot reorder roles above its own highest role.
"# solarirepublic" 
"# solarirepublic" 
