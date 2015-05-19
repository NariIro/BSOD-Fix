@echo off
:: Ghost typer
setlocal enableextensions enabledelayedexpansion

set lines=8


set "line1=**********************************************************************"
set "line2=**********************************************************************"
set "line3=**Welcome to the WolfRoms BSOD (Black Screen Of Death) Fixer.       **"
set "line4=**                                                                  **"
set "line5=**             Http://www.wolfroms.com                              **"
set "line6=**                wolfroms@gmail.com                                **"
set "line7=**********************************************************************"
set "line8=**********************************************************************"


for /f %%a in ('"prompt $H&for %%b in (1) do rem"') do set "BS=%%a"

for /L %%a in (1,1,%lines%) do set num=0&set "line=!line%%a!"&call :type

pause>nul
goto :EOF

:type
set "letter=!line:~%num%,1!"
set "delay=%random%%random%%random%%random%%random%%random%%random%"
set "delay=%delay:~-5%"
if not "%letter%"=="" set /p "=a%bs%%letter%" <nul

:: adjust the 3 in the line below: higher is faster typing speed

for /L %%b in (1,5,%delay%) do rem
if "%letter%"=="" echo.&goto :EOF
set /a num+=1
goto :type

:welcome
echo ***************************************************************
echo **Welcome to the WolfRoms BSOD (Black Screen Of Death) Fixer.**
echo **                                                           **
echo **Http://www.wolfroms.com                                    **
echo ***************************************************************
Pause
cls
echo This tool will walk you thru the steps required to get your Nexus 5 Back up and running incase you happened to flash the wrong kernel and you only have a black screen
Pause
cls
echo Please make sure you have ALL drivers installed before running this tool
Pause
cls
goto :welcome
:start
echo ***************************************************************
echo **Welcome to the WolfRoms BSOD (Black Screen Of Death) Fixer.**
echo **                                                           **
echo **Http://www.wolfroms.com                                    **
echo ***************************************************************
echo -Begin (Start BSOD fix.)
echo -Reboot 1 (Reboot into Recovery mode.)
echo -Reboot 2 (Reboot Into Bootloader.)
echo -Donate (Donate to me if this helped.)
echo -XDA (Go to the XDA forum page for questions.)
echo -Check (Check adb devices)
echo.
set /p Program= Select your Option.
goto %Program%



:Begin
echo This will begin the BSOD fix process
pause
PATH=%PATH%;"%SYSTEMROOT%\System32"
adb shell
pause
su
dd if="/dev/block/mmcblk0p11" of="/dev/block/mmcblk0p6
fastboot flash bootloader bootloader-hammerhead-hhz12f.img
pause
fastboot flash radio radio
cls
goto :start
pause
cls
goto :start


:Reboot 1
echo This will reboot your device for the first time
pause
PATH=%PATH%;"%SYSTEMROOT%\System32"
adb reboot recovery 
pause
cls
goto :start


:Reboot 2
echo This will reboot your device into bootloader
tools\fastboot.exe reboot bootloader
pause
cls
goto :start


:Donate
start chrome http://forum.xda-developers.com/donatetome.php?u=3742830
cls
goto :start

:XDA
start chrome http://forum.xda-developers.com/google-nexus-5/help/guide-how-to-fix-bsod-bootloader-t2763370
pause
cls
goto :start

:check
\tools\fastboot.exe adb devices
pause
cls
goto :start



