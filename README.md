# JustTeams

<p align="center">
<img src="https://i.imgur.com/5pLvtnY.png" alt="JustTeams Logo" width="1000"/>
</p>

<p align="center">
<strong>High-performance team management plugin for Paper, Folia, and proxy networks with advanced cross-server synchronization</strong>
</p>

<p align="center">
<img src="https://img.shields.io/badge/Version-2.3.6-brightgreen?style=for-the-badge" alt="Version" />
<img src="https://img.shields.io/badge/API-1.21+-blue?style=for-the-badge" alt="API Version" />
<img src="https://img.shields.io/badge/Java-21+-orange?style=for-the-badge" alt="Java" />
<img src="https://img.shields.io/badge/Folia-Supported-purple?style=for-the-badge" alt="Folia" />
</p>

<p align="center">
<a href="https://discord.gg/HRjcmEYXNy">
<img src="https://img.shields.io/discord/1389677354753720352?color=5865F2&label=Discord&logo=discord&logoColor=white&style=for-the-badge" alt="Discord" />
</a>
</p>

---

## Overview

JustTeams is a feature-rich team management plugin designed for modern Minecraft servers. Built with performance and reliability in mind, it supports single servers, Velocity/BungeeCord networks, and Folia's multi-threaded regions.

### Key Features

- **High Performance** - Asynchronous operations and optimized database queries
- **Cross-Server Support** - Real-time synchronization via Redis + MySQL backend
- **Dual-Mode Sync** - Redis for instant updates (<100ms), MySQL polling fallback
- **Comprehensive Admin Tools** - Full-featured admin GUI with permission editing
- **Team Management** - Create, invite, promote, demote, kick, and transfer teams
- **Team Features** - Home system, warps, PvP toggle, team chat, shared ender chest
- **Admin Chat Spy** - Monitor all team chats with permission-based access
- **Economy Integration** - Vault support with team bank system
- **Rich Visuals** - MiniMessage formatting with gradients and custom colors
- **Customizable GUIs** - Dummy items support for enhanced visual customization
- **Permission System** - Role-based permissions (Owner, Admin, Moderator, Member)
- **Hook Support** - Vault, PlaceholderAPI, PvPManager (all optional)
- **Folia Ready** - Full support for multi-threaded region servers with optimized scheduler---

## Installation

### Quick Start

1. Download `JustTeams.jar` from releases
2. Place in your server's `plugins` folder
3. Restart the server to generate configuration files
4. Configure `config.yml` to your needs
5. Reload with `/team reload`

### Dependencies

**Required:**
- Java 21 or higher
- Paper 1.21+ (or Folia, Spigot compatible)

**Optional:**
- **Vault** - Economy and team bank support
- **PlaceholderAPI** - Placeholder expansion for other plugins
- **PvPManager** - Enhanced PvP mode integration
- **MySQL** - Cross-server team synchronization
- **Redis** - Instant cross-server updates (<100ms latency)

### Cross-Server Setup

For network-wide team synchronization with instant updates:

1. Install JustTeams on all network servers
2. Set up shared MySQL database
3. Configure `config.yml` with MySQL connection details:
   ```yaml
   storage:
     type: "mysql"
     mysql:
       host: "your-mysql-host"
       port: 3306
       database: "justteams"
       username: "your-username"
       password: "your-password"
   ```
4. **(Optional but Recommended)** Enable Redis for instant sync:
   ```yaml
   redis:
     enabled: true
     host: "your-redis-host"
     port: 6379
     password: ""
   ```
5. Restart all servers

**Sync Performance:**
- **With Redis:** <100ms latency (instant cross-server updates)
- **MySQL Only:** ~1-second polling (reliable fallback)
- **Hybrid Mode:** Redis for speed + MySQL for persistence

---

## Commands

### Player Commands

| Command | Description | Permission | Default |
|---------|-------------|------------|---------|
| `/team` | Open team GUI | `justteams.command.info` | Everyone |
| `/team create <name>` | Create a new team | `justteams.command.create` | Everyone |
| `/team disband` | Disband your team (Owner only) | `justteams.command.disband` | Everyone |
| `/team invite <player>` | Invite a player to your team | `justteams.command.invite` | Everyone |
| `/team accept <team>` | Accept a team invitation | `justteams.command.accept` | Everyone |
| `/team deny <team>` | Deny a team invitation | `justteams.command.deny` | Everyone |
| `/team join <team>` | Join a public team | `justteams.command.join` | Everyone |
| `/team leave` | Leave your current team | `justteams.command.leave` | Everyone |
| `/team kick <player>` | Kick a member from team | `justteams.command.kick` | Everyone |
| `/team info [team]` | View team information | `justteams.command.info` | Everyone |
| `/team list` | View all teams (paginated) | `justteams.command.info` | Everyone |
| `/team top` | View team leaderboard | `justteams.command.top` | Everyone |
| `/team chat` | Toggle team chat mode | `justteams.command.chat` | Everyone |
| `/teammsg <message>` | Send a team message | `justteams.command.teammsg` | Everyone |

### Team Management Commands

| Command | Description | Permission | Default |
|---------|-------------|------------|---------|
| `/team promote <player>` | Promote a team member | `justteams.command.promote` | Everyone |
| `/team demote <player>` | Demote a team member | `justteams.command.demote` | Everyone |
| `/team transfer <player>` | Transfer team ownership | `justteams.command.transfer` | Everyone |
| `/team settag <tag>` | Set team display tag | `justteams.command.settag` | Everyone |
| `/team setdescription <text>` | Set team description | `justteams.command.setdescription` | Everyone |
| `/team public` | Make team public | `justteams.command.public` | Everyone |
| `/team private` | Make team private | `justteams.command.public` | Everyone |
| `/team pvp` | Toggle team PvP mode | `justteams.command.pvp` | Everyone |
| `/team requests` | View join requests | `justteams.command.requests` | Everyone |

### Home & Warp Commands

| Command | Description | Permission | Default |
|---------|-------------|------------|---------|
| `/team sethome` | Set team home location | `justteams.command.sethome` | Everyone |
| `/team home` | Teleport to team home | `justteams.command.home` | Everyone |
| `/team setwarp <name>` | Create a team warp | `justteams.command.setwarp` | Everyone |
| `/team delwarp <name>` | Delete a team warp | `justteams.command.delwarp` | Everyone |
| `/team warp <name>` | Teleport to team warp | `justteams.command.warp` | Everyone |
| `/team warps` | List all team warps | `justteams.command.warps` | Everyone |

### Economy Commands

| Command | Description | Permission | Default |
|---------|-------------|------------|---------|
| `/team bank` | View team bank balance | `justteams.command.bank` | Everyone |
| `/team bank deposit <amount>` | Deposit money to team | `justteams.command.bank` | Everyone |
| `/team bank withdraw <amount>` | Withdraw money from team | `justteams.command.bank` | Everyone |

### Admin Commands

| Command | Description | Permission | Default |
|---------|-------------|------------|---------|
| `/team reload` | Reload all configurations | `justteams.command.reload` | OP |
| `/team admin` | Open admin panel GUI | `justteams.command.admin` | OP |
| `/team chatspy` | Toggle chat spy (monitor all team chats) | `justteams.chatspy` | OP |

### Command Aliases

**Main Command Aliases:**
- `/team` → `/guild`, `/clan`, `/party`, `/t`, `/g`, `/c`, `/p`

