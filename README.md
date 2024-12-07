# Rojo-Roblox Studio Workflow Template
###### rojoworkflow-template, Not final as it's still under progress!
This is the standard Rojo-Roblox Studio Workflow, open for everyone who doesn't want to go through creating whole repos and stuff. This tutorial (seen below) assumes that you have knowledge about GitHub and the installation of stuff and have already handled the required resources. This also uses VSC (Visual Studio Code) as its text editor, so if you have anything else, sorry not sorry~

Guide Completion: 53%
## Tutorial Outline
### 0: Tips!
### 1: Setup Rojo
### 2: Setup Stylua and Selene
### 3: CI Pipeline
### 4: Setup rbxcloud*
### 5: CD Pipeline*
### 5: Closing Remarks

## Before proceeding, know these tips!
Hey, just a reminder that Rojo does delete everything it finds in defined structures. So, for example, if it finds an unknown instance not defined in DataModel\ReplicatedStorage\SharedCodebase, it will make them **p o o f**.

You don't want that, right? Maybe there are instances, like a sound, that you want to keep in folders next to your scripts. In my case, my characters in Zenless Battlegrounds have accessories for the system to reference, but I don't want the hard work to be drained. That is why I put a *json* file in every necessary folder. You can find the said file under the project structure—*init.meta.json*, to be exact.

Also... How can I say this... VSC is blind when coding Luau files. It doesn't recognize the Roblox LSP natively. So you'll need yet another extension for your collection of 103 plugins. !(I don't have that many extensions...)

Search for Roblox LSP in the extension store, then install it. It has everything you can ask for, even compatibility with Rojo!
![image](https://github.com/user-attachments/assets/9cd136ac-1416-4136-a8d1-91434ea8fc2f)

Alrighty, now let's get into the real stuff.

## Setting up Rojo (Is it 'Ro-Jo' or 'Ro-Ho'?)
We'll start with getting Rojo into our project. It's pretty straightforward.

First start with installing the Rojo extension in Visual Studio. Search up Rojo in the extension store and you'll find it. *Rojo - Roblox Studio Sync*
![image](https://github.com/user-attachments/assets/dff681a3-9ec8-4418-b6b1-46d1ffc0bd0e)
I also recommend downloading other useful extensions, such as icon packs. *Rojo UI* is broken as I'm typing this, so don't mind it.


You're then going to your command thing at the top and enter the Rojo menu. (Tip: press the *>* key and find Rojo there!)

![image](https://github.com/user-attachments/assets/254784d2-6c4f-4d17-bbca-5e83c2888f6d)

You'll then have to create your project files if you didn't set them up. (Somewhat)
![image](https://github.com/user-attachments/assets/bc4063d9-e915-4d73-86ad-fbf71513c6e1)

![image](https://github.com/user-attachments/assets/dc5ae77a-3542-447c-b94b-61a75cf908a9)


#### Ta-Da! Rojo's now in your Repository!

If you want, you can launch *rojo build -0 game.rbxl* into your command terminal to build your game. You'll find a file called *game.rbxl* in your explorer after that!

You'll also need the Rojo plugin in your IDE to sync Roblox Studio and Rojo together. Start up the Rojo Ext then, start the Rojo plugin in your IDE.

## Setting up Stylua and Selene
This is where it becomes optional. You don't need it, but it's really **REALLY** useful!

Get this, you want to read your subordinates' work and provide input on it. Turns out you need to learn another language to see one line of their atrocious code!
Stylua is the go-to for programmers to enforce styling formats in *✨LOuaU✨* files.

Selene, on the other hand, is a linting tool. In simple terms, it reads your code in real time and throws obvious lines at you when you do something bad. For example; repeated lines, voided expressions, unused variables, and more.


Start by installing the Stylua and Selene extensions in VSC. It's pretty straightforward.
![image](https://github.com/user-attachments/assets/697f9510-64fb-460e-9ef5-91f29a1ddfde)
![image](https://github.com/user-attachments/assets/490d3f02-76f6-4d8d-82c9-f9859ec6df58)


In your *aftman.toml* file, throw in the following...
```
stylua = "johnnymorganz/stylua@0.14.2"
selene = "Kampfkarren/selene@0.27.1"
```
Keep in mind that you'll probably need to update the packages, knowing they won't be the same versions as stated here.

Create the *selene.toml* file in the root of your project.

![image](https://github.com/user-attachments/assets/1065ca1b-f4c2-4d0b-a1e6-0fe2c4e4ebdd)

Then throw this in there once created.
```
std = "roblox"
```

Create a settings.json file under your .vscode folder, and slap this code in it. (You can create one if you don't have one!)
```
{
    "[lua]": {
        "editor.defaultFormatter": "JohnnyMorganz.stylua",
        "editor.formatOnSave": true,
        "editor.formatOnPaste": true
    }
}
```

That's it, wasn't so hard right?


## CI Pipeline and Pull Requests
There is a feature called *Pull Requests* in GitHub, essentially people will request to push their work into the *main/base* branch of your repo, allowing you to review it before making it official. But what if you're too lazy one day? What if you don't want to review 1000 lines of code to find a single error at the end? What if you had the person accidentally send the wrong revision of the code so you have to wait an entire day for them to finally get back on and fix it, to find that you found another error and they have to fix it again, and it breaks the whole script- 

Ahem, apologies for my outburst. With the CI Pipeline, every time you make a pull request or direct push, it will get checked by the system and will do the work for you!

(There are some stuff you can do to protect your precious repo. Like locking your main branch, having branch protection rules, etc.)

Start with creating a workflow folder. Inside the *.github* folder (if you have one, if not feel free to make one!)

![image](https://github.com/user-attachments/assets/59313c7d-900f-4184-8071-5017abbbc682)

You're then gonna have to create a *ci.yaml* file under dat, containing every action that's going to be processed when someone pushes a change.
```
name: build
on: [push]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
      - name: Setup Aftman
        uses: ok-nick/setup-aftman@v0.3.0
        with:
          version: 'v0.2.7'
          token: ${{ secrets.GITHUB_TOKEN }}
      - name: Generate standard library
        run: selene generate-roblox-std
      - name: Run Selene
        run: selene src
```
This is the default build I put in almost each of my projects. It does the job and has the bare minimum for what we need. It essentially checks if tools are running properly, checking your codebase after that's done. Here's a reminder that it won't yield or prevent a change if a user pushes directly to a branch instead of requesting a pull.

There you go, you're almost done with this tutorial!

## Using rbxcloud
H

## Continuous Delivery (CD) and its uses
H


## Closing Remarks
Well, this is it! You now have a Rojo-Roblox Studio workflow at your fingertips. You don't have to do everything within VSC, do note that Rojo isn't necessary for Roblox games. It's just a valuable tool for professional developers, big studios, and people who like source control and GitHub.

Thanks to sleitnick (this guy here --> https://www.youtube.com/@sleitnick1) for his amazing *Advanced Roblox Project Setup* video. I still use it for my projects and look up to him as one of my motivations. This guide is his video but shorter?

Any questions can be asked in issues or discussions, I'll be happy to answer them. Just note that I'm still actively learning the whole... "Git thing, CD/CI Pipeline thingy, whatever complicated term out there", so we're in this together!

Anyway, toodles! I gotta prepare a bowl of cereal.
