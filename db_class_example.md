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
 
Usuwanie danych z bazy danych
public function delete($tabela, $pola_danych){
 
}
 
public function update($tabela, $ustawienia_pol, $warunek_pol){
}
 
// Znajdź funkcję w tabeli
 
public function search($tabela, $pola){
}
 
}</pre>
