KikiShield 0.6.0

Made By Kiki #72385
A local incoming-action shield for Bondage Club R132.
English interface with a compact dark menu and the supplied elf-and-shield icon.

INSTALL / UPDATE

Direct installer (opens the userscript manager confirmation):
https://raw.githubusercontent.com/Lilja000/KikiShield/main/KikiShield.user.js

Replace the previous KikiShield userscript with KikiShield.user.js in
Tampermonkey or Violentmonkey, then reload the entire game page.
Keep only one enabled KikiShield copy. Keep the userscript header intact.
If you downloaded the ZIP, extract it and import KikiShield.user.js.
The ZIP is a release bundle, not a Tampermonkey settings-backup ZIP.
You may instead paste the complete .user.js into a new userscript and save.

Run at document-start in the page context, before the game connects.
Existing per-account preferences and the icon position are retained.
Tap the round icon for Protection / Automation / Activity; drag it to move it.
A mint dot means the ingress filter is active, gold means waiting, and pink
means it needs attention. Read the status, rather than just checking the icon.
KikiShield now also appears in ModSDK diagnostics when the SDK is available.
To disable it, turn off the userscript and reload the game.

DEFAULTS AND ADDON SELECTION

Block BCC is ON. Block LSCG is OFF. The older combined isolation preference,
if enabled, migrates to both switches ON. Explicit individual choices win.
Each switch blocks that addon's identifiable incoming commands AND metadata,
even from trusted people. BCC custom activity messages are also isolated.
This is incoming protection: it does not uninstall a local addon, switch off
its local features, or stop its own outgoing metadata publication.
Ordinary BC item/appearance packets do not carry a trusted addon identity;
those packets always follow recipient permissions, whatever addon sent them.

With a switch OFF, the core permission, list, target, shape and unsafe-relay
checks stay active. Normal authorized addon behavior can then pass to that
addon's own checks. Keep Strict hidden-message filter OFF for normal addon
communication. Known BCX and KikiLink metadata/communication stay available.

WHAT CHANGED IN 0.6.0

- Three compact tabs: Protection for access and addon switches, Automation for
  automatic list rules, and Activity for recorded events and their details.
- A shorter permission selector, concise status, compact Activity totals and
  collapsible secondary settings keep the menu readable on narrow screens.
- A red launcher badge and the Activity tab count new events, including repeats
  combined into an existing row. The display shows 99+ above 99 events.
- Viewing Activity clears the unread count. Incoming events stay read while
  Activity is open in a visible browser tab, including when a severity filter is
  selected. Opening another menu tab does not mark Activity as read.
- A closed panel, background browser tab or Panic screen does not mark events
  as read. Clear Activity, switching account or reloading resets the counter.
  Reading Activity does not delete its entries or reset the session totals.
- Updates are coalesced into one deferred refresh per event burst. The badge
  adds no network traffic or additional polling interval.

RETAINED FROM 0.5.0

- Expand an Activity entry to inspect the command, sender, target, blocking
  reason, assessment and retained incoming packet. Filter entries by severity.
- Serious, Caution, Background and System labels distinguish direct rejected
  operations from uncertain commands, routine metadata and shield diagnostics.
  These labels describe the available evidence, not a person's intent.
- Optional automatic blacklist or ghost actions, with separate rules for serious
  blocked attempts, observed BCC traffic and observed LSCG traffic. Automation is
  OFF by default. Trusted-person exclusions, member-ID exceptions, a serious-event
  threshold, action limits and conditional Undo help avoid unintended list changes.
- Activity can now retain private command arguments and appearance data locally.
  Payloads are bounded, ordinary chat and Panic contents are excluded, and exports
  require the same care as other files containing private game information.

RETAINED FROM 0.4.0

- Separate BCC and LSCG isolation, with BCC isolated by default. This also stops
  incoming BCC storage from driving new controller/reflection metadata behavior.
- Panic: an opaque page curtain, incoming communication/interaction pause,
  native audio/notification hooks, and reversible known-media muting.
