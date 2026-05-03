Palvelinten Hallinta, Palvelinten hallinta - ICI001AS3A-3013 - to 11:00 pa5001 - Tero - 2026p4 - +ph13
h6 Miniprojekti
Sami Ylikörkkö, Ville Suikki


Ansible-automaatio: Verkkopalvelinalustan pystytys
Tämä projekti toteuttaa automatisoidun tavan pystyttää ja konfiguroida verkkopalvelinalusta Debian-pohjaisille palvelimille. 

Lähtövaatimus
Tavoitteena on luoda nopeasti toistettava, uusittava ja helposti hallittava automaatio useammalle palvelimelle. Käytimme Ansiblea, jolla varmistetaan, että kaikilla kohdekoneilla on uusimmat ohjelmistoversiot ja ne on konfiguroitu identtisesti.

____________________________________________________________________________________________________________________

Tekninen toteutus

Projekti on jaettu modulaarisesti taskeihin ja handlereihin:

Playbook: playbook.yml ohjaa koko asennusprosessia.

Taskit: Järjestelmän päivitys, Apachen, PHP:n ja MariaDB:n asennus sekä testisivun luonti.

Handlerit: Palveluiden (Apache, MariaDB) hallittu uudelleenkäynnistys konfiguraatiomuutosten jälkeen.

Asennus, käyttö ja testaus

Kloonataan repo: git clone https://github.com/vilsui/h6-Miniprojekti
Siirrytään kansioon: cd h6-Miniprojekti
Ajetaan playbook: ansible-playbook playbook.yml -i hosts.ini --ask-become-pass 


Testataan

- PHP testi: curl localhost/testi.php
- Nettisivun testaus: curl localhost
- apache2 testaus: systemctl status apache2
- mariaDB'n testaus: sudo mariadb -e "SHOW DATABASES;"

____________________________________________________________________________________________________________________

Lopputulema

Automaation tuloksena palvelimelle on asennettu ja konfiguroitu:

- Apache2 -verkkopalvelin.
- MariaDB -tietokanta.
- PHP ja tarvittavat moduulit.
- Automaattisesti generoitu index.html -testisivu, joka varmistaa ympäristön toimivuuden.

Lopputuleman tarkistus komennolla: curl localhost
____________________________________________________________________________________________________________________

Jatkojalostus

Projekti on suunniteltu laajenemaan seuraavilla ominaisuuksilla:

- Täysiverinen WordPress-tuotantopalvelin.
- Tietoturvan parantaminen UFW-palomuuriasetuksilla.
- Sertifikaattien hallinta (Let's Encrypt / HTTPS).

<img width="1736" height="1972" alt="image" src="https://github.com/user-attachments/assets/dc2d6daf-1e4f-490e-ac27-0571bf299887" />

