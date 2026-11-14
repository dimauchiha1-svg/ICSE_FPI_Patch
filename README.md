[README.md](https://github.com/user-attachments/files/34856098/README.md)
# Improved Camera SE: First Person Interactions fix

Makes the animations of **First Person Interactions** (by GiraPomba) visible with **Improved Camera SE**.

## The problem

First Person Interactions plays its interaction animations (looting, doors, lockpicking, harvesting, and so on) on the
**first person arms**. Improved Camera SE shows the **third person arms** of your body whenever no weapon is drawn, and hides
the first person arms. So the animation plays, but on arms that are not shown, and your visible arms do not move.

## What the fix does

First Person Interactions sets the animation graph variable `bOffsetGPMA` while one of its animations is playing. The fix
reads that variable. While it is set, Improved Camera shows the first person arms and hides the third person arms, the same
way it already does for the "TakeItem" animation of Animated Interactions. Nothing changes when the variable is not set.
The first and last frame of every animation is written to `ImprovedCameraSE.log` ("FirstPersonInteractions: first person arm animation started/ended").

The change is in one file (`patches/fpi-first-person-arms.patch`, 31 added lines, nothing removed).

## Building it

1. Create a new repository on GitHub and upload the contents of this folder (including the hidden `.github` folder).
2. Open the **Actions** tab, choose **Build Improved Camera SE with the First Person Interactions fix**, press **Run workflow**.
3. When it finishes, download the artifact `ImprovedCameraSE-FPI-fix` and take `SKSE/Plugins/ImprovedCameraSE.dll` from it.
4. Replace the DLL of Improved Camera SE with it (in Mod Organizer 2, put it into a separate mod below Improved Camera,
   or overwrite the file). Your settings and profiles stay as they are.

The workflow builds the official source at commit `2e441c1` (the 2025-08-31 version) plus the patch.
It needs a Windows runner with Visual Studio 2022; GitHub provides one for free.

## License and sharing

Improved Camera SE is licensed under MPL 2.0. The patch modifies one source file, so the modified source is this patch plus the
original repository. The Nexus page of Improved Camera asks not to share modified files without the author's permission,
so keep the built DLL for yourself, and if it works, send the patch to ArranzCNL (a pull request to
https://github.com/ArranzCNL/ImprovedCameraSE-NG) instead of uploading a DLL.