- Muted packets are rejected before Socket.IO buffering, so resuming does not
  replay messages received during Panic. Connection/room lifecycle continues.
- Fullscreen exit, inert background, focus containment, and handling of another
  addon's modal dialog/popover without closing that addon's window.
- Compact menu, collapsible advanced settings, and Made By Kiki #72385 credit.
- Stronger BCC spell validation when BCC isolation is OFF: known effects/icons,
  safe parameter types, nested gift templates capped at depth 2, and bounded
  LZString outfit decoding. Malformed outfits cannot reach the BCC JSON parser.
- BCC-Audit.html covers the public BCC 2.0.0–2.2.3 history, every functional
  module, old/new behavior, actual protection and unavoidable public-data copying.

Retained: recipient-only roles, caster binding, blocked unsafe relays, target
checks, native item/lock validation, bounded appearance restoration, narrow
R132 mask recovery, private bounded logs and early Socket.IO filtering.

PANIC BUTTON

Tap Panic in the menu. The game, chat and page addon interfaces disappear behind
an opaque curtain; keyboard input stays on Resume. All incoming chat (including
Hidden addon packets and self echoes), beeps and game-action messages are dropped
before game/addon listeners. Foreign interactions with your appearance are denied.
Room/account/connection lifecycle remains available; this does NOT leave the room,
log out, hide your online presence or conceal your avatar from other players.

Panic blocks new native sound/notification calls and mutes page audio/video plus
known native AudioDialog/AudioBackgroundMusic elements, restoring their previous
mute state on Resume. Existing private WebAudio contexts or detached audio owned
by independent addons, and operating-system notifications already shown, are not
universally controllable by this page script. Use browser/device mute if absolute
silence is required. No AudioContext/Image/WebGL prototype patch is installed.

Resume restores the page and settings. There is no replay of packets received
during Panic. Earlier chat remains in the game's history. Panic itself sends no
chat announcement; existing appearance restoration may still send bounded normal
updates. It does not cancel already accepted spell timers or other local addons.
Panic is temporary per-tab state and is not kept after a page reload.

PERMISSIONS AND COVERAGE

BC rules follows AllowedInteractions (legacy ItemPermission fallback):
0 / 1: everyone except your blocked/ghosted players.
2: owner, lovers, whitelist, or native dominance threshold.
3: owner, lovers or whitelist.
4: owner or lovers.
5: owner.

Whitelist requires your whitelist IN ADDITION to the above permissions.
No one refuses incoming interactions in the protected channels.
Ordinary chat from nonblocked players remains available in both modes.
Your friends list is not automatically a BC whitelist. BCC's separate Friend
role and BC's script-property friend permissions still have their own meaning.

Path                         Handling
---------------------------  -----------------------------------------------
Direct wardrobe/clothing     Own SyncItem / SyncSingle / SyncCharacter updates
and restraints               require interaction permission. Native BC body,
                             cosplay, blocked/limited item and lock validation
                             remains in the receiving path.
Full room snapshots          Preserve this tab's accepted appearance and pose;
                             retain room membership and relationship metadata.
Activity / Action            Current and legacy target dictionaries are checked
                             using the authenticated outer sender.
Hidden commands              Require interaction permission, with narrow known
                             metadata/communication exceptions.
BCC spells                   Default: blocked. If enabled: BC access, own effect
                             roles and bounded per-effect payload validation.
BCC active control           Requires the active caster and current permissions.
BCC control claims           Require an observed local cast in this room/session.
LSCG commands/broadcasts      Check sender, target, command shape and BC access;
                             the addon's own additional checks still apply.
Structured Leash beeps       LSCG commands checked; unknown BCC request protocols
                             remain isolated in the audited BCC version.
KikiLink                     Chat/presence frames pass; your blacklist/ghostlist
                             still apply to room and beep transport.
BCX                          Metadata/read requests pass; edits and remote
                             command requests additionally require BC access.
Game envelopes               Check blocked senders; gate targeted LARP/MagicBattle
                             actions, KD/bounty and unknown game commands.
                             ClubCard keeps its own participant/spectator checks.
