KikiShield 0.4.0

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
Tap the round icon for Protection / Activity; drag it to move it.
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

WHAT CHANGED IN 0.4.0

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

Use BC permissions follows AllowedInteractions (legacy ItemPermission fallback):
0 / 1: everyone except your blocked/ghosted players.
2: owner, lovers, whitelist, or native dominance threshold.
3: owner, lovers or whitelist.
4: owner or lovers.
5: owner.

Whitelist only requires your whitelist IN ADDITION to the above permissions.
Block interactions refuses incoming interactions in the protected channels.
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

Activity contains at most 100 in-memory records, combining repeated events.
It records time, channel, reason, member number and count, not packet contents,
chat text, spell arguments, outfits or image URLs. Export produces JSON; Clear
removes records without resetting the session counters. Review member numbers
before sharing an export. Preferences are local per account and game domain.

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

116 Node regression tests passed, including real source handlers and 1,800 bounded
malformed-wire cases inside one test. 44 Chromium UI checks and 16 real WebGL/CORS
checks passed. See VERIFICATION.txt and tests/*-results.json.
No live player or game account was used. Firefox Android, the userscript manager
and the entire installed addon pack were not exercised end to end.

Quick local tests with Node 24:
  node --test tests/policy.test.cjs tests/hardening.test.cjs tests/panic.test.cjs

Source-based tests require the audited source workspace in KIKISHIELD_UPSTREAM:
  KIKISHIELD_UPSTREAM=/path/to/audit node --test tests/*.test.cjs

Browser tests additionally require Playwright and Chromium with WebGL2 support:
  KIKISHIELD_UPSTREAM=/path/to/audit KIKISHIELD_CHROMIUM=/path/to/chromium node tests/browser.cjs
  KIKISHIELD_UPSTREAM=/path/to/audit KIKISHIELD_CHROMIUM=/path/to/chromium node tests/render.browser.cjs

tests/SOURCE-MANIFEST.json identifies the upstream files/revisions. Audit sources
and browser binaries are not bundled; the standalone policy tests need neither.
The UI fixture blocks external requests. The rendering fixture uses two loopback
HTTP servers to exercise real CORS, with external requests blocked.

KikiShield code is MIT; see LICENSE.txt. The supplied icon is embedded unchanged.
assets/launcher.jpg contains the original image bytes.
