## FUNCIÓN PARA DARME LOS PROCESOS QUE TENGAN MENOS DE UN VALOR DE CPU

```Powershell
#Primero hago la función
 function ConsumoDeLosProcesosDelPC ($parametro,$valordecpu) 
 
 #$parametro lo utilizo para referirme a CPU y $valordecpu para que salgan procesos con cpu menor que ese número.
{
$parametro
$valordecpu

    Get-Process  | Where-Object $parametro -LT $valordecpu
}

#Pongo el nombre de la función, acompañado primero de $parametro y seguido de $valorcpu
ConsumoDeLosProcesosDelPC CPU 50 

```
## SACAR LOS PRIMEROS X PROCESOS Y QUE ESTOS SE GUARDEN EN UN FICHERO .TXT

```Powershell

$var = 7
Get-Process | select -first $var | Out-File fichero.txt

```
## Obtener el nombre de un proceso y sus hilos
```Powershell
foreach($proceso in Get-Process)
{
    $proceso.Name
    $proceso.Threads.Count
    Start-Sleep -Seconds 5
}
```
