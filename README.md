# Swifty's MacOS setup

Resources:
Article about how to run: https://irving-swift.com/setup-your-mac-with-ansible/

## How to run

```
$ ./setup.sh
$ bin/bootstrap
```

To re-run the playbook later (e.g. after adding software), run `bin/apply`.

## What this includes

 - 👨‍💻 Developer tools:
   - DataGrip (https://www.jetbrains.com/datagrip)
   - Zed (https://zed.dev/)
   - 💻 xCode
   - 📱 Android Studio
   - 🐳 OrbStack (https://orbstack.dev/)
   - 🖥️ Terminal
     - ~~ITerm2 (https://iterm2.com/)~~ (Moved to Ghostty)
     - Warp (Referral link: https://app.warp.dev/referral/MELL3R)
     - Ghostty (https://ghostty.org/)
     - cmux (https://www.cmux.dev/) - Ghostty-based terminal with vertical tabs and notifications for AI coding agents
     - Oh My Zsh with a generated `~/.zshrc` (put personal config in `~/.zshrc.personal.before` / `~/.zshrc.personal.after`)
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
       - openai-whisper (speech recognition from the terminal)
   - Programming Languages
     - Python 3 (via Homebrew)
       - uv (fast Python package installer and resolver)
     - Go
     - nodejs (latest LTS, managed with nvm)
 - 📈 Productivity Tools
   - Superhuman (Referral link: https://superhuman.com/refer/tnw03qfq)
   - Whatsapp (https://www.whatsapp.com/)
   - Claude (https://claude.com/download)
   - Google Drive
   - Slack
 - 🎼 Music Tools
   - Focusrite Control (Scarlett 2i2 driver)
 - 🛠️ Utilities
   - Raycast (https://www.raycast.com/store)
   - Vorssaint (https://github.com/vorssaint/vorssaint-utils) - Menu bar toolkit with keep-awake, system monitor and volume mixer

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

### Default software clean up

This script also removed the following:
- Keynote
- Numbers
- Pages
- iMovie

After the script is complete, you will have to empty the Trash.
 
## What could be considered missing?

Currently, I have no need for the following packages and thus I have omitted them

- Docker Desktop (replaced by OrbStack)
- Kubernetes

## Known Issues

### PNPM error

```
ERR_PNPM_NO_GLOBAL_BIN_DIR  Unable to find the global bin directory\n\nRun \"pnpm setup\" to create it automatically, or set the global-bin-dir setting, or the PNPM_HOME env variable. The global bin directory should be in the PATH.\n
```

For some reason, `source ~/.zshrc` doesn't always seem to do the trick, if you get this error, just close your shell, open a new one and run `bin/apply`. 
