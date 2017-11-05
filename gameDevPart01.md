How to Make Video Games Part I - Outline

Index
=====
i.		Introduction/Goals
ii.		Description of Tools/Platform
iii.	Project Basics
iv.		Lua Basics
v.		Löve Basics
vi.		Life Cycle of a Game
vii.	Pong I (in which we make the ball)
viii.	Pong II (in which we make the paddle)
ix.		Pong III (in which we make the ball hit the paddle)
x.		Pong IV (in which we make another paddle and keep score)
xi.		Pong V (in which we add winning and losing)
xii.	Graphics Basics
xiii.	Sound Basics
xiv.	Breakout I (in which we make a level)
xv.		Breakout II (in which we make the player and the ball)
xvi.	Breakout III (in which we make the bricks and scoring)
xvii.	Breakout IV (in which we make pick-ups)
xviii.	Breakout V (in which we make power-ups)
xix.	Breakout VI (in which we add winning and losing)
xx.		Breakout VII (in which we add graphics)
xxi.	Tetris Challenge

Introduction/Goals
==================

So you want to learn how to make games, eh? Well that's just great, but first you'll have to start from the very bottom. And that can be hard. Luckily, I'm gonna throw this little guide together to make picking up the basics a bit easier.

Before we start, know that when I say basics, I mean absolute bare minimum. If you think your going to be making the next Final Fantasy XV after you're through then you've got another thing coming. In fact, you won't even be able to halfway make Final Fantasy I. But we'll get there eventually.

The most important thing while following these tutorials is to make sure you understand everything in the current section before moving on to the next. If there's anything that doesn't make sense, try following these four steps to arrive at a conclusion:
* Keep watching/reading. The answer to your question might be just around the corner!
* Try it out. The best part about coding is that you can experiment with zero repercussions! You won't run out of code and have to go buy more; no one's gonna die if your Goombas clip through the floor.
* Google it. By now, the majority of questions about anything coding/gaming related have been asked on Google. If you can't find a solution there, then you're likely in uncharted territory. That means it's up to you(!) to find a solution.
* Ask an expert! Feel free to message me if you've exhausted your other resources. That being said, I'll try not to just give outright answers, since that really wouldn't help either of us.

Okay so let's get an idea of what we want to accomplish with these tutorials. Hopefully you've already seen the Outline. We'll start with the basics of a development environment. Then we'll move on to a basic Pong clone. Afterwards, a clone of Breakout should put the lid on rudimentary 2D game writing. By the end of this all, you'll have learnt enough to build a basic clone of the smash hit Tetris! Along the way, I'll describe some of the key principles in game programming and teach you a few tools and tricks of the trade.

A small disclaimer: Everything you're about to hear regarding tools and certain specific techniques (I'll make note of these) are based off of my personal work-flow. This isn't the only way to do things. Like I said, feel free to experiment and explore! That being said, these tutorials are tailored to _"writing"_ games and not _"making"_ games. What do I mean by that? Well we'll use the verb "write" to denote that we are making theses games by hand: actually writing code. We'll use the verb make when we talk about using game engines that generate code automatically or re-utilise existing code. Be proud! games that are "written" have more artistic and intellectual merit than games that are "made" /s.

Description of Tools/Platform
=============================