**Message Command Aliases:**
- `/teammsg` → `/guildmsg`, `/clanmsg`, `/partymsg`, `/tm`, `/tmsg`, `/gmsg`, `/cmsg`, `/pmsg`

Aliases can be customized in `commands.yml`

---

## Team Roles & Permissions

JustTeams uses a hierarchical role system with customizable permissions per role.

### Role Hierarchy

| Role | Level | Capabilities |
|------|-------|--------------|
| **Owner** | 4 | Full control: manage all members, settings, and can disband team |
| **Admin** | 3 | Invite, kick, promote/demote (up to Moderator), manage settings |
| **Moderator** | 2 | Invite players, kick Members, manage home/warps |
| **Member** | 1 | Basic permissions: use home, warps, chat, bank deposit |

### Permission Types

**Per-Member Permissions** (configurable via Admin GUI):
- `CAN_WITHDRAW` - Withdraw from team bank
- `CAN_USE_ENDERCHEST` - Access team ender chest
- `CAN_SET_HOME` - Set team home location
- `CAN_USE_HOME` - Teleport to team home

**Role-Based Permissions:**
- Invite players (Admin+)
- Kick members (Moderator+)
- Promote/demote (Admin+)
- Change team settings (Admin+)
- Disband team (Owner only)
- Transfer ownership (Owner only)

---

## Configuration

JustTeams uses modular configuration files for clean organization and easy management:

### Core Configuration Files

| File | Purpose |
|------|---------|
| `config.yml` | Main settings, database, Redis, features, proxy settings |
| `messages.yml` | All text output with MiniMessage formatting (398 lines) |
| `gui.yml` | Complete GUI configuration for all menus (760+ lines) |
| `commands.yml` | Command name and alias configuration |
| `placeholders.yml` | PlaceholderAPI placeholder definitions |

### Key Configuration Options

**Basic Settings (`config.yml`):**
```yaml
# Proxy Configuration
proxy_settings:
  type: "NONE"          # Options: NONE, BUNGEE, VELOCITY

# Storage Configuration
storage:
  type: "mysql"         # Options: h2, mysql, mariadb
  mysql:
    host: "localhost"
    port: 3306
    database: "justteams"
    username: "root"
    password: ""
    
  connection_pool:
    max_size: 10        # Maximum connections
    min_idle: 3         # Minimum idle connections
    idle_timeout: 300000    # 5 minutes
    max_lifetime: 1800000   # 30 minutes
```

**Redis Configuration (Optional but Recommended):**
```yaml
redis:
  enabled: true         # Enable instant cross-server sync
  host: "localhost"
  port: 6379
  password: ""
  use_ssl: false
  timeout: 5000         # Connection timeout (ms)
  
  pool:
    max_total: 20       # Max total connections
    max_idle: 10        # Max idle connections
    min_idle: 2         # Min idle connections
```

**Feature Toggles:**
```yaml
features:
  # Core Team Management
  team_creation: true
  team_disband: true
  team_invites: true
  team_join_requests: true
  team_blacklist: true
  team_transfer: true
  team_public_toggle: true
  team_rename: true
  
  # Member Management
  member_kick: true
  member_promote: true
  member_demote: true
  member_leave: true
  
  # Information Features
  team_info: true
  team_tag: true            # Set to false to disable team tags entirely
  team_description: true
  team_leaderboard: true
  
  # Home System
  team_home: true
  team_home_set: true
  team_home_teleport: true
  
  # Warp System
  team_warps: true          # Enable team warp system
  team_warp_set: true
  team_warp_delete: true
  team_warp_teleport: true
  
  # PvP Features
  team_pvp: true            # Enable team PvP toggle
  team_pvp_toggle: true
  
  # Economy Features (Requires Vault)
  team_bank: true           # Enable team bank system
  team_bank_deposit: true
  team_bank_withdraw: true
  
  # Storage Features
  team_enderchest: true     # Shared team ender chest
  
  # Communication Features
  team_chat: true
  team_message_command: true
  
  # Cross-Server Display
  show_cross_server_status: true
```

**Team Settings:**
```yaml
teams:
  # Team Creation
  max_name_length: 16
  min_name_length: 3
  max_tag_length: 6
  max_description_length: 100
  allowed_name_characters: "a-zA-Z0-9_"
  
  # Team Size Limits
  default_max_members: 10
  absolute_max_members: 50  # Hard limit
  
  # Team Home
  home_teleport_delay: 3    # Seconds before teleport
  home_cooldown: 300        # 5 minutes cooldown
  
  # Team Bank
  starting_balance: 0.0
  max_balance: 1000000.0
  
  # Team Warps
  max_warps: 5              # Max warps per team
  warp_teleport_delay: 3
  warp_cooldown: 60
```

**Team Chat Configuration:**
```yaml
team_chat:
  # Chat prefix character for quick team messages
  # Example: "#Hello team!" sends "Hello team!" to team chat
  character_enabled: true
  character: "#"            # Must be non-empty
  require_space: false      # "#message" or "# message"
  
  # Chat format (supports MiniMessage)
  format: "<gradient:#4C9DDE:#FFD700>[%team_tag%]</gradient> <white>%player_name%</white> <gray>»</gray> %message%"
```

**Performance Settings:**
```yaml
settings:
  # Debug mode for troubleshooting
  debug: false
  
  # Single server optimization
  # Set to 'true' if you have ONLY ONE server
  # - Disables cross-server features for better performance
  # - Use with H2 database for standalone servers
  single_server_mode: false
  
  # Update checking
  update_check: true
  
  # Async operations
  async_database_operations: true
```

---

## Admin GUI System

JustTeams features a comprehensive admin GUI system for managing teams across your network.

### Admin Panel Hierarchy

```
/team admin (Main Admin Panel)
    ├─→ Manage Teams (All Teams List, Paginated)
    │       └─→ Team Management Panel
    │               ├─→ Edit Member Permissions
    │               ├─→ View Team Ender Chest
    │               └─→ Edit Team Settings
    └─→ View Ender Chest (Direct Access)
```

### Main Admin Panel (`/team admin`)

**Size:** 27 slots (3 rows)

| Slot | Item | Action | Description |
|------|------|--------|-------------|
| 9 | Compass | Manage Teams | Opens paginated team list (45 teams per page) |
| 12 | Ender Chest | View Ender Chest | Opens specific team's shared ender chest |
| 14 | Redstone | Reload Plugin | Reloads all configuration files |
| 22 | Barrier | Close | Closes the inventory |

### Team Management Panel

**Size:** 54 slots (6 rows)  
**Features:** Edit all team settings, manage members, view stats

#### Team Settings (Row 1)

| Slot | Action | Cross-Server Sync | Description |
|------|--------|-------------------|-------------|
| 0 | Team Info | ❌ | Display team name, owner, member count |
| 1 | Edit Description | ✅ Redis + MySQL | Chat input for team description |
| 2 | Rename Team | ✅ Redis + MySQL | Chat input for new team name |
| 3 | Edit Tag | ✅ Redis + MySQL | Chat input for team tag (max 6 chars) |

#### Team Toggles & Actions (Row 2)

