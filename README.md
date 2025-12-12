# 📘 README — TP Sécurité Applicative (RSA + HMAC)
---
## 🔐 Sécurisation d’un Portail Universitaire

Chiffrement RSA + Signature HMAC (Java)

Ce projet met en œuvre deux mécanismes fondamentaux de la sécurité informatique :

- Confidentialité via le chiffrement asymétrique RSA

- Intégrité via la signature HMAC-SHA256

Toutes les étapes sont documentées avec captures d’écran.

## 📚 Table des matières

1.Contexte du TP

2.Arborescence du projet

3.RSA avec OpenSSL

- Génération clé privée

- nExtraction clé publique

- Message original

- Chiffrement

- Déchiffrement

4.HMAC en Java

- Génération HMAC

- Vérification "Message intact"

- Détection message modifié

5.Captures d’écran complètes

6.Conclusion

---

## 📌 Contexte du TP

Le portail universitaire manipule des données sensibles.
L'objectif est d'assurer :

🔒 Confidentialité → RSA

🛡️ Intégrité → HMAC

✔️ Preuves → captures d’écran

---

## 📁 Arborescence du projet

```
tp-securite/
│ README.md
│ private.pem
│ public.pem
│ message.txt
│ message.enc
│ message_decrypted.txt
│ HmacExample.java
└── screenshots/
```

# 🔑 RSA avec OpenSSL
## 1️⃣ Génération de la clé privée RSA
```
openssl genpkey -algorithm RSA -aes256 -out private.pem -pkeyopt rsa_keygen_bits:2048
```

<img width="2559" height="1286" alt="image" src="https://github.com/user-attachments/assets/40fe1284-d393-4ce6-a834-6667f6fa110e" />
## Explication :
Une clé privée RSA de 2048 bits est générée et protégée par une passphrase.
Elle servira pour le déchiffrement.

--- 

## 2️⃣ Extraction de la clé publique RSA
```
openssl rsa -in private.pem -pubout -out public.pem
```


<img width="1856" height="219" alt="image" src="https://github.com/user-attachments/assets/d7f2cf23-f17e-4233-b5ea-f4c51cfda96c" />

## Explication :

La clé publique est dérivée de la clé privée et peut être diffusée.
--- 
## 3️⃣ Message original : message.txt

Ce fichier contient le message sensible à protéger.

<img width="2559" height="626" alt="image" src="https://github.com/user-attachments/assets/cdd7b0d2-c685-4141-8fee-af27b4ba49e6" />

 ---
## 4️⃣ Chiffrement RSA du message
```
openssl rsautl -encrypt -pubin -inkey public.pem -in message.txt -out message.enc
```

Résultat attendu : contenu illisible → cryptogramme

<img width="1873" height="269" alt="image" src="https://github.com/user-attachments/assets/94dcca86-a7e3-4af4-bc06-0c05fccc5c0c" />
<img width="2559" height="595" alt="image" src="https://github.com/user-attachments/assets/9225ef01-1294-47d4-a3f9-5fff84057a05" />

--- 
## 5️⃣ Déchiffrement RSA
```
openssl rsautl -decrypt -inkey private.pem -in message.enc -out message_decrypted.txt

```


<img width="1872" height="231" alt="image" src="https://github.com/user-attachments/assets/43ca8b55-2d5a-4077-b39a-ed298c5d97d8" />
<img width="2559" height="646" alt="image" src="https://github.com/user-attachments/assets/26d8e9bc-287a-4976-a4c3-58affcb40a0e" />
## Explication :
Le message déchiffré doit être identique au message original.
--- 

## 🧾 HMAC en Java
## 6️⃣ Génération d’une signature HMAC
<img width="1854" height="278" alt="image" src="https://github.com/user-attachments/assets/97ee08b3-ed5e-4a7a-b42f-6c6fef9aca3a" />

## Explication :
Un HMAC garantit que le message n’a pas été modifié (intégrité).

--- 

## 7️⃣ Vérification d’intégrité → “Message intact.”

Le HMAC est recalculé : s’il est identique → message non modifié.

```
Message intact.
```


<img width="2559" height="970" alt="image" src="https://github.com/user-attachments/assets/e1f2e77c-4172-448d-9d72-0b6e416c14e5" />

# 8️⃣ Détection d’une modification → “Message modified!”

## Résultat :
```
Message modified!
```
<img width="2559" height="1272" alt="image" src="https://github.com/user-attachments/assets/848f3e78-3767-40e2-9d62-4273291f6514" />























