# Sauvegarde DNS – ancien site houraformation.fr

Relevé le 24/11/2026, juste avant la bascule de houraformation.fr vers la page de maintenance (GitHub Pages).

## Où est l'ancien site
- Hébergeur : **LWS** (panel.lws.fr), compte client LWS-796238, formule « Perso », domaine houraformation.fr
- Les fichiers de l'ancien site (environ 2 970 fichiers, 0,6 Go, site statique en .html + 1 base MySQL) sont **toujours sur l'hébergement LWS** (Gestionnaire de fichiers). Rien n'a été supprimé.
- Adresse IP de l'hébergement web LWS : **193.37.145.80** (IPv6 par défaut LWS : 2a00:7ee0:1:0:3:2204:0:35f)
- Le domaine n'est pas enregistré chez LWS (registrar ailleurs), mais la zone DNS est gérée chez LWS : ns21 / ns22 / ns23 / ns24.lwsdns.com

## Comment remettre l'ancien site en ligne
Dans LWS Panel → houraformation.fr → Zone DNS :
1. Supprimer les 4 enregistrements `A @ 185.199.10x.153` (GitHub)
2. Remettre `A @ 193.37.145.80`
3. Remettre `CNAME www @`
4. Attendre la propagation (quelques minutes à quelques heures)

Pour afficher l'ancien site sur un autre nom de domaine : faire pointer ce domaine (`A @`) vers **193.37.145.80** et l'ajouter dans LWS → « Multi Domaines ».

## Zone DNS complète avant la bascule

| Type | Nom | Valeur |
|---|---|---|
| A | @ | 193.37.145.80 |
| A | lms | 193.203.239.86 |
| A | mail | 193.203.239.42 |
| AAAA | lms | 2a00:7ee0:8:0:3:3225:0:48a |
| CNAME | cfa | houraformation.fr |
| CNAME | email.mails | mailgun.org |
| CNAME | ftp | @ |
| CNAME | houra.fr | houraformation.fr |
| CNAME | imap | mail.houraformation.fr. |
| CNAME | pop | mail.houraformation.fr. |
| CNAME | smtp | mail.houraformation.fr. |
| CNAME | vtc | houraformation.github.io. |
| CNAME | www | @ |
| MX | @ | 10 mail.houraformation.fr. |
| MX | mails | mxb.mailgun.org |
| MX | mails | mxa.mailgun.org |
| NS | @ | ns21.lwsdns.com. |
| NS | @ | ns22.lwsdns.com. |
| NS | @ | ns23.lwsdns.com. |
| NS | @ | ns24.lwsdns.com. |
| TXT | @ | v=spf1 mx:houraformation.fr a:mail.houraformation.fr a:mailphp.lws-hosting.com -all |
| TXT | dkim._domainkey | v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC8C8Xh049AFp+LuKVCUlwahtRFxO85rrJ0dE0idCfNAsI5Nlobf02gik8jesZ04clvZ0lxaM+L8IU50AKVHeFva83Y7LVJdeaXk14fO3gwQ1r/asNhzvg++88bfhSaLKD5M4Eid13mBrpsV3gP/MeGIzsty0AMUUNpDwe0otnv3wIDAQAB |
| TXT | mails | v=spf1 include:spf.leadconnectorhq.com include:mailgun.org ~all |
| TXT | pic._domainkey.mails | k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDoFMpuw6Fjab0P0ShvZVTzNsj9bej1Aatwgq3sXZGQJ+fpSCHwRNK9K08EfAfM9lJIfEcIkv2wGfRe+XbwLT2pcCwMYf1hxDJVSAdlAMc6tRK69EQKbfpomPFhrwSbYIGOFRYWPsRWWjaiPPpF7zUtZ8nac6MYb4qwfO9EktvCJwIDAQAB |
| TXT | _dmarc | v=DMARC1; p=quarantine; |
| TXT | _dmarc.mails | v=DMARC1;p=none; |

## Journal des modifications DNS réellement faites le 24/11/2026

| Heure | Action | Avant | Après |
|---|---|---|---|
| ~11 h 55 | Modifié | A @ 193.37.145.80 (TTL 6 h) | A @ 185.199.108.153 |
| ~11 h 55 | Supprimé automatiquement par LWS (conséquence du changement ci-dessus) | AAAA @ 2a00:7ee0:1:0:3:2204:0:35f (IPv6 web LWS par défaut) | — |
| ~11 h 56 | Ajouté | — | A @ 185.199.109.153 |
| ~11 h 57 | Ajouté | — | A @ 185.199.110.153 |
| ~11 h 58 | Ajouté | — | A @ 185.199.111.153 |
| ~11 h 59 | Supprimé (erreur, non demandé) | CNAME ftp @ (TTL 24 h) | — |
| ~12 h 05 | Remis comme avant | — | CNAME ftp @ (TTL 6 h au lieu de 24 h) |
| ~12 h 06 | Modifié | CNAME www @ (TTL 24 h) | CNAME www houraformation.github.io. |

Aucun autre enregistrement n'a été touché (emails, mailgun/GHL, lms, vtc, cfa, houra.fr, SPF, DKIM, DMARC, NS).

### Pour tout annuler (revenir à l'ancien site)
1. Supprimer les 4 lignes `A @ 185.199.10x.153`
2. Ajouter `A @ 193.37.145.80`
3. (optionnel) Ajouter `AAAA @ 2a00:7ee0:1:0:3:2204:0:35f`
4. Modifier `CNAME www` → `@`
