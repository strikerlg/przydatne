Zarządzanie zapytaniami do bazy danych, oferuje wiele zabezpieczeń przed SQL injection, z funkcją:
<pre>
$mysqli->prepare();
</pre><br><br>

<b>Wiele zapytań</b><br>
Możliwość uruchamiania wielu zapytań w jednym połączeniu<br><br>

<pre>
$sqla  = "SELECT * from klienci;"
$sqlb .= "SELECT * FROM rachunki ORDER BY id_klienta"
$mysqli->multi_query($sqla; sqlb)
</pre>

Tworzymy klasę PHP z metodami i właściwościami manipulowania oraz zarządzania dowolną bazą danych. Klasa będzie wyglądała następująco:
<pre>
class dbmysqli{
 
// Deklarujemy zmienną którą będziemy używać do podłączenia z bazą danych
 
public $polacz_z_db;
 
// Deklarujemy konstruktor klasy
 
public function __construct($host, $user_db, $password_db, $db_name){
     
}
 
// Funkcja tworzenia tabel
 
public function createtable($sql){
 
}
 
// Zapisać nowe dane w bazie danych
public function insert($tabela, $pola_danych){
 
}
 
// Usuwanie danych z bazy danych
public function delete($tabela, $pola_danych){
 
}
 
public function update($tabela, $ustawienia_pol, $warunek_pol){
}
 
// Znajdź funkcję w tabeli
 
public function search($tabela, $pola){
}
 
}
</pre><br>
<b>Połączenie i klasy MySQLi</b></br>
Do połączenia z bazą danych musimy odwołać się do metod konstruktora i przesłać do bazy cztery argumenty w nim zawarte:
host (adres hosta np, localhost), nazwę użytkownika bazy danych, hasło i nazwą bazy danych.</b>

W konstruktorze dodajemy dane do połączenia z serwerem:

<pre>
public function __construct($host, $user_db, $password_db, $db_name)
 
    {
  $this->polacz_z_db = new mysqli($host, $user_db, $password_db);
 
     }
     
</pre>
Następnie wywołać w następujący sposób:
<pre>
// Połącz się z serwerem i bazy danych
$polacz_db = new db_mysqli("localhost","root","abc123"c,"Vehiculosdb");
</pre>
Definiujemy metodę tworzenia tabel dynamicznie:
<pre>
// Funkcja, która tworzy tabele
 
public function createtable($sql) {
 
if ($this->polacz_z_db->query($sql) === TRUE) {
 
echo "Prawidłowo utworzono tabelę w bazie danych";
 
  } else {
 
echo "Uwaga: nie utworzono tabeli" .$this->polacz_z_db->error;
 
  }
 
}
</pre>
Następnie wywołujemy funkcję tworzenia tabeli w bazie danych z zapytań SQLzawartych w funkcji <b>createtable()</b>:
<pre>
$sql=”DROP TABLE IF EXISTS `klienci`; CREATE TABLE IF NOT EXISTS `klienci` (
 
  `id_klienta` int(11) NOT NULL AUTO_INCREMENT,  `nazwa` varchar(255) NOT NULL,
  PRIMARY KEY (`id_klienta`))”
 
$polacz_db ->createtable($sql);
</pre>
<br>
<b>Określić metodę wstawiania / zapisu danych</b><b>

Tworzymy metode zwaną CRUD, która będzie odpowiedzialna za zarządzanie tabelami w naszej bazie. Aby ustawić parametry dla każdej metody użyjemy wartości pozyskanych z tablic, gdzie indeks tablicy będzie polem tabeli a wartość tego indeksu będzie danymi z pola tablicy. <br>Każda nazwa indeksu musi być wyrażona w cudzysłowach i mieć podane wartości według następujących zasad:<br>
<ul>
<li>Łańcuch ciągów powinien  umieszczony w pojedynczy cudzysłów.. Przykład: "name" => 'Maria'</li>
<li>Wartości liczbowe nie muszą zawierać cudzysłowów. Przykład: "Cena” => 10,50</li>
<li>NULL lub puste pole nie musi zawierać cudzysłowów. Przykład: "Cena" => NULL</li>
</ul>
<pre>
// Tworzymy funkcję, która pobiera jako parametr pola matrix => dane

public function insert($tabela, $pola_danych){

   // Jeśli wiele danych, oddzielić dane 

  $pole = implode(", ", array_keys($pola_danych));

  $i=0;
  foreach($pola_danych as $indeks=>$wartość) {

   $data[$i] = "'".$wartość."'";
      $i++;

  }

  $data = implode(", ",$data);

  // Wstawiamy wartości w każdym polu

if($this->polacz_db->query("INSERT INTO $tabela ($indeks) VALUES ($data)") === TRUE){
   echo "Wstawiony Nowy klient w bazie danych";

  }else{
   echo "Błąd, nie jest wstawiano nowegp klienta do bazy danych".$this->polacz_db->error;

  }

}
</pre>
