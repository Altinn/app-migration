---
name: 'Issue: App som skal migreres'
about: Beskrivelse av en tjeneste som skal migreres fra Altinn 2 til Altinn 3
title: '[App navn]'
labels: kind/app
assignees: ''
type: 'Epic'
---

## Innledning

| Beskrivelse av tjenesten | Legg inn kort beskrivelse |
| ------------------------ | ------------------------- |
| **Tjenestekode**         |                           |
| **Tjenesteutgavekode**   |                           |

## Generelle egenskaper

#### Hvordan benyttes Tjenesten?

Kun portal-innsending (J/N):  
Kun sluttbrukersystem-innsending (J/N):  
Både portal- og sluttbrukersystem-innsending (J/N):

Har tjenesten underskjema/skjemasett (J/N)

## Skjermbilder

> Legg inn (relevante) skjermbilder av tjenesten her. Tips: legg inn skjermbilder fra TUL som viser tilgangsinfo (sikkerhetsnivå, rollekrav, avgiverkrav osv)

## Behov for funksjonalitet

> Fyll ut

## Lenker og filer

#### Altinn 2

| Område            | Lenke |
| ----------------- | ----- |
| Skjemakatalogen   |       |
| TUL               |       |
| Altinn 2.0 (test) |       |

#### Altinn 3

| Område            | Lenke |
| ----------------- | ----- |
| Altinn Studio     | ....  |
| Altinn 3.0 (test) | ....  |

## Tasks

- [ ] Logo
- [ ] Språkfiler
- [ ] Applikasjonsprosess
- [ ] Sikkerhetsnivå
- [ ] Aktørtype (organisasjon/person/konkursbo...)
- [ ] Rollekrav
- [ ] Godkjent i test/TT02 av tjenesteeier
- [ ] Review
- [ ] Produksjon
- [ ] Oppdatere tekst/lenke på Infoportal (TT)

#### Code Review

**Textresources:**

- [ ] Check app logo
- [ ] Check that it has Alternative text for logo
- [ ] Check Appowner
- [ ] Check Camelcase on id

**Layout files:**

- [ ] Camelcase on id
- [ ] Use Groups that can be reused in summary and pdf
- [ ] If app has an attachment component it should have the same values such as min and max count as in applicationmeta data file.
- [ ] Check that it has a file called 01Intro
- [ ] Check that it has a file called 99Summary
- [ ] Check that it has a pdfReceipt file
- [ ] Check Grid and inner grid and make sure it has both xs: and md:

**Applicationmetadata:**

- [ ] Logo
- [ ] Check that displayAppOwnerNameInHeader: false
- [ ] Logo "size" same as the other applications

**App.csproj:**

- [ ] Make sure PackageReference version = 7.15.1

**Data model:**

- [ ] Delete minOccurs on required fields.
- [ ] Pascal case on name in data model

**Options file:**

- [ ] Make sure all plain text is referred to though text resource id

**Logic files:**

- [ ] Make sure all plain text is referred to though text resource id
- [ ] Make sure all custom service implementations is added in Program.cs
