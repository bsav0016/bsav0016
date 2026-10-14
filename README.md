# Brian Savidge — Software Engineer & Technical Lead

I build and ship software products end to end, from architecture and backend services to mobile interfaces, payments, and production deployment.

- **Product development:** Built and published mobile applications, including the AFT Score Calculator, with 84,000+ downloads.
- **Full-stack engineering:** TypeScript, React, React Native, Python, Django, SQL, and cloud deployment.
- **Technical leadership:** Army technical leader with experience leading developers and data teams and translating operational needs into software.
- **Robotics:** M.S. in Computer Science from Georgia Tech, focused on computational perception and robotics, with hands-on UAS and sensor-fusion experience.

I'm interested in senior software engineering, hands-on technical leadership, and robotics / controls engineering roles, particularly in defense tech, robotics, and software products. Open to remote, or in Knoxville, Nashville, Chattanooga, Lexington or Asheville.

[LinkedIn](https://www.linkedin.com/in/brian-savidge) · [Email](mailto:bsav0016@gmail.com)

## Featured projects

<p>
<a href="https://github.com/bsav0016/collagecreations"><img src="https://raw.githubusercontent.com/bsav0016/collagecreations/main/docs/screenshots/light-dark-preview.png" alt="Collage Creations: light and dark preview of a heart-shaped photo mosaic" height="200"></a>
<a href="https://github.com/bsav0016/ACFTScoreCalculatorFrontend"><img src="https://raw.githubusercontent.com/bsav0016/ACFTScoreCalculatorFrontend/main/docs/screenshots/calculator.png" alt="AFT Score Calculator: event results entered and scored" height="200"></a>
<a href="https://github.com/bsav0016/Discores"><img src="https://raw.githubusercontent.com/bsav0016/Discores/main/docs/screenshots/overview.png" alt="Discores: disc golf scorecard, course search and round history" height="200"></a>
<a href="https://github.com/bsav0016/AlgoTrackerFrontend"><img src="https://raw.githubusercontent.com/bsav0016/AlgoTrackerFrontend/master/docs/screenshots/backtest-results.png" alt="AlgoTracker: back-test chart with buy and sell markers and return, Sharpe and Sortino ratios" height="200"></a>
</p>

### 🖼️ [Collage Creations](https://github.com/bsav0016/collagecreations) – live at [collagecreations.org](https://collagecreations.org)
An online shop that turns customers' photos into printed photo mosaics. React + TypeScript storefront with a real-time progress bar, Stripe checkout and sign-in (Google, Microsoft, emailed code); Django + Celery backend that builds the collage with OpenCV, stores images in object storage and deploys automatically from CI. *(Backend repo is private; happy to walk through it.)*
`React` `TypeScript` `Vite` `Tailwind` `Django` `Celery` `Redis` `PostgreSQL` `OpenCV` `Stripe`

### 🪖 [AFT Score Calculator](https://github.com/bsav0016/ACFTScoreCalculatorFrontend) – on the [App Store](https://apps.apple.com/us/app/updated-acft-score-calculator/id1619926227)
Army Fitness Test scoring app with percentile rankings, a goal planner and saved results. Expo / React Native, with scoring tables generated from the official charts by Python scripts, and a Django API that computes privacy-preserving percentiles (no result is shown for groups under 20). *(Backend repo is private.)*
`React Native` `Expo` `JavaScript` `Django` `PostgreSQL` `EAS`

### ⛳ [Discores](https://github.com/bsav0016/Discores) – offline-first disc golf scorecard
Keeps score on the course with no signal: rounds are written to on-device SQLite and synced idempotently to Supabase. Includes friends and shared rounds with confirmation, QR invites, report/block tools, Apple and Google sign-in, and in-app account deletion. Type-checked and tested in CI.
`Expo` `TypeScript` `SQLite` `Supabase` `PostgreSQL` `Jest`

### 📈 [AlgoTracker](https://github.com/bsav0016/AlgoTrackerFrontend) – build, back-test and follow trading strategies
Build strategies from seven technical indicators, back-test them on historical prices, and subscribe to get a push notification when one signals a trade. Expo / React Native app on a Django REST API: back-tests run server-side with pandas, a separate websocket worker streams a live price feed into RQ jobs, and credits are bought through Stripe or RevenueCat. The backend runs as a six-service Docker Compose stack behind Caddy. The API is in [AlgoTrackerBackend](https://github.com/bsav0016/AlgoTrackerBackend).
`React Native` `Expo` `TypeScript` `Django` `pandas` `Redis` `PostgreSQL` `Docker Compose` `Stripe`

## More projects

- [Tax Projection](https://github.com/bsav0016/Tax-Projection) – browser-only wage projection with Excel export ([live](https://bsav0016.github.io/Tax-Projection/))
- [Diagonal Duel](https://github.com/bsav0016/DiagonalDuelFrontend) – online and offline strategy board game with an alpha-beta AI and Elo ratings
- [Math Mad Minute](https://github.com/bsav0016/MadMinute) – 60-second arithmetic drill app

## Engineering notes

- [A security and correctness review of my own projects](docs/engineering-notes/secrets-and-webhook-review.md) – credentials in git history, an unauthenticated webhook and game-rule bugs: what I found, how I handled it and what I do differently now

## Tech

**Languages:** TypeScript · JavaScript · Python
**Front end / mobile:** React · React Native · Expo · Vite · Tailwind CSS · React Router
**Back end:** Django · Django REST Framework · Celery · RQ · Redis · Supabase
**Data:** PostgreSQL · SQLite
**Payments & services:** Stripe · RevenueCat · Sentry · Resend · Firebase
**Infra & tooling:** Docker Compose · GitHub Actions · DigitalOcean · Heroku · EAS · Caddy · nginx
**Testing:** Jest · Django test runner
