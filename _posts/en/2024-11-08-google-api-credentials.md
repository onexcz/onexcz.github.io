---
layout: post
title:  "How to get a Google API client ID and not go crazy"
date:   2024-11-08 11:00:00 +0100
permalink: /en/google-cleint-id-through-google-auth-platform
categories: en google auth api
---

This is how to get a Google API client ID through [Google Auth Platform](https://console.cloud.google.com/auth/audience) and not go crazy.

Google Auth Platform is an alternative to the traditional way of configuring OAuth client IDs, which should be disappearing soon. See warning:
> OAuth consent screen management is changing. This page has been replaced with a new, easier-to-use experience. The current pages will only be available for a few more days.


TLDR;
If you use the old way of setting the OAuth client ID, it should work. This article is about the new administration via [Google Auth Platform](https://console.cloud.google.com/auth/audience). And it has bugs.

## When should I read this article?
- I want to implement Sign-In with Google in my application
- I don't want to spend hours trying to figure out why it doesn't work
- The old way of setting up OAuth no longer works
- I want to learn with Google Auth Platform

## Before we get started
If the old administration still works and if you don't want to learn a new one, just follow one of the tutorials.

- [Google tutorial](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid)
- [Slightly better tutorial](https://www.balbooa.com/help/gridbox-documentation/integrations/other/google-client-id)

## How to get Google client ID
First you need to create a project in [Google Cloud Console](https://console.cloud.google.com/).

It's free, you just need to be logged into your Google Account. You can create 10 projects for free. After that you can apply for an increase.

### 1. Create a project in Google Cloud Console
Go to [Google Cloud Console](https://console.cloud.google.com/), click "**Select project**" and click "**New Project**" in the top right corner.

After creating a project, switch to the project via the "**Select project**" button.

If you try to create an OAuth client now, it will turn out like this.

![Create OAuth client without consent screen](/assets/images/google-client-id/image-4.png)

### 2. Configuring the OAuth Consent Screen
>You cannot create an OAuth client ID without a completed OAuth Consent Screen.

Either you clicked the "**CONFIGURE CONSENT SCREEN**" button in the previous step or you can move to the OAuth consent screen configuration as follows:

1. In the project's dasboard, click on the "**APIs & Services**" tab (or via the drop-down menu in the upper left corner)
2. Select OAuth consent screen in the menu (in the left or right side of the page).

This will take you to the classic (old) configuration (see screenshot).

**We now click on the "GO TO NEW EXPERIENCE "** button.

![OAuth consent screen old configuration](/assets/images/google-client-id/image-5.png)

This will redirect you to [Google Auth Platform](https://console.cloud.google.com/auth/audience).

![OAuth consent screen new configuration](/assets/images/google-client-id/image-6.png)

Click on "**GET STARTED**" and fill out the form. Click on "**CREATE**".

![OAuth consent screen new form](/assets/images/google-client-id/image-7.png)

After successful creation, you will be redirected to the Overview tab where there is a button "**CRATE OAUTH CLIENT**".

![Google Auth Platform Overview](/assets/images/google-client-id/image-9.png)

This is where the hell starts.

When you click the "**CRETE OAUTH CLIENT**" button, you are taken to the Clients tab where you see the "**CONFIGURE CONSENT SCREEN**" button again.

![Google Auth Platform Clients](/assets/images/google-client-id/image-10.png)

And you're in hell.

When you click on the "**CONFIGURE CONSENT SCREEN**" button again, you are taken to the Branding section, where the information from the form you filled out a moment ago is already pre-populated.

You can change anything, fill in all the fields.. nothing helps (you can trust me).

### 3. Getting out of hell

The solution is as follows:

**You have to publish the app.**

You can publish the app in the Audience tab via the "**Publish App**" button.

![alt text](/assets/images/google-client-id/image-12.png)

One project was easy - all I had to do was publish the app. For another one, I still had to do some magic in **the Verification Center**.

If publishing the app doesn't help. Try setting up some sensitive scopes (Data Access menu). 

Then you will get a warning about verifying the app. 

In the **Verification Center** tab, the "**CREATE OAUTH CLIENT**" button will pop up when you click the arrow on the text "PREPARE FOR VERIFICATION". 

![Verification center](/assets/images/google-client-id/image-11.png)

And this button works! 

It redirects you to the same "Clients" tab - but you can already create a client.

![Create OAuth client ID](/assets/images/google-client-id/image-13.png)

Before you create the client, you can return the application status back to Testing. 

Gross? Yes. 

But you can create a Client ID for your app. And that's what we're all about!

onex