| Slot | Action | Cross-Server Sync | Description |
|------|--------|-------------------|-------------|
| 9 | Toggle Public/Private | ✅ Redis + MySQL | Instant toggle with material change |
| 10 | Toggle PvP | ✅ Redis + MySQL | Enable/disable team PvP |
| 11 | Edit Balance | ✅ Redis + MySQL | Chat input for team bank balance |
| 12 | Edit Stats (K/D) | ✅ Redis + MySQL | Chat input for kills and deaths |
| 13 | View Ender Chest | ❌ | Direct access to team ender chest |
| 14 | Disband Team | ✅ Redis + MySQL | Confirmation GUI → Delete team |

#### Member Management (Rows 3-6)

| Slot Range | Item | Action | Description |
|------------|------|--------|-------------|
| 18-26 | Yellow Glass | Divider | Visual separator |
| 27-47 | Player Heads | Click to Edit | Opens member permission editor (21 members per page) |
| 48 | Left Arrow | Previous Page | Navigate to previous member page |
| 49 | Player Head | Info | Shows member count and current page |
| 50 | Right Arrow | Next Page | Navigate to next member page |

**Member Head Format:**
- **Owner:** Gold star ⭐ in lore
- **Admin:** `<gradient:#FFD700:#FFA500>Admin</gradient>`
- **Moderator:** `<#4ECDC4>Moderator</#4ECDC4>`
- **Member:** `<gray>Member</gray>`

### Member Permission Editor

**Size:** 54 slots (6 rows)  
**Features:** Full control over individual member permissions

| Slot | Item | Action | Cross-Server Sync | Description |
|------|------|--------|-------------------|-------------|
| 4 | Player Head | Member Info | ❌ | Display name, role, join date |
| 19 | Lime/Gray Dye | Toggle Withdraw | ✅ Redis + MySQL | Bank withdrawal permission |
| 20 | Lime/Gray Dye | Toggle Ender Chest | ✅ Redis + MySQL | Ender chest access permission |
| 21 | Lime/Gray Dye | Toggle Set Home | ✅ Redis + MySQL | Set home permission |
| 22 | Lime/Gray Dye | Toggle Use Home | ✅ Redis + MySQL | Teleport to home permission |
| 29 | Emerald | Promote Member | ✅ Redis + MySQL | Promote to next role |
| 30 | Redstone | Demote Member | ✅ Redis + MySQL | Demote to previous role |
| 33 | TNT | Kick Member | ✅ Redis + MySQL | Remove from team |
| 45 | Arrow | Back | ❌ | Return to team management panel |

**Permission Toggle Visualization:**
- **Enabled:** Lime Dye with `<green>✔ Enabled</green>` lore
- **Disabled:** Gray Dye with `<red>✘ Disabled</red>` lore

**Owner Protection:**
- Team owners cannot be edited by admins
- Attempting to edit owner shows warning message
- Owner must use `/team transfer` to change ownership

### Cross-Server Synchronization

All admin actions are instantly synchronized across your network:

**Sync Flow:**
1. Admin performs action (e.g., toggle PvP, kick member)
2. **Database Updated First** (MySQL/MariaDB) for data persistence
3. **Redis Publish** instant update to all servers (<100ms latency)
4. **MySQL Fallback** polling every 1 second if Redis unavailable
5. All affected players notified on their current server
6. GUIs refresh automatically to show updated data

**Supported Update Types:**
- `ADMIN_BALANCE_SET` - Team bank balance changed
- `ADMIN_STATS_SET` - Team kills/deaths changed
- `ADMIN_PERMISSION_UPDATE` - Member permission toggled
- `ADMIN_MEMBER_PROMOTE` - Member promoted by admin
- `ADMIN_MEMBER_DEMOTE` - Member demoted by admin
- `ADMIN_MEMBER_KICK` - Member kicked by admin
- `PUBLIC_STATUS_CHANGED` - Public/private toggle
- `PVP_STATUS_CHANGED` - PvP enabled/disabled
- `TEAM_UPDATED` - General team settings changed

**Latency:**
- **With Redis:** <100ms (measured in production)
- **MySQL Only:** ~1 second (polling interval)

### GUI Customization with Dummy Items

JustTeams allows you to add decorative items to any GUI for enhanced visual customization.

**Configuration (gui.yml):**
```yaml
dummy-items:
  decoration-diamond:
    material: DIAMOND
    display-name: "<gradient:#00FFFF:#0080FF>✦ Premium Team ✦</gradient>"
    lore:
      - "<gray>Exclusive decoration"
    slots: [10, 16]
    custom-model-data: 1001
    enchanted: true
  
  corner-skulls:
    material: PLAYER_HEAD
    display-name: "<gold>★</gold>"
    slots: [0, 8, 45, 53]
```

**Features:**
- Place items in single or multiple slots
- Custom model data support for resource packs
- Enchantment glow effect
- MiniMessage formatting for display names and lore
- Fully configurable per GUI

**Static Utility Method:**
```java
GUIManager.loadDummyItems(inventory, configSection)
```

---
## Team Features

### Team Home System

Set and teleport to a team home location with configurable cooldowns and delays.

**Commands:**
- `/team sethome` - Set team home at your current location
- `/team home` - Teleport to team home

**Configuration:**
```yaml
teams:
  home_teleport_delay: 3    # Seconds before teleport
  home_cooldown: 300        # 5 minutes between uses
```

**Permissions:**
- Per-member permission: `CAN_SET_HOME`, `CAN_USE_HOME`
- Bypass cooldown: `justteams.bypass.home.cooldown`

**Cross-Server Support:** ✅ Team home syncs across network

---

### Team Warp System

Create multiple warp points for quick team navigation.

**Commands:**
- `/team setwarp <name>` - Create a warp at current location
- `/team delwarp <name>` - Delete a team warp
- `/team warp <name>` - Teleport to team warp
- `/team warps` - List all team warps (GUI)

**Configuration:**
```yaml
teams:
  max_warps: 5              # Maximum warps per team
  warp_teleport_delay: 3    # Teleport delay
  warp_cooldown: 60         # 1 minute cooldown
```

**Permissions:**
- Set warps: Moderator+ role
- Delete warps: Admin+ role
- Use warps: All team members
- Bypass cooldown: `justteams.bypass.warp.cooldown`

**Cross-Server Support:** ✅ Warps sync across network

---

### Team Bank System

Shared economy system with deposits and withdrawals (requires Vault).

**Commands:**
- `/team bank` - View bank balance
- `/team bank deposit <amount>` - Deposit money
- `/team bank withdraw <amount>` - Withdraw money

**Configuration:**
```yaml
features:
  team_bank: true
  team_bank_deposit: true
  team_bank_withdraw: true

teams:
  starting_balance: 0.0
  max_balance: 1000000.0
```

**Permissions:**
- Deposit: All team members
- Withdraw: Requires `CAN_WITHDRAW` permission (configurable per member)
- Bypass: `justteams.bypass.bank.withdraw`

**Cross-Server Support:** ✅ Balance syncs instantly via Redis/MySQL

---

### Team Ender Chest

Shared ender chest storage accessible by authorized team members.

**Access Methods:**
1. `/team` GUI → Click ender chest button
2. Admin GUI → View any team's ender chest
3. Right-click ender chest block (if enabled)

**Configuration:**
```yaml
features:
  team_enderchest: true

enderchest:
  require_permission: true  # Use CAN_USE_ENDERCHEST permission
  require_role: "MEMBER"    # Minimum role required
```

**Permissions:**
- Per-member: `CAN_USE_ENDERCHEST` (configurable in admin GUI)
- Bypass: `justteams.bypass.enderchest.use`

**Storage:** 54 slots (6 rows) per team, saved to database

### Team Chat System

Dedicated team communication with multiple input methods and admin monitoring.

**Methods:**
1. **Toggle Mode:** `/team chat` - All messages go to team
2. **Prefix Character:** `#Hello team!` - Quick team message
3. **Direct Command:** `/teammsg Hello team!` - Single team message

**Configuration:**
```yaml
team_chat:
  character_enabled: true
  character: "#"            # Prefix character for quick messages
  require_space: false      # "#msg" or "# msg"
  
  # MiniMessage format (supports gradients, colors, hover text)
  format: "<gradient:#4C9DDE:#FFD700>[%team_tag%]</gradient> <white>%player_name%</white> <gray>»</gray> %message%"
```

**Features:**
- Rich MiniMessage formatting
- Cross-server team chat via Redis/MySQL
- Toggle mode persists across sessions
- Customizable chat format per server
- Automatic profanity filter (configurable blacklist)
- **Admin Chat Spy** - Monitor all team chats with permission

**Commands:**
- `/team chat` - Toggle team chat mode
- `/team chatspy` or `/team spy` - Toggle admin chat spy (requires `justteams.chatspy`)
- `/teammsg <message>` - Send team message (aliases: /tm, /tmsg)
- `/guildmsg`, `/clanmsg`, `/partymsg` - Alternative aliases

**Admin Chat Spy:**
- **Permission:** `justteams.chatspy` (default: OP)
- **Usage:** `/team chatspy` to toggle spy mode
- **Format:** `[SPY] [TeamName] PlayerName: message` (gray/red/white formatting)
- **Behavior:** See all team chat messages from teams you're not in
- **Privacy:** Players are not notified when being monitored
**Commands:**
- `/team chat` - Toggle team chat mode
- `/teammsg <message>` - Send team message (aliases: /tm, /tmsg)
- `/guildmsg`, `/clanmsg`, `/partymsg` - Alternative aliases

---

### Team PvP System

Toggle PvP protection for team members.

**Usage:**
- `/team pvp` - Toggle PvP for your team (Owner/Admin only)
- Admin GUI → Toggle PvP button

**Behavior:**
- **Enabled:** Team members can damage each other
- **Disabled:** Team members cannot attack each other

**Configuration:**
```yaml
features:
  team_pvp: true
  team_pvp_toggle: true

pvp:
  default_enabled: false    # New teams start with PvP disabled
```

**Integration:**
- Works with PvPManager plugin for advanced PvP control
- Respects other plugin protections (WorldGuard, GriefPrevention, etc.)

**Cross-Server Support:** ✅ PvP status syncs across network

---

### Team Information & Leaderboard

View team details and rankings.

**Commands:**
- `/team info [team]` - View team information
- `/team list` - Browse all teams (paginated GUI)
- `/team top` - View team leaderboard

**Team Info Display:**
- Team name and tag
- Owner and member list
- Member count and max members
- Team creation date
- Public/Private status
- PvP enabled/disabled
- Bank balance (if economy enabled)
- Team statistics (kills, deaths, K/D ratio)

**Leaderboard Sorting:**
- Most members
- Highest bank balance
- Most kills
- Best K/D ratio

**Configuration:**
```yaml
features:
  team_info: true
  team_leaderboard: true
  
leaderboard:
  refresh_interval: 300     # Update every 5 minutes
  max_entries: 10           # Top 10 teams displayed
```

---

### Join Requests System

Allow players to request to join private teams.

**Player Flow:**
1. Player uses `/team join <team>` on private team
2. Request sent to team owner/admins
3. Owner/Admin reviews via `/team requests` GUI
4. Accept or deny request with one click

**Commands:**
- `/team join <team>` - Request to join a team
- `/team requests` - View pending join requests (Owner/Admin)

**Configuration:**
```yaml
features:
  team_join_requests: true
  
join_requests:
  expire_after: 86400       # Requests expire after 24 hours
  max_pending: 10           # Max pending requests per team
```

**GUI Features:**
- Player head display with join date
- Accept (green) / Deny (red) buttons
- Pagination for multiple requests
- Real-time updates across servers

---

### Team Blacklist System

Prevent specific players from joining your team.

**Usage:**
- `/team` GUI → Blacklist button
- Add/remove players from blacklist
- Blacklisted players cannot join or request to join

**GUI Features:**
- Player head display
- Add player by name
- Remove with single click
- Pagination support

**Configuration:**
```yaml
features:
  team_blacklist: true

blacklist:
  max_entries: 50           # Max blacklisted players per team
```

**Cross-Server Support:** ✅ Blacklist syncs across network

---

## Discord Webhooks

JustTeams can send real-time notifications to Discord channels using webhooks. Get instant updates about team events, member changes, and economy transactions directly in Discord.

### Quick Setup

1. **Create a Discord Webhook:**
   - Open Discord → Server Settings → Integrations → Webhooks
   - Click "New Webhook"
   - Choose a channel (e.g., `#team-logs`)
   - Copy the webhook URL

2. **Configure JustTeams:**
   Open `plugins/JustTeams/webhooks.yml`:
   ```yaml
   webhook:
     enabled: true
     url: "https://discord.com/api/webhooks/YOUR_WEBHOOK_URL"
     username: "JustTeams Bot"
     server_name: "My Minecraft Server"
   ```

3. **Enable Events:**
   ```yaml
   events:
     team_create:
       enabled: true
     player_join:
       enabled: true
     player_kick:
       enabled: true
   ```

4. **Reload Plugin:**
   ```
   /team reload
   ```

### Available Events

| Event | Description | Default | Color |
|-------|-------------|---------|-------|
| `team_create` | Team created | ✅ Enabled | 🟢 Green |
| `team_delete` | Team disbanded | ✅ Enabled | 🔴 Red |
| `player_join` | Player joined team | ✅ Enabled | 🟢 Green |
| `player_leave` | Player left team | ✅ Enabled | 🔴 Red |
| `player_kick` | Player kicked | ✅ Enabled | 🔴 Red |
| `player_promote` | Player promoted | ✅ Enabled | 🟡 Gold |
| `player_demote` | Player demoted | ✅ Enabled | 🔵 Blue |
| `ownership_transfer` | Owner changed | ✅ Enabled | 🟡 Gold |
| `team_rename` | Team name changed | ✅ Enabled | 🔵 Blue |
| `team_tag_change` | Team tag changed | ✅ Enabled | 🔵 Blue |
| `team_pvp_toggle` | PvP toggled | ❌ Disabled | 🔵 Blue |
| `team_public_toggle` | Public/Private toggled | ❌ Disabled | 🔵 Blue |
| `player_invite` | Player invited | ❌ Disabled | 🟢 Green |
| `bank_deposit` | Money deposited | ❌ Disabled | 🟣 Purple |
| `bank_withdraw` | Money withdrawn | ❌ Disabled | 🟣 Purple |

### Event Configuration Examples

**Team Creation Notification:**
```yaml
events:
  team_create:
    enabled: true
    color: 5763719  # Green (decimal)
    title: "🎉 New Team Created"
    description: "**{player}** created a new team!"
    show_fields: true
    fields:
      - name: "Team Name"
        value: "{team}"
        inline: true
      - name: "Team Tag"
        value: "`{tag}`"
        inline: true
      - name: "Owner"
        value: "{player}"
        inline: true
    footer: "Team created on {server}"
    timestamp: true
```

