---
name: 'Sub-issue: Valider sikkerhetskrav'
about: Sub-issue mal for validering av sikkerhetskrav.
title: Valider sikkerhetskrav
labels: ''
assignees: ''
type: 'Task'
---

Følgende sikkerhetskrav er relevante for skjemautvikling og skal verifiseres for hver app vi utvikler. De originale sikkerhetskravene er på [Confluence](https://digdir.atlassian.net/wiki/spaces/BTAM/pages/3039002762/Sikkerhetskrav).

### Sikkerhetstesting

- [ ] Verifiser at SAST Scan av app er gjennomført, og at oppdaget issues er analysert og utbedret der nødvendig. Alle sikkerhetssårbarheter (Security og Security Hotspots) og andre funn med medium eller høyere alvorlighetsgrad skal vurderes og utbedres om nødvendig. **(V10.2.1, V10.3.2, V5.2.4, V5.3.8, V5.3.6, V5.3.10, V5.5.3)**
- [ ] Verifiser at SCA test av app er gjennomført og at alle oppdagete sårbarheter er vurdert og utbedret om nødvendig. **(V10.2.1, V10.3.2, V12.3.6)**
- [ ] Verifiser at SBOM av app for å dokumentere alle avhengigheter er gjennomført. **(V1.1.4, V10.3.2)**

### Kravspekk, arkitektur og design

- [ ] Verifiser at sikkerhetsbegrensinger i kravspesifikasjonen er identifisert og fulgt opp med tjenesteeier. Eksempel på sikkerhetsbegrensninger kan være: "Bruker skal ikke få mulighet til å bruke API til å hente opplysninger om andre enn seg selv", eller "bruker har kun mulighet til å redigere disse datamodellfeltene". **(V1.1.3)**
- [ ] Verifiser at vesentlige dataflyter samt bruk av andre komponenter (Altinn-produkter og tredjepartsprodukter/-tjenester) er dokumentert og begrunnet i README. Dette inkluderer nuget pakker (utenom standard app-pakker), eksterne APIer og andre Altinn tjenester (for eksempel Altinn Melding). **(V1.1.4)**
- [ ] Verifiser at applikasjonskomponenter, som klasser og metoder, er dokumentert med XML-dokumentasjon kode, og at denne dokumentasjonen beskriver hvilke forretnings- og eller sikkerhetsfunksjoner de utfører. **(V1.11.1)**
- [ ] Verifiser at applikasjonens eksterne nuget pakker har gjennomgått en sikkerhetsanalyse, kommer fra en pålitelig kilde, er aktivt vedlikeholdt, og er hentet fra https://nuget.org (sjekk i Visual Studio tools>options>Nuget package at packet source kun er https://nuget.org). **(V1.1.5, V14.2.4, V10.3.2, V12.3.6)**
- [ ] Verifiser at applikasjonens eksterne APIer har gjennomgått en sikkerhetsanalyse, kommer fra en pålitelig kilde, er aktivt vedlikeholdt, sikret med TLS (http**S**). Verifiser at sertifikatet ikke har blitt tilbakekalt med `CheckCertificateRevocationList = true` som under. **(V1.1.5, V1.2.2, V9.2.3, V14.2.4)**
```
HttpClientHandler httpClientHandler  = new HttpClientHandler() { CheckCertificateRevocationList = true };
HttpClient httpClient = new HttpClient(handler)
``` 

- [ ] Verifiser at tilstand ikke deles på tvers av instanser. I `Program.cs` blir `services.AddTransient` brukt i stedet for `services.AddSingleton` med mindre det finnes en god begrunnelse for å dele tilstand. Verifiser at data ikke blir hentet i konstruktører, men der den skal brukes. Verifiser at `IHttpContextAccessor.HttpContext` ikke blir brukt i konstruktører ([docs](https://docs.altinn.studio/nb/altinn-studio/v8/reference/analysis/rules/altinnapp0500/)). **(V1.11.2)**
- [ ] Verifiser at ingen hemmelig informasjon er lagret i koden, at dotnet user-secrets blir brukt lokalt og Azure Key Vault blir brukt i TT02/Prod. **(V1.6.2, V2.10.4, V6.4.1, V6.4.2)**

### Validering

- [ ] Verifiser at all validering foregår i backend der det ikke kan påvirkes av sluttbrukeren. Validering skal kjøres som C# kode eller som dynamiske uttrykk i backend ([kjøre-valideringene-i-backend](https://docs.altinn.studio/nb/altinn-studio/v8/reference/logic/validation/expression-validation/#kj%C3%B8re-valideringene-i-backend)). **(V1.5.3)**
- [ ] Verifisert at all upålitelig input (fra sluttbruker eller eksterne API) er validert med positiv validering. Det vil si at appen kun godtar input som oppfyller alle kravene som er satt, og avviser alt annet, i motsetning til å spesifisere hva som ikke er lov. For eksempel kun godta små bokstaver i motsetning til å ikke godta tall og store bokstaver (spesialtegn har da blitt lov). **(V5.1.3)**
- [ ] Verifiser at strukturerte data blir validert mot et forhåndsdefinert regelsett som bestemmer gyldigheten basert på antall tegn, gyldige tegn, mønster og/eller forholdet med andre datafelter. Eksempel på strukturert data er e-postadresser, telefonnummer, bankkontonummer og at postnummer og poststed matcher. **(V5.1.4)**
- [ ] Verifiser at ustrukturerte data (som fritekstfelt) blir validert mot makslengde og eventuelt lovlige tegn. Makslengde på tekst kan settes i `datamodel.cs` med `[MaxLength(int lengde)]` satt for strengen. Dette blir satt automatisk datamodell verktøyet i Studio gjennom "Største mulige lengde"-feltet.  **(V5.2.2)**

### Sanitering og enkoding

- [ ] Om appen sender epost, verifiser at det blir sendt ved hjelp av `IEmailNotificationClient` i app-lib-dotnet **(V5.2.3)**
- [ ] Verifiser at appen ikke kjører dynamisk kode (kode som blir bygget i runtime). Eksempler på dette er `System.Reflection.Emit.AssemblyBuilder` og `Type.InvokeMember`. **(V5.2.4, V12.3.6)**
- [ ] Verifiser at appen ikke gjør kall direkte mot operativsystemet eller starter kommandolinjeverktøy, eks med Process.Start. Om absolutt nødvendig, verifiser at upålitelig brukerinput aldri blir brukt direkte, men blir enkodet forsvarlig. **(V5.3.8)**
- [ ] Verifiser at upålitelig data ikke blir direkte brukt i URL eller andre http parametere. Om strengt nødvendig, verifiser format på brukerinput før http-kallet blir sendt. **(V5.2.6)**
- [ ] Verifiser at deserialisering av upålitelig data (eks eksterne API) er minimert med DTO-objekter som kun henter data appen behøver, og er gjennomført med trygge deserialiserings-biblioteker (json: `System.Text.Json`, xml: `System.Xml.XmlReader` med `DtdProcessing.Prohibit` og `XmlResolver = null`) **(V5.3.6, V5.3.10, V5.5.3)**

### Tilgangskontroll

- [ ] Verifiser at prinsippet om minste privilegium er ivaretatt. Policy filen gjøres så restriktiv som mulig. Ingen har en tilgangstype (eks read/write) i en task de ikke trenger. **(V4.1.3)**
- [ ] Verifiser at appen krever ekstra autorisasjon for å utføre handlinger med ulike autorisasjonsnivå. For eksempel at brukeren har nødvendige rettigheter definert av `actionRequiredToRead` og `actionRequiredToWrite` for å lese eller skrive til sensitive datatyper ([Beskyttede data](https://docs.altinn.studio/nb/altinn-studio/v8/concepts/data-model/restricted-data/#hva-er-beskyttede-data)). Dersom applikasjonen tilbyr funksjonalitet basert på ulike sikkerhetsnivå (0–4), skal riktig nivå håndheves. Tilganger som kreves for å benytte eksponerte, [egendefinerte API-er](https://docs.altinn.studio/nb/altinn-studio/v8/reference/api/expose/) skal være tydelig definert og verifisert. **(V4.3.3)**

### Feilhåndtering og logging

- [ ] Verifiser at appen ikke logger betalingsinformasjon, innloggingsinformasjon, eller sensitiv data i henhold til Personopplysningsloven og Digdirs retningslinjer. Logging av personlig identifiserbar informasjon skal begrenses så langt det lar seg gjøre. **(V7.1.1, V7.1.2)**
- [ ] Verifiser at `ILogger` blir brukt for å logge data med beskrivende tekst-input. Nødvendig metadata for etterforskning blir da tilgjengeliggjort i Application Insight. **(V7.1.4)**
- [ ] Verifiser at upålitelig brukerinput ikke blir inkludert i loggene for å unngå log injections. Om brukerinput må være med skal det saneres/enkodes forsvarlig. **(V7.3.1)**
- [ ] Verifiser at feilhåndtering blir brukt (`try` `catch`) der appen er forventet å kunne feile. Feil logges med stacktrace (`ILogger.LogError(ex, "…")`) **(V7.4.2)**

### Beskyttelse av data og ondsinnet kode

- [ ] Verifiser at applikasjonen minimerer antall parametere i en forespørsel. Send kun et minimum av data til eksterne API-er for å hente nødvendig informasjon. **(V8.1.3)**
- [ ] Verifiser at appen ikke sender data til uautoriserte tredjeparter. **(V10.2.1)**

### Forretningslogikk

- [ ] Verifiser at applikasjonen kun behandler forretningslogikkflyt for samme instans i sekvensiell rekkefølge, uten å hoppe over steg. Ha en Task for hvert forretnigslogikk-steg og verifiser at det ikke er mulig for sluttbrukeren og endre [flytkontrollen](https://docs.altinn.studio/nb/altinn-studio/v8/reference/process/flowcontrol/) ved å manipulere data. **(V11.1.1)**
- [ ] Verifiser at appen beskytter mot alle identifiserte forretningsrisikoer. Eksempler på forretningsrisikoer kan være tap av inntekter ved at brukeren manipulerer beløp før betaling, operasjonelle forstyrrelser for eksempel ved at appen sender data som ikke kan bli behandlet av mottaket, eller omdømmeskade. **(V11.1.5)**

### Filer og ressurser

- [ ] Verifiser at appen ikke aksepterer store/mange filer så storrage blir fyllt opp, ved å definere `"maxCount"` og `"maxSize"` for brukerkontrollerte datatyper i `applicationmetadata.json`. **(V12.1.1)**
- [ ] Verifiser at appen ikke dekomprimerer komprimerte filer lastet opp av brukeren (eks `.zip`, `.gz`, `.docx`, `.odt`). Om absolutt nødvendig sjekk først at dekomprimert filstørrelse ikke overskriver maks filstørrelse eller maks antall filer. **(V12.1.2)**
- [ ] Verifiser at filer fra upålitelige kilder (sluttbruker) valideres for å sikre at de er av forventet type basert på filens faktiske innhold. Dette innebærer følgende:
  - Kontroller at `FileUpload`-komponenter har spesifisert forventede filtyper i `"validFileEndings"` og at `"hasCustomFileEndings"` er satt til `true`.
  - I `applicationmetadata`, bekreft at datatypen har tilsvarende MIME-typer definert i `"allowedContentTypes"` og at [MIME-type validering](https://docs.altinn.studio/nb/altinn-studio/v8/reference/logic/validation/files/#hvordan-konfigurere-og-aktivere-standard-mime-type-validering-i-applikasjonen-din) er aktivert. **(V12.2.1)**
- [ ] Verifiser at filens innhold eller metadata som er kontrollert av brukeren ikke blir direkte brukt i applikasjonskoden uten å bli enkodet på en trygg måte. For eksempel sjekk at filnavn (`dataElement.filename`) kun består av bokstaver og tall før den blir brukt i app-koden. **(V12.3.1, V12.3.2, V12.3.3, V12.3.4, V12.3.5, V12.3.6)**
- [ ] Verifiser at filer fra upålitelige kilder øyeblikkelig blir scannet med antivirus før appen blir sendt inn. Dette gjøres med å ha satt `“enableFileScan": true` og `"validationErrorOnPendingFileScan": true` for datatypen i `applicationmetadata`. **(V12.4.2)**
