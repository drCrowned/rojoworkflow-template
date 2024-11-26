# Rojo-Roblox Studio Workflow Template
###### rojoworkflow-template
The standard Rojo-Roblox Studio Workflow, opened for everyone who don't want to go through creating whole repos and stuff. This tutorial (seen below) assumes that you have knowledge about GitHub, installation of stuff, and have already handled the required resources. This also uses VSC (Visual Studio Code) as its text editor, so if you have anything else, sorry not sorry!

## Tutorial Outline
### 0: Tips!
### 1: Setup Rojo
### 2: Setup Stylua and Selene

## Before proceeding, know these tips!
Hey, just a reminder that Rojo does delete everything it finds in defined structures. So if it finds an unknown instance that was not defined in DataModel\Replicated Storage\SharedCodebase, it will make them **poof**.

You don't want that, right? Maybe there are instances, like a sound that you wanna keep in folders next to your scripts? In my case, my characters in Zenless Battlegrounds have accessories for the system to reference, but I don't want the hard work to be drained. That is why I put in a *json* file in every folder that's necessary for. You can find said file under the project structure. *init.meta.json* to be exact.

Also... How can I say this... VSC is blind when coding luau files. It doesn't recognize the Roblox LSP natively. So you'll need yet another extention for your collection of 103~ plugins. (I hope you don't have that many extentions.)

Search for Roblox LSP in the extention store, then install it. It has everything you can ask for, even compability with Rojo!
![image](https://github.com/user-attachments/assets/9cd136ac-1416-4136-a8d1-91434ea8fc2f)

Alrighty, now let's get into the real stuff.

## Setting up Rojo
We'll start with getting Rojo into our project. It's pretty straight forward.

First start with installing the Rojo extension in Visual Studio. Search up Rojo in the extention store and you'll find it. *Rojo - Roblox Studio Sync*
![Screenshot 2024-11-25 215443](https://github.com/user-attachments/assets/fce0eabe-e0bc-4402-9f09-d793ff2ef3bf)
I also recommend downloading other useful extension, such as icon packs. *Rojo UI* is broken as I'm typing this, so don't mind it.


You're then going to your command thing at the top, and enter the Rojo menu. (Tip: press the *>* key and find Rojo there!)

![image](https://github.com/user-attachments/assets/254784d2-6c4f-4d17-bbca-5e83c2888f6d)

You'll then have to create your project files, if you didn't set them up. (somewhat)
![image](https://github.com/user-attachments/assets/bc4063d9-e915-4d73-86ad-fbf71513c6e1)

![image](https://github.com/user-attachments/assets/dc5ae77a-3542-447c-b94b-61a75cf908a9)


#### Ta-Da! Rojo's now in your Repository!

If you want, you can launch *rojo build -0 game.rbxl* into your command terminal in order to build your game. You'll find a file called *game.rbxl* in your explorer after that!

In order to sync Roblox Studio and Rojo together, you'll also need the Rojo plugin in your IDE. Start-up the Rojo Ext to then, start the Rojo plugin in your IDE.

## Setting up Stylua and Selene
This is where it become optional. You don't really need it, but it's really REALLY useful!