**Player Kicked Notification:**
```yaml
events:
  player_kick:
    enabled: true
    color: 15548997  # Red
    title: "🚫 Player Kicked"
    description: "**{kicked}** was kicked from **{team}**"
    show_fields: true
    fields:
      - name: "Kicked Player"
        value: "{kicked}"
        inline: true
      - name: "Kicked By"
        value: "{kicker}"
        inline: true
      - name: "Team"
        value: "{team} `{tag}`"
        inline: true
    footer: "Kicked on {server}"
    timestamp: true
```

**Bank Transaction Notification:**
```yaml
events:
  bank_deposit:
    enabled: true
    color: 10181046  # Purple
    title: "💰 Bank Deposit"
    description: "**{player}** deposited money to **{team}**"
    show_fields: true
    fields:
      - name: "Player"
        value: "{player}"
        inline: true
      - name: "Amount"
        value: "${amount}"
        inline: true
      - name: "New Balance"
        value: "${balance}"
        inline: true
    footer: "Transaction on {server}"
    timestamp: true
```

### Available Placeholders

**Common Placeholders (all events):**
- `{player}` - Player name
- `{team}` - Team name
- `{tag}` - Team tag
- `{server}` - Server name (from config)
- `{time}` - Current timestamp

**Event-Specific Placeholders:**

| Event | Additional Placeholders |
|-------|------------------------|
| `team_delete` | `{member_count}` |
| `player_join` | `{member_count}` |
| `player_leave` | `{member_count}` |
| `player_kick` | `{kicker}`, `{kicked}` |
| `player_promote` | `{promoter}`, `{old_role}`, `{new_role}` |
| `player_demote` | `{demoter}`, `{old_role}`, `{new_role}` |
| `ownership_transfer` | `{old_owner}`, `{new_owner}` |
| `team_rename` | `{old_name}`, `{new_name}` |
| `team_tag_change` | `{old_tag}`, `{new_tag}` |
| `team_pvp_toggle` | `{pvp_status}` (Enabled/Disabled) |
| `team_public_toggle` | `{public_status}` (Public/Private) |
| `player_invite` | `{inviter}`, `{invited}` |
| `bank_deposit` | `{amount}`, `{balance}`, `{new_balance}` |
| `bank_withdraw` | `{amount}`, `{balance}`, `{new_balance}` |

### Customizing Embed Colors

Discord uses **decimal color codes** for embeds. Convert hex to decimal:

**Common Colors:**
| Color | Hex | Decimal | Use Case |
|-------|-----|---------|----------|
| 🟢 Green | `#58C27D` | 5763719 | Success events (create, join) |
| 🔴 Red | `#ED4245` | 15548997 | Destructive events (kick, delete) |
| 🔵 Blue | `#5DADE2` | 5814783 | Info events (rename, toggle) |
| 🟡 Gold | `#FFC300` | 16766720 | Special events (promote, transfer) |
| 🟣 Purple | `#9B59B6` | 10181046 | Economy events (bank) |
| ⚪ Gray | `#95A5A6` | 9807270 | Neutral events |

**Color Converter:** https://www.spycolor.com/ (hex to decimal)

### Rate Limiting & Performance

Prevent Discord API rate limits with built-in rate limiting:

```yaml
webhook:
  rate_limiting:
    enabled: true
    max_per_minute: 20      # Max webhooks per minute
    min_delay_ms: 1000      # 1 second between sends
  
  retry:
    enabled: true
    max_attempts: 3         # Retry failed sends
    retry_delay_ms: 2000    # 2 seconds between retries
```

**Recommended Settings:**
- **Small Server (1-10 players):** `max_per_minute: 20`
- **Medium Server (10-50 players):** `max_per_minute: 15`, disable spammy events
- **Large Server (50+ players):** `max_per_minute: 10`, only enable critical events

**Disable Spammy Events for Large Servers:**
```yaml
events:
  player_invite:
    enabled: false        # Can be very spammy
  team_pvp_toggle:
    enabled: false        # Players toggle frequently
  team_public_toggle:
    enabled: false        # Not critical
  bank_deposit:
    enabled: false        # High traffic
```

### Multi-Server Setup

For networks with multiple servers, set unique names per server:

**Server 1 (Survival):**
```yaml
webhook:
  server_name: "Survival"
```

**Server 2 (Creative):**
```yaml
webhook:
  server_name: "Creative"
```

**Server 3 (SkyBlock):**
```yaml
webhook:
  server_name: "SkyBlock"
```

All servers can use the **same webhook URL** - the `{server}` placeholder differentiates them in Discord.

### Advanced: Custom Embed Formatting

Full control over Discord embed appearance:

```yaml
events:
  team_create:
    enabled: true
    
    # Embed color (decimal)
    color: 5763719
    
    # Main title with emoji
    title: "🎉 New Team Created"
    
    # Description with Discord markdown
    description: "**{player}** created a new team!"
    
    # Enable/disable fields section
    show_fields: true
    
    # Custom fields (up to 25 fields per embed)
    fields:
      - name: "Team Name"
        value: "{team}"
        inline: true          # Display side-by-side
      
      - name: "Team Tag"
        value: "`{tag}`"      # Inline code formatting
        inline: true
      
      - name: "Owner"
        value: "{player}"
        inline: true
      
      - name: "Members"
        value: "{member_count}/10"
        inline: false         # Full width
    
    # Footer text with icon
    footer: "Team created on {server}"
    
    # Show timestamp
    timestamp: true
```

**Discord Markdown Support:**
- `**bold**` → **bold**
- `*italic*` → *italic*
- `__underline__` → __underline__
- `` `code` `` → `code`
- `~~strikethrough~~` → ~~strikethrough~~

### Troubleshooting Webhooks

**Webhooks not sending:**
1. Verify webhook URL is correct (copy from Discord)
2. Check `enabled: true` in webhooks.yml
3. Enable debug mode in config.yml: `debug: true`
4. Review console for webhook errors
5. Test webhook URL with online tester: https://discohook.org/

**Discord says "Invalid Webhook Token":**
- Webhook URL was deleted/regenerated in Discord
- Copy new webhook URL from Discord webhook settings

**Messages not appearing:**
- Check Discord channel permissions for webhook
- Verify webhook is not muted/disabled
- Check rate limiting (may be queued)

**Rate limit errors (429):**
- Reduce `max_per_minute` in config
- Disable unnecessary events
- Increase `min_delay_ms` between sends

**Getting Help:**
Enable debug logging to see detailed webhook activity:
```yaml
# config.yml
settings:
  debug: true
```

Console will show:
```
[DEBUG] Webhook sent: TEAM_CREATE for team "TheBuilders"
[DEBUG] Webhook response: 204 No Content (success)
[DEBUG] Rate limit: 5/20 webhooks sent this minute
```

---

## Permissions

### Core Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `justteams.*` | All plugin permissions | OP |
| `justteams.admin` | All admin permissions | OP |
| `justteams.user` | All standard player permissions | Everyone |

