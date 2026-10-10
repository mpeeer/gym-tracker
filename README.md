# KINETIC

**Train with intention. Track the work. Build consistency over time.**

KINETIC is a training tracker for planning workouts, logging sets, and reviewing your progress. It combines adaptable Push, Pull, Legs, and equipment-free Home routines with custom programs, recovery-friendly streaks, and a private account.

[Open KINETIC in Production](https://site-b2c1a53ecc6940c68e97b59b212d1900.freebuff.page) · [KINETIC landing page](https://mpeeer.github.io/gym-tracker/)

> The movement animations are stylized visual cues, not instructional videos, form checks, or medical advice. Recommendations are adjustable starting points, not individualized prescriptions or guaranteed outcomes.

## What you can do

### Plan training that fits your situation

- Answer a short onboarding flow about experience, goals, available equipment, and movement preferences.
- Choose **Push**, **Pull**, **Legs**, or **Home**. The Home routine requires no equipment.
- Create and manage your own routines: add movements, choose sets, reps, and rest, reorder exercises, edit or duplicate plans, and remove routines.
- Open an exercise to see its target muscles, notes, and a simple looping movement illustration. Pause or play the animation.
- See suggested sets and reps based on your selected training goal and experience level. Adjust them in the exercise view; save a new personal plan or update the matching custom routine or active session.

### Log workouts and review progress

- Record reps and load for each set, then mark completed sets as you go.
- Use the rest timer, including pause and add-time controls.
- Review completed sessions and your training history.
- Track weekly training, streaks, recovery check-ins, experience points, levels, and milestones. Intentional recovery check-ins count toward consistency; the app does not reward exercising every day.
- See approximate workout-duration ranges based on planned sets, reps, prescribed rest between sets, warm-up, and transitions. Real workout times vary.
- Switch between kilograms and pounds; export your training data as JSON when you want a copy.

### Personalize your space

- Choose Sage, Slate, Stone, or Plum, then pick a custom accent color.
- Theme preferences are saved with the signed-in account.
- Choose metric or imperial units and update measurements or weekly goals later.

## Getting started

1. Open [KINETIC](https://site-b2c1a53ecc6940c68e97b59b212d1900.freebuff.page).
2. Choose **Log in** if you already have an account or **Create an account** to sign up through Freebuff.
3. Complete onboarding to get a starting routine.
4. Optionally add height, weight, and a target in the post-account setup; measurements can be skipped or edited later.
5. Start a session, open an exercise to review its notes and adjustable targets, then log each set.
6. Check Preferences to edit your profile, themes, units, data export, or training data.

## Goals and measurements

The training track is a flexible planning aid—not an optimized medical or nutrition plan. Height and weight alone cannot determine a safe goal or predict results. KINETIC does not prescribe calories, promise muscle or weight gain, or promise a completion date.

For some adult users who choose a weight-loss goal, the app may show a broad illustrative range based on the requested change and a general public-health reference. The range is not a prediction or recommendation to lose weight. It is withheld when the app’s limited safety checks indicate it should not be shown. BMI is a screening measure, not a diagnosis or measure of body composition. Consider a qualified health professional for personal guidance, especially if you are under 20, pregnant, have a relevant health condition, or have concerns about eating or weight.

References: [CDC: losing weight](https://www.cdc.gov/healthy-weight-growth/losing-weight/index.html) · [CDC: adult BMI categories](https://www.cdc.gov/bmi/adult-calculator/bmi-categories.html) · [NHS: healthy ways to gain weight](https://www.nhs.uk/live-well/healthy-weight/managing-your-weight/healthy-ways-to-gain-weight/)

## Account, privacy, and your data

- Sign-in and account creation use **Sign in with Freebuff**. KINETIC does not handle your Freebuff password.
- Signed-in workout state is stored server-side in a private database and scoped to the authenticated account. The server—not browser-provided profile identifiers—determines which account’s data can be read or changed.
- Account training data is not saved to browser `localStorage`; session tokens are not placed in browser storage.
- You can export a JSON copy or clear KINETIC training data in Preferences. Exported files may include measurements; keep them somewhere private.
- Clearing KINETIC training data does not delete your Freebuff account.
- Changes made offline or during a save error may not reach your account. Wait for the saved status before closing the tab. If another tab has changed the record, KINETIC reports a conflict rather than silently overwriting it.
- Older local-only data is not automatically merged into a signed-in account. Export it before clearing browser data if you need to keep it.

## Training and safety notes

KINETIC is a tracker, not a healthcare provider or substitute for a qualified coach. Exercise suggestions and movement illustrations are general, and may not be suitable for every person. Select a comfortable range and a load you can control; stop if you feel pain. If you have an injury, health condition, are returning after illness, or need individualized advice, consult an appropriate professional. Seek urgent care for emergency symptoms.

The **Real help** area links to general resources from ACSM, AAOS, the CDC, and NHS. Those links do not diagnose or treat an individual condition.

## For contributors and developers

### Tech stack

- React and TypeScript with Vite
- Tailwind CSS, Lucide icons, and Canvas-based low-poly muscle views
- Cloudflare Worker API, D1 database, and Sign in with Freebuff
- Vitest, Testing Library, and workerd/Miniflare tests

### Requirements and local setup

Use Node.js 20.19+ or 22.12+.

```sh
npm ci
npm run typecheck
npm test
npm run build
```

For local Worker/API testing, start Wrangler in one terminal:

```sh
npm run dev:worker
```

Then start the Vite frontend in another:

```sh
npm run dev -- --host 0.0.0.0 --port 3000
```

Vite proxies `/api` and `/auth` to the local Worker at `http://localhost:8787`. Use the registered **development** auth configuration locally; production auth configuration is managed by the hosting environment. Never put secrets or platform tokens in the repository.

`npm run build` typechecks and builds the frontend to `dist/`, then bundles `server/worker.ts` to `deployment/worker.js`. Freebuff Sites publishes the Worker and static assets using `deployment/manifest.json`. The GitHub Pages workflow publishes only `landing-page/`, a small standalone KINETIC splash page; it does not build or host the interactive tracker.

### Tests

```sh
npm run typecheck
npm test
npm run build
```

The test suite covers onboarding, routine editing, set logging, timer behavior, goal recommendations, duration estimates, themes, persistence, and account-data protection. Worker API tests exercise authentication boundaries and D1 behavior in a local Workers runtime. A passing local suite does not replace a real browser sign-in, responsive-layout, or end-to-end production check.

## Project structure

```text
landing-page/       GitHub Pages KINETIC splash page
.github/workflows/  GitHub Pages publishing workflow
src/                React app, components, styles, and frontend tests
server/             Worker API and Worker runtime tests
deployment/         Worker bundle and Freebuff Sites manifest
public/             Static public assets
```

## License

See [LICENSE](LICENSE).
