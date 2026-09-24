# Katla Cookie Consent — Google Tag Manager template

A Community Template for installing Katla from Google Tag Manager, with Google Consent Mode v2.

## Why a template and not Custom HTML

GTM runs a Custom HTML tag by inserting its script into the page, and that script executes
after the Initialization event. A Consent Mode default declared from it therefore arrives
after Google tags on the Initialization trigger have already read consent, and Tag Assistant
reports "A tag read consent state before a default was set". A template's
`setDefaultConsentState` applies synchronously during Consent Initialization, ahead of every
other tag.

## What the tag does

1. Declares the default: `ad_storage`, `analytics_storage`, `ad_user_data` and
   `ad_personalization` denied, with `wait_for_update` (500 ms unless changed).
2. For a returning visitor, reads `_katla_consent` and sends their stored choice as an
   update straight away.
3. Sets `window.__katlaGcmDefault` and injects `https://cdn.katla.app/{siteId}.consent.js`.
   The engine shows the banner, runs the cookie guard and sends `gtag('consent', 'update')`
   when the visitor chooses: `analytics` → `analytics_storage`, `marketing` → the three ad
   signals.

Optional: `ads_data_redaction` and `url_passthrough`.

## Setup

1. Templates → Tag Templates → New → ⋮ → Import, and choose `template.tpl`
   (or add "Katla Cookie Consent" from the Community Template Gallery once published).
2. Tags → New → Katla Cookie Consent. Enter the site ID from Settings → Site ID.
3. Trigger: **Consent Initialization - All Pages**.
4. Leave Consent Mode enabled for the site in Katla; remove any Custom HTML Katla tag.

## Gallery submission

The gallery reads `template.tpl` and `metadata.yaml` from the root of a public GitHub
repository. Mirror this folder to one, set the commit sha in `metadata.yaml`, and submit it at
https://tagmanager.google.com/gallery/#/submit.

The tests in `template.tpl` run in the GTM template editor (Tests tab).
