# WU Tomb Raider 2

## Résolution

La référence à un "piège antique" peut éventuellement orienter sur la cryptographie antique.
Le code César est le plus connu et fait partie de la famille des chiffrements par substitution.

Nous disposons d'un texte relativement long ce qui permet d'analyser la fréquence des lettres.
Il est fortement probable vu que le CTF est en français que le texte le soit aussi. Nous pouvons donc nous baser sur la fréquence d'utilisation des lettres dans la langue française. 

https://fr.wikipedia.org/wiki/Fr%C3%A9quence_d%27apparition_des_lettres_en_fran%C3%A7ais

Il ne reste plus qu'à comparer avec les fréquences relevées dans ce texte : 

St eioyyktdtfm hak lwzlmomwmogf tlm wft mteifojwt rt eioyyktdtfm wmosoltt rthwol zotf sgfumtdhl hwoljwt st eioyykt rt Etlak tf tlm wf eal hakmoewsotk.
St lodhst eioyyktdtfm hak lwzlmomwmogf tlm yaeost a ealltk hak afasblt rtl yktjwtfetl rtl stmmktl rw mtvmt eioyykt a egfromogf r'axgok wf mtvmt alltn sgfu.
MLLK{Ror_b0w_s34kf_l0dtmi1fu?}

```
T	45×	16.36%	 L	26×	9.45%   M	25×	9.09%	  O	23×	8.36%	  F	19×	6.91%	  K	17×	6.18%	  W	16×	5.82%	  A	14×	5.09%	  E	13×	4.73%	  S	12×	4.36%   Y	12×	4.36%
R	10×	3.64%	  H	8×	2.91%	  I	7×	2.55%	  G	7×	2.55%	  D	6×	2.18%	  Z	3×	1.09%	  J	3×	1.09%	  U	3×	1.09%	  B	2×	0.73%	  V	2×	0.73%	  X	1×	0.36%	  N	1×	0.36%	
```

On peut en déduire l'alphabet de substitution suivant : AZERTYUIOPQSDFGHJKLMWXCVBN
On laisse les chiffres et les caractères spéciaux tel quel

Ce qui donne : 

Le chiffrement par substitution est une technique de chiffrement utilisée depuis bien longtemps puisque le chiffre de César en est un cas particulier.
Le simple chiffrement par substitution est facile à casser par analyse des fréquences des lettres du texte chiffré à condition d'avoir un texte assez long.
TSSR{Did_y0u_l34rn_s0meth1ng?}
