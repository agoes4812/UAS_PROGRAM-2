# UAS_PROGRAM-2
DATA COVID19
DELETE
<?php  include 'validasi.php'; ?>
<?php 
    include 'koneksi.php';
    
    $idArtikel = $_GET['id'];
    
    $query = mysqli_query($koneksi,"DELETE FROM covid WHERE id='$idArtikel'");
    
    header("location: index.php");

 ?>

EDIT
<?php  include 'validasi.php'; ?>
<?php  include 'koneksi.php';

    $id = $_GET['id'];
    $query = mysqli_query($koneksi, "SELECT * FROM covid WHERE id='$id' ");
    $row = mysqli_fetch_array($query);

?>
<!DOCTYPE html>
<html>
<head>
    <title>Form Artikel</title>
    <link rel="stylesheet" href="style.css">
    <style type="text/css">
    
        *{
                margin: 0;
                padding: 0;
                box-sizing: border-box;
                outline: none;
                font-family: 'Josefin Sans', sans-serif;
            }

        
        #container { 
                width:500px; 
                margin:50px auto; 
                border:0px solid #555; 
                box-shadow:0px 0px 2px #555; 
            }

        input[type="text"]{}
        input[type="text"], input[type=date], textarea { padding:5px; margin:2px 0px; border: 1px solid #777; width:450px;}
        input[type="submit"], input[type="reset"] { padding: 5px 20px; margin:2px 0px; font-weight:bold; cursor:pointer; }

          h1 {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
          }
          form {  
            background-color: #fffdf3;
            padding: 25px;
            border-radius: 10px;
            background-color: beige;
          }
          blockquote {
                font: 2em/1em 'Open Sans', sans-serif;
                -webkit-text-stroke: 1px black;
                text-shadow: 2px 2px #000;
                margin: 20px 0 15px 0;
                color: #fff;
        }

        </style>
</head>
<body>
    <div id="container">
    <center><blockquote>Form Edit Data</blockquote></center>
        
        <form action="prosesedit.php" method="POST">
            <p>
                <input type="hidden" name="idartikel" value="<?= $row['id'];?>"/>
            </p>
            <p>
                <b>nama :</b><br>
                <input type="text" name="nama" value="<?= $row['nama'];?>" />
            </p>
            <p>
                <b>alamat :</b><br>
                <input type="text" name="alamat" value="<?= $row['alamat'];?>" />
            </p>
            <p>
            <b>Provinsi :</b><br>
                <form action="" method="POST">
                    <select name="provinsi">
                        <option>-- PILIH PROVINSI</option>
                    <?php 
                        $sql = mysqli_query($koneksi,"SELECT * from provinsi ");
                        while($data = mysqli_fetch_array($sql)) :?>
                        <option><?= $data['provinsi']; ?></option>
                        <?php endwhile ?>
            </select>
            </p>
            <p>
                <b>email :</b><br>
                <input type="text" name="email" value="<?= $row['email'];?>" />
            </p>
            <p>
                <b>No tlp :</b><br>
                <input type="text" name="hp" value="<?= $row['hp'];?>" />
            </p>
            <p>
                <b>ahli :</b><br>
                <input type="text" name="ahli" value="<?= $row['ahli'];?>" />
            </p>
            
            <p>
                <input type="submit" name="edit" value="Update" class="tombol"/> 
            </p>
        </form>
    </div>
</body>
</html>

INDEX
<?php include 'koneksi.php'; ?>
<?php include 'validasi.php'; ?>
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    <link href="https://fonts.googleapis.com/css?family=Bungee|Bungee+Shade|Covered+By+Your+Grace" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans:800" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="style.css">
    <title>Data Relawan Covid-19</title>
</head>
<style>
        #partyTimeButton {
        background-color: #222;
        width: 60px;
        font-family: 'Bungee', cursive;
        font-size: 13px;
        color: #fff;
        border: none;
        border-radius: 50px;
        padding: 10px 0;
        margin-top: 20px;
        }

        blockquote {
        font: 2em/1em 'Open Sans', sans-serif;
        -webkit-text-stroke: 1px black;
        text-shadow: 2px 2px #000;
        margin: 0px 0 10px 0;
        color: #fff;
        }       
        h4 {
            font-size: 40px;
            font-family: 'Bungee', cursive;
            margin-bottom: 20px;
            margin-top: 10px;
        }
            h1, h2, h3, h6 {
            font-family: 'Bungee Shade', cursive;
            margin-top: 0px;
        }
    *{
                margin: 0;
                padding: 0;
                box-sizing: border-box;
                outline: none;
                font-family: 'Josefin Sans';
            }
    .table-bordered td, .table-bordered th {
    border: 1px solid #dee2e6;
    background: whitesmoke;
    }
