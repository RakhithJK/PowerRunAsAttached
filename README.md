# PowerRunAsAttached

**PowerRunAsAttached** is a ported version of [RunAsAttachedLocal](https://github.com/DarkCoderSc/run-as-attached-local) in Powershell with inline CSharp.

This script allows to spawn a new interactive console as another user account in the same calling console (console instance/window).

One possible example is that this tool gives you with ease the possibility to do vertical / horizontal privilege escalation through your already established Netcat / WinRM session.

## Usage

You can use this script both as a PowerShell Module or Raw Script (Pasted, from Encoded Base64 String, DownloadString(...) etc...).

### As a Module

Choose a registered PowerShell Module location (see echo $env:PSModulePath)

Create a folder called PowerRunAsAttached and place the PowerRunAsAttached.psm1 file inside the new folder.

Open a new PowerShell Window and enter Import-Module PowerRunAsAttached

The module should be imported with available functions:

* Invoke-RunAsAttached

### As a Raw Script

You can import this script alternatively by:

* Pasting the whole code to a new PowerShell window
* `. .\PowerRunAsAttached`
* Importing a Base64 encoded version of the code through IEX/Invoke-Expression
* Remote Location through DownloadString(...) then IEX/Invoke-Expression
* Your imagination

## Available Commands

### `Invoke-RunAsAttached`

Run a new `cmd.exe` as another user.

Notice, it starts `cmd.exe` by default, but you can replace it with `powershell.exe` or even add an extra argument to the function to support another shell. You can anyway run `powershell.exe` from `cmd.exe`. What I like to call shell inception is perfectly supported.

#### Parameters

* `Username` (MANDATORY): A Valid Microsoft Windows User Account
* `Password` (MANDATORY): Associated account password

##### Example

`Invoke-RunAsAttached -Username "darkcodersc" -Password "testmepliz"`

![Example](images/example.png)

## Demo Video

https://www.youtube.com/watch?v=n71apwuPZYw

## CSharp Version: `SharpRunAsAttached`

You will find a version of this project in pure C# [HERE](https://gist.github.com/DarkCoderSc/60a18484fbda7bbb2a1ec0f2b1d42cb7#file-sharprunasattached-cs)

## Pure PowerShell Version Notes

At first place, my goal was to create a pure PowerShell version of that script (without inline CSharp) but I faced multiple difficulties mostely because of Asynchronous Reading Operation issues and lack of threading functionalities that would fit my needs.

The difficulty I faced was caused by my need to read both `Stdout` / `Stderr` in parallel of waiting for user input. Briefly, making the whole thing interactive was a huge pain in pure Powershell.

### Update 20 December 2021

I finally managed to do something stable in pure powershell. You will find it in the folder `PowerRunAsAttached` as `PowerRunAsAttached_PSOnly.psm1`

The `Stderr` handling works pretty nicely now but it is not yet perfect.
