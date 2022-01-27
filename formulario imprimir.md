# INTERFAZ DEL FORMULARIO

```powershell

Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
 
#Crear un formulario, añadir una etiqueta, dos botones y una caja de texto
#Funcionalidad para el formulario:
#Pulsar la tecla Enter almacena en una variable el contenido de la caja de texto y se muestra
#Pulsar la tecla Escape sale del formulario
 



#Formulario
$Form = New-Object System.Windows.Forms.Form
$Form.Text="TRABAJO Nº3"
$Form.Size=New-Object System.Drawing.Size(500,500)
$Form.StartPosition="CenterScreen"
 
#Etiqueta
$Label=New-Object System.Windows.Forms.Label
$Label.Text="IMPRIMIR LO QUE HAY EN LA CARPETA DE UPLOADS"
$Label.AutoSize=$True
$Label.Location=New-Object System.Drawing.Size(20,40)
 

 
#Botón1
$Button1=New-Object System.Windows.Forms.Button
$Button1.Size=New-Object System.Drawing.Size(75,23)
$Button1.Text="Imprimir"
$Button1.Location=New-Object System.Drawing.Size(50,100)
 

#Botón2
$Button2=New-Object System.Windows.Forms.Button
$Button2.Size=New-Object System.Drawing.Size(75,23)
$Button2.Text="Cerrar"
$Button2.Location=New-Object System.Drawing.Size(50,130)


#Botón3
$Button3=New-Object System.Windows.Forms.Button
$Button3.Size=New-Object System.Drawing.Size(180,23)
$Button3.Text="EXPLORADOR DE ARCHIVOS"
$Button3.Location=New-Object System.Drawing.Size(50,70)

#Botón4
$Button4=New-Object System.Windows.Forms.Button
$Button4.Size=New-Object System.Drawing.Size(200,25)
$Button4.Text="¿Cómo funciona este formulario?"
$Button4.Location=New-Object System.Drawing.Size(160,160)

 
#Funcionalidad para el formulario:
#Pulsar la tecla Enter almacena en una variable el contenido de la caja de texto y se muestra
#Pulsar la tecla Escape sale del formulario
$Form.KeyPreview = $True
$Form.Add_KeyDown({if ($_.KeyCode -eq "Enter"){

foreach ($archivo in Get-ChildItem "C:\xampp\htdocs\uploads")
{$nombre=$archivo.Name
$ruta="C:\xampp\htdocs\impresiones\" + "$nombre"
$rutanombre=(get-date).Ticks
Start-Process -FilePath($archivo|select fullname).fullname-Verb print 
Start-Sleep -Seconds 5
[System.Windows.Forms.SendKeys]::SendWait("{ENTER}")
Start-Sleep -Seconds 2
[System.Windows.Forms.SendKeys]::SendWait($ruta + $rutanombre)
Start-Sleep -Seconds 2
[System.Windows.Forms.SendKeys]::SendWait("{ENTER}")
Start-Sleep -Seconds 2 

Remove-Item  "C:\xampp\htdocs\uploads\$archivo"}

}})
$Form.Add_KeyDown({if ($_.KeyCode -eq "Escape"){$Form.Close()}})
 
#Funcionalidad para el botón:
#Pulsar Enter almacena en una variable el contenido de la caja de texto y se muestra
#Pulsar Escape sale del formulario
$Button1.Add_Click({

foreach ($archivo in Get-ChildItem "C:\xampp\htdocs\uploads")
{$nombre=$archivo.Name
$ruta="C:\xampp\htdocs\impresiones\" + "$nombre"
$rutanombre=(get-date).Ticks
Start-Process -FilePath($archivo|select fullname).fullname-Verb print 
Start-Sleep -Seconds 5
[System.Windows.Forms.SendKeys]::SendWait("{ENTER}")
Start-Sleep -Seconds 2
[System.Windows.Forms.SendKeys]::SendWait($ruta + $rutanombre)
Start-Sleep -Seconds 2
[System.Windows.Forms.SendKeys]::SendWait("{ENTER}")
Start-Sleep -Seconds 2 

Remove-Item  "C:\xampp\htdocs\uploads\$archivo"}

})
$Button2.Add_Click({$Form.Close()})
$Button3.Add_Click({explorer.exe "C:\xampp\htdocs\uploads\"})
$Button4.Add_Click({Function Mostrar-MensajeCuadroDialogo {
Param
(
[string]$Mensaje, 
[string]$Titulo, 
[System.Windows.Forms.MessageBoxButtons]$Botones, 
[System.Windows.Forms.MessageBoxIcon]$Icono
)
    return [System.Windows.Forms.MessageBox]::Show($Mensaje, $Titulo, $Botones, $Icono)
}

Mostrar-MensajeCuadroDialogo -Mensaje "-BOTON EXPLORAR: Abre el exploarador de archivos para mandar lo que sea a la carpeta de uploads.`n`n-BOTON IMPRIMIR:Imprime lo que hay en la carpeta de uploads, las borra y las envia a otra carpeta.`n`n-BOTON CANCELAR: Cierra el formulario." -Titulo "Indice" -Botones  OK -Icono information
})

 
#Añadir etiqueta
$Form.Controls.Add($Label)
 
#Añadir botones
$Form.Controls.Add($Button1)
$Form.Controls.Add($Button2)
$Form.Controls.Add($Button3)
$Form.Controls.Add($Button4)


 
#Añadir caja de texto
#$Form.Controls.Add($TextBox)
 
$Form.ShowDialog()


```

## FUNCIONALIDAD DE LOS BOTONOS