Other characters             Their appearance/pose sync and room lifecycle stay
                             available. Your account/relationship server events
                             are not rewritten to fake ownership or membership.

INTENTIONAL COMPATIBILITY LIMITS

BCC AnimaFurta changeAppearance and publishAction are blocked even from a
trusted active caster: those branches misattribute authority or relay arbitrary
packets as the recipient. Use ordinary BC wardrobe/actions instead.
BCC control claims after a reload or room change may require a new local cast.
Unknown BCC command variants and generic BCC requests are not automatically trusted.
Authorized LSCG commands still depend on the addon's own module/consent settings.
Unknown hidden commands require BC interaction access, so a module that grants
broader remote access than your BC settings can lose that remote feature.

Selected addon isolation blocks commands and metadata even from trusted players.
Strict hidden-message filter can interrupt native features, KikiLink, BCX and
other addon communication. BCC is isolated by default; LSCG is not.

Spell limits: compressed outfits up to 8,192 characters, decoded JSON up to
262,144 characters, up to 256 appearance entries, gift nesting depth 2. These
are intentional bounds, not unrestricted acceptance of every custom payload.
Only the audited 12 effect IDs and 22 spell icons are accepted. Native BCC
validation still applies after these checks when a command is permitted.

RESTORE APPEARANCE

A refused appearance change can schedule a restore of your current accepted
outfit: coalesced for 350 ms, at most 3 updates in 30 seconds. Only your own
character is passed to the normal game update function. The limiter recovers
after its cooldown. A restore is cancelled if the account/room changes, the
connection is gone, or restoration was switched off.

This is not an atomic server transaction. Other clients can temporarily see a
server-accepted change before your correction. If repeated attacks exhaust the
restore limit, leaving the room stops relying on an exhausted local correction.

THE GRAPHICS ERROR

The reproduced error is the R132 alpha-mask loader uploading a tainted canvas
to WebGL. An image from another origin without the required CORS permission can
cause this. The submitted stack does not identify the exact image URL or prove
which addon supplied it. BC Feather's reviewed mask patch touches cache usage;
its presence in the stack alone does not establish fault.

Recover image masks is on by default. A low-priority ModSDK hook runs after the
reviewed BCC/Echo URL mappings, immediately before the patched native loader.
It checks cached mask images, skips only unsafe layers and attempts one anonymous
CORS reload of an already-used HTTP(S) image URL. A successful clean image replaces
only the matching cache entry and triggers native character image invalidation.
Healthy mask layers and BC Feather's patch remain in the chain.

A host that does not allow CORS cannot be fixed by a userscript on the game page.
Its unsafe mask is omitted and may look different. No browser security setting,
proxy or credential workaround is used. Retries are bounded: at most 8 pending
and 128 distinct URLs per page, one attempt per URL, with a 12-second timeout.
No URLs or image contents are written to the activity log.

Only the mask-upload SecurityError has a recovery path. Unrelated exceptions
continue to the normal error reporter. KikiShield does not hide global errors,
unhandled promises, change global Image/WebGL prototypes, or remove addon hooks.
The filter does not depend on ModSDK; mask recovery and local-cast observation do.
If the renderer signature is unsupported, the menu says recovery is unavailable.

ACTIVITY / PRIVACY

Tap an Activity entry to expand it. It shows the command or action, the sender's
server-attributed member number when available, target, channel, blocking reason,
severity explanation, retained incoming packet and automatic-action result.
Known command arguments appear as text, never executable HTML. The packet is a
serialized snapshot of the received data; encoded fields remain encoded.

Severity      Meaning
------------  ---------------------------------------------------------------
Serious       A recognized direct operation was rejected by your permissions,
              lists or a covered unsafe-relay rule. This is evidence of the
              operation, not proof of the sender's intent.
Caution       An isolated, unknown, malformed or incompletely assessed command.
              Addon isolation alone does not establish a permission bypass.
