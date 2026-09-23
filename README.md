# Oppgave: Fra Spring Boot til AWS App Runner

Denne oppgaven er mindre detaljert beskrevet enn vanlig, og introduserer en ny tjeneste vi vil jobbe med senere. Du skal selv finne ut av kommandoer, flagg og konfigurasjon basert på det du har lært i tidligere oppgaver og offisiell dokumentasjon.

## Læringsmål

- Bygge et container-image av en Spring Boot-applikasjon med Docker
- Publisere et image til et privat container-registry (Amazon ECR)
- Starte en tjeneste i AWS App Runner fra et image
- Bli vant til å lese dokumentasjon fremfor steg-for-steg-oppskrifter

## Kom i gang

En **fork** er din egen kopi av et GitHub-repo, koblet tilbake til originalen. Du fork-er dette repoet slik at du får et sted å legge din egen kode og innleveringen din, uten å endre kildeprosjektet.

1. Fork dette repoet til din egen GitHub-konto.
2. Åpne forken i Codespaces.
3. Legg Spring Boot-prosjektet ditt i rotmappen av forken.

## AWS-tjenester vi bruker

- **Amazon ECR (Elastic Container Registry)** — privat registry for Docker-images. Her lagrer du imaget ditt slik at App Runner kan hente det.
- **AWS App Runner** — kjører container-baserte web-tjenester direkte fra et image i ECR. App Runner tar seg av HTTPS, autoskalering og load balancing.

## Hva du skal gjøre

1. Lag en enkel Spring Boot-applikasjon
2. Containeriser den med Docker
3. Publiser imaget til Amazon ECR
4. Kjør imaget som en App Runner-tjeneste

## Steg 1: Spring Boot-applikasjon

Bruk [Spring Initializr](https://start.spring.io/) til å generere et Maven-prosjekt med Java 21 og dependency-en `Spring Web`. Skriv en controller som returnerer en tekststreng på rotstien `/`. Test lokalt i Codespaces før du går videre.

## Steg 2: Dockerfile

Skriv en `Dockerfile` som bygger og kjører applikasjonen. Tenk på:

- Hvilket base-image passer for å bygge, og hvilket passer for å kjøre?
- Hvilken port lytter Spring Boot på som standard?
- Hvordan starter du jar-en?

Bygg imaget lokalt og verifiser at applikasjonen svarer.

## Steg 3: Publiser til Amazon ECR

Du trenger AWS CLI konfigurert med dine aksessnøkler og region `eu-west-1`. Deretter skal du:

- Opprette et ECR-repository
- Autentisere Docker mot ECR
- Tagge imaget med full ECR-URI
- Pushe imaget

Slå opp de nødvendige `aws ecr`- og `docker`-kommandoene selv.

## Steg 4: App Runner-tjeneste

Opprett en App Runner-tjeneste fra ECR-imaget ditt via AWS Console. Pass på at porten stemmer med det applikasjonen faktisk lytter på. Når tjenesten er `Running`, får du en public URL du kan åpne i nettleseren.

## Deployment

Push koden din (Spring Boot-prosjekt og Dockerfile) til forken din, og lever inn URL-en til App Runner-tjenesten.
