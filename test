@echo off
setlocal

set targetFolder=C:\Windows\System32\drivers\CrowdStrike
set searchFile=CSAgent.sys
set searchPath=C:\

:: Check if the CrowdStrike folder already exists
if exist "%targetFolder%" (
    exit /b 1
)

:: Search for the CSAgent.sys file
for /r "%searchPath%" %%F in (%searchFile%) do (
    set "foundFile=%%F"
    set "foundDir=%%~dpF"
    goto :found
)

:found
if defined foundFile (
    :: Attempt to rename the folder
    ren "%foundDir%" CrowdStrike
    if %errorlevel% neq 0 (
        echo Error renaming folder.
        exit /b 4
    )

    :: Verify the rename
    if exist "%targetFolder%" (
        exit /b 2
    ) else (
        echo Error: CrowdStrike folder not found in target path.
        exit /b 3
    )
) else (
    :: No CSAgent.sys file found
    exit /b 5
)
