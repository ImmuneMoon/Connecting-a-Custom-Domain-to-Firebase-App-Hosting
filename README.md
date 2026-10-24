# README: Connecting a Custom Domain to Firebase App Hosting

## 📖 Overview
**Connecting a Custom Domain to Firebase App Hosting** is a step-by-step guide to publishing a website on Firebase App Hosting under your own domain, written for someone doing it for the first time. It follows the whole process in order:
- a domain registered at Squarespace;
- its DNS moved to Cloudflare, with `www` redirected and HTTPS enforced;
- a Firebase project with sign-in and a database;
- the code published to GitHub;
- an App Hosting backend;
- the domain and a second address connected, with their certificates;
- a live site, tested end to end.

Every step says where to click and what you should see. The snags that cost hours the first time are written in where they happen: the wrong Squarespace page, records Firebase sees late, the redirect warning that isn't one, and the header that decides which address a visitor asked for. They're gathered again in a troubleshooting table.

The guide was written from a real setup and checked against the official Squarespace, Cloudflare, Firebase and GitHub documentation as of October 2026. A Sources section links to every page it was checked against.

## 🗂 Contents of the Guide
The main document (`custom_domain_firebase_app_hosting_guide.md`) is organized into fourteen sections, after a short **Before You Start** checklist:
1. **How the Pieces Fit Together** - Registrar, nameservers, hosting and code host in plain words; the DNS record types; Cloudflare's orange and grey clouds; why new records can look missing for half an hour.
2. **Move Your DNS from Squarespace to Cloudflare** - Adding the domain to Cloudflare, which imported records to delete and which to keep, turning off DNSSEC first, switching to custom nameservers, and checking the result yourself.
3. **Set Up Cloudflare: HTTPS, Encryption and the www Redirect** - Always Use HTTPS, choosing an encryption mode (and why Flexible loops), and a `www` redirect done entirely in Cloudflare.
4. **Create and Prepare the Firebase Project** - The project ID you can't change, Analytics on or off, the Blaze plan with a budget alert, sign-in (email and password, Google, and sign-in links by email) and authorized domains, Firestore's permanent location, and the public web config in `apphosting.yaml`.
5. **Put Your Code on GitHub** - Keeping secrets out, publishing the folder you already have with GitHub Desktop, and getting your work onto `main`.
6. **Create the App Hosting Backend** - Region, connecting GitHub, root directory, live branch, automatic rollouts, the first rollout, and reading a failed build.
7. **Connect Your Custom Domains** - The A, TXT and certificate CNAME records, exactly how they go into Cloudflare, verifying them, why Firebase can see some late, and the certificate.
8. **Test the Live Site** - Command-line checks for every address and redirect, and a real sign-in, with what to check if the server disagrees.
9. **Two Addresses, One Backend: X-Forwarded-Host** - Serving a second domain from the same backend, with a Next.js example, a local test, a spoofing test and a caching note.
10. **Deploying Changes from Now On** - Push to `main`, watch the rollout.
11. **GitHub Actions on a Private Repository** - Why a frequent schedule runs out of free minutes, and waking a workflow from another repository with `repository_dispatch` and a narrowly scoped token.
12. **Signing In the GitHub Command Line** - `gh auth login`, step by step.
13. **Troubleshooting** - Every snag in one table: what you see, why, and what to do.
14. **Sources** - The official pages the guide was checked against.

## ⚠️ Important Notes
* **Turn DNSSEC off before switching nameservers.** If it's still on at Squarespace when Cloudflare takes over, the domain can stop working for a day or more. Section 2.3 covers it.
* **Keep every Firebase record "DNS only" (grey cloud).** An orange cloud on Firebase's records can break certificates, and with the Flexible encryption mode it causes a redirect loop.
* **On App Hosting, your domain arrives in `X-Forwarded-Host`, not `Host`.** Code that reads `Host` works on your own computer and then, live, can't tell your addresses apart. Section 9 covers it.
* **The Firebase web config is public; service account keys are not.** Committing the config is normal. A service account key in a repository is a full-power credential, and App Hosting doesn't need one.
* **Private repositories have limited free Actions minutes,** and each run counts as at least a minute. A job every 15 minutes uses more than the free allowance. Section 11 shows the alternative.
* **The Blaze plan is pay-as-you-go.** Set a budget alert (Section 4.2). It emails you; it doesn't stop spending.

## 🚀 How to Use
Open `custom_domain_firebase_app_hosting_guide.md` in any Markdown viewer, text editor or code editor (such as VS Code, Obsidian or GitHub's built-in preview). Read **Before You Start**, then work through Sections 2 to 8 in order. Most of the time goes on waiting for DNS and certificates, and each wait is a safe place to stop.
- Section 9 is only for a site with more than one address.
- Section 11 is only if you use GitHub Actions in a private repository.

For building the app itself (Firebase setup, emulators, security rules), see the companion guide, [Building Firebase Apps in Google Antigravity IDE](https://github.com/ImmuneMoon/Building-Firebase-Apps-in-Google-Antigravity-IDE).

## ☕ Support the Project

If you find this project helpful and want to support further development by Fulllion Creative Works, consider leaving a tip!

* [Donate via PayPal](https://www.paypal.com/donate/?hosted_button_id=LCDZX75HR4CLC)
* [Support on Ko-fi](https://ko-fi.com/fulllion)

---
© 2026 Fulllion Creative Works. All rights reserved.
