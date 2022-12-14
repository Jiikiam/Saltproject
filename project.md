Projektin tarkoituksena on tehdä oma salttila ja ajaa se onnistuneesti minionille. Lähtötilanne: Masteri (versio 3004.1) on asennettu ubuntu serverille (version 22.04.1 LTS). Minion (versio 3004.1) on asennettu ubuntudesktopille (versio 22.04.1). Kumpaakin konetta pyöritetään virtualboxin päällä.

# Saltin asentaminen

Salt masterin asennus ubuntu serverille.

    $ sudo apt-get install salt-master
    $ hostname -I
    
Hostname -I näyttää masterin sijainnin eli ip-osoitteen. Sen pitää lisätä kohta minionille.

Asennetaan salt minion desktopille koneelle.

    $ sudo apt-get install salt-minion
