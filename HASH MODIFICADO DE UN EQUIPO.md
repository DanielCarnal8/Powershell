# COMPROBAR SI EL HASH DE UN PROGRAMA DE UN EQUIPO ES IGUAL QUE EL DE MI ORDENADOR (PARA VER QUE ESTE NO HA SIDO MODIFICADO).

## PRIMERO CONECTARSE A SQL
```powershell
[void][System.Reflection.Assembly]::LoadWithPartialName("MySql.Data")
$Connection = ([MySql.Data.MySqlClient.MySqlConnection]::new("server=" + "localhost" + ";port=3306;uid=" + "usuario" + ";pwd=passwordsecreto" + ";database="+"powershell1"+";SslMode=none"))
$Connection.Open()
```

## SEGUNDO REALIZAR UN INSERT INTO EN LA TABLA PARA METER EL HASH DE TU ORDENADOR 
```powershell
$nombredehash = (Get-FileHash C:\Windows\system32\notepad.exe).HASH
$programa = "notepad.exe"

$Query = 'INSERT INTO hash (HASH,PROGRAMA) VALUES ("'+$nombredehash+'","'+$programa+'");'
$Command = New-Object MySql.Data.MySqlClient.MySqlCommand($Query, $Connection)
$DataAdapter = New-Object MySql.Data.MySqlClient.MySqlDataAdapter($Command)
$DataSet = New-Object System.Data.DataSet
$RecordCount = $dataAdapter.Fill($dataSet, "data")
$DataSet.Tables[0]

$Connection.Close()
```
## REALIZAR UNA QUERY PARA VER QUE SE HA METIDO CORRECTAMENTE EL HASH
```powershell
$Query = 'select * from hash;'
$Command = [MySql.Data.MySqlClient.MySqlCommand]::new($Query, $Connection)
$DataAdapter = [MySql.Data.MySqlClient.MySqlDataAdapter]::new($Command)
$DataSet = [System.Data.DataSet]::new()
$DataAdapter.Fill($DataSet)
$DataSet.Tables
```
## SACAR DE FORMA REMOTA EL HASH DEL OTRO EQUIPO
```powershell
$w10 = Invoke-Command -ScriptBlock { (Get-FileHash C:\Windows\system32\notepad.exe).HASH } -ComputerName "DESKTOP-OJRROSB"
```
## COMPROBAR SI EL HASH COINCIDE CON EL DE NUESTRO ORDENADOR
```powershell
if (($DataSet.Tables).hash -eq $w10 ) 
{
    "hash está bien"


} else
{
 "hash está mal"
}
```
