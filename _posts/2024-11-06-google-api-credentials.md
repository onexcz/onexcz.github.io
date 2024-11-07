---
layout: post
title:  "Jak získat Google API client ID a nezbláznit se"
date:   2024-11-06 19:06:56 +0100
categories: google auth api
---

Tohle je postup, jak získat Google API client ID přes [Google Auth Platform](https://console.cloud.google.com/auth/audience) a nezbláznit se u toho.

Google Auth Platform by měla zanedlouho nahradit klasický způsob konfigurace OAuth Consent Screen a OAuth klienta. Viz upozornění:
> OAuth consent screen management is changing. This page has been replaced with a new, easier-to-use experience. The current pages will only be available for a few more days.


TLDR;
Pokud použijete starý způsob nastavení OAuth Consent Screen a OAuth klienta, nemusíte řešit. Článek se týká nové administrace ([Google Auth Platform](https://console.cloud.google.com/auth/audience)). A ta má ještě nějaké mouchy.

## Kdy bych měl číst tenhle článek?
- Chci implementovat přilašování přes Google (Sign-In with Google)
- Nechci strávit hodiny času googlením proč to nefunguje
- Starý způsob nastavení OAuth už nefunguje

## Než se do toho pustíme
Pokud stále funguje stará administrace a nechcete se učit novou, stačí postupovat podle jednoho z návodů.

- [Google tutorial](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid)
- [Trochu lepší tutorial](https://www.balbooa.com/help/gridbox-documentation/integrations/other/google-client-id)


## Postup
Nejdříve je potřeba založit projekt v [Google Cloud Console](https://console.cloud.google.com/).

Je to zdarma, stačí být přihlášený do Google Account. Bezplatně lze založit 10 projektů. Potom můžete zažádat o navýšení.

### 1. Jak založit projekt v Google Cloud Console
Jděte na adresu https://console.cloud.google.com/, klikněte na "Select project" a v pravém horním rohu klikněte na tlačítko "New Project".

![New project screenshot](image.png)

Jméno projektu může být téměř jakkékoliv (bez diakritiky) - mezery jsou povoleny. Google vygneruje unikátní Project ID na základě tohoto jména.

![Create project screenshot](image-1.png)

Po založení projektu se přes tlačítko "Select project" přepněte do projektu.

Pokud se teď pokusíte vytvořit OAuth klienta, dopadne to takhle.

![Create OAuth client without consent screen](image-4.png)

### 2. Konfigurace OAuth Consent Screen
>Bez vyplněné OAuth Consent Screen nejde vytvořit OAuth clienta a bez OAuth clienta nezískáte client ID.

Bud jste v předchozím kroku kliknuli na "CONFIGURE CONSENT SCREEN" tlačítko, nebo se do konfigurace OAuth consent screen přepněte takhle:

1. klikněte na kartu "APIs & Services".
2. V menu vyberte OAuth consent screen

![APIs & Services btn](image-2.png)
![OAuth Consent Screen menu](image-3.png)

Tím se dostanete do klasické (staré) konfigurace (viz screenshot).

**My teď klikneme na tlačítko "GO TO NEW EXPERIENCE"**

![OAuth consent screen old configuration](image-5.png)

To vás přesměruje sem.

![OAuth consent screen new configuration](image-6.png)

Klikneme na "GET STARTED" a vyplníme formulář. Klikneme na "CREATE".

![OAuth consent screen new form](image-7.png)

Po úspěšném vytvoření budete přesměrování do záložky Overview, kde je tlačítko "CRATE OAUTH CLIENT".

![Google Auth Platform Overview](image-9.png)

Tím se dostáváme do pekla.

Po kliknutí na tlačítko "CRETE OAUTH CLEINT" jste přesměrování do záložky Clients, kde svítí tlačítko "CONFIGURE CONSENT SCREEN".

![Google Auth Platform Clients](image-10.png)

A jste v pekle.

Když znovu kliknete na tlačítko "CONFIGURE CONSENT SCREEN", jste přesměrování do sekce Branding, kde už jsou předvyplněné informace z formuláře, který jste před chvílí vyplňovali.

Můžete cokoliv změnit, vyplnit všechna pole .. nic nepomůže. Já už na tom hodiny strávil, nepalte na tom čas.

Řešení je následující.

Musíte vypublikovat appku.

U jednoho projektu mi stačilo pouze appku vypublikovat. U druhého jsem ještě musel "zneužít Verification Center".

![alt text](image-12.png)

Pokud vypublikování aplikace nepomůže. Zkuste nastavit nějaké sensitive scopes (Data Access záložka). 

Potom se zobrazí upozornění ohledně verifikace aplikce. V záložce **Verification Center** pak na vás, po najetí šipkou na text "PREPARE FOR VERIFICATION" vyskočí tlačítko "CREATE OAUTH CLIENT". 

![Verification center](image-11.png)

A tohle tlačítko funguje! Přesměruje vás na tu samou záložku "Clients", ale už můžete vytvořit klienta.

![Create OAuth client ID](image-13.png)

Ještě předtím, než klienta vytvoříte, můžete vrátit status aplikace zpět do Testing. OAuth client by už měl jít vytvořit.

Hnus? Ano. 

onex