### Command Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `justteams.command.create` | Create teams | Everyone |
| `justteams.command.disband` | Disband own team | Everyone |
| `justteams.command.invite` | Invite players | Everyone |
| `justteams.command.accept` | Accept invitations | Everyone |
| `justteams.command.deny` | Deny invitations | Everyone |
| `justteams.command.join` | Join public teams | Everyone |
| `justteams.command.leave` | Leave team | Everyone |
| `justteams.command.kick` | Kick members | Everyone |
| `justteams.command.info` | View team info | Everyone |
| `justteams.command.chat` | Use team chat | Everyone |
| `justteams.command.teammsg` | Send team messages | Everyone |
| `justteams.command.promote` | Promote members | Everyone |
| `justteams.command.demote` | Demote members | Everyone |
| `justteams.command.transfer` | Transfer ownership | Everyone |
| `justteams.command.settag` | Set team tag | Everyone |
| `justteams.command.setdescription` | Set description | Everyone |
| `justteams.command.sethome` | Set team home | Everyone |
| `justteams.command.home` | Use team home | Everyone |
| `justteams.command.setwarp` | Create warps | Everyone |
| `justteams.command.delwarp` | Delete warps | Everyone |
| `justteams.command.warp` | Use warps | Everyone |
| `justteams.command.warps` | View warps | Everyone |
| `justteams.command.pvp` | Toggle PvP | Everyone |
| `justteams.command.bank` | Use team bank | Everyone |
| `justteams.command.enderchest` | Use ender chest | Everyone |
| `justteams.command.top` | View leaderboard | Everyone |
| `justteams.command.public` | Toggle public status | Everyone |
| `justteams.command.requests` | View join requests | Everyone |
| `justteams.command.reload` | Reload configs | OP |
| `justteams.command.admin` | Access admin GUI | OP |
| `justteams.chatspy` | Monitor all team chats | OP |

### Bypass Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `justteams.bypass.bank.withdraw` | Bypass withdraw restrictions | OP |
| `justteams.bypass.enderchest.use` | Bypass ender chest restrictions | OP |
| `justteams.bypass.home.cooldown` | Bypass home cooldown | OP |
| `justteams.bypass.warp.cooldown` | Bypass warp cooldown | OP |

### Wildcard Permissions

```yaml
justteams.*:              # All permissions
  - justteams.admin       # All admin permissions
  - justteams.user        # All user permissions

justteams.user:           # All standard commands
  - justteams.command.*   # All command permissions

justteams.admin:          # Admin access
  - justteams.command.reload
  - justteams.command.admin
  - justteams.bypass.*    # All bypass permissions
```

---

## PlaceholderAPI

**Requirement**: Install [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) to use these placeholders.

All placeholders support per-player context and update in real-time across servers. **Note:** Most placeholders support both short and long versions (e.g., `%justteams_tag%` and `%justteams_team_tag%`).

### Team Information Placeholders

| Placeholder | Aliases | Description | Example Output |
|------------|---------|-------------|----------------|
| `%justteams_name%` | `%justteams_team_name%` | Player's team name | `The Builders` |
| `%justteams_tag%` | `%justteams_team_tag%` | Player's team tag | `BUILD` |
| `%justteams_color_name%` | - | Team name with color codes | `<#4C9DDE>The Builders</#4C9DDE>` |
| `%justteams_color_tag%` | - | Team tag with color codes | `<#FFD700>BUILD</#FFD700>` |
| `%justteams_plain_name%` | - | Team name without any formatting | `The Builders` |
| `%justteams_plain_tag%` | - | Team tag without any formatting | `BUILD` |
| `%justteams_owner%` | `%justteams_team_owner%` | Team owner name | `kotori` |
| `%justteams_member_count%` | `%justteams_team_members%`, `%justteams_team_size%` | Member count | `5` |
| `%justteams_max_members%` | `%justteams_team_max_members%`, `%justteams_team_capacity%` | Max member limit | `10` |
| `%justteams_members_online%` | - | Online member count | `3` |
| `%justteams_has_team%` | - | Boolean team check | `true` or `false` |
| `%justteams_team_id%` | - | Internal team ID | `12345` |
| `%justteams_description%` | `%justteams_team_description%` | Team description | `We build awesome stuff!` |
| `%justteams_display%` | - | Formatted team display (configurable in placeholders.yml) | `<#4C9DDE>⚔ [BUILD]</#4C9DDE>` |

### Team Status Placeholders

| Placeholder | Description | Example Output |
|------------|-------------|----------------|
| `%justteams_team_public%` | Public/Private status | `Public` or `Private` |
| `%justteams_team_pvp%` | PvP enabled status | `Enabled` or `Disabled` |
| `%justteams_is_public%` | Boolean public check | `true` or `false` |
| `%justteams_pvp_enabled%` | Boolean PvP check | `true` or `false` |
| `%justteams_team_full%` | Boolean full team check | `true` or `false` |

### Member Role Placeholders

| Placeholder | Description | Example Output |
|------------|-------------|----------------|
| `%justteams_role%` | Player's role in team | `OWNER`, `CO_OWNER`, `MEMBER` |
| `%justteams_role_level%` | Numeric role level | `4` (Owner), `3` (Co-Owner), `1` (Member) |
| `%justteams_is_owner%` | Boolean owner check | `true` or `false` |
| `%justteams_is_admin%` | Boolean admin check (Owner or Co-Owner) | `true` or `false` |
| `%justteams_is_co_owner%` | Boolean co-owner check | `true` or `false` |
| `%justteams_is_member%` | Boolean member check | `true` or `false` |
| `%justteams_join_date%` | Date player joined team | `03 Nov 2025` |

### Team Economy Placeholders

| Placeholder | Description | Example Output |
|------------|-------------|----------------|
| `%justteams_bank_balance%` | Team bank balance (formatted) | `5,000.50` |
| `%justteams_bank_formatted%` | Formatted balance with currency | `$5,000.50` |
| `%justteams_bank_balance_raw%` | Raw numeric balance (for ajLeaderboards) | `5000.50` |

### Team Statistics Placeholders

| Placeholder | Aliases | Description | Example Output |
|------------|---------|-------------|----------------|
| `%justteams_kills%` | - | Team total kills | `150` |
| `%justteams_deaths%` | - | Team total deaths | `50` |
| `%justteams_kd%` | `%justteams_kdr%` | Team K/D ratio | `3.00` |

### Team Home & Warp Placeholders

| Placeholder | Description | Example Output |
|------------|-------------|----------------|
| `%justteams_has_home%` | Boolean home check | `true` or `false` |
| `%justteams_home_location%` | Home coordinates | `world, 100, 64, 200` |
| `%justteams_warp_count%` | Number of warps | `3` |
| `%justteams_max_warps%` | Max warp limit | `5` |

### Special Placeholders

| Placeholder | Description | Example Output |
|------------|-------------|----------------|
| `%justteams_created_at%` | Team creation date | `Unknown` (placeholder) |

### Usage Examples

**Testing Placeholders:**
```
/papi parse me %justteams_tag%
/papi parse me %justteams_name%
/papi parse me %justteams_display%
/papi bcparse me %justteams_role%
```

**Scoreboard Integration (with DeluxeMenus, FeatherBoard, etc.):**
```yaml
- "Team: <gradient:#4C9DDE:#FFD700>%justteams_tag%</gradient>"
- "Members: %justteams_member_count%/%justteams_max_members% (%justteams_members_online% online)"
- "Role: %justteams_role%"
- "Balance: %justteams_bank_formatted%"
- "K/D: %justteams_kd%"
```

