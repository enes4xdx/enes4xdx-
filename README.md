# enes4xdx-
Git clone https://github.com/enes4xdx/enes4xdx.git
Git clone https://github.com/enes4xdx/enes4xdx
<?php
error_reporting(0);
include("config2.php");
include("info.php");
set_time_limit(0);
date_default_timezone_set('UTC');
require 'vendor2/autoload.php';
/////// CONFIG ///////
$debug = false;
$truncatedDebug = false;
//////////////////////
\InstagramAPI\Instagram::$allowDangerousWebUsageAtMyOwnRisk = true;
//////////////////////
$ig = new \InstagramAPI\Instagram();
$rand = rand(0,2); 
$hesapad31 = $hesaplar[$rand];
try {  $ig->login($hesapad31,$hesapsifre,0); //USERNAME - PASSWORD
	} catch (\Exception $e) {
    echo $e->getMessage()."\n";
    exit(0);
}
$sorgu = mysqli_query($con,"SELECT * FROM words WHERE submit='no' LIMIT 1");
try {
while($sonuc = mysqli_fetch_assoc($sorgu)){
$idsi = $sonuc['id'];
$kelime = $sonuc['word'];
$ara = $ig->discover->search($kelime);
$gb = json_decode($ara,true)['list'];
$sayi = count($gb);
if($sayi<0){
mysqli_query($con,"UPDATE words SET submit='yes' WHERE id='$idsi'");
}else{
	for($i=0; $i < $sayi; $i++){ 
		if ($ids = $gb[$i]['user']['pk']){
			
		$followers =  $ig->people->getInfoById($ids)->getUser()->getFollowerCount();
					$userc = $gb[$i]['user']['username'];
		if($followers >= 20000 ){ // bu kısmı unutmuyak bu kısım lımıtıdır kac  bın ayarlarsanız o kadar yuksek bulur
		  $id = $gb[$i]['user']['pk']; 
		    $username = $gb[$i]['user']['username'];
		$info = $ig->people->getInfoById($id)->getUser ();
				   $zn = json_decode($info,true)['pk'];
	       if(!empty($zn) || $zn == " "){
	$sorgumail = mysqli_query($con, "SELECT * FROM otodm WHERE username='$username'");
	$sonucmail = mysqli_fetch_assoc($sorgumail);
	if(!$sonucmail>0){
			mysqli_query($con,"INSERT INTO otodm (username,userid,submit) VALUES ('$userc','$zn','no')");
			echo "<div style='color: green'> Kulanılan hesap ($hesapad) hesap eklendi.  [$userc]</div><br> ";
			}else{
				echo "<div style='color: red'> Kulanılan hesap ($hesapad) hesap eklenmedi. [$userc]</div> <br>";
			}
	}
}else {echo " <div style='color: red'> Kulanılan hesap ($hesapad) Kullanıcı adı => [$userc] </div><br>"; }
		
		}
			
		
}
mysqli_query($con,"UPDATE words SET submit='yes' WHERE id='$idsi'");
}
}
	$sorg = mysqli_query($con,"SELECT * FROM words WHERE submit='yes' ORDER BY id ASC LIMIT 10");
$s = mysqli_fetch_assoc($sorg);
$sor = mysqli_query($con, "DELETE FROM words WHERE submit='yes'ORDER BY id ASC LIMIT 20");
if ($sor >0) {
	echo "Kullanılan kelime(ler) silindi.";
}else{
	echo "Kullanılan kelime(ler) silinmedi!";
}
} catch (\Exception $e) {
    echo $e->getMessage()."\n";
	
}
// coded by fr1end
?>
<?php
include("info.php");
$rand2 = rand(0,1); 
$sayi = 1; // Burayı elleme.
////////////// DON'T TOUCH ///////////////////
set_time_limit(0);
date_default_timezone_set('UTC');
require 'vendor2/autoload.php'; 
include("config2.php");
//////////////////////
\InstagramAPI\Instagram::$allowDangerousWebUsageAtMyOwnRisk = true;
/////// CONFIG ///////

///////////////////////////////
$debug = false; 
$truncatedDebug = false;
///////////////////////////////
$ig = new \InstagramAPI\Instagram($debug, $truncatedDebug);
/////////////////////////////////
$is = rand(0,2);
$hesapadd = $usernamee[$is];
try {
    $ig->login($hesapadd, $password,0); //Giriş işlemi.
} catch (\Exception $e) {
    echo 'sorun var: '.$e->getMessage()."\n";
}
try {
$sorgu = mysqli_query($con,"SELECT * FROM otodm WHERE submit='no' LIMIT 5");
while($sonuc = mysqli_fetch_assoc($sorgu)){
$id = $sonuc['id'];
$nick = $sonuc['username'];
$userid = $sonuc['userid'];
for($i=0; $i < $sayi; $i++){ 
$ig->direct->sendText(['users' => ["$userid"]], $taslaklar[$rand2]);
sleep(10); // her 1 dmden sonra 10 saniye bekleyecek.
mysqli_query($con,"UPDATE otodm SET submit='yes' WHERE id='".$sonuc['id']."'");
}
}
} catch (\Exception $e) {
    echo 'sorun var '.$e->getMessage()."\n";
} // coded by disorder
<?php
$con = mysqli_connect("localhost","root","","dmvideo");
mysqli_set_charset($con, "utf8");
?>
