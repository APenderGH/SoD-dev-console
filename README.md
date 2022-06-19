# DnSpy and Unity Games
I hadn't done any reversing until I participated in the [CSCG CTF](https://earth.cscg.live/), it had three introductory reversing challenges. In all three challenges you're given a single executable and told that it's a .NET application.

After doing some research I found that .NET applications are particularly easy to reverse, just try decompile them with **DnSpy**!

# School of Dragons (some random Unity game)
One night in the name of procrastination I downloaded a game my siblings used to play called 'School of Dragons'. I must admit, my intention was to try to break the game in whatever way I could, it's just what I enjoy doing. Problem was that I don't actually have a lot of experience with game hacking beyond some basic trainers, so I didn't expect to find anything.

Anyway, I played the game for a bit then decided to search for existing cheats for the game, just to see how other people had done it. Unfortunately, I couldn't find anything about this game in particular so I widened my scope. 'How to reverse Unity games' is what I searched, and to my surprise I saw a mention of DnSpy, turns out [Unity uses .NET](https://docs.unity3d.com/Manual/overview-of-dot-net-in-unity.html). Someone recommended decompiling a .dll named `Assembly-CSharp.dll`, so I did that...

DnSpy spat out heaps of C# code, time to do some reading!

Pretty quickly I came across this:

![image](https://user-images.githubusercontent.com/104875856/174466783-52898e0c-9175-45bd-89b4-58dbfb97fdbe.png)

Now this looks promising! A quick read through the class and we find that we can open this `KAconsole` using CTRL + SHIFT + \`

![image](https://user-images.githubusercontent.com/104875856/174466835-0f536964-27b6-42d0-be2b-51834fe43130.png)

Quickly launching the game to see if this would work, and **BAM!**

![image](https://user-images.githubusercontent.com/104875856/174466992-a884c3ef-a516-40ae-a2a3-1046a6514c4f.png)

Hmm, but any input gives us this response...

![image](https://user-images.githubusercontent.com/104875856/174467042-736e70e9-06f8-43e8-a864-86673d1769bc.png)

Luckily we saw earlier that at the very top of the `KAConsole` class there's a boolean that defines whether or not this console is 'unlocked'. Lets just change that to return true and we'll save the modified module in DnSpy.
```C#
public static bool pUnlocked
{
	get
	{
		return true; //Application.isEditor || (ProductConfig.pInstance != null && WsMD5Hash.GetMd5Hash(KAConsole.mUnlockCommand) == ProductConfig.pInstance.ConsolePassword);
	}
}
```
Brilliant! Inputting `help` now gives us a list of commands for us to use. There's even some that aren't listed here that you can find in the dissassembled code, though I must admit they aren't overly interesting.

![image](https://user-images.githubusercontent.com/104875856/174467322-acbd27cc-d393-46ba-9274-f27cc2134e04.png)

Doing this even gives us a nice little performance display in the top right of our screen.

![image](https://user-images.githubusercontent.com/104875856/174467336-5423e53b-68b6-4ddd-b888-e81c752cddcf.png)

 Needless to say, this gives us quite some power over the game. I spent a while exploring the possibilities and it's a lot of fun to just see how the game works and what commands the developers are working with. Anyway, before I talk more about 

