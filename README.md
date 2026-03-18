# Lab 2 Container Security

I den här labben har jag jobbat med container-säkerhet genom att först skapa en medvetet sårbar image och sedan göra en säkrare version av den.

Det jag gjorde var att bygga en enkel Flask-app och skanna den sårbara imagen med Trivy. Där såg jag att det fanns väldigt många HIGH och CRITICAL vulnerabilities. Efter det gjorde jag en härdad Dockerfile där jag bytte till en nyare och mindre base image, uppdaterade Flask, använde non-root user och lade till healthcheck.

Efter hardening skannade jag imagen igen med Trivy och jämförde resultatet med den första skanningen. Skillnaden blev stor både när det gäller storlek på imagen och antal allvarliga sårbarheter.

Jag genererade också en SBOM i CycloneDX-format för att kunna se vilka komponenter och beroenden som finns i imagen.

I Gatekeeper Lab testade jag policies i Kubernetes. Bad Pod stoppades eftersom den bröt mot flera regler, medan Hardened Pod gick igenom men med en varning om default service account. Det visar också att det fortfarande går att förbättra säkerheten ytterligare, till exempel genom att använda ett eget service account i stället för default.

I repot finns följande filer:

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

Screenshots läggs i mappen screenshots.
