---
name: 'Issue: App som skal utvikles'
about: Beskrivelse av en tjeneste som skal utvikles.
title: '[App navn]'
labels: kind/app
assignees: ''
type: 'Epic'
---

# Om applikasjonen

<!-- Her kan du legge inn en beskrivelse av applikasjonen. -->

## Egenskaper

<!--  -->

| Egenskap                                | Verdi                                            |
| --------------------------------------- | ------------------------------------------------ |
| Migrering eller ny tjeneste?            | _TBD (Migrering/Ny)_                             |
| Figma skisse                            | _TBD (J/N – legg til Figma lenke)_               |
| Språk                                   | _TBD_                                            |
| API                                     | _TBD_                                            |
| eFormidling                             | _TBD (J/N)_                                      |
| Frontend skal låses før produksjon?     | _TBD (J/N)_                                      |
| Bruk av events ved mottak av skjemadata | _RegisterEventsWithEventsComponent (True/False)_ |

### Lenker

#### Altinn 2

<!-- Denne tabellen fjernes dersom det er en ny tjeneste. -->

| Område            | Lenke |
| ----------------- | ----- |
| Skjemakatalogen   |       |
| TUL               |       |
| Altinn 2.0 (test) |       |

#### Altinn 3

| Område            | Lenke |
| ----------------- | ----- |
| Altinn Studio     |       |
| Altinn 3.0 (test) |       |

### Sikkerhetsinnstillinger

| Egenskap                                      | Verdi                                                                                 |
| --------------------------------------------- | ------------------------------------------------------------------------------------- |
| PartyTypesAllowed                             | bankruptcyEstate, organisation, person, subUnit (ta vekk de som ikke skal ha tilgang) |
| Sikkerhetsnivå                                | _TBD_                                                                                 |
| Automatisk sletting etter innsending          | true/false                                                                            |
| Skjul i arkivet til brukeren etter innsending | true/false                                                                            |
| Brukeren kan kopiere eksemplaret              | true/false                                                                            |
| Vis eksemplarer som er startet på             | true/false                                                                            |

### Roller

<!-- Legg til rollene og evt. steg de skal ha rettigheter på. -->

| Kode  | Navn         | Kategori     | Les                | Skriv              | Slett          | Start          | Bekreft | Betal | Signer | Avslå | Bekreft mottatt tjenesteeier |
| ----- | ------------ | ------------ | ------------------ | ------------------ | -------------- | -------------- | ------- | ----- | ------ | ----- | ---------------------------- |
| DAGL  | Daglig leder | Rolle        | Task_1 - Utfylling | Task_1 - Utfylling | Hele tjenesten | Hele tjenesten |         |       |        |       |                              |
| [org] | Tjenesteeier | Organisasjon | Hele tjenesten     | Hele tjenesten     |                | Hele tjenesten |         |       |        |       | Hele tjenesten               |

### Prosess steg

<!-- Se [mermaid sin dokumentasjon](https://mermaid.js.org/syntax/flowchart.html) for oppsett av prosessen. -->

```mermaid
graph LR;
    StartEvent@{ shape: circle, label: 'Instansiering' }
    Task_1@{ shape: process, label: 'Utfylling' }
    EndEvent@{ shape: double-circle, label: 'Innsending' }

    StartEvent ---> Task_1
    Task_1 ---> EndEvent
```

### Vedlegg

<!-- Her kan du legge ved informasjon om vedleggene i skjemaet. -->

| ID  | [allowedContentTypes](https://developer.mozilla.org/en-US/docs/Web/HTTP/MIME_types/Common_types) | maxSize | minCount | maxCount |
| --- | ------------------------------------------------------------------------------------------------ | ------- | -------- | -------- |
|     |                                                                                                  |         |          |          |

## Huskeliste

- [ ] Legg til følgende kode i `.gitignore`:
  ```
  # Do not include secrets.json file
  secrets.json
  ```
