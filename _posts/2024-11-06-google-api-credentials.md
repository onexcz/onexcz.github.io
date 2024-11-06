---
layout: post
title:  "Jak získat Google API Credentials a nezbláznit se"
date:   2024-11-06 19:06:56 +0100
categories: google auth api
---

Tohle je postup, jak získat Google API Credentials a nezbláznit se u toho.

## Kdy bych měl číst tenhle článek?
- Chci používat Google API
- Nechci ztrávit hodiny času hledáním návodů na internetu
- Nechci ztrávit hodiny času nastavováním OAuth Consent Screen v Google API Console

## Postup
1. Založit projekt v [Google Cloud Console](https://console.cloud.google.com/)
2. Vyplnit OAuth Consent Screen
3. Vytvořit OAuth Client ID
4. Povolit v projektu API a služby, které chcete používat
5. Zkopírovat Client ID a Client Secret
6. Vložit Client ID a Client Secret do konfigurace aplikace
