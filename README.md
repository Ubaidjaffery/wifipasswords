# Wi-Fi Password Extractor

# Script Descrption
Wi-Fi Password Extractor is a Windows based script specifically designed for Windows 7 , 10 operating system. this script execute a command called "Netsh". and in the loop statement it actually captures all the stored password in clear text from the system.


# Wi-fi Batch Script
@echo off
setlocal enabledelayedexpansion
for /f "tokens=2 delims=:" %%a in ('netsh wlan show profile') do (
	set "ssid=%%~a"
	call :getpwd "%%ssid:~1%%"
)
:getpwd
set "ssid=%*"
for /f "tokens=2 delims=:" %%i in ('netsh wlan show profile name^="%ssid:"=%" key^=clear ^|findstr /C:"Key Content"') do (
	echo Wi-Fi Name: %ssid% Password: %%i 
	echo Wi-Fi Name: %ssid% >> StoredPasswords.txt && echo Password: %%i >> StoredPasswords.txt  
)

setlocaldelayedexpansion: Delayed Expansion will cause variables within a batch file to be expanded at execution time rather than at parse time.
%%~a: stores a result in the veriable.
~1%% : %1 is the first argument form the invoking command line.
:getpw: a function that actually extract the stored Wi-fi passwords with the help of their SSID.

# Testing Environment 
Microsoft Windows 7 (Professional, Home, Enterprise)
Microsoft Windows 10 (Professional, Enterprise E3-E5, Education)
