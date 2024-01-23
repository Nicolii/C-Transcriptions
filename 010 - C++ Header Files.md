Let's go somewhere fun today.  
Alright let's try something new. Hey what's up guys.  
My name is The Cherno, welcome back to my C++ series.  
So today, header files.  
And we're actually we're actually out.  
Started off is a great day then it started raining, but I decided to get out of town because...  
So we're here, somewhere in Australia, and we're going to be talking about C++.  
Hope you guys don't start to think that header files are so boring that I felt the need to just get out of town to cover them, that's just what I just felt like doing.  
Alright so header files.  
What are they? Why do we need them? Why do they even exist in C++?  
A lot of other languages that you might have been used to like Java or C#, they don't actually have header files, or any kind of concept of, of two different file types.  
Where we have our compilation file that we actually compile like a C++ file a translation unit, and then we also have a header file, which is just this weird kind of file that we always include in places.  
And why is it even there?  
Header files are actually much more useful, and they're used for much more than just to kind of declare certain declarations that you want to use in multiple $.cpp$ files.  
And as the series kind of goes on we're just going to learn so many new concepts that really do require header files in order to work, so don't dismiss them too quickly.  
As far as the basics of C++ goes header files are traditionally used to declare certain types of functions, so they can be used throughout your program.  
If you think back to my C++ compiler and linker videos, I talked about how we need certain declarations to actually exist so that we know what functions and types we have available to us.  
For example: if we create function in one file and we want to use it in another file, C++ isn't going to know that that function even exists when we try and compile that other file.  
So we need a common place to kind of store just declarations, not definitions, because remember we can only define a function once.  
We need a common place to store declarations for functions, just declarations, no actual definitions, no body for the functions. But just a place that says "hey this function exists".  
Let's take a simple example here:  
So suppose that I have a function here, called `Log()`, that is supposed to log something to the console. It's going to take in a `const char* message`, and it's going to simply `cout` that message.  
If I then go ahead and create an additional file, we're going to call this $Log.cpp$.  
And then maybe that additional file has something that initializes our `Log()`, and decides to log something to the console.  
We are going to get an error because this `Log()` function doesn't actually exist in this file, this file doesn't know about the `Log()` function.  
Of course back in $Main.cpp$ here it is.  
The `Log()` function exists fine and we can actually replace our `"Hello World!"` logging to use that `Log()` function.  
And if I try and compile my program by hitting **CTRL+F7** you'll see that it works fine and we don't get any errors, however back in `Log()` if I try and compile this, we get an error.  
Because of course as far as this file is concerned `Log()` doesn't exist.  
So what does $Log.cpp$ actually need in order to not error us?  
How do we tell it that that `Log()` function does actually exist but it's just defined elsewhere?  
That is where a function declaration comes in.  
If we go back to our code here, I need to simply declare that `Log()` does exist.  
If we go back to $Main.cpp$ and we take a look at this actual signature, you'll see that `Log()` is a function that returns void and takes in one parameter which is a constant `char` pointer.  
And some child is chasing the kangaroos... that's funny.  
So this is the function signature, we can literally just copy this, go back to $Log.cpp$ paste this in and just close it with a semicolon.  
The fact that this function doesn't actually have a body means that it is the declaration of the function, we haven't defined what the function actually is, what the function actually does.  
We've just said hey there's a function called `Log()` that returns `void` and takes in a `const char*`, we've, that, that function exists.  
You can see that our intellisense error has gone away, and if I hit **CTRL+F7**, we do compile.  
And if I **RIGHT-CLICK** on $HelloWorld$ and click build to actually build my program you can see that it links fine as well, because it's, it's found that `Log()` function.  
All right, fantastic.  
So great. we've found a way to actually tell our $Log.cpp$ that, that `Log()` function exists somewhere.  
But what if we make another file?  
What if I what if I make some other file that needs to use this `Log()` function?  
Does that mean that I also have to copy and paste this void log declaration everywhere I go?  
The answer is yes, you actually do need to do that.  
However there is a way to make that easier.  
Header files. Right?  
What are header files?  
What are header files traditionally, I should say.  
Because really this is C++ what you can you can do anything with anything.  
But header files the usually files that get included into $.cpp$ files.  
So basically what we do is copy and paste the content of header files into $.cpp$ files, and we do that via the `#include` pre-processor directive.  
So `#include` has the ability to copy and paste files into other files, and that is exactly what it seems that we need to do here.  
We need to copy and paste this `Log()` declaration into every file that needs to use that `Log()` function.  
So let's have a go at making a header file.  
I'm going to **RIGHT-CLICK** on $Header~Files$.  
Now note these folders here are called filters, they're not actual real folders.  
I can create a header file under source files.  
There's going to be a few videos on how a Visual Studio works in the future, but for now just know these are kind of fake folders. It doesn't matter which one you **RIGHT-CLICK** on to create your header file.  
I'm going to create it under $Header~Files$ because that makes sense, but it doesn't really matter.  
I'm going to make a header file called $Log.h$.  
You'll notice that it straight away inserted some code for me automatically that says `#pragma once`, we'll talk about that in just a second.  
So here I'm going to put in my declaration, I'm going to cut my declaration from $Log.cpp$ file, and put it into here, into my header file.  
So now the idea is this this header file, $Log.h$ - I can include everywhere where I want to be able to use `Log()`.  
And of course, it's going to do for me what I didn't want to do manually, and that is copy and paste this everywhere throughout every file that requires it.  
I don't want to have to do that copying and pasting myself, so I've basically found a way to kind of make it look a bit tidy and automated to some extent.  
So back in $Log.cpp$, you can see we get an error now because we're not actually declaring that function.  
However if I type in `#include "Log.h"`, check that out, we don't get an error, and our file compiles. Fantastic.  
What we can also do is actually included into $Main.cpp$.  
Now $Main.cpp$ contains the actual definitions for the function, so it doesn't really require it, we can call `Log()` anyway.  
But just so you know it's not going to hurt for us to actually `#include "Log.h"`into here and compile, that's not going to be a problem.  
All right so back in $Log.cpp$ you can see we've defined this fantastic function called `InitLog()`, however no one actually knows about it except for $Log.cpp$.  
If I want to be able to call it from $Main.cpp$ I'm going to need that declaration.  
If I call `InitLog()` over here it's going to give me an error, because that's not declared anywhere.  
So let's go ahead and add that function signature `InitLog()` into our $Log.h$ header file. just like that, fantastic.  
Make sure that it matches the function signature that you've actually declared in your in your $.cpp$ file.  
So now everything seems well in the world.  
I'm also going to go ahead and cut and paste this log definition into my $Log.cpp$ file, because that makes a lot more sense.  
Now I get an error here telling me `cout` is not found, that's okay I can just `#include <iostream>`. Awesome.  
So back in $Main.cpp$, if I run my program, we can see that we managed to initialize our log, and then log "Hello World!" to the console. Fantastic.  
All right, brilliant.  
So let's go back to that header file and take a look at what that `#pragma once` statement actually was.  
So here we have a statement that Visual Studio has seemingly inserted for us, called `#pragma once`, what is this?  
So firstly anything that begins with a hash, is known as a preprocessor command or a preprocessor directive.  
It means that this is going to be evaluated by the C++ preprocessor before this file actually gets compiled.  
`#pragma` is essentially an instruction that is sent to the compiler, or to the preprocessor and what `#pragma once` essentially means - is that only include this file once.  
So `#pragma once` is something called a header guard.  
What it does is it prevents us from including a single header file multiple times into a single translation unit.  
Now I chose my words there very carefully, because you have to understand that it does not prevent us from including our header file into multiple places in our program, just into a single translation unit, so a single $.cpp$ file.  
The reason is that if we accidentally include a file multiple times into a single translation unit we can get duplicate errors.  
Because we'll be copying and pasting that entire header file multiple times.  
one of the best ways to demonstrate this, is if we were to create a `struct` for example.  
If I create a `struct` here called `Player`, I can leave it empty doesn't really matter.  
If I were to include this file twice into a single translation unit with no header guards, it would actually include that file twice.  
Which means that I would have two structures with exactly the same name: `player`.  
We can take a look at this example by commenting out our `#pragma once`, and then back and $Log.cpp$ I will `#include "Log.h"` twice.  
If I try and compile my file, you can see that we get a:  
"_'Player' : 'struct' type redefinition_" error.  
Because we're redefining that `struct player`.  
We can only define one `struct` called `Player`. Structs need unique names.  
So again you say "Cherno why would I do this?  
I'm not a stupid programmer,  
I'm not as dumb as you think.  
Why would I include a file twice?"  
Well, young one...  
This comes back to how `#include` works.  
Remember how `#include` works, is it copies and pastes filed into other files, meaning you can create a bit of a chain of includes.  
So you could have a header file called $Player.h$ which includes $Log.h$ then $Players.cpp$ included in some other file, and then maybe that third file contains every include.  
So if I create another header file here called $Common.h$.  
Common is just going to contain some common `#includes` for example it will `#include Log.h`.  
If I go to $Log.h$ and make sure that `#pragma once` is commented out, and into $Log.cpp$, I `#include Log.h` and `#include Common.h`.  
If I compile my file, guess what?  
I still get that error, because that `struct Player` is being redefined.  
If we were to resolve what the preprocessor actually did, you could see that it actually has included $Log.h$ twice.  
However back in $Log.h$ if we get rid of that comment, and try and compile our file, we don't get that error.  
Because it recognizes that $Log.h$ has already been included, and it does not include it twice.  
Now there is one other way that we could add a header guard, and I actually kind of like this for teaching purposes, because it makes a little bit more sense than some kind of `#pragma once`, although `#pragma once` does look a lot cleaner.  
The traditional way to add header guards is actually via an "if def".  
So what we can do is we can actually type in an `#ifndef`, and then we can get it to check some kind of symbol, for example `_LOG_H`.  
We're going to `#define _LOG_H` and then at the very end of our file we're going to type an `#endif`.  
So what this is going to do is, first of all check to see if a symbol called `_LOG_H` is actually defined.  
If it's not defined, it's going to go ahead and include the following code in compilation.  
If this was defined, then none of this will be included, it will be all disabled.  
So once we do pass this initial check, we're going to define `_LOG_H`, which basically means that next time we go through this code, it will be defined, so it will not be repeated.  
A really easy way to demonstrate this is just to copy and paste this entire file into our $Log.cpp$ file.  
And then if we take a look at this.  
I'll also comment out `#include "Log.h"`, and `#include "Common.h"`.  
So you can see over here that the first time this is all fine, it includes the file and everything's okay.  
And then the second time it's all grayed out because `_LOG_H` has already been defined.  
So this kind of header guard is something that was used a lot in the past, however now we have this new preprocessor statement called `#pragma once`, and so, we mostly use that.  
It doesn't matter which one you use to some extent, although `#pramga once` is lot cleaner, so it's something that I personally use, and it's something that most people do use in the industry.  
Pretty much every compiler now supports `#pragma once` so there isn't it's not like a Visual Studio only thing.  
GCC, Clang, MSVC, they all support `#pragma once` so don't be afraid to use it.  
That being said if you do find legacy code, or just code that people have written using different styles, you may encounter this `#ifndef` header guard, so just be wary of what it is.  
But again I would never write `#ifndef`, I would always use `#pragma once`.  
Last thing I want to show you is with header guides we have this kind of discrepancy between `#include` statements, some `#include` statements use quotes some `#include` statements use angular brackets.  
What is the deal?  
Deals actually pretty simple, they mean two different things.  
When we compile our program we have the ability to tell the compiler of certain include paths.  
These are basically paths to folders in our computer that contained include files.  
If the include file that we want to `#include` is inside one of these folders, we can use angular brackets to tell the compiler to search our "include" path folders.  
Where as quotes on the other hand are usually used to include files that are relative to the current file.  
So for example: if I had a file called $Log.h$ that was up one directory from this current $Log.cpp$ file.  
I could use `../` to go back, and that would actually go back to a directory, because this is relative to this current file.  
Whereas with angular brackets, they are never relative to this current file, they just have to be in one of the include directories.  
We'll talk more about setting up include directories and all that in the future, I want to complicate things too much.  
But that's basically the gist of how this works.  
Now quotes can also be used to specify files that are relative to include directories that are pass through our compiler.  
So you can actually use quotes anywhere.  
I can replace this `<iostream>` to be in quotes and it would totally work.  
So angular brackets, only for compiler include paths. quotes for everything, however I usually like to use them just for relative paths, since you might as well use the angular brackets for something.  
All right final thing for today.  
One other thing that you might notice is this `<iostream>` doesn't actually look like a file, because it doesn't contain any extension, it's just called iostream.  
What's up with that?  
Well it actually is a file, it's just that it doesn't have an extension.  
This is something that whoever wrote the C++ standard library decided to do.  
to basically separate out C standard library header files, C++ standard library header files.  
Header files that are in the C standard library will often have a $.h$ extension on the end, however C++ files do not.  
So this is just one other way you can differentiate between what is in the C standard library and a C++ standard library, whether on it has that $.h$ extension.  
$iostream$ is a file just like anything else.  
In fact in Visual Studio if we **RIGHT-CLICK** on it and hit "Open Document", you can see that it takes us to this $iostream$ header file.  
And if we **RIGHT-CLICK** on that on this tab here, and hit "Open Containing Folder", you'll see where it's actually located on our computer, inside this directory.  
And here it is, that $iostream$ header file.  
Alright so that's it, header files, pretty easy.  
We're going to be using this extensively in this series, so there'll be plenty of examples to follow.  
You'll see how I use them, you'll see how you should be using them.  
But you should now understand how they work, and what they're used for.  
So anyway I'm going to get out of here cause it's getting really, really cold.  
But I hope you guys enjoyed this video.  
Let me know what you think of this whole like me going out, and doing stuff in, in... I mean this is way more fun. I love traveling, so this is way more fun for me to do than just sitting at home, especially on a Saturday afternoon.  
Even though the weather today was pretty bad, so I probably should have just sat home.  
But anyway I'm here now.  
Let me know what you think of this.  
You can follow me on Twitter and Instagram.  
I'm going to be posting some of the photos I took today on Instagram, so be sure to follow me there.  
If you really enjoy the series and you want to see more of these videos you can support me on Patreon.com/TheCherno.  
And I will see you guys in the next video.  
Goodbye.