</style>
<body style="text-align: center;">

</div>
    <div class="container" style="margin-top: 20px;">
    <blockquote>Data Relawan Covid19 wilayah DKI Jakarta</blockquote>
    <blockquote> Per <?php 
        echo date('d-F-Y')." ";
        echo date('H:i:s e');?></blockquote>        
    <table class="table table-striped table-hover table-sm table-bordered">
        <thead class="thead-dark">
            <tr>
                <th scope="col">Id</th>
                <th scope="col">nama</th>
                <th scope="col">alamat</th>
                <th scope="col">provinsi</th>
                <th scope="col">email</th>
                <th scope="col">hp</th>
                <th scope="col">ahli</th>
                <th scope="col">action</th>
            </tr>
        </thead>
        
        <?php 
        // perintah query untuk menampilkan / mengambil data dari database
        $query = mysqli_query($koneksi, "SELECT * from covid  ORDER BY id desc");
    
        // while digunakan untuk id / no yang menggunakan tipe data int auto increment
        $no = 0;
        while ($data = mysqli_fetch_array($query)) {
            $no++
         ?>
         <tbody>
            <tr>
                <!-- perintah untuk menampilkan data yang sudah diambil dari database ke browser html -->
                <th scope="row"><?= $no; ?></th>
                <td><?= $data['nama'];?></td>
                <td><?= $data['alamat'];?></td>
                <td><?= $data['provinsi'];?></td>
                <td><?= $data['email'];?></td>
                 <td><?= $data['hp'];?></td>
                 <td><?= $data['ahli'];?></td>
                <td>
                    <a href="edit.php?id=<?= $data['id']?>" class="btn btn-primary">Edit</a>
                    <a href="delete.php?id=<?= $data['id']?>" class="btn btn-danger" >Delete</a>
                </td>
            </tr>
         </tbody>
        <?php } ?>
    </table>
    <a href="input.php" class="btn" id="partyTimeButton">input</a>
    <a href="logout.php" class="btn" id="partyTimeButton">logut</a>
    
</div>
</body>
</html>

INPUT
<?php include 'koneksi.php'; ?>
<?php include 'validasi.php'; ?>

