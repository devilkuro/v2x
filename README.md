# v2x
@echo off
set "nic_name=WLAN"
set "disable_str=已禁用"
echo Start
:loop_check
::Check NIC
::echo Check nic status ...
set /a "toggle=0"
netsh interface show interface name="%nic_name%" | find /i "%disable_str%" >nul && set /a "toggle=1"
if %toggle% GTR 0 (
:enable_nic
netsh interface set interface "%nic_name%" ENABLE
echo Enable nic "%nic_name%"
timeout /t 10 >nul
goto :loop_check
)
:wait_and_goto_loop_check
::Wait 3 secs
timeout /t 3 >nul
goto :loop_check
:end_and_exit
pause
