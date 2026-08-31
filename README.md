<h1 align="center">zmux</h1>
<p align="center">A Ghostty-based macOS terminal with vertical tabs and notifications for AI coding agents</p>

zmux 是 [cmux](https://github.com/manaflow-ai/cmux) 的独立分叉。它使用自己的 App、签名、回调、Keychain、状态、Socket 和通知命名空间，可以与 cmux 同时运行而不共享产品身份。

此分发版本面向个人 Apple Developer 会员。稳定版 DMG 仅由维护者在本机完成 Developer ID 签名和 Apple 公证，不通过 GitHub Actions 发布，也不提供自动更新。发布产物不包含内置浏览器或原生 Passkey/安全密钥桥接，并且不会复用 cmux 的签名凭据。

<p align="center">
  English | <a href="README.ja.md">日本語</a> | <a href="README.vi.md">Tiếng Việt</a> | <a href="README.zh-CN.md">简体中文</a> | <a href="README.zh-TW.md">繁體中文</a> | <a href="README.ko.md">한국어</a> | <a href="README.de.md">Deutsch</a> | <a href="README.es.md">Español</a> | <a href="README.fr.md">Français</a> | <a href="README.it.md">Italiano</a> | <a href="README.da.md">Dansk</a> | <a href="README.pl.md">Polski</a> | <a href="README.ru.md">Русский</a> | <a href="README.bs.md">Bosanski</a> | <a href="README.ar.md">العربية</a> | <a href="README.no.md">Norsk</a> | <a href="README.pt-BR.md">Português (Brasil)</a> | <a href="README.th.md">ไทย</a> | <a href="README.tr.md">Türkçe</a> | <a href="README.km.md">ភាសាខ្មែរ</a> | <a href="README.uk.md">Українська</a>
</p>

<p align="center">
  <a href="https://x.com/manaflowai"><img src="https://img.shields.io/badge/@manaflow-555?logo=x" alt="X / Twitter" /></a>
  <a href="https://discord.gg/xsgFEVrWCZ"><img src="https://img.shields.io/badge/Discord-555?logo=discord" alt="Discord" /></a>
  <a href="https://github.com/manaflow-ai/cmux"><img src="https://img.shields.io/github/stars/manaflow-ai/cmux?style=flat&logo=github&label=stars&color=4c71f2" alt="GitHub stars" /></a>
</p>

<p align="center">
  <img src="./docs/assets/main-first-image.png" alt="cmux screenshot" width="900" />
</p>

<p align="center">
  <a href="https://www.youtube.com/watch?v=i-WxO5YUTOs">▶ Demo video</a> · <a href="https://cmux.com/blog/zen-of-cmux">The Zen of cmux</a>
</p>

## Features

<table>
<tr>
<td width="40%" valign="middle">
<h3>Notification rings</h3>
Panes get a blue ring and tabs light up when coding agents need your attention
</td>
<td width="60%">
<img src="./docs/assets/notification-rings.png" alt="Notification rings" width="100%" />
</td>
</tr>
<tr>
<td width="40%" valign="middle">
<h3>Notification panel</h3>
See all pending notifications in one place, jump to the most recent unread
</td>
<td width="60%">
<img src="./docs/assets/sidebar-notification-badge.png" alt="Sidebar notification badge" width="100%" />
</td>
</tr>
<tr>
<td width="40%" valign="middle">
<h3>Vertical + horizontal tabs</h3>
Sidebar shows git branch, linked PR status/number, working directory, listening ports, and latest notification text. Split horizontally and vertically.
</td>
<td width="60%">
<img src="./docs/assets/vertical-horizontal-tabs-and-splits.png" alt="Vertical tabs and split panes" width="100%" />
</td>
</tr>
<tr>
<td width="40%" valign="middle">
<h3>SSH</h3>
<code>cmux ssh user@remote</code> creates a workspace for a remote machine. Pass <code>--command 'omp "investigate auth"'</code> to run an initial command once in its first remote terminal. Browser panes route through the remote network so localhost just works. Drag an image into a remote session to upload via scp.
</td>
<td width="60%">
<img src="./docs/assets/ssh.png" alt="cmux SSH" width="100%" />
</td>
</tr>
<tr>
<td width="40%" valign="middle">
<h3>Claude Code Teams</h3>
<code>cmux claude-teams</code> runs Claude Code's teammate mode with one command. Teammates spawn as native splits with sidebar metadata and notifications. No tmux required.
</td>
<td width="60%">
<img src="./docs/assets/claude-code-teams.png" alt="Claude Code Teams" width="100%" />
</td>
</tr>
</table>

- **Browser import** — Import cookies, history, and sessions from Chrome, Firefox, Arc, and 20+ browsers so browser panes start authenticated
- **Custom commands** — Define project-specific actions in [`cmux.json`](https://cmux.com/docs/custom-commands) that launch from the command palette
- **Programmable** — CLI and socket API to create workspaces, split panes, send keystrokes, and inspect terminals
- **Native macOS app** — Built with Swift and AppKit, not Electron. Fast startup, low memory.
- **Ghostty compatible** — Reads your existing `~/.config/ghostty/config` for themes, fonts, and colors
- **GPU-accelerated** — Powered by libghostty for smooth rendering
- **Keyboard shortcuts** — Extensive shortcuts for workspaces, splits, terminals, and notifications
- **Open source** — Free and GPL-licensed

## Install

### DMG（推荐）

从维护者处获取已经签名和公证的 `zmux-X.Y.Z.dmg`，并用同目录的
`zmux-X.Y.Z.sha256` 校验文件。打开 DMG 后，将 `zmux.app` 拖入“应用程序”。

本项目不再通过 GitHub Release、Homebrew 或 Sparkle 分发更新。升级时请获取维护者手动提供的新 DMG；首次启动时，macOS 会显示已识别开发者确认提示。

## Why cmux?

I run a lot of Claude Code and Codex sessions in parallel. I was using Ghostty with a bunch of split panes, and relying on native macOS notifications to know when an agent needed me. But Claude Code's notification body is always just "Claude is waiting for your input" with no context, and with enough tabs open I couldn't even read the titles anymore.

I tried a few coding orchestrators but most of them were Electron/Tauri apps and the performance bugged me. I also just prefer the terminal since GUI orchestrators lock you into their workflow. So I built cmux as a native macOS app in Swift/AppKit. It uses libghostty for terminal rendering and reads your existing Ghostty config for themes, fonts, and colors.

The main additions are the sidebar and notification system. The sidebar has vertical tabs that show git branch, linked PR status/number, working directory, listening ports, and the latest notification text for each workspace. The notification system picks up terminal sequences (OSC 9/99/777) and has a CLI (`cmux notify`) you can wire into agent hooks for Claude Code, OpenCode, etc. When an agent is waiting, its pane gets a blue ring and the tab lights up in the sidebar, so I can tell which one needs me across splits and tabs. Cmd+Shift+U jumps to the most recent unread.

Terminal and workspace operations are scriptable through the CLI and socket API — create workspaces/tabs, split panes, send keystrokes, and inspect terminal state.

## The Zen of cmux

cmux is not prescriptive about how developers hold their tools. Public zmux keeps the terminal, workspace, notification, and CLI parts of that model.

zmux is a primitive, not a solution. It gives you terminals, notifications, workspaces, splits, tabs, and a CLI to control them without forcing an agent workflow.

The best developers have always built their own tools. Nobody has figured out the best way to work with agents yet, and the teams building closed products definitely haven't either. The developers closest to their own codebases will figure it out first.

Give a million developers composable primitives and they'll collectively find the most efficient workflows faster than any product team could design top-down.

## Documentation

For more info on how to configure cmux, [head over to our docs](https://cmux.com/docs/getting-started?utm_source=readme).

## Keyboard Shortcuts

### Workspaces

| Shortcut | Action |
|----------|--------|
| ⌘ N | New workspace |
| ⌘ 1–8 | Jump to workspace 1–8 |
| ⌘ 9 | Jump to last workspace |
| ⌃ ⌘ ] | Next workspace |
| ⌃ ⌘ [ | Previous workspace |
| ⌘ ⇧ W | Close workspace |
| ⌘ ⇧ R | Rename workspace |
| ⌥ ⌘ E | Edit workspace description |
| ⌘ B | Toggle sidebar |
| ⌥ ⌘ B | Toggle right sidebar |
| ⌘ ⇧ E | Toggle right sidebar focus |

### Surfaces

| Shortcut | Action |
|----------|--------|
| ⌘ T | New surface |
| ⌘ ⇧ ] | Next surface |
| ⌘ ⇧ [ | Previous surface |
| ⌃ Tab | Next surface |
| ⌃ ⇧ Tab | Previous surface |
| ⌃ 1–8 | Jump to surface 1–8 |
| ⌃ 9 | Jump to last surface |
| ⌘ W | Close surface |

### Split Panes

| Shortcut | Action |
|----------|--------|
| ⌘ D | Split right |
| ⌘ ⇧ D | Split down |
| ⌥ ⌘ ← → ↑ ↓ | Focus pane directionally |
| ⌘ ⇧ H | Flash focused panel |

### Browser

Browser developer-tool shortcuts follow Safari defaults and are customizable in `Settings → Keyboard Shortcuts`.
Command palette navigation shortcuts, including ⌃ P, are also customizable and can be cleared so the keypress reaches the active terminal.

| Shortcut | Action |
|----------|--------|
| ⌘ ⇧ L | Open browser in split |
| ⌘ L | Focus address bar |
| ⌘ [ | Back |
| ⌘ ] | Forward |
| ⌘ R | Reload page |
| ⌥ ⌘ I | Toggle Developer Tools (Safari default) |
| ⌥ ⌘ C | Show JavaScript Console (Safari default) |

### Notifications

| Shortcut | Action |
|----------|--------|
| ⌘ I | Show notifications panel |
| ⌘ ⇧ U | Jump to latest unread |
| ⌥ ⌘ U | Toggle current item unread state |
| ⌃ ⌘ U | Mark current item as oldest unread and jump to next latest unread |

### Find

| Shortcut | Action |
|----------|--------|
| ⌘ F | Find |
| ⌘ ⇧ F | Find in directory |
| ⌘ G / ⌥ ⌘ G | Find next / previous |
| ⌥ ⌘ ⇧ F | Hide find bar |
| ⌘ E | Use selection for find |

### Terminal

| Shortcut | Action |
|----------|--------|
| ⌘ K | Clear scrollback |
| ⌘ C | Copy (with selection) |
| ⌘ V | Paste |
| ⌘ + / ⌘ - | Increase / decrease font size |
| ⌘ 0 | Reset font size |

### Window

| Shortcut | Action |
|----------|--------|
| ⌘ ⇧ N | New window |
| ⌘ ⇧ O | Reopen previous session |
| ⌘ , | Settings |
| ⌘ ⇧ , | Reload configuration |
| ⌘ Q | Quit |

## Session restore

Quitting cmux saves the current session. On relaunch, cmux restores app-owned
state:
- Window/workspace/pane layout
- Working directories
- Terminal scrollback (best effort)

cmux does not checkpoint arbitrary live process state. tmux, vim, shells, and
unsupported terminal apps reopen as normal terminals.

Supported agent sessions can resume when hooks have saved a native session ID.
Install hooks after installing the agent CLI so its binary is on `PATH`:

```bash
cmux hooks setup
cmux hooks setup codex
cmux hooks setup --agent opencode
```

`cmux hooks setup` installs supported agents it can find and prints a summary
for skipped agents. Supported resume integrations include Claude Code, Codex,
Grok, OpenCode, Pi, Amp, Cursor CLI, Gemini, Rovo Dev, Copilot, CodeBuddy,
Factory, and Qoder. Claude Code is handled by the cmux Claude wrapper when Claude
integration is enabled in Settings.

Advanced users and integrations can attach a custom resume command to the
current terminal surface. This is useful for tools with their own durable state,
such as tmux sessions or custom agent CLIs:

```bash
cmux surface resume set --kind tmux --checkpoint work --shell "tmux attach -t work"
cmux surface resume show --json
cmux surface resume clear --checkpoint work
```

The binding stays attached to the cmux surface. Public CLI or socket-created
bindings are stored for inspection and manual restore unless you approve a
signed command prefix for automatic restore. Approved prefixes are also bound to
the working directory and exact environment values, when present. Review or edit
approvals in **Settings > Terminal > Resume Commands**. cmux only auto-runs
resume bindings it marks trusted, such as live process-detected tmux bindings or
user-approved prefixes. Sensitive environment keys such as tokens, passwords,
secrets, and API keys are dropped before a resume binding is stored.

To keep restored agent terminals idle instead of automatically running their resume commands,
turn off **Settings > Terminal > Resume Agent Sessions on Reopen** or set this in
`~/.config/cmux/cmux.json`:

```json
{
  "terminal": {
    "autoResumeAgentSessions": false
  }
}
```

This only disables automatic agent resume commands. cmux still restores the saved layout,
working directories, scrollback, and browser history.

If you need to reapply the last saved snapshot manually, use:
- `File > Reopen Previous Session`
- `⌘ ⇧ O`
- `cmux restore-session`

Under the hood, cmux writes a versioned snapshot under
`~/Library/Application Support/cmux/` and agent hooks write session mappings
under `~/.cmuxterm/`. On restore, cmux rebuilds the layout first, then runs the
supported agent's native resume command when automatic agent resume is enabled.

Read the full guide at <https://cmux.com/docs/session-restore>.

## FAQ

### How does cmux relate to Ghostty?

cmux is not a fork of Ghostty. It uses [libghostty](https://github.com/ghostty-org/ghostty) as a library for terminal rendering, the same way apps use WebKit for web views. Ghostty is a standalone terminal; cmux is a different app built on top of its rendering engine.

### What platforms does it support?

macOS only, for now. cmux is a native Swift + AppKit app.

### Is there an iOS app?

Yes, in beta. Pair your iPhone with your Mac from the Mobile Connect window and attach to your terminals from your phone, with optional forwarding of terminal notifications. It ships on TestFlight as cmux BETA. Early access is included with [cmux Founders Edition](https://github.com/manaflow-ai/cmux#founders-edition). See the [iOS docs](https://cmux.com/docs/ios).

### What coding agents does cmux work with?

All of them. cmux is a terminal, so any agent that runs in a terminal works out of the box: Claude Code, Codex, OpenCode, Gemini CLI, Kiro, Aider, Goose, Amp, Cline, Cursor Agent, and anything else you can launch from the command line.

### Can cmux orchestrate multiple agents and subagents?

Yes. When an agent spawns subagents or teammates, cmux turns them into native panes and splits instead of hidden background processes. It supports [Claude Code teams](https://cmux.com/docs/agent-integrations/claude-code-teams) and [oh-my-opencode](https://cmux.com/docs/agent-integrations/oh-my-opencode) multi-model orchestration, so every agent in a run is visible and controllable.

### Can I use cmux with remote machines?

Yes. Open workspaces over SSH and attach to remote tmux sessions, so agents can run on a remote host while you drive them from cmux. See [SSH and remote](https://cmux.com/docs/ssh).

### How do notifications work?

When a process needs attention, cmux shows notification rings around panes, unread badges in the sidebar, a notification popover, and a macOS desktop notification. These fire automatically via standard terminal escape sequences (OSC 9/99/777), or you can trigger them with the [cmux CLI](https://cmux.com/docs/notifications#cli-usage) and [agent hooks](https://cmux.com/docs/notifications#integration-examples). Any agent that supports hooks or OSC works, including Claude Code, Codex, OpenCode, and pi.

### Is cmux programmable?

Yes. Terminal and workspace actions are available through the zmux CLI and Unix socket: create workspaces, open split panes, send input, read screen contents, and take screenshots.

### Why is the embedded browser unavailable?

Public zmux builds target personal Apple Developer distribution. They remove the managed WebAuthn entitlement and native Passkey bridge, disable every embedded-browser entry point, and leave web links and account sign-in to the system default browser. The authentication callback remains the product-owned `zmux://auth-callback` scheme.

### Does cmux have skills?

Yes. Skills are reusable workflows you can give any agent running in zmux for CLI control, workspace automation, and settings. The upstream [cmux-skills](https://github.com/manaflow-ai/cmux-skills) collection may describe browser surfaces that are not shipped by public zmux builds.

### Can I customize keyboard shortcuts?

Terminal keybindings are read from your Ghostty config file (`~/.config/ghostty/config`). zmux-specific shortcuts for workspaces, splits, and notifications can be customized in Settings.

### Can I customize cmux?

Yes. Terminal rendering uses your Ghostty config, so themes, fonts, colors, and cursor carry over directly. cmux's own settings in `~/.config/cmux/cmux.json` control the sidebar, tab bar, split panes, and behavior, and every [keyboard shortcut](https://cmux.com/docs/keyboard-shortcuts) is editable. See [configuration](https://cmux.com/docs/configuration).

### Are my sessions saved?

Yes. cmux restores your windows, workspaces, panes, working directories, and scrollback when you relaunch, and the state survives a full computer restart, not just quitting the app. Agent sessions like Claude Code, Codex, and OpenCode come back too. See [session restore](https://cmux.com/docs/session-restore).

### How does it compare to tmux?

tmux is a terminal multiplexer that runs inside any terminal. zmux is a native macOS app with vertical tabs, split panes, notifications, and a socket API. It can also be used together with SSH and tmux.

### Is cmux free?

Yes, cmux is free to use. The source code is available on [GitHub](https://github.com/manaflow-ai/cmux).

### How can I support cmux?

cmux is free and open source, and always will be. If you want to back development and get early access to what's next, including cmux AI, the iOS app, and Cloud VMs, check out [cmux Founders Edition](https://github.com/manaflow-ai/cmux#founders-edition).

### I have a feature request or found a bug?

Open an [issue](../../issues) or pull request in this fork. Use the upstream trackers only for behavior reproduced in the original cmux project.

## Star History

<a href="https://www.star-history.com/?repos=manaflow-ai%2Fcmux&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=manaflow-ai/cmux&type=date&theme=dark&legend=top-left&sealed_token=N5E-Mdh7zIesE2fP9_q8wEZyOg3un2Ki7u61afJnUUu6ZIUEUsrH_dsPrA8CWrw12owIEezjOyhDiXcfIEoSzAlIybOqvxTk-xCpuXbpnFk86SkJzfErObW1u0MrAuLp-_tXZDM1kAMI2jMtAeXZK3_VEe2HH9dNyhXxgMTCns6c7lMmCJ_kSIgtooYf" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=manaflow-ai/cmux&type=date&legend=top-left&sealed_token=N5E-Mdh7zIesE2fP9_q8wEZyOg3un2Ki7u61afJnUUu6ZIUEUsrH_dsPrA8CWrw12owIEezjOyhDiXcfIEoSzAlIybOqvxTk-xCpuXbpnFk86SkJzfErObW1u0MrAuLp-_tXZDM1kAMI2jMtAeXZK3_VEe2HH9dNyhXxgMTCns6c7lMmCJ_kSIgtooYf" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=manaflow-ai/cmux&type=date&legend=top-left&sealed_token=N5E-Mdh7zIesE2fP9_q8wEZyOg3un2Ki7u61afJnUUu6ZIUEUsrH_dsPrA8CWrw12owIEezjOyhDiXcfIEoSzAlIybOqvxTk-xCpuXbpnFk86SkJzfErObW1u0MrAuLp-_tXZDM1kAMI2jMtAeXZK3_VEe2HH9dNyhXxgMTCns6c7lMmCJ_kSIgtooYf" />
 </picture>
</a>

## Contributing

Ways to get involved:

- Follow us on X for updates [@manaflowai](https://x.com/manaflowai), [@lawrencecchen](https://x.com/lawrencecchen), and [@austinywang](https://x.com/austinywang)
- Join the conversation on [Discord](https://discord.gg/xsgFEVrWCZ)
- Create and participate in [GitHub issues](https://github.com/manaflow-ai/cmux/issues) and [discussions](https://github.com/manaflow-ai/cmux/discussions)
- Let us know what you're building with cmux

## Community

- [Discord](https://discord.gg/xsgFEVrWCZ)
- [WhatsApp](https://chat.whatsapp.com/Fblh7FB58lOI2cx6ccdIqY?mode=gi_t)
- [GitHub](https://github.com/manaflow-ai/cmux)
- [X / Twitter](https://twitter.com/manaflowai)
- [YouTube](https://www.youtube.com/channel/UCAa89_j-TWkrXfk9A3CbASw)
- [LinkedIn](https://www.linkedin.com/company/manaflow-ai/)
- [Reddit](https://www.reddit.com/r/cmux/)

<p>
  <strong>WeChat:</strong> Scan the QR code to join the community.<br />
  <img src="./docs/assets/wechat-community-qr.jpg" alt="WeChat QR code to join the cmux community" width="240" />
</p>

## Founder's Edition

cmux is free, open source, and always will be. If you'd like to support development and get early access to what's coming next:

**[Get Founder's Edition](https://buy.stripe.com/3cI00j2Ld0it5OU33r5EY0q)**

- **Prioritized feature requests/bug fixes**
- **Early access: cmux AI that gives you context on every workspace, tab and panel**
- **Early access: iOS app with terminals synced between desktop and phone**
- **Early access: Cloud VMs**
- **Early access: Voice mode**
- **My personal iMessage/WhatsApp**

## License

zmux is distributed under [GPL-3.0-or-later](LICENSE), with upstream and third-party copyright notices retained. Source changes corresponding to distributed binaries must remain available to recipients under the license. Any commercial terms offered by Manaflow apply only to rights Manaflow controls and do not replace the obligations of this independently distributed fork.
