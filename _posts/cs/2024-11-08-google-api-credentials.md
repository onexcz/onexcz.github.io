---
layout: post
title:  "Jak získat Google API client ID a nezbláznit se"
date:   2024-11-08 11:00:00 +0100
permalink: /cs/google-cleint-id-pres-auth-platform
categories: cs google auth api
---

Tohle je postup, jak získat Google API client ID přes [Google Auth Platform](https://console.cloud.google.com/auth/audience) a nezbláznit se u toho.

Google Auth Platform je alternativa ke klasickému způsobu konfigurace OAuth client ID, která by měla brzy zmizet. Viz upozornění:
> OAuth consent screen management is changing. This page has been replaced with a new, easier-to-use experience. The current pages will only be available for a few more days.


TLDR;
Pokud použijete starý způsob nastavení OAuth client ID, mělo by to fungovat. Článek se týká nové administrace přes [Google Auth Platform](https://console.cloud.google.com/auth/audience). A ta má mouchy.

## Kdy bych měl číst tenhle článek?
- Chci implementovat přilašování přes Google (Sign-In with Google) ve své aplikaci
- Nechci strávit hodiny času hledáním proč to nefunguje
- Starý způsob nastavení OAuth už nefunguje
- Chci se naučit s Google Auth Platform

## Než se do toho pustíme
Pokud stále funguje stará administrace a nechcete se učit novou, stačí postupovat podle jednoho z návodů.

- [Google tutorial](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid)
- [Trochu lepší tutorial](https://www.balbooa.com/help/gridbox-documentation/integrations/other/google-client-id)


## Postup
Nejdříve je potřeba založit projekt v [Google Cloud Console](https://console.cloud.google.com/).

Je to zdarma, stačí být přihlášený do Google Account. Bezplatně lze založit 10 projektů. Potom můžete zažádat o navýšení.

### 1. Založení projektu v Google Cloud Console
Jděte na adresu [Google Cloud Console](https://console.cloud.google.com/), klikněte na "**Select project**" a v pravém horním rohu klikněte na tlačítko "**New Project**".

Po založení projektu se přes tlačítko "**Select project**" přepněte do projektu.

Pokud se teď pokusíte vytvořit OAuth klienta, dopadne to takhle.

![Create OAuth client without consent screen](/assets/images/google-client-id/image-4.png)

### 2. Konfigurace OAuth Consent Screen
>Bez vyplněné OAuth Consent Screen nelze vytvořit OAuth client ID.

Buď jste v předchozím kroku klikli na tlačítko "**CONFIGURE CONSENT SCREEN**", nebo se do konfigurace OAuth consent screen přesunete následovně:

1. V dasboardu projektu klikněte na kartu "**APIs & Services**" (nebo přes rozbalovací menu v levém horním rohu)
2. V menu vyberte OAuth consent screen

Tím se dostanete do klasické (staré) konfigurace (viz screenshot).

**My teď klikneme na tlačítko "GO TO NEW EXPERIENCE"**

![OAuth consent screen old configuration](/assets/images/google-client-id/image-5.png)

To vás přesměruje do [Google Auth Platform](https://console.cloud.google.com/auth/audience).

![OAuth consent screen new configuration](/assets/images/google-client-id/image-6.png)

Klikneme na "**GET STARTED**" a vyplníme formulář. Klikneme na "**CREATE**".

![OAuth consent screen new form](/assets/images/google-client-id/image-7.png)

Po úspěšném vytvoření budete přesměrování do záložky Overview, kde je tlačítko "**CRATE OAUTH CLIENT**".

![Google Auth Platform Overview](/assets/images/google-client-id/image-9.png)

Tím se dostáváme do pekla.

Po kliknutí na tlačítko "**CRETE OAUTH CLIENT**" jste přesměrování do záložky Clients, kde svítí tlačítko "**CONFIGURE CONSENT SCREEN**".

![Google Auth Platform Clients](/assets/images/google-client-id/image-10.png)

A jste v pekle.

Když znovu kliknete na tlačítko "**CONFIGURE CONSENT SCREEN**", jste přesměrování do sekce Branding, kde už jsou předvyplněné informace z formuláře, který jste před chvílí vyplňovali.

Můžete cokoliv změnit, vyplnit všechna pole .. nic nepomůže (můžete mi věřit).

### 3. Jak se dostat z pekla

Řešení je následující:

**Musíte vypublikovat appku.**

Vypublikovat aplikaci můžete v záložce Audience přes tlačítko "**Publish App**".

![alt text](/assets/images/google-client-id/image-12.png)

U jednoho projektu mi stačilo pouze appku vypublikovat. U druhého jsem ještě **musel *zneužít Verification Center***.

Pokud vypublikování aplikace nepomůže. Zkuste nastavit nějaké sensitive scopes (Data Access záložka). 

Potom se zobrazí upozornění ohledně verifikace aplikce. 

V záložce **Verification Center** pak na vás - po najetí šipkou na text "PREPARE FOR VERIFICATION" - vyskočí tlačítko "**CREATE OAUTH CLIENT**". 

![Verification center](/assets/images/google-client-id/image-11.png)

A tohle tlačítko funguje! 

Přesměruje vás na tu samou záložku "Clients" - ale už můžete vytvořit klienta.

![Create OAuth client ID](/assets/images/google-client-id/image-13.png)

Ještě předtím, než klienta vytvoříte, můžete vrátit status aplikace zpět do Testing. 

Hnus? Ano. 

Ale můžete vytvořit Client ID pro svojí aplikaci. A o to nám přece šlo!

onex