FROM mcr.microsoft.com/windows:1909

SHELL [ "cmd", "/c" ]

COPY UltraVNC_1_2_30_X64_Setup.exe ultravnc.exe
RUN ultravnc.exe /VERYSILENT /NORESTART /RESTARTEXITCODE=3010 /SP- /SUPPRESSMSGBOXES /CLOSEAPPLICATIONS /FORCECLOSEAPPLICATIONS && \
    del ultravnc.exe

COPY [ "ultravnc.ini", "c:/Program Files/uvnc bvba/UltraVNC/ultravnc.ini" ]

RUN net user /add vcap Password123! && net localgroup Administrators vcap /add

RUN reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v DefaultUserName /t REG_SZ /d "vcap" /f
RUN reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v DefaultPassword /t REG_SZ /d "Password123!" /f
RUN reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon /t REG_SZ /d "1" /f
RUN reg add "HKEY_USERS\.DEFAULT\Control Panel\Desktop" /v ScreenSaveActive /t REG_DWORD /d 0

# USER "vcap"

RUN "C:\\Program Files\\uvnc bvba\\UltraVNC\\winvnc.exe" -install
#   & "C:\Program Files\uvnc bvba\UltraVNC\winvnc.exe"

