<?php

//create database connection
$host = "localhost";
$dbname = "espi8884";
$username = "espi8884";
$password = "secret";

//establishes database connection
$dbConn = new PDO("mysql:host=$host;dbname=$dbname", $username, $password);

//shows errors when connecting to database
$dbConn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION); 

$sql = "SELECT deathID 
        FROM deathmembers ";

$stmt = $dbConn -> prepare($sql);
$stmt -> execute();
$deathNames = $stmt->fetchAll();

if (isset ($_GET['deathID'])) {
   $deathID = $_GET['deathID'];
   $sql = "SELECT * 
           FROM deathmembers 
           WHERE deathID = :deathID ";
        
   $stmt = $dbConn -> prepare($sql);
   $stmt -> execute( array (':deathID' => $deathID));
   $deathInfo = $stmt->fetch();
}

?>

<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">

    <title>Freeman Funeral Home</title>

    <!-- Bootstrap Core CSS -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom CSS -->
    <link href="css/business-casual.css" rel="stylesheet">

    <!-- Fonts -->
    <link href="http://fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,600italic,700italic,800italic,400,300,600,700,800" rel="stylesheet" type="text/css">
    <link href="http://fonts.googleapis.com/css?family=Josefin+Slab:100,300,400,600,700,100italic,300italic,400italic,600italic,700italic" rel="stylesheet" type="text/css">

    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->

</head>

<body>

    <div class="brand">Freeman Funeral Home</div>
    <div class="address-bar">3481 Lake Drive | Metro, CA 95351 | 123.456.7890</div>

    <!-- Navigation -->
    <nav class="navbar navbar-default" role="navigation">
        <div class="container">
            <!-- Brand and toggle get grouped for better mobile display -->
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                <!-- navbar-brand is hidden on larger screens, but visible when the menu is collapsed -->
                <a class="navbar-brand" href="index.html">Freeman Funeral Home</a>
            </div>
            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav">
                    <li>
                        <a href="index.html">Home</a>
                    </li>
                    <li>
                        <a href="about.html">About</a>
                    </li>
                    <li>
                        <a href="blog.html">Search</a>
                    </li>
                    <li>
                        <a href="contact.html">Contact</a>
                    </li>
                </ul>
            </div>
            <!-- /.navbar-collapse -->
        </div>
        <!-- /.container -->
    </nav>

    <div class="container">

        <div class="row">
          
               
                        <div class="box">
                        
                        	<img class="img-responsive img-full" src="img/slide-3.jpg" alt="">

                    <h2 class="brand-before">
                        <small>Welcome to</small>
                    </h2>
                    <h1 class="brand-name">Freeman Funeral Home</h1>
                    <hr class="tagline-divider">
                   
                     </div>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="box">
                <div class="col-lg-12">
                    <hr>
                    <h2 class="intro-text text-center">Search                        <strong>People</strong>
                    </h2>
             <form>

         <select name="deathID">
           <option value="-1"> - Select -</option>
           <?php
                foreach ($deathNames as $death) {
                    echo "<option  value=" . $death['deathID'] . ">" . $death['deathID'] . "</option>";
                }         
             
           ?>   
         </select>
         <input type="submit" value="Get Info!" />
     </form>
     
      <?php
    
        if (isset($deathInfo) && !empty($deathInfo)) {
            echo $deathInfo['FirstName'] . "<br />";
            echo $deathInfo['LastName'] . "<br />";
			echo $deathInfo['Gender'] . "<br />";
			echo $deathInfo['Birthdate'] . "<br />";
			echo $deathInfo['Died'] . "<br />";
			echo $deathInfo['CauseOfDeath'] . "<br />";
			echo $deathInfo['Cemetary'] . "<br />";
            echo $deathInfo['City'] . ", " . $deathInfo['State'] . " " . $deathInfo['Zip']  . " <br />";
        }
    
    ?>
     <?php
    
    $dbConn = null; //closes the database connection.
    
    ?>

  
                </div>
            </div>
        </div>
    </div> 
    <!-- /.container -->

    <footer>
        <div class="container">
            <div class="row">
                <div class="col-lg-12 text-center">
                    <p>Copyright &copy; Freeman Funeral Home 2015</p>
                </div>
            </div>
        </div>
    </footer>

    <!-- jQuery -->
    <script src="js/jquery.js"></script>

    <!-- Bootstrap Core JavaScript -->
    <script src="js/bootstrap.min.js"></script>

    <!-- Script to Activate the Carousel -->
    <script>
    $('.carousel').carousel({
        interval: 5000 //changes the speed
    })
    </script>

</body>

</html>

