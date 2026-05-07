Palvelinten Hallinta, Palvelinten hallinta - ICI001AS3A-3013 - to 11:00 pa5001 - Tero - 2026p4 - +ph13
h6 Miniprojekti
Sami Ylikörkkö, Ville Suikki
 
Projektin tarkoitus

Projektin tavoitteena on siirtyä manuaalisesta järjestelmänhallinnasta moderniin Infrastructure as Code (IaC) -malliin. Toteutimme automaation, joka muuttaa puhtaan Debian-palvelimen täysin toimivaksi ja WordPress-valmiiksi verkkopalvelinalustaksi yhdellä komennolla.

Tämä mahdollistaa:

- Skaalautuvuuden: Saman konfiguraation ajamisen usealle eri palvelimelle samanaikaisesti.
- Idempotenssin: Ansible varmistaa palvelimen tilan tekemättä turhia muutoksia jos asetukset ovat jo kunnossa.
- Standardoinnin: Inhimilliset virheet poistuvat, kun asennus noudattaa täsmälleen samaa koodia.
____________________________________________________________________________________________________________________

Tekninen arkkitehtuuri (LAMP-pino)
   
Projekti pystyttää LAMP-pinon, joka on dynaamisten verkkosovellusten (kuten WordPress) perusedellytys:

Eri komponenttien rooli järjestelmässä:

Apache2	HTTP-verkkopalvelin: Toimii "ovena"
MariaDB	Tietokanta: Toimii järjestelmän "muistina", jonne WordPress tallentaa artikkelit, käyttäjät ja asetukset.
PHP	Skriptikieli: Toimii "moottorina", joka suorittaa WordPressin logiikan ja hakee tiedot tietokannasta.

Modulaarinen rakenne:

Playbook (playbook.yml): yhdistää taskit ja handlerit.
Taskit: Suorittavat varsinaisen asennuksen (pakettien päivitys, ohjelmistojen asennus, konfiguraatiotiedostojen luonti).
Handlerit: Huolehtivat palveluiden älykkäästä hallinnasta. Palvelut käynnistetään uudelleen vain, jos konfiguraatioihin on tehty muutoksia.
____________________________________________________________________________________________________________________

Asennus ja käyttö

Esivaatimukset:
- Palvelimella on SSH-yhteys ja Python asennettuna.
- hosts.ini tiedostoon on määritetty kohdepalvelimen IP-osoite.

Käyttöönotto

Bash
1. Kloonataan repo
git clone https://github.com/vilsui/h6-Miniprojekti
cd h6-Miniprojekti

2. Ajetaan automaatio
ansible-playbook playbook.yml -i hosts.ini --ask-become-pass

____________________________________________________________________________________________________________________

Testaus ja laadunvarmistus

Automaation onnistuminen varmistetaan neljällä eri testillä, jotka kattavat koko pinon:

1.	Varmistetaan, että verkkopalvelin on aktiivinen ja käynnissä: systemctl status apache2 
2.	Sovelluskerroksen testi: curl localhost/testi.php – Testataan, että PHP-tulkki on integroitu oikein Apacheen ja pystyy tuottamaan dynaamista sisältöä. Tässä tapauksessa kellonajan.
3.	Viestintätesti: curl localhost varmistaa että automaattisesti generoitu testisivu näkyy ulospäin.
4.	Tietokantatesti: sudo mariadb -e "SHOW DATABASES;" – Varmistetaan, että MariaDB on pystyssä


Lopputulema ja WordPress-yhteys
Vaikka projekti ei asenna itse WordPress-ohjelmistoa, se luo sille standardoidun infrastruktuurin. Loppukäyttäjä saa tällä valmiin ympäristön, jossa on PHP, Apache ja MariaDB valmiina. Käyttäjä tarvitsee vain purkaa oma sovelluksensa (WordPress) tähän ympäristöön ja aloittaa käyttö.
 
____________________________________________________________________________________________________________________

Jatkojalostus

- Automaattinen WordPress-deploy: Taski, joka lataa ja purkaa WordPressin lähdekoodin suoraan /var/www/html/ kansioon.
- Tietoturvapaketti: UFW-palomuurin konfigurointi sallimaan vain portit 80 (HTTP) ja 443 (HTTPS).
- Salaus: Let's Encrypt -sertifikaattien automaattinen haku ja HTTPS-pakotus.


<img width="1862" height="1532" alt="image" src="https://github.com/user-attachments/assets/12dee8fb-9734-4f0a-a8c3-6b8dda36c4a7" />