**Chat Format Integration (with ChatManager, EssentialsChat, etc.):**
```yaml
# Show team tag before player name
format: "%justteams_display% %player_name%: %message%"

# Alternative: Show team tag in brackets
format: "[%justteams_tag%] %player_name%: %message%"
```

**Tab List Integration (with TAB, NametagEdit, etc.):**
```yaml
# Show team tag as prefix
prefix: "%justteams_display% "

# Show role as suffix
suffix: " [%justteams_role%]"

# Combined example
prefix: "[%justteams_tag%] "
suffix: " (%justteams_role_level%)"
```

**DeluxeMenus Example:**
```yaml
item:
  material: PLAYER_HEAD
  name: "<gold>%justteams_name%</gold>"
  lore:
    - "<gray>Tag: <white>%justteams_tag%</white></gray>"
    - "<gray>Owner: <white>%justteams_owner%</white></gray>"
    - "<gray>Members: <white>%justteams_member_count%/%justteams_max_members%</white></gray>"
    - "<gray>Balance: <green>%justteams_bank_formatted%</green></gray>"
    - ""
    - "<gray>Your Role: <yellow>%justteams_role%</yellow></gray>"
```

---

## Message Customization

All messages support **MiniMessage** formatting for rich text, colors, gradients, and hover/click events.

### MiniMessage Format Examples

**`messages.yml` (398 lines of customizable messages):**
```yaml
# Simple colors
prefix: "<dark_gray>[<gradient:#4C9DDE:#FFD700>Teams</gradient>]</dark_gray>"
team_created: "<prefix> <green>Team created successfully!"
team_disbanded: "<prefix> <red>Team has been disbanded.</red>"

# Gradients
member_joined: "<prefix> <gradient:#20B2AA:#7FFFD4>%player% joined the team!</gradient>"
member_left: "<prefix> <gradient:red:yellow>%player% left the team.</gradient>"

# Hover & Click Events
team_invite: "<hover:show_text:'Click to accept'><click:run_command:/team accept %team%><prefix> <yellow>You've been invited to join <gold>%team%</gold>! Click to accept.</click></hover>"

# Role-specific formatting
promoted: "<prefix> <gradient:#FFD700:#FFA500>You've been promoted to %role%!</gradient>"
demoted: "<prefix> <gray>You've been demoted to %role%.</gray>"

# Action bar messages
home_teleporting: "<yellow>⏳ Teleporting to team home in %seconds%s..."
warp_teleporting: "<aqua>✈ Teleporting to warp: %warp%"

# Admin messages
admin_balance_set: "<prefix> <gold>Set %team%'s balance to $%balance%</gold>"
admin_member_kicked: "<prefix> <red>Kicked %player% from %team%</red>"
```

### Available Message Placeholders

Messages support these internal placeholders:

**Player Placeholders:**
- `%player%` / `%player_name%` - Player name
- `%player_uuid%` - Player UUID
- `%target%` / `%target_player%` - Target player name

**Team Placeholders:**
- `%team%` / `%team_name%` - Team name
- `%team_tag%` - Team display tag
- `%team_owner%` - Team owner name
- `%team_members%` - Current member count
- `%team_max_members%` - Maximum member limit
- `%team_description%` - Team description

**Role & Permission Placeholders:**
- `%role%` - Member role (Owner, Admin, Moderator, Member)
- `%old_role%` - Previous role (for promotions/demotions)
- `%new_role%` - New role (for promotions/demotions)

**Economy Placeholders:**
- `%balance%` - Team bank balance
- `%amount%` - Transaction amount
- `%cost%` - Cost for action

**Location Placeholders:**
- `%world%` - World name
- `%x%`, `%y%`, `%z%` - Coordinates
- `%warp%` - Warp name

**Status Placeholders:**
- `%status%` - Public/Private status
- `%pvp_status%` - PvP enabled/disabled
- `%seconds%` - Countdown seconds

### Customizable Message Categories

**Team Management:**
- Team creation, disband, rename, description, tag changes
- Public/private toggle, PvP toggle
- Team limits reached, name/tag validation errors

**Member Management:**
- Invitations sent, accepted, denied, expired
- Join requests sent, accepted, denied
- Member joined, left, kicked
- Promotions, demotions
- Permission changes

**Team Features:**
- Home set, home teleport, home cooldown
- Warp created, deleted, teleport, cooldown
- Bank deposit, withdraw, balance
- Ender chest access, insufficient permissions

**Admin Actions:**
- Balance changes, stats updates
- Permission toggles, role changes
- Team disband, member kick
- Reload confirmation

**Error Messages:**
- No permission, feature disabled
- Invalid input, player not found
- Team not found, already in team
- Cooldown active, insufficient funds

For complete MiniMessage syntax, see: https://docs.advntr.dev/minimessage/format.html

---

## Performance Optimization

### Database Connection Pooling

HikariCP connection pooling for optimal performance:

**`config.yml` - Connection Pool Settings:**
```yaml
connection_pool:
  # H2 defaults: max_size=4, min_idle=1
  # MySQL defaults: max_size=10, min_idle=3
  max_size: 10              # Maximum connections
  min_idle: 3               # Minimum idle connections
  
  # Timeouts in milliseconds
  idle_timeout: 300000      # 5 minutes
  max_lifetime: 1800000     # 30 minutes
  connection_timeout: 30000 # 30 seconds
  validation_timeout: 5000  # 5 seconds
  
  # Connection testing
  connection_test_query: "SELECT 1"
  
  # Leak detection (0 = disabled)
  leak_detection_threshold: 0
```

Benefits:
- Reuses database connections (no overhead per query)
- Automatic connection health checks
- Graceful recovery from network issues
- Optimal for both H2 and MySQL

---

### Redis Real-Time Sync

For large networks, enable Redis for instant cross-server updates:

**`config.yml` - Redis Configuration:**
```yaml
redis:
  enabled: true
  host: "localhost"
  port: 6379
  password: ""
  use_ssl: false
  timeout: 5000             # Connection timeout (ms)
  
  pool:
    max_total: 20           # Max total connections
    max_idle: 10            # Max idle connections
    min_idle: 2             # Min idle connections
```

**Performance Benefits:**
- **<100ms latency** for cross-server updates (measured in production)
- Instant GUI refresh across all servers
- Real-time notifications to affected players
- No polling overhead

**MySQL Fallback:**
- If Redis unavailable, automatically falls back to MySQL polling
- 1-second polling interval ensures updates still propagate
- Data always persists in MySQL for reliability

---

### Async Operations

All database operations run asynchronously to prevent server lag:

```yaml
settings:
  async_database_operations: true
```

**Async Operations:**
- Team creation, disband, rename
- Member add, remove, role updates
- Permission changes
- Bank transactions
- Home/warp updates
- All admin GUI actions

**Main Thread Operations:**
- GUI opens/closes
- Player teleportation
- Inventory updates

---

### Folia Support

JustTeams is fully compatible with Folia's regionized threading:

- All operations are region-aware
- No global state modifications
- Safe concurrent team operations
- Optimal performance on Folia servers
- Tested on Folia 1.21+

**Configuration:**
```yaml
# In plugin.yml
folia-supported: true
```

---

### Single Server Optimization

For standalone servers, enable single-server mode:

