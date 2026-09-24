# Oppgave: Fra Spring Boot til Amazon ECS Express mode

Denne oppgaven er mindre detaljert beskrevet enn vanlig, og introduserer en ny tjeneste vi vil jobbe med senere. Du skal selv finne ut av kommandoer, flagg og konfigurasjon basert på det du har lært i tidligere oppgaver og offisiell dokumentasjon.

## Læringsmål

- Bygge et container-image av en Spring Boot-applikasjon med Docker
- Publisere et image til et privat container-registry (Amazon ECR)
- Starte en tjeneste i Amazon ECS med **Express mode** fra et image
- Bli vant til å lese dokumentasjon fremfor steg-for-steg-oppskrifter

## Kom i gang

En **fork** er din egen kopi av et GitHub-repo, koblet tilbake til originalen. Du fork-er dette repoet slik at du får et sted å legge din egen kode og innleveringen din, uten å endre kildeprosjektet.

1. Fork dette repoet til din egen GitHub-konto.
2. Åpne forken i Codespaces.
3. Legg Spring Boot-prosjektet ditt i rotmappen av forken.

## AWS-tjenester vi bruker

- **Amazon ECR (Elastic Container Registry)** — privat registry for Docker-images. Her lagrer du imaget ditt slik at ECS kan hente det.
- **Amazon ECS (Elastic Container Service) — Express mode** — en forenklet måte å kjøre containere på ECS. Express mode setter opp cluster, task-definisjon, service, Application Load Balancer, target groups, security groups og auto-scaling for deg, slik at du kan gå fra et image i ECR til en offentlig URL uten å konfigurere hver komponent manuelt. Du betaler kun for de underliggende ressursene.

## Hva du skal gjøre

1. Lag en enkel Spring Boot-applikasjon
2. Containeriser den med Docker
3. Publiser imaget til Amazon ECR
4. Kjør imaget som en ECS-tjeneste i Express mode

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

## Steg 4: ECS-tjeneste i Express mode

Opprett en ECS-tjeneste fra ECR-imaget ditt via AWS Console ved å velge **Express mode**. Underveis skal du:

- Peke på ECR-imaget du nettopp pushet
- Angi containerporten som samsvarer med det Spring Boot lytter på
- La Express mode opprette load balancer og nettverk for deg
- Vente til tjenesten er `Running` og health-checks er grønne

Når tjenesten er oppe, får du en offentlig URL (via load balanceren) som du kan åpne i nettleseren.

> Tips: Express mode kan også opprettes med Terraform via ressursen `aws_ecs_express_gateway_service` i AWS-provideren. Det er ikke nødvendig for denne oppgaven, men greit å vite til senere når vi går over til IaC.

## Deployment

Push koden din (Spring Boot-prosjekt og Dockerfile) til forken din, og lever inn URL-en til ECS-tjenesten.
