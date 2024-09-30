## ceci est un compte rendu de la mise en place d'un lab redondance avec ip fixe

Tout d'abord présenté ici toute les ressources utilisées 

- documentation trouvé dans le fichier redondance.md : https://github.com/Groupe-Citypassenger-Inc/Documentation/blob/master/dev-preprod/redondance/redondance.md
  
- 2 boitiers v16 qui sont les boitiers a redonder  , 1 boitier v20 pour fournir l'accès internet et permettre au boitiers redondés de sortir avec leur ip fixe via un lan dans le même réseau
  
!!! warning
    Un des boitiers de test ayant son interface em1 down nous n'utiliserons pas le lan correspondant, aussi son état apparait dans les logs
- liens des boitiers 

v20 : https://admin.citypassenger.com/CityDevice/fr/index.html#/a-may-zing/wifi-ap-test-switch-dlink

v16 : https://admin.citypassenger.com/CityDevice/fr/index.html#/a-may-zing/lab-redondance-wifi6

les boitiers sont branchées selon le schéma réseau suivant : 
https://urlr.me/Hxrz4


selon les instructions la conf LAN et WAN reprend celle de RGG Bolton redundancy , lien :
https://admin.citypassenger.com/CityAccounts/fr/index.html#/rrg-uk/rrg-bolton-redundancy

j'ai donc réalisé le flashage des boitiers ainsi que vérifié le fonctionnement en mode " normal" c'est a dire tout est branché comme sur le schéma et la borne donne bien un accès internet sur le SSID CP_internal

Cependant contrairement a une configuration avec DHCP réalisé précédemment déroulé sans encombre si nous tentons de vérifier la redondance nous observons des problèmes

!!! note Problèmes  et observations
    - lorsque les deux boitiers sont connecté comme exposé précédemment la conf semble fonctionner, cependant si l'on fait tomber la wan du master le backup ne prend jamais le relais.
  
    - si l'on enlève le lien de redondance et le lien wan le second boitier fini par marcher mais c'est logique car il est désormais seul comme un boitier  normal et agit en master
  
    - comme l'on ne peut accéder au backup que par l'interface RED en accès admin impossible de vérifier les logs ou la raison du non fonctionnement.

    - si l'on branche seulement un boitier puis que l'on rajoute l'autre par le lien de redondance alors le premier reste master comme si l'autre n'avait pas été rajouté

    - Quand l'on a récupéré la supervision sur le master on peut voir des logs normaux , (ex dans mon cas on a juste des logs qui concernent la borne wifi et qu'il n'y a pas de nouveau tag a faire passer)



En bref lors de la réalisation d'un lab de test la configuration avec ip fixe ne semble pas marcher.