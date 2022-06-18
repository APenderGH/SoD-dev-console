# DnSpy and Unity Games
I hadn't done any reversing until I participated in the [CSCG CTF](https://earth.cscg.live/), it had three introductory reversing challenges. In the first challenge you're given a single executable and told that it's a .NET application.

After doing some research I found that .NET applications are particularly easy to reverse, just try decompile them with **DnSpy**!

# School of Dragons (some random Unity game)
One night in the name of procrastination I downloaded a game my siblings used to play called 'School of Dragons'. I must admit, my intention was to try to break the game in whatever way I could, it's just what I enjoy doing. Problem was that I don't actually have a lot of experience with game hacking beyond some basic trainers, so I didn't expect to find anything.

Anyway, I played the game for a bit then decided to search for existing cheats for the game, just to see how other people had done it. Unfortunately, I couldn't find anything about this game in particular so I widened my scope. 'How to reverse Unity games' is what I searched, and to my surprise I saw a mention of DnSpy, turns out [Unity uses .NET](https://docs.unity3d.com/Manual/overview-of-dot-net-in-unity.html). Someone recommended decompiling a .dll named `Assembly-CSharp.dll`, so I did that...

To my surprise DnSpy spat out heaps of C# code, time to do some reading!
