#Si quieres que tu carpeta tenga un nombre distinto luego de ser bloqueada 
#debes cambiar --> Control Panel.{21EC2020-3AEA-1069-A2DD-08002B30309D} <-- que Esta 
#es el nombre por defecto una vez bloqueda, eso solo si queres acceder a ella sin la clave o la hayas olvidado
#Recomendo una vez cambiado lo necesario combertir en archivo .bat a .exe
#con bat_to_exe_convert o alguno similar que lo permita

cls
@ECHO OFF

set "folder= Nombre De Tu Carpeta Aqui"
set "passw= Tu Contrasena Aqui"
if EXIST "Control Panel.{21EC2020-3AEA-1069-A2DD-08002B30309D}" goto UNLOCK
if NOT EXIST %folder% goto MDLOCKER
:CONFIRM
echo Esta Seguro de que quiere proteger la Carpeta(S/N)
set/p "cho=>"
if %cho%==S goto LOCK
if %cho%==s goto LOCK
if %cho%==n goto END
if %cho%==N goto END
echo Seleccion invalida.
goto CONFIRM
:LOCK
ren %folder% "Control Panel.{21EC2020-3AEA-1069-A2DD-08002B30309D}"
attrib +h +s "Control Panel.{21EC2020-3AEA-1069-A2DD-08002B30309D}"
echo %folder%, carpeta protegida con exito
goto End
:UNLOCK
echo Ingrese su Contrasena para proteger su carpeta
set/p "pass=>"
if NOT %pass%== %passw% goto FAIL
attrib -h -s "Control Panel.{21EC2020-3AEA-1069-A2DD-08002B30309D}"
ren "Control Panel.{21EC2020-3AEA-1069-A2DD-08002B30309D}" %folder%
echo Carpeta desbloqueada con exito
goto End
AIL
echo Contrasena invalida
goto end
:MDLOCKER
md %folder%
echo %folder%, carpeta creada con exito
goto End
:End