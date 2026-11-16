# MH Gold – Old is Gold
## Rotary AI for Good: Create Lasting Impact

**Area of focus:** Health — social connection, active aging and everyday well-being.

MH Gold is a community app concept for Mountain House residents age 55+. It helps neighbors find company for walks, exercise, games and small gatherings, and explore accessible wellness information.

## Fastest way to review

Open the public demo:

https://mountain-house-together.enjoyableoasis.chatgpt.site/

No account, sign-in, API key or address is needed. The default app opens as a fictional neighbor. The yellow demo banner explains the simulation. Use a recent Chrome, Edge, Safari or Firefox browser.

**Demo data is fictional.** RSVPs and messages stay in the current page's memory. Reloading or selecting **Reset demo** clears changes. No real residents are contacted and no real event registration is made.

## Run locally from the repository

### Requirements

- Node.js **24 LTS**, including npm. Node 24 is recommended because the API integration tests use its built-in SQLite support.
- Internet access to install dependencies. Source links and official event pages also require internet access.
- A terminal opened in the project folder containing `package.json`.

### Steps

If reviewing a GitHub repository, clone its actual URL and enter its folder:

```sh
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

Replace those placeholders with the submitted repository. If using the ZIP, extract it and open the terminal inside its **MH-Gold** folder instead.

Install dependencies and start the development server:

```sh
npm ci
npm run dev
```

Open **http://localhost:5173/**, or the URL printed by the terminal if it differs. Keep the terminal running while reviewing; press **Ctrl+C** to stop it.

The normal demo needs **no environment variables, database migration, API key, sign-in or residency approval**. Keep the included hidden `.openai` folder: the build imports its configuration. Do not copy checkout-local `.sites-runtime` state or `node_modules` from another computer.

## Suggested 3–5 minute walkthrough

1. **Our neighborhood:** Note the app branding, 55+ audience and clear demo banner. Try the **Aa** larger-text control.
2. **Gather & connect:** Join the fictional morning walk. Its participant count increases. Open its **Discussion**, type a sample message, and send it. The message is local to your page; no real person receives it.
3. **My plans:** See joined gatherings. Return to the gathering and leave it to explore the RSVP behavior.
4. **Healthy Living:** Read wellness and home-safety tips with NIH source links. Ask “How can I sleep better?” in the curated guide. A medication question should direct you to a qualified professional rather than prescribe treatment.
5. **Healthy habits together:** Choose **Plan this activity**, confirm the prefilled title and description, then select a future date, time, public place and group size. Create the sample gathering and see it in your plans.
6. **Activity preferences:** Choose interests, pace and setting, acknowledge the local preview notice, and select **Preview activity matches**. Sample matches are explicitly labeled as interest matching, not live AI output.
7. **Play together:** Select **Play a demo neighbor** and open the board. You play X against a simple computer O. Alternatively try the same-device two-person practice board.
8. **Reset demo:** Clear changes and restore the fictional starting state.

## AI implementation and honest limits

The source includes a server-side OpenAI Responses API integration in `app/api/recommend/route.ts`. It uses selected interests, pace and setting to rank dated official city listings. It validates returned event IDs against the original candidate list, uses the original event details and URLs, and does not send resident addresses, email addresses, medical details or private member gatherings.

**Live AI is not connected in this submission's public demo.** The no-sign-in demo shows explicitly labeled, local sample matches. This is not AI-generated output. Activating the live integration requires an owner-supplied `OPENAI_API_KEY` server secret; optional `OPENAI_MODEL` defaults to `gpt-4.1-mini`. The live endpoint requires authenticated access and consent. End-to-end calls to a live model have not been validated.

The wellness question guide is curated topic matching with NIH links, **not an AI medical assistant**. It does not diagnose, recommend medication changes or provide medical treatment.

## Other boundaries

- Official city events come from a dated snapshot, not a real-time feed. Confirm current availability, fees and registration with the organizer. Demo gatherings are fictional and separate from city listings.
- Real member enrollment includes a geographic address check and separate moderator residency review. The demo does not perform or prove these checks.
- The production backend retains authentication and membership checks; demo mode does not bypass them. The protected live app can be selected with `?mode=live` for a separately configured pilot.
- No email/push alerts, background checks, personal care services or emergency monitoring are provided.
- This is an independent community project, not an official City of Mountain House service.

## Optional validation commands

From the project root, with Node 24:

```sh
npx tsc --noEmit
node --test tests/rules.test.mjs
node --experimental-loader ./tests/loader.mjs --test tests/demo.test.mjs
node --experimental-loader ./tests/loader.mjs tests/recommend.integration.mjs
node --experimental-loader ./tests/loader.mjs tests/api.integration.mjs
```

Integration checks use synthetic identities and an in-memory database, not resident data. Recommendation checks cover authentication, consent, invalid input and the disconnected state; they do not call a live model. Node may print experimental loader/SQLite warnings.

## Hosting

Uploading to GitHub stores the code; it does not deploy the backend. GitHub Pages cannot host its Worker/D1 API. The current app uses React, TypeScript, Vinext and Cloudflare Worker/D1, with ChatGPT Sites authentication. A different hosting provider needs its own trusted authentication, storage bindings and secret configuration. Never expose an API key in browser code or commit secrets.