```yaml
settings:
  single_server_mode: true
```

**Optimizations When Enabled:**
- Disables cross-server sync features
- Reduces MySQL query overhead
- Skips Redis connection attempts
- Faster team operations (no sync delay)
- Best used with H2 database

---

### Performance Tips

**For Single Servers:**
- Use H2 database (`storage.type: "h2"`)
- Enable `single_server_mode: true`
- Disable Redis (`redis.enabled: false`)

**For Small Networks (2-5 servers):**
- Use MySQL with default connection pool (max_size: 10)
- Enable Redis for instant sync
- Keep `single_server_mode: false`

**For Large Networks (5+ servers):**
- Use MySQL with larger connection pool (max_size: 20)
- Enable Redis with larger pool (max_total: 30)
- Consider dedicated MySQL/Redis servers
- Monitor connection pool usage in debug mode

**General Optimization:**
- Disable unused features in `config.yml` (`features` section)
- Reduce `home_cooldown` and `warp_cooldown` if not needed
- Use MiniMessage formatting sparingly in high-traffic messages
- Enable async operations (default: true)

---

## Troubleshooting

### Common Issues

**"You are not in a team"**
- Player has left or been kicked from team
- Team was disbanded by owner or admin
- Cross-server desync (run `/team reload` or wait 1 second)

**Team not syncing across servers**
- Verify MySQL connection in console logs
- Check `storage.type: "mysql"` in config.yml
- Confirm same MySQL database on all servers
- Test with `/team admin` → View team on different server
- If using Redis, verify connection with `redis.enabled: true`

**Redis not connecting**
- Check Redis server is running: `redis-cli ping`
- Verify host/port in config.yml
- Check password if Redis requires authentication
- Review console logs for connection errors
- Plugin will auto-fallback to MySQL if Redis fails

**Admin GUI not opening**
- Verify permission: `justteams.command.admin`
- Check console for errors
- Ensure MySQL/H2 database is accessible
- Try `/team reload` to refresh configurations

**Ender chest items disappearing**
- Database connection issue (check MySQL status)
- Verify `features.team_enderchest: true`
- Check for storage corruption (backup database)
- Ensure same database across all servers

**Team chat not working**
- Verify `character: "#"` is set (not empty)
- Check `team_chat.character_enabled: true`
- Ensure player has toggled team chat: `/team chat`
- Review `team_chat.format` in config.yml

**Bank balance incorrect**
- Check Vault plugin is installed and loaded
- Verify economy plugin (EssentialsX, CMI, etc.) is working
- Review console for economy errors
- Use Admin GUI to view/adjust balance

**Home/Warp cooldown not working**
- Verify player doesn't have bypass permission
- Check cooldown values in config.yml
- Review `home_cooldown` and `warp_cooldown` settings

**"Feature is disabled"**
- Check `features` section in config.yml
- Ensure specific feature is set to `true`
- Restart server after changing features
- Some features require dependencies (Vault for bank)

### Debug Mode

Enable detailed logging in `config.yml`:
```yaml
settings:
  debug: true
```

This will output:
- Database query execution times
- Redis publish/subscribe events
- Team cache operations
- Cross-server sync latency
- Permission checks
- GUI open/close events
- All command executions

**Debug Log Examples:**
```
[DEBUG] Team created: TeamName (UUID: 12345)
[DEBUG] MySQL query executed in 15ms: SELECT * FROM teams WHERE id = ?
[DEBUG] Redis published MEMBER_KICKED update for team: TeamName
[DEBUG] Cross-server sync latency: 87ms
[DEBUG] Team cache updated for player: PlayerName
```

### Database Troubleshooting

**MySQL Connection Issues:**
1. Verify MySQL server is running
2. Check credentials in config.yml
3. Test connection: `mysql -h HOST -u USER -p DATABASE`
4. Review `connection_timeout` and `socket_timeout` settings
5. Check firewall allows MySQL port (3306)

**H2 Database Corruption:**
1. Stop server
2. Backup `plugins/JustTeams/teams.db`
3. Delete corrupted database
4. Restart server (new database created)
5. Import from backup if available

**Slow Database Performance:**
1. Enable `debug: true` to measure query times
2. Check connection pool settings (increase if needed)
3. Verify database server resources (CPU, RAM, disk I/O)
4. Consider dedicated database server for large networks
5. Review slow query logs on MySQL

### Getting Help

If you encounter issues not covered here:

1. **Enable debug mode** and review console logs
2. **Check configuration files** for syntax errors
3. **Verify dependencies** (Vault, PlaceholderAPI) are up-to-date
4. **Test database connection** directly (MySQL/Redis)
5. **Review server resources** (RAM, CPU, disk space)
6. **Check for plugin conflicts** (disable other team plugins)

---

## Technical Specifications

| Component | Details |
|-----------|---------|
| **Plugin Version** | 2.3.6 |
| **Minecraft Version** | 1.21+ |
| **Server Software** | Paper, Folia, Spigot, Purpur |
| **Java Version** | 21+ required |
| **API Version** | 1.21 |
| **Database Support** | H2 (embedded), MySQL 8.0+, MariaDB 10.5+ |
| **Cache Support** | Redis 5.0+ (optional) |
| **Dependencies** | Vault, PlaceholderAPI, PvPManager (all optional) |
| **License** | CC BY-NC-SA 4.0 |
| **Author** | kotori |

### Feature Matrix

### Feature Matrix

| Feature | Status | Requirements |
|---------|--------|--------------|
| Team Creation & Management | ✅ Core | None |
| Cross-Server Sync | ✅ Available | MySQL |
| Real-Time Sync | ✅ Available | Redis (optional) |
| Team Home System | ✅ Available | None |
| Team Warp System | ✅ Available | None |
| Team Bank | ✅ Available | Vault |
| Team Ender Chest | ✅ Available | None |
| Team Chat | ✅ Available | None |
| Admin Chat Spy | ✅ Available | justteams.chatspy |
| Team PvP Toggle | ✅ Available | None |
| Join Requests | ✅ Available | None |
| Team Blacklist | ✅ Available | None |
| Admin GUI | ✅ Available | justteams.command.admin |
| Permission Editor | ✅ Available | Admin GUI |
| Role System | ✅ Available | None |
| Team Tags (Optional) | ✅ Configurable | team_tag: true |
| GUI Dummy Items | ✅ Available | None |
| Economy Integration | ✅ Available | Vault |
| PlaceholderAPI | ✅ Available | PlaceholderAPI |
| PvPManager Hook | ✅ Available | PvPManager |
| Folia Support | ✅ Full Support | Folia |
| MiniMessage Formatting | ✅ Available | None |
| Database Connection Pooling | ✅ Available | None |
| Async Operations | ✅ Available | None |
## Changelog

### Version 2.3.6 (Current)

**Bug Fixes:**
- Fixed team creation validation when team_tag feature is disabled
- Fixed setTeamTag() method to check if feature is enabled before execution
- Ensured empty tags are properly handled when tag feature is disabled
- Improved feature toggle consistency across all tag-related operations

## License & Credits

**JustTeams** is developed and maintained with care by **kotori**.

This plugin is open-source software, licensed under the CC BY-NC-SA 4.0 License.

---

**Need help?** Review the troubleshooting section above or enable debug mode and check your console logs.

**Enjoying JustTeams?** Consider leaving feedback or supporting continued development!
