# GD3D11 [![GitHub Actions](https://github.com/kirides/GD3D11/actions/workflows/build.yml/badge.svg)](https://github.com/Kirides/GD3D11/actions) [![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/Kirides/GD3D11?include_prereleases)](https://github.com/Kirides/GD3D11/releases)

With this mod for the games "Gothic" and "Gothic 2", I want to bring the engine of those games into a more modern state. Through an own implementation of the DirectDraw-API and using hooking and assemblercode-modifications of gothics intern engine calls, I have managed to completely replace gothics old rendering architecture with a new one, which is able to utilize more of the current GPU generations power for rendering.
Since Gothic's engine in its original state tries to cull as much as possible, this takes a lot of work from the CPU, which was slowing down the game even on todays processors. While the original renderer did a really great job with the tech from 2002, GPUs have grown much faster.

And now, that they can actually use their power to render, we not only get a big performance boost on most systems, but also more features.

## Bugs & Problems

If you have problems with building GD3D11 after following these instructions or experience bugs/problems with GD3D11 itself, open an issue on this GitHub page or post in the D3D11 thread on ["World of Gothic" (WOG)](http://forum.worldofplayers.de/forum/forums/104-Editing).  
But first take a look at the [KNOWN ISSUES](./known_issues.md)

## Building

### Latest version

Building the mod is currently only possible with windows, but should be easy to do for anyone. To build the Mod, you need to do the following:

- Download & install **Git** (or any Git client) and clone this GitHub repository to get the GD3D11 code.
- Download & install **Microsoft Visual Studio 2019** (Community Edition is fine, make sure to enable C++ Tools during installation!) from Microsoft.
	- might work on 2015 or 2017 but untested.
- ~~Download ... DirectX SDK ...~~ **NEW**: Not dependent on DirectX SDK anymore.
- Set environment variables "G2_SYSTEM_PATH" and/or "G1_SYSTEM_PATH", which should point to the "system"-folders of the games.
- Download & install the latest release version of the mod into your game from the latest [WOG](http://forum.worldofplayers.de/forum/forums/104-Editing) D3D11 thread.

To build GD3D11, open its solution file (.sln) with Visual Studio. It will the load all required projects. There are multiple build targets, one for release and one for developing / testing, for both games each:

* Gothic 2 Release: "Release"
* Gothic 1 Release: "Release_G1"
* Gothic 2 Develop: "Release_NoOpt"
* Gothic 1 Develop: "Release_NoOpt_G1"

(Note: A real "debug" build is not possible, since mixing debug- and release-DLLs is not allowed, but for the Develop targets optimization is turned off, which makes it possible to use the debugger from Visual Studio with the built DLL when using a Develop target.)

Select the target for which you want to built (if you don't want to create a release, select one of the Develop targets), then build the solution. When the C++ build has completed successfully, the DLL with the built code and all needed files (pdb, shaders) will be copied into the game directory as you specified with the environtment variables.

After that, the game will be automatically started and should now run with the GD3D11 code that you just built.

When using a Develop target, you might get several exceptions during the start of the game. This is normal and you can savely continue to run the game for all of them (press continue, won't work for "real" exceptions of course).
When using a Release target, those same exceptions will very likely stop the execution of the game, which is why you should use Develop targets from Visual Studio and test your release builds by starting Gothic 2 directly from the game folder yourself.

### Producing the Redistributables
- Compile the version that you want (`Release` or `Release_G1`)
- Run `CreateRedistG1` or `CreateRedistG2` depending on which version you compiled.
	- There should now be a `redist_g1` or `redist_g2` directory inside the solution directory.
- To distribute the Renderer, zip the contents of `redist_gX` and let your consumers unzip the contents into their `Gothic\System\` directory.


### Older versions

If you check out the appropriate commits, you can build older versions/commits of GD3D11. All commits on branch "master" since #3183e4d (7 Jun 2016, after 17.2) can be built with Visual Studio 2015.

Since the older commits/version on "master" branch can not be compiled with Visual Studio 2015 without fixing some things, there is a seperate branch "master_vs2015" which contains all commits between 13.0 and the above commit, but a little bit modified, so they actually work with Visual Studio 2015 the same way the newer commits/versions do.

So its very easy to build any version back to 13.0, just make sure to switch to the branch "master_vs2015" for the older commits. Most commits on both "master" as well as "master_vs2015", that represent a released version, are tagged with that version number. This should make it easy to for you to navigate through commits in git.

### Other

- Using HBAO+ files from https://github.com/dboleslawski/VVVV.HBAOPlus/tree/master/Dependencies/NVIDIA-HBAOPlus

### Special Thanks

... to the following people

- @ataulien (Degenerated @ WoG) for creating this project.
- Bonne6 @ WoG for providing the base for this modified version.
- Keks1 @ WoG for testing, helping with conversions and implementing several features.

### License

- HBAO+ is licensed under [GameWorks Binary SDK EULA](https://developer.nvidia.com/gameworks-sdk-eula)
