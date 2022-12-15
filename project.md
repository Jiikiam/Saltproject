Projektin tarkoituksena on tehdä oma salttila, joka asentaa virtualboxin ja nginx web-palvelimen onnistuneesti minionille. Lähtötilanne: Masteri (versio 3004.1) on asennettu ubuntu serverille (version 22.04.1 LTS). Minion (versio 3004.1) on asennettu ubuntudesktopille (versio 22.04.1). Kumpaakin konetta pyöritetään virtualboxin päällä.

# Saltin asentaminen

Salt masterin asennus ubuntu serverille.

    $ sudo apt-get install salt-master
    $ hostname -I
    
Hostname -I näyttää masterin sijainnin eli ip-osoitteen. Sen pitää lisätä kohta minionille.

Asennetaan salt minion desktopille koneelle.

    $ sudo apt-get install salt-minion
    $ sudoedit /etc/salt/minion 
 
Kerrotaan minionille masterin sijainti ja nimetään minion. Sitten käynnistetään minion uudestaan.
 
 ![Alt text](/project/p7.png)
 
    $ systemctl restart salt-minion.service
    
Käydään hyväksymässä masterilla minionin avain.

     $ sudo salt-key -A
     
Nyt voidaan tehdä nopea testi toimiiko yhteys masterin ja minonin välillä.

     $ sudo salt ’ubuntudesktop’ test.ping
     
# Salttilan tekeminen lokaalisti. Tarkoituksena on asentaa saltilla virtualboxin ja nginx web-palvelin masterille.

Uusi project kansio /srv/salt kansion ja init.sls tiedoston luominen project kansioon.

     $ cd /srv/salt/
     $ sudo mkdir project
     $ cd project/
     $ sudo nano init.sls
     
Kirjoitetaan init.sls tiedostoon tarvittavat paketit.

 ![Alt text](/project/p8.png)
 
 Ajetaan salttila lokaalistin.
 
     $ sudo salt-call --local state.apply project
 
  ![Alt text](/project/p9.png)
  
 Läpi meni ja tarkitetaan onko palvelut käynnissä.
  
    $ service status nginx
    $ service status virtualbox
    
# Salttilan ajaminen masterilta minionille.

Yritetään ajaa salttila minonille.

    $ sudo salt 'ubuntudesktop' state.apply project
    
 ![Alt text](/project/p3.png) 
 
 Näytti menneen läpi. Tarkistetaan, että kumpikin palvelu on päällä.
 
 ![Alt text](/project/p4.png) 
 
 ![Alt text](/project/p5.png) 
 
 Hakemalla minionin ip osoittetta selaimella voidaan varmistaa nginx toiminta.
 
 ![Alt text](/project/p2.png) 
 
 Käydään avaamassa virtualbox.
 
 ![Alt text](/project/p10.png) 
 
 Lopputulos näiden osalta oli onnistunut. 
 
 Yritin myös asentaa vscodea salt furmulalla, mutta moti meni, kun liian monta tuntia meni vain pähkäillessä miksi en saanut sitä toimimaan.
    
    
    
    
    
    
    
 
     
     
     
     
     
     
     
     
     
     
     
     
     
