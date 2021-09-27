## Como saber que usuario es administrador. Uso de una función:
```powershell
function usu($usuario)
{
$usuario
Get-LocalGroupMember administradores | where name -Match  $usuario
}

usu pepe
```
## Cambiar contraseña a usuarios:

```powershell
$pass2=ConvertTo-SecureString "Pa$$word" -asplaintext -force
Set-LocalUser -Name pepe -Password $pass2

```
## Eliminar usuarios(paa esto hay que ejecutar PS como admin):
```powershell 
Remove-LocalUser pepe

```

## Crear usuarios
```powershell
New-LocalUser -Name "pepe" -Description "Adminitrador desde 2018" -NoPassword

Name    Enabled  Description
----    -------  -----------
pepe  True     Adminitrador desde 2018.
```
