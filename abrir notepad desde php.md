
# ABRIR DESDE UN HTML NOTEPAD

## PHP INTERNO CON HTML

```php

<?php

$salida = shell_exec("powershell -encodedcommand cwB0AGEAcgB0ACAAbgBvAHQAZQBwAGEAZAA=");
echo $salida;

?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <style>
            h1{text-align: center;}
            body{background-color: rgb(181, 233, 235);}
            button{background-color: rgb(236, 159, 44);
                    position: relative;
                    left: 47%;}
    </style>
    <div class="formulario">
        <h1 class="tit">INICIAR UN PROCESO <br> </h1>
        

            <form action=<?php echo $_SERVER['PHP_SELF'] ?> method="post">
            <button type="submit"  formmethod="post">Notepad</button>

            
            
    </div>


</body>
</html>

```
![Captura1](https://user-images.githubusercontent.com/72084639/143288068-23396049-1b7b-4370-9fca-d98ae6cc95dc.PNG)

