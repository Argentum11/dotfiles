# dotfiles

## Setup

```bash
# 1. Run install script
cd ~/dotfiles
chmod +x install.sh
./install.sh

# 2. Add the source line to ~/.zshrc
echo 'source ~/dotfiles/shell/aliases.sh' >> ~/.zshrc

# 3. Reload your shell
source ~/.zshrc

# 4. Install global Claude Code instructions
mkdir -p ~/.claude
cp ./claude/CLAUDE.md ~/.claude/
```