Background    Routine synchronization, unchanged items, another target, muted
              events or other traffic without a verified direct violation.
System        KikiShield diagnostics, such as restoration or graphics recovery.

Native item and direct appearance updates count as serious only when a meaningful
change to your character can be established. Full room snapshots and relationship
synchronization never justify an automatic violation action. LSCG broadcasts with
another or unspecified target are not treated as direct attempts against you.
Unknown commands can be blocked without being counted as serious violations.

Up to 100 records are held in memory in this tab. Identical recent events may be
combined; different commands and retained payloads remain separate. Each retained
payload is capped at 64 KiB of UTF-8 text, with a 1 MiB total payload budget. Older
records are removed when either limit is reached. Truncated or omitted payloads
are explicitly marked; a truncated payload is not a complete packet or valid JSON.
Malformed unidentified envelopes and unsafe data may be omitted entirely.

Ordinary chat and Panic contents are not retained. Command packets can still
contain private text, spell arguments, settings, outfits or embedded URLs. Graphics
recovery does not put image URLs or image contents in the log. Inspect all retained
details and member IDs before sharing an Export JSON file. No log is uploaded
automatically or saved with preferences. Reloading or changing account clears it.

Clear removes the records and cancels queued automatic actions without resetting
session counters or reversing completed list changes. Undo is available only from
a retained entry, so clear the log after reviewing any changes you may want to undo.
Preferences are local per account and game domain.

AUTOMATIC BLACKLIST / GHOSTLIST

Open Automation. Choose Off, Blacklist, or Ghost + blacklist.
Off is the default. BC's native GhostList add also adds BlackList and removes a
whitelist entry; a native blacklist add removes a whitelist entry as well. These
are real saved BC list changes, not temporary KikiShield-only filters.

Rule                         Default   Behavior
---------------------------  --------  ---------------------------------------
Serious blocked attempts     ON        When automation is enabled, acts after
                                       1, 2 or 3 qualifying events by the same
                                       sender within 60 seconds. Default: 1.
Observed BCC use              OFF       Acts on the first recognized BCC protocol
                                       event, including routine metadata.
Observed LSCG use             OFF       Acts on the first recognized LSCG protocol
                                       event, including routine metadata.
Protect trusted people       ON        Excludes your owner, lovers, whitelist
                                       and friends from automatic list changes.
Member-ID exceptions         Empty     Up to 100 explicitly excluded numeric IDs.

Observed traffic is not definitive proof that a particular addon is installed,
and addon use is not an attack. Silent users cannot be detected. The presence rules
are separate from the serious-attempt threshold: enabling either can act on routine
metadata even if Block BCC or Block LSCG is OFF. They do not sweep existing room
members or infer addon use from a nickname, chat text or somebody else's claims.

Only a verified outer sender who is still in the current room can be selected.
The shield never automatically lists your own account. Trusted-person checks wait
for the required relationship lists to be available; unknown relationships are
not treated as permission to act. Exceptions and trusted-person exclusions affect
automatic list changes only: the incoming protection checks remain active.

Actions are queued outside packet handling and rechecked against the current
account, room, connection, settings, list state and exemptions before BC's own
list API is called. Settings changes cancel queued actions and reset accumulated
serious-attempt counts. Panic, disconnects, room/account changes and an unavailable
native list API prevent queued actions from applying. No custom list packet is sent.

At most 5 automatic member actions may apply in one minute and 50 in one session.
The queue holds at most 20 distinct members. Events exceeding a rate/session limit
are skipped, not held for a later batch. After the minute cooldown, a new qualifying
event is required. Reloading resets session state. Check the Activity result for
skips, exceptions, partial native changes or an unavailable API. These limits affect
automation only; they do not allow an otherwise blocked incoming action through.

