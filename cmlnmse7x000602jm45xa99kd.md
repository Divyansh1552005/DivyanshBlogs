---
title: "Creating Custom System Commands in Linux"
seoTitle: "Custom Linux Commands: A Step-by-Step Practical Guide"
seoDescription: "Learn to create custom system commands in Linux, like the 'gpush' command, to streamline and automate repetitive tasks in your terminal"
datePublished: Sun Feb 15 2026 10:57:17 GMT+0000 (Coordinated Universal Time)
cuid: cmlnmse7x000602jm45xa99kd
slug: creating-custom-system-commands-in-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1771152745988/9ed11fe2-24d5-4ab1-b5d5-5a4ad316e7fd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1771153013371/9697abdf-ec53-4fa2-9693-25a1bc4701fc.png
tags: linux, development, bash, zsh, developer, environment, development-tools, bash-scripting, shell-script, bash-script, development-environments

---

# Introduction

In this post, we’ll learn how to create **custom system commands in Linux** and use them like native terminal commands, with the help of a practical example in which we’ll build a command called `gpush` that combines `git add`, `git commit`, and `git push` into a single command.

# Custom Git Command: gpush

The `gpush` command combines three commonly used Git commands into one:

* `git add .`
    
* `git commit -m "<commit message>"`
    
* `git push`
    

Once set up, you can use `gpush` from **any Git repository** just like a normal terminal command.

---

## What `gpush` Does

Instead of typing:

```bash
git add .
git commit -m "your message"
git push
```

You can run:

```bash
gpush "your message"
```

---

## Step 1: Create a `bin` Directory in Home

```bash
mkdir -p ~/bin
```

This directory is commonly used for personal system commands.

---

## Step 2: Add `~/bin` to PATH

Open your Zsh or bash configuration file:

```bash
nano ~/.zshrc
# or if you use bash as your default shell
# nano ~/.bashrc
```

Add this line at the **end of the file**:

```bash
export PATH="$HOME/bin:$PATH"
```

Reload the configuration:

```bash
source ~/.zshrc
# source ~/.bashrc
```

Verify:

```bash
echo $PATH
```

You should see `/home/username/bin` at the beginning of the output.

---

## Step 3: Create the `gpush` Script

Create the script file:

```bash
nano ~/bin/gpush
```

Paste the following code:

```bash
#!/usr/bin/env bash

if [ $# -eq 0 ]; then
  echo "Commit message required"
  echo "Usage: gpush \"your commit message\""
  exit 1
fi

git add .

git commit -m "$*"

git push
```

Save and exit the editor.

---

## Step 4: Make the Script Executable

```bash
chmod +x ~/bin/gpush
```

---

## Step 5: Use the Command

Inside any Git repository:

```bash
gpush "Initial commit"
```

---

## Example

Command:

```bash
gpush "Updated README and fixed layout"
```

What happens internally:

```bash
git add .
git commit -m "Updated README and fixed layout"
git push
```

---

# Conclusion

By creating your own custom commands in Linux, you can significantly reduce repetitive work and tailor the terminal to match your workflow. The `gpush` example shows how simple scripts placed in a personal `bin` directory can behave like native system commands. This approach scales well, you can extend it to automate any frequently used command sequence and gradually build a more efficient, personalized development environment.