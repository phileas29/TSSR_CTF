# WU Suis le lapin blanc 2

## Obtention du nom du profil utilisateur et du mot de passe


### Obtention des infos de ruches

Pour trouver le compte et les mots de passes deux ruches nous intéressent :

```bash
/volatility_2.6_lin64_standalone -f /home/debian/Téléchargements/lapin_blanc.vmem --profile=Win8SP1x64_18340 hivelist
Volatility Foundation Volatility Framework 2.6
Virtual            Physical           Name
------------------ ------------------ ----
0xffffc0004767c000 0x000000002b72c000 \SystemRoot\System32\Config\SAM
0xffffc00046c28000 0x00000000001f1000 \REGISTRY\MACHINE\SYSTEM
```

### Obtention des hash de compte

Option -y : adresse virtuelle de \REGISTRY\MACHINE\SYSTEM
Option -s : adresse virtuelle de \SystemRoot\System32\Config\SAM

On va utiliser la fonction hashdump de Volatility : 


```bash
./volatility_2.6_lin64_standalone -f /home/debian/Téléchargements/lapin_blanc.vmem --profile=Win8SP1x64_18340 hashdump -y 0xffffc00046c28000 -s 0xffffc0004767c000 > ./output/hash.txt
cat output/hash.txt
Administrateur:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Invit:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Neo:1001:aad3b435b51404eeaad3b435b51404ee:2d20d252a479f485cdf5e171d93985bf:::
```

Nous avons désormais la 1ere partie du flag. En effet le compte utilisateur se trouve être Neo.

### Crack du hash

Avant de se lancer dans john ou hashcat, il peut être intéressant de tester le hash sur crackstation.net si le mot de passe est vraiment simple ou que le hash est déjà connu. 

On entre donc la partie droite du hash : 2d20d252a479f485cdf5e171d93985bf


Crackstation nous trouve facilement le mot de passe suivant : qwerty

Le format du flag est TSSR{Compte_motdepasse}

Le flag est donc : TSSR{Neo_qwerty}