<!DOCTYPE html>
<html>
<head>
    <title>Input Data Relawan Covid-19</title>
        <link rel="stylesheet" href="style.css">
    <style type="text/css">
        blockquote {
                font: 2em/1em 'Open Sans', sans-serif;
                -webkit-text-stroke: 1px black;
                text-shadow: 2px 2px #000;
                margin: 20px 0 15px 0;
                color: #fff;
        }
        *{
                margin: 0;
                padding: 0;
                box-sizing: border-box;
                outline: none;
                font-family: 'Josefin Sans', sans-serif;
            }

        #container { 
                width:500px; 
                margin:50px auto; 
                border:0px solid #555; 
                box-shadow:0px 0px 2px #555; 
            }

        input[type="text"]{}
        input[type="text"], input[type=date], textarea { padding:5px; margin:2px 0px; border: 1px solid #777; width:450px;}
        input[type="submit"], input[type="reset"] { padding: 5px 20px; margin:2px 0px; font-weight:bold; cursor:pointer; }

          h1 {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
          }
          form {  
            background-color: #fffdf3;
            padding: 25px;
            border-radius: 10px;
            background-color: beige;
          }
        

        </style>
</head>
<body>

<div id="container" >
<center><blockquote>Input Data Relawan Covid-19</blockquote></center>
        
        <form action="proses.php" method="post">
            <p>
                <b>Nama :</b><br>
                <input type="text" name="nama"/>
            </p>
            <p>
                <b>Alamat :</b><br>
                <input type="text" name="alamat"/>
            </p>

            <p>
                <b>Provinsi :</b><br>
                <form action="" method="POST">
                    <select name="provinsi">
                        <option>-- PILIH PROVINSI --</option>
                    <?php 
                        $sql = mysqli_query($koneksi,"SELECT * from provinsi ");
                        while($data = mysqli_fetch_array($sql)) :?>
                        <option><?= $data['provinsi']; ?></option>
                        <?php endwhile ?>
                </form>
            </select>
            </p>
            <p>
                <b>Email :</b><br>
                <input type="text" name="email"/>
            </p>
            <p>
                <b>No Hp :</b><br>
                <input type="text" name="hp"/>
            </p>
            <p>
                <b>Keahlian :</b><br>
                <input type="text" name="ahli"/>
            </p>
            <p>
                <input type="submit" name="submit" value="Add" class="tombol"/> 
                <input type="reset" name="batal" value="Reset" class="tombol"/>
            </p>
        </form>
    </div>
</body>

</html>
KONEKSI
<?php 
    
    $koneksi = mysqli_connect("localhost","root","","relawan" );

    if (!$koneksi) {
        die("Gagal Terhubung dengan database".mysqli_connect_error());
    }

 ?>
LOGIN
<!DOCTYPE HTML>
<html>
    <head>
    <link href="https://fonts.googleapis.com/css?family=Bungee|Bungee+Shade|Covered+By+Your+Grace" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans:800" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="style.css">
        <title>Halaman Login</title>
        <style>

        blockquote {
            font: 2em/1em 'Open Sans', sans-serif;
            -webkit-text-stroke: 1px black;
            text-shadow: 2px 2px #000;
            margin: -80px 0 100px 0;
            color: #fff;
        }
            
        h4 {
            font-size: 40px;
            font-family: 'Bungee', cursive;
            margin-bottom: 20px;
            margin-top: 10px;
        }
            h1, h2, h3, h6 {
            font-family: 'Bungee Shade', cursive;
            margin-top: 0px;
        }
        .login {
            padding: 2em;
            margin: 8em auto;
            width: 17em;
            background: #fff;
            border-radius: 3px;
        }               
        input[type="password"],
        input[type="text"],
        input[type="email"],
        textarea {
        padding: 8px;
        width: 95%;
        background: #efefef;
        border: 0;
        font-size: 10pt;
        margin: 6px 0px;
        }
        h4 {
            font-size: 40px;
            font-family: 'Bungee', cursive;
            margin-bottom: 20px;
            margin-top: 10px;
        }
        </style>
    </head>
    <body>
    <div class="container">
        <div class="row">
            <div class="col-lg-8 col-sm-12 mx-auto">
            
                <div class="login">
                <center><h4>Login</h4></center>
            <form method="post">
                <input type="text" name="user" placeholder="USER"><br>
                <input type="password" name="pass" placeholder="PASSWORD"><br>
                <input class="btn" type="submit" name="login" id="partyTimeButton" value="Login">
                
            </form>
        </div>  
        
        <?php 
session_start();
    if (isset($_POST['login'])) {
            $user = $_POST['user'];
            $pass = $_POST['pass'];
    if ($user === "dianeka" && $pass == "0000") {
        $_SESSION['login'] = $user;
        echo "<script>alert('Anda Berhasil Login')</script>";
        echo "<center><br><br><blockquote id='timeEvent'><a href='index.php'>Form Data relawan</blockquote></center>";
    }else {
    
    }
}
 ?>
    </body>
</html>
LOGOUT
<!DOCTYPE HTML>
<html>
    <head>
<link href="https://fonts.googleapis.com/css?family=Bungee|Bungee+Shade|Covered+By+Your+Grace" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans:800" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="style.css">
        <title>Halaman Login</title>
        <style>
        blockquote {
            font: 2em/1em 'Open Sans', sans-serif;
            -webkit-text-stroke: 1px black;
            text-shadow: 2px 2px #000;
            margin: -35px 0 100px 0;
            color: #fff;
        }
        .login {
            padding: 2em;
            margin: 8em auto;
            width: 17em;
            background: #fff;
            border-radius: 3px;
        }   
        h4 {
            font-size: 40px;
            font-family: 'Bungee', cursive;
            margin-bottom: 20px;
            margin-top: 10px;
        }
            h1, h2, h3, h6 {
            font-family: 'Bungee Shade', cursive;
            margin-top: 0px;
        }
        </style>
        <body>
<?php 

    session_start();
    if (isset($_SESSION['login'])) {
        unset($_SESSION);
        session_destroy();
        echo "<center>
        <h1>Anda berhasil logout</h1>
        <blockquote>Anda berhasil logout</blockquote>
        <h1>Anda berhasil logout</h1>
        <blockquote>Anda berhasil logout</blockquote>
        <h1>Anda berhasil logout</h1>
        <blockquote>Anda berhasil logout</blockquote>
        <h1>Anda berhasil logout</h1>
        <blockquote>Anda berhasil logout</blockquote>
        <h1>Anda berhasil logout</h1>
        <blockquote>Anda berhasil logout</blockquote>
        ";
        }
    else{
        echo "Silahkan Login Terlebih Dahulu";
    }
 ?>
<?php header( "refresh:5;url=login.php" );?>
</body>
<script>alert('redirecting to login page in 5 second')</script>
</html>
PROSES

<?php   
    include 'koneksi.php';
    

    $nama = $_POST['nama'];
    $alamat = $_POST['alamat'];
    $provinsi = $_POST['provinsi'];
    $email = $_POST['email'];
    $hp = $_POST['hp'];
    $ahli = $_POST['ahli'];


    $query = mysqli_query($koneksi, "INSERT INTO covid VALUES('','$nama', '$alamat', '$provinsi', '$email', '$hp', '$ahli')") or die (mysqli_error($koneksi,$query));

    if ($query) {
        header("location: index.php");
            }else{
        echo "<h2 align=center>Proses Penginputan gagal</h2>";
    }
 ?>

PROSESEDIT
<?php
include "koneksi.php";

        $ID = $_POST['idartikel'];
        $nama = $_POST['nama'];
        $alamat = $_POST['alamat'];
        $provinsi = $_POST['provinsi'];
        $email = $_POST['email'];
        $hp = $_POST['hp'];
        $ahli = $_POST['ahli'];
        

        $update="UPDATE covid  SET nama='$nama', alamat='$alamat', provinsi='$provinsi', email='$email', hp='$hp', ahli='$ahli' WHERE id='$ID'";
        
        $hasil=mysqli_query($koneksi,$update);

            if ($hasil) {
                header("location: index.php");
            } else {
                echo "Artikel gagal di update";
            }
?>


VALIDASI
<!DOCTYPE HTML>
<html>
    <head>
<link href="https://fonts.googleapis.com/css?family=Bungee|Bungee+Shade|Covered+By+Your+Grace" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans:800" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="style.css">
        <title>Halaman Login</title>
        <style>
        .login {
            padding: 2em;
            margin: 8em auto;
            width: 17em;
            background: #fff;
            border-radius: 3px;
        }               
        
        h4 {
            font-size: 40px;
            font-family: 'Bungee', cursive;
            margin-bottom: 20px;
            margin-top: 10px;
        }
        blockquote {
            font: 2em/1em 'Open Sans', sans-serif;
            -webkit-text-stroke: 1px black;
            text-shadow: 2px 2px #000;
            margin: 0px 0 100px 0;
            color: #fff;
        }
        h1, h2, h3, h6 {
            font-family: 'Bungee Shade', cursive;
            margin-top: 150px;
        }
        </style>
        <body>

<?php
session_start();
//pemeriksaan session
if (isset($_SESSION['login'])) {
//jika sudah login
//menampilkan isi session

echo "<center><blockquote>Selamat Datang ". $_SESSION['login'] ."</blockquote></center><br>";
} else {
//session belum ada artinya belum login
die ("<center><br><br><blockquote>Anda belum login! Anda tidak berhak masuk ke halaman
ini
<br>Silahkan login <a href='login.php'>di sini</a></blockquote></center>"); 
}
 ?>
 </body>
</html>
