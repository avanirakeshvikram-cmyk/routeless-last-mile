
Build one single index.html file (HTML, CSS and JavaScript together, no backend). It’s the easiest thing to deploy and the hardest to break.
Open the file in your browser after every step. If something breaks, use the debug prompt at the bottom.
STEP 1: Core app
I'm in a 3-hour hackathon "Prompt Battle" called ROUTELESS: THE LAST MILE.
Problem: rural students depend on a few government buses. When buses are
unavailable, routes are disrupted, or demand exceeds capacity, students can't
reach school or college. Build an AI-powered rural transportation platform.

Build ONE single-file web app (index.html, vanilla HTML/CSS/JS, no frameworks,
no backend, works offline) with:
1. A student registration form: name, age, village (dropdown), destination
   institution (dropdown), preferred departure time, and a checkbox
   "Has exam today" plus exam time.
2. Sample data: 8 villages, 3 institutions, 6 buses (each with capacity, route
   as a list of villages, departure time), and 30 pre-generated students.
3. A dashboard showing: total students, total bus capacity, students assigned,
   students left unassigned.
4. Clean, mobile-friendly design with a green/blue theme.
Add clear comments in the code. Give me the complete file.
STEP 2: Smart bus allocation
Add an intelligent allocation engine to index.html. Rules:
- Assign each student to a bus that passes through their village and reaches
  their destination on time.
- Prioritize students with exams (earliest exam time first), then younger
  students (use the age field), then everyone else.
- Never exceed bus capacity.
- Show a table: bus, route, capacity, seats used, list of assigned students.
- Show a list of unassigned students with the reason.
Add a button "Run Allocation". Return the full updated file.
STEP 3: Alternatives for students with no bus
For every unassigned student, suggest an alternative: shared auto, carpool
with a nearby student, or walking if the distance is under 3 km. Add a village
distance matrix (sample data) and pick the cheapest feasible option. Show each
suggestion as a card with the estimated cost and travel time. Return the full file.
STEP 4: Demand prediction (this is the “AI” part judges look for)
Add a demand prediction panel. Using sample weekly data per village, predict
tomorrow's student demand with a simple moving average plus a weekday factor.
Show a bar chart (use plain canvas or CSS bars, no libraries) comparing
predicted demand vs. bus capacity per village, and flag villages where demand
will exceed capacity in red. Return the full file.
STEP 5: Polish
Polish the UI: add a header with the project name "ROUTELESS", a short
tagline, a summary banner, smooth animations, and make sure it works on a
phone screen. Also add an "Add Student" feature so new students can be
registered live and the allocation re-runs. Return the full file.
DEPLOY (do this before the surprise hurdle appears)
Go to github.com, click New repository, name it routeless, set it to Public, and tick “Add a README”.
Click Add file → Upload files, drag in index.html and prompts.md, then Commit.
Open Settings → Pages. Under Branch choose main and / (root), then Save.
After about 1 minute your live link appears: https://yourusername.github.io/routeless/
Open that link and check that it works. Submit the live link and the repo link.
SURPRISE HURDLE: “Exam Day Crisis” (100 minutes)

Do this on top of your working app. Push each version to GitHub as you go.

Hurdle prompt 1: crisis mode

Now handle a surprise crisis. Add a "Trigger Exam Day Crisis" button th…
