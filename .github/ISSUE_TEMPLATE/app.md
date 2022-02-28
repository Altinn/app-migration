---
name: App
about: Beskrivelse av en tjeneste som skal migreres
title: "[App navn]"
labels: kind/app
assignees: ''

---

## App beskrivelse

body:
  - type: dropdown
    id: eksisterende
    attributes:
      label: Eksisterende eller ny tjeneste?
      multiple: true
      options:
        - Ny
        - Eksisterende

