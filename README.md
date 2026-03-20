# Lab 2 Container Security

I den här labben har jag jobbat med container-säkerhet genom att först skapa en medvetet sårbar image och sedan göra en säkrare version av den.

Jag byggde en enkel Flask-app och skannade först den sårbara imagen med Trivy. Där såg jag att det fanns många HIGH och CRITICAL vulnerabilities. Efter det gjorde jag en hardad Dockerfile där jag bytte till en nyare och mindre base image, uppdaterade Flask, använde non-root user och lade till healthcheck.

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