An applied action offers Undo in its expanded Activity entry. Undo runs only for
the same account when that member's blacklist, ghostlist and whitelist membership
still match the recorded post-action state. It restores the memberships changed by
that action, including a pre-existing blacklist entry that native ghost removal
would otherwise remove, or a whitelist entry removed by the add. If the list state
has changed, it skips rollback rather than overwriting the current state. A native
API failure or partial update is reported for manual review. Undo does not reset
automation counters. Reloading, account changes or clearing/evicting the entry makes
its Undo unavailable; completed native list changes remain until you remove them.

The icon is embedded. There are no remote code imports, analytics, external
fonts or automatic updates. Image recovery can retry existing image URLs; outfit
restoration uses the game's existing connection. Neither sends telemetry.
The page API is read-only: KikiShield.status() and KikiShield.getLog().

BOUNDARIES

This is protection in one tab, not a promise of perfect security or universal
compatibility. It relies on authentic server Sender / Source / SourceMemberNumber.
It cannot stop someone opening wardrobe in THEIR modified client, cloning or exporting outfits, inspecting
already public appearance or taking screenshots. It can reject incoming changes
through the audited paths; it cannot make public appearance private.

A local BCC installation can publish qam.cloneBackup, Masquerada lastOutfit,
spell libraries and settings in its outgoing storage. KikiShield's incoming
switch does not suppress that publication or retract copies already received.

It does not prevent room administrator actions, network denial of service,
server compromise, or malicious code already installed in the same page.
It does not undo earlier spells, timers or saved effects. A command already
accepted before a permission change can have effects scheduled inside its addon.
Use one game tab: preserving this tab's appearance in snapshots can conflict
with synchronizing one account across tabs/devices.

Ordinary chat/emote text triggers in other addons, unknown/future protocols,
unavailable private BCC 1.x code and every module of every installed addon have
not been exhaustively secured. Native item-validation tests establish that
KikiShield leaves those rules intact; they do not prove every local addon uses
the native validator when applying its own accepted effects.

VERIFICATION

0.6.0: 187 Node regression tests and 13 Node DOM interface regression groups
passed. These include the actual R132 list updater and tests for false positives,
sender attribution, payload retention limits, trusted exclusions and guarded Undo.
The interface checks include unread-count lifecycle, three-tab navigation and
closing Activity before a deferred event paint. They used LinkeDOM; no browser
layout engine was run for 0.6.0. The cloud browser cannot open the local fixture.

The previous 0.4.0 release passed 116 Node regression tests, including real source
handlers and 1,800 bounded malformed-wire cases inside one test, plus 44 Chromium
UI checks and 16 real WebGL/CORS checks. Those historical counts do not certify the
new Activity/automation features. See VERIFICATION.txt and tests/*-results.json for
the final release results.
No live player or game account was used. Firefox Android, the userscript manager
and the entire installed addon pack were not exercised end to end.

Quick local tests with Node 24:
  node --test tests/policy.test.cjs tests/hardening.test.cjs tests/panic.test.cjs

Source-based tests require the audited source workspace in KIKISHIELD_UPSTREAM:
  KIKISHIELD_UPSTREAM=/path/to/audit node --test tests/*.test.cjs

Browser tests additionally require Playwright and Chromium with WebGL2 support:
  KIKISHIELD_UPSTREAM=/path/to/audit KIKISHIELD_CHROMIUM=/path/to/chromium node tests/browser.cjs
  KIKISHIELD_UPSTREAM=/path/to/audit KIKISHIELD_CHROMIUM=/path/to/chromium node tests/render.browser.cjs

New DOM simulation (optional linkedom package; no browser required):
  KIKISHIELD_DOM_MODULES=/path/to/node_modules node --test tests/activity-dom.cjs tests/unread-dom.cjs
The downloadable KikiShield-0.6.0.zip contains these test sources and results.

tests/SOURCE-MANIFEST.json identifies the upstream files/revisions. Audit sources
and browser binaries are not bundled; the standalone policy tests need neither.
The UI fixture blocks external requests. The rendering fixture uses two loopback
HTTP servers to exercise real CORS, with external requests blocked.

KikiShield code is MIT; see LICENSE.txt. The supplied icon is embedded unchanged.
assets/launcher.jpg contains the original image bytes.
