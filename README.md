# Swifty's MacOS setup

Resources:
Article about how to run: https://irving-swift.com/setup-your-mac-with-ansible/

## How to run

On a fresh Mac (Apple Silicon only, since every path assumes Homebrew lives in `/opt/homebrew`):

```
$ bin/bootstrap
```

`bin/bootstrap` installs the Xcode Command Line Tools, Homebrew and Ansible (via Homebrew, so nothing touches the system Python), then runs the playbook. If the Command Line Tools dialog appears, let it finish and run `bin/bootstrap` again.

To re-run the playbook later (e.g. after adding software), run `bin/apply`.

## What this includes

 - 👨‍💻 Developer tools:
   - DataGrip (https://www.jetbrains.com/datagrip)
   - Zed (https://zed.dev/)
   - 💻 xCode
   - 📱 Android Studio
     - Android SDK platform-tools and command-line tools
     - bundletool (manipulate Android App Bundles)
   - 🐳 OrbStack (https://orbstack.dev/)
   - 🖥️ Terminal
     - ~~ITerm2 (https://iterm2.com/)~~ (Moved to cmux)
     - cmux (https://www.cmux.dev/) - Ghostty-based terminal with vertical tabs and notifications for AI coding agents
     - Oh My Zsh with a generated `~/.zshrc` (put personal config in `~/.zshrc.personal.before` / `~/.zshrc.personal.after`)
       - auto-switches node version on `cd` when a `.nvmrc` is present
     - Terminal commands
       - doctl (CLI for Digital Ocean)
       - fzf (Fuzzy Finder)
       - tree (view folders in a tree-like structure from your terminal)
       - imagemagick (manipulate images from terminal)
       - mas (install app store packages from command-line)
       - dockutil (manage osx dock from command-line)
       - gh (github-cli)
       - pnpm (my node package manager of choice)
         - EAS CLI (for using Expo application services)
       - gitmoji (Great for cleaner git commit messages with emojis)
       - neovim
       - ffmpeg
       - mysql-client
       - fastlane (build and release mobile apps)
       - cocoapods (dependency manager for iOS projects)
       - awscli (AWS command-line interface)
       - doppler (secrets and config CLI)
       - stripe (Stripe CLI, from the stripe/stripe-cli tap)
       - gitleaks (audit git repos for secrets)
       - mkcert (locally trusted dev certificates)
       - nmap (port scanning)
       - wget
       - yt-dlp (audio/video downloader)
       - vips (image processing library)
       - openai-whisper (speech recognition from the terminal)
   - Programming Languages
     - Python 3 (via Homebrew)
       - uv (fast Python package installer and resolver)
       - pipx (run Python CLI tools in isolated environments)
     - Go
     - Java 17 (openjdk@17, keg-only)
     - PHP tooling: composer
     - nodejs (latest LTS, managed with nvm)
 - 📈 Productivity Tools
   - Superhuman (Referral link: https://superhuman.com/refer/tnw03qfq)
   - Whatsapp (https://www.whatsapp.com/)
   - Claude (https://claude.com/download)
   - Google Drive
   - Slack
 - 🎮 Games & Chat
   - Steam
   - Discord
 - 🎼 Music Tools
   - Focusrite Control (Scarlett 2i2 driver)
 - 🛠️ Utilities
   - Raycast (https://www.raycast.com/store)
   - Vorssaint (https://github.com/vorssaint/vorssaint-utils) - Menu bar toolkit with keep-awake, system monitor and volume mixer

### Dotfiles

The playbook also writes these from `templates/`. They are overwritten on every run, so change the template, not the file in `$HOME`:

| File | Template | Notes |
| --- | --- | --- |
| `~/.zshrc` | `.zshrc.j2` | personal additions go in `~/.zshrc.personal.before` / `.after` |
| `~/.gitconfig` | `.gitconfig.j2` | name/email come from `vars` at the top of the playbook; private config goes in `~/.gitconfig.local` |
| `~/.config/git/ignore` | `gitignore_global` | global git ignore |
| `~/.config/nvim/init.vim` | `init.vim` | Neovim config |

### Dock clean up 🧹

As I find the default MacOS dock is cluttered, this playbook will also remove the following from the dock:
- Keynote
- Numbers
- Pages
- Freeform
- Contacts
- Maps
- Mail
- Messages
- Notes
- TV
- App Store
- Safari
- System Settings
- FaceTime

It then adds these to the dock (in this order, after whatever is already there): Apps, Music, Superhuman, WhatsApp, and the Downloads folder.

### macOS defaults

The playbook sets these preferences (captured from my machine with `defaults read`):

- Dark mode (applies at next login)
- Dock: auto-hide, 64px icons
- Finder: column view, path bar shown, new windows open at Computer, no warning when changing a file extension, external drives shown on the desktop but not internal ones

`bin/apply --tags defaults` or `bin/apply --tags dock` re-runs just that part.

### Default software clean up

This script also removes the following (via `mas uninstall`, or by deleting the app bundle when mas can't because the app is owned by root):
- Keynote
- Numbers
- Pages
- iMovie

 
## Manual steps

Things the playbook can't do for you. In order:

**Before running `bin/bootstrap`**
1. Sign in to iCloud and the App Store (System Settings), otherwise the `mas install` tasks fail.

**After the playbook has run**
1. Generate an SSH key and add it to GitHub: `ssh-keygen -t ed25519 -C "james@irving-swift.com"`, then `gh auth login` (which can upload the key for you).
2. Open a new shell so the generated `~/.zshrc` is picked up, then re-run `bin/apply` if anything failed on the first pass.
3. Sign in to the apps that need it: Raycast, Superhuman, Slack, WhatsApp, Claude, Google Drive, Discord, Steam, DataGrip.
4. Secrets (API keys etc.) go in `~/.zshrc.personal.after`, never in the generated `~/.zshrc`.
5. Open Xcode once to install its additional components, then Android Studio to let it download the SDK.
6. Empty the Trash to finish removing the default Apple apps.

## Troubleshooting

**`It seems there is already an App at '/Applications/X.app'`** or **`sudo: a terminal is required`** in the cask task — the app was installed by hand, not by Homebrew. The playbook passes `--adopt`, but brew usually needs `sudo` to fix the app's permissions, and it can't prompt for a password from inside Ansible. Run this once in a terminal (use `--force` instead of `--adopt` if the installed version differs from the cask), then re-run `bin/apply`:

```
brew install --cask --adopt <name>
```

**`KeyError: 'pop from an empty set'` in the homebrew task** — an old `community.general` collection. `bin/bootstrap` (or `ansible-galaxy install -r requirements.yml`) installs the pinned release, which needs ansible-core 2.18+. If `ansible --version` shows something older, it is a leftover pip install: `brew install ansible` and make sure `/opt/homebrew/bin` is first on your PATH.

## What could be considered missing?

Currently, I have no need for the following packages and thus I have omitted them

- Docker Desktop (replaced by OrbStack)
- Kubernetes
