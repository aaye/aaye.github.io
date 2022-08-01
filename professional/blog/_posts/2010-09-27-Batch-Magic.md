---
layout: blogpost
title: Batch Magic
date: 2010-09-27
categories: [script]
music: Jewel - 0304
---
I have always had only a fairly loose grasp on the DOS batch language. Whenever, I needed to do something I would spent large amounts of time either with the old DOS manuals or later on, online looking for examples. I only ever used it lightly, primarily because I rarely needed to do anything in DOS itself. However, while working at Obsidian, the Chief Technology Office (Chris Jones) wrote the initial build system in DOS batch and I ended up having to debug, maintain and extend the system. It was interesting and sometimes challenging to get the language to do what I wanted. Thankfully, the command line interpreter in NT has some really useful extensions to the standard DOS batch that making using it a little easier. For my own sanity here is an example set of batch files that I use for processing all of the files in my source tree to generate the resulting html found in this web page.

<!--more-->

**update_web.bat**
@echo off

set BATCH_WEB_ROOT_PATH=%CD%\web
set BATCH_ROOT_PATH=%CD%
call process_directory "%CD%" "inc"
call process_directory "%CD%" "src"
set BATCH_ROOT_PATH=
set BATCH_WEB_ROOT_PATH=




**process_files.bat**
@REM Execute the command in the first parameter for all files
@REM giving the file as the source - and its parallel web
@REM location as the dest
FOR %%F in ("*.*") DO (
    %1 "%%~nxF" "%BATCH_WEB_ROOT_PATH%\%%~nxF"
)

**process_directory.bat**
@REM Check to see if the web path exist parallel to the
@REM directory, create it, and store it for the file batch
if not exist "%BATCH_WEB_ROOT_PATH%"
    mkdir "%BATCH_WEB_ROOT_PATH%"
pushd "%BATCH_WEB_ROOT_PATH%"
if not exist %2 mkdir %2
set BATCH_WEB_ROOT_PATH=%CD%\%~2
popd

@REM Recursively execute this batch for all directories
pushd %2
FOR /D %%F in (*.*) DO (
    call "%BATCH_ROOT_PATH%\process_directory.bat" %1 "%%~xnF"
)

@REM Process this directory
call "%BATCH_ROOT_PATH%\process_files.bat" <insert command here>
popd

@REM Restore the previous web root
pushd "%BATCH_WEB_ROOT_PATH%"
cd ..
set BATCH_WEB_ROOT_PATH=%CD%
popd

