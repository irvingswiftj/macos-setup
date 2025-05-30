# Swifty's MacOS setup

Resources:
Article about how to run: https://irving-swift.com/setup-your-mac-with-ansible/

## How to run

```
$ ./setup
$ bin/bootstrap
```

## What this includes

 - 👨‍💻 Developer tools:
   - DataGrip (https://www.jetbrains.com/datagrip)
   - Visual Studio Code (https://code.visualstudio.com/)
     - gitlens
     - code spell checker
     - vscode todo plus
   - 💻 xCode
   - 📱 Android Studio
   - 🚀 Postman
   - 🐳 OrbStack (https://orbstack.dev/)
   - 🖥️ Terminal
     - ~~ITerm2 (https://iterm2.com/)~~ (Moved to Ghostty)
     - Warp (Referral link: https://app.warp.dev/referral/MELL3R)
     - Ghostty (https://ghostty.org/)
     - Terminal commands
       - doctl (CLI for Digital Ocean)
       - fzf (Fuzzy Finder)
       - tree (view folders in a tree-like structure from your terminal)
       - imagemagick (manipulate images from terminal)
       - mas (install app store packages from command-line)
       - dockutil (manage osx dock from command-line)
       - asdf (managed versions of node, ruby, python, etc)
       - gh (github-cli)
       - pnpm (my node package manager of choice)
       - gitmoji (Great for cleaner git commit messages with emojis)
       - neovim 
       - ffmpeg
       - mysql-client
   - Programming Languages
     - Python (3.13.1)
     - nodejs (22.12.0)
       - EAS CLI (for using Expo application services)
 - 🌐 Browsers
   - Brave Browser (https://brave.com/)
   - Arc (https://arc.net/)
 - 📈 Productivity Tools
   - Notion (https://www.notion.com/)
   - Superhuman (Referral link: https://superhuman.com/refer/tnw03qfq)
   - Whatsapp (https://www.whatsapp.com/)
   - ChatGPT (https://openai.com/index/chatgpt/)
   - Google Drive
   - Slack
 - 🎼 Music Tools
   - Scarlet 2i2 Driver
 - 🛠️ Utilities
   - Mos (https://mos.caldis.me)
   - Raycast (https://www.raycast.com/store)
 
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

- Docker
- Kubernetes

## Known Issues

### PNPM error

```
ERR_PNPM_NO_GLOBAL_BIN_DIR  Unable to find the global bin directory\n\nRun \"pnpm setup\" to create it automatically, or set the global-bin-dir setting, or the PNPM_HOME env variable. The global bin directory should be in the PATH.\n
```

For some reason, `source ~/.zshrc` doesn't always seem to do the trick, if you get this error, just close your shell, open a new one and run `bin/apply`. 
