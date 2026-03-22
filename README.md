# Lab 2 Container Security

I den här labben har jag jobbat med container-säkerhet genom att först skapa en medvetet sårbar image och sedan göra en säkrare version av den.

Jag byggde en enkel Flask-app och skannade först den sårbara imagen med Trivy. Där såg jag att det fanns många HIGH och CRITICAL vulnerabilities. 
Efter det gjorde jag en hardad Dockerfile där jag bytte till en nyare och mindre base image, uppdaterade Flask, använde non-root user och lade till healthcheck.

Efter hardening skannade jag imagen igen med Trivy och jämförde resultatet med den första skanningen. Skillnaden blev stor både i antal allvarliga sårbarheter och i hur mycket säkrare imagen blev.

Jag genererade också en SBOM i CycloneDX-format för att kunna se vilka komponenter och beroenden som finns i imagen.

I Gatekeeper Lab testade jag policies i Kubernetes. Bad Pod stoppades eftersom den bröt mot reglerna, medan Hardened Pod visade hur en säkrare konfiguration beter sig mot policy-kontrollerna.

## Verktyg
- Docker
- Trivy
- Flask
- Kubernetes
- Gatekeeper

## Filer i repot
- Dockerfile.vulnerable
- Dockerfile.hardened
- app.py
- requirements.txt
- scan-before.txt
- scan-after.txt
- sbom.json
- policies/require-labels-template.yaml
- policies/require-team-label.yaml
- reflection.txt

## Screenshots
- [Trivy before](screenshots/trivy-before.png)
- [Trivy after](screenshots/trivy-after.png)
- [Gatekeeper deny](screenshots/gatekeeper-deny.png)
- [Gatekeeper pass](screenshots/gatekeeper-pass.png)

## Reflektion

Det här momentet gjorde det tydligt för mig hur stor skillnad små säkerhetsförändringar faktiskt kan göra i en container. När jag först körde Trivy på den sårbara imagen såg jag att det fanns många allvarliga sårbarheter, och det gjorde det lättare att förstå varför hardening behövs i praktiken.
När jag sedan byggde den hardade versionen blev det också tydligt att val av base image, uppdaterade paket och att inte köra som root spelar stor roll. Jag tyckte också att det var nyttigt att skapa en SBOM eftersom man då får bättre koll på vad imagen faktiskt innehåller. Gatekeeper-delen hjälpte mig att förstå hur policies kan användas för att stoppa osäkra konfigurationer innan de deployas i klustret. Det svåraste för mig var inte alltid själva kommandona, utan att förstå varför vissa fel uppstod och vad som faktiskt behövde ändras. Men när jag testade steg för steg blev det mer begripligt. Det jag tar med mig mest från labben är att container-säkerhet inte är en enda sak, utan flera lager som tillsammans gör stor skillnad.
