# 🧩 Python Greetings Pipeline (Jenkins)

CI/CD piegādes konveijers Python mikropakalpojumam, izstrādāts ar **Jenkins**.  
Šis projekts demonstrē Jenkins deklaratīvo piegādes konveijera konfigurāciju ar vairāku vides testēšanu un izvietošanu.

## 🎯 Mērķis
Izveidot piegādes konveijeru, kas:
- klonē Python un testu repozitorijus no GitHub,
- instalē nepieciešamās Python bibliotēkas,
- izvieto aplikāciju vairākās vidēs (dev, staging, preprod, prod),
- veic API testus ar `course-js-api-framework`.

## ⚙️ Izmantotās tehnoloģijas
- **Jenkins** – CI/CD konveijera platforma  
- **Python** – aplikācijas kods  
- **PM2** – servisa pārvaldība  
- **Node.js + NPM** – API testu izpilde  
- **Groovy (Jenkinsfile)** – konveijera skripta valoda  

## ▶️ Darbība
Konveijers definēts failā `Jenkinsfile`.  
Tas izpilda posmus `install-pip-deps`, `deploy-to-env`, un `tests-on-env`, izmantojot Jenkins agent un PM2 servisu pārvaldību.