When it comes to carpentry, the first decisions the burgeoning carpenter must make is which tools and material to use. In much the same way, the developer is faced with similar decisions. With certain programming languages - the "wood," so to speak - certain tools immediately come to mind. But it's somewhat foolish to choose a particular wood just because you're a fan of the tools you'll get to use with it. Some woods are suited for certain purposes, and other woods for others. Coding has the benefit that the majority of woods... err... languages share similar properties and can be used in a variety of situations. That being said here is a general subset of popular languages for game development:
* C/C++ (especially for 3D games and their engines)
* C#
* Java (particularly Android)
* Flash (ActionScript or whatever it's called these days)
* Objective C (particularly iOS)
* HTML5 (for web)
* Lua (for auxiliary scripts)

These are all good and useful in their own rights (except Java, which sucks,) but if I were to recommend any as must-haves, I'd pick C/C++ and Lua. This is partly due to bias and partly practical. C, as a general rule, has the best performance in speed of all of these (and many other) languages. C++ is close to it, and most of the input and graphics libraries typically used in games are written in C or C++. As such, these two are fairly foundational; learning them would be a good starting point for grasping other languages. Lua on the other hand is on the opposite side of foundational. In fact, Lua is written in C! Many developers use it to provide a scripting interface to their engines. This is to allow for easy readability and quick alterations of non-architectural game features (speech trees, quest descriptions, boss behaviours etc.) Most scripting languages (Python and Ruby are some other examples) are easier to pick up and feature quality of life features that the more fundamental languages don't have. The cost of this is speed. I'm not 100% sure why, but I believe Lua is a gaming favourite because it balances performance with accessibility; it retains some of the power and speed of C but still has the legibility of Python.

For these tutorials we're going to stay within the world of 2D games, and we also want to stay out of the deep weeds of the complex C languages. To do this, we'll use Lua from top to bottom. Typically it's only used for its scripting capabilities, but with a little help from some friends, it can wield enough power to make even a complex 3D game! These powerful friends are OpenGL and SDL: two names you can't go far without hearing in the game dev world. OpenGL is a powerful graphics library and SDL is a media and IO library. The lovely people over at Löve2D have glued several parts together to create the Löve2D framework. A framework is essentially a set of features that can be used to accomplish hardware or system specific tasks without having to redo development for each combination/alteration of hardware or software. It's not quite at the level of a game engine in terms of functionality, but it should get us off the ground.

In addition to our framework, we're going to need something to write the game with. Our pen and paper, as it were. Fun fact: when my parents were in school, they wrote programs on - essentially - note cards by punching holes in them. The computer would ingest these cards in order to "read" the program! Anyway, things are a lot more civilised now, and we can write our code on the computer using a text editor. There are as many different text editors on the net as stars in the sky (maybe more). Just as the warrior carefully chooses his weapon, so too must you choose an editor. Their capabilities range from too simple to be useful (MS Notepad/plastic spoon) to needing god-like powers just to hold them (Vim/Mjolnir/Sikanda). The most important aspect is that you know how to use it efficiently. I'm a big fan of Sublime Text (about an Excalibur on the weapon scale), and it's my go-to editor, even/especially at work. Many people use Atom (fairly-good-imitation-Excalibur-but-you-can-tell-it's-fake), which is similar and I also recommend, or also Notepad++ (butter knife), which I'm fairly convinced is garbage. One thing to note, is that if you're developing on Windows you'll want an editor that supports Unix style line endings. If you don't know what that means, then USE THE FOUR STEPS OUTLINED EARLIER IN THIS GUIDE. Ahem. Here's a link to sublime ;D https://www.sublimetext.com/.

Project Basics
==============

Now that we know our material and our primary tool, let's take a look at how to start working them. The first thing we'll need to do is create a folder to store the files we'll be writing. My habit is to create a "Projects" folder in my home folder and the for each new project, create another folder inside.

For this first part of the guide, we'll be using A single source code file for each of these games. So theoretically you could just drop the single file in a "Projects" folder, but don't. It's good practice to keep your workspace well organised.

You should also know that I'm developing on Linux, so I'll be running my code from the command line. Frankly I'm not aware of any other way to run my code, but for Löve, you should be able to drag the folder containing your source code onto the Löve icon on your desktop in order to launch a game. That's pretty disgusting, but do whatever you need to, I guess.

Last thing is file extensions. Maybe you've grown up thinking that the .xxx at the end of a file name holds some sort of magic property. You'd be wrong. The .xxx, or file extensions, is just a way to help us as developer know at a glance what sort of information a file contains. It's also used by your OS to choose a program to open a file with, but this still doesn't mean the contents will be legible by the program. Changing a .png to a .jpeg will not convert your file. Changing a .lua to a .zip will not compress your file. All files of any type can be opened and read with a text editor, but certain, binary files (such as image files or executables) will be unintelligible to the human brain. Doesn't mean they aren't fun to look at though! We'll be working primarily with the .lua extension since we're using Lua, but really our source code is plain text (.txt). all this means is that every character in our files will correspond directly to one of the 256 standard ASCII characters with the same corresponding meaning ('a' means 'a' and so on). Later on we might get in to custom file formats where 'a'
 might mean "grass" and 'b' might mean 11938 in our own .applebees file, but we'll burn that bridge when we get there.

Lua Basics
==========



Löve Basics
===========



Lifecycle of a Game
===================



Pong I 
======
(in which we make the ball)
---------------------------



Pong II 
=======
(in which we make the paddle)
-----------------------------



Pong III 
========
(in which we make the ball hit the paddle)
------------------------------------------



Pong IV 
=======
(in which we make another paddle and keep score)
------------------------------------------------



Pong V 
======
(in which we add winning and losing)
------------------------------------



Graphics Basics
===============



Sound Basics
============



Breakout I 
==========
(in which we make a level)
--------------------------



Breakout II 
===========
(in which we make the player and the ball)
------------------------------------------



Breakout III 
============
(in which we make the bricks and scoring)
-----------------------------------------



Breakout IV 
===========
(in which we make pickups)
--------------------------



Breakout V 
==========
(in which we make powerups)
---------------------------



Breakout VI 
===========
(in which we add winning and losing)
------------------------------------



Breakout VII 
============
(in which we add graphics)
--------------------------



Tetris Challenge
================
