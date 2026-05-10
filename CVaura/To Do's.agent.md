To Do's

####---> need to change the email address to pushparaj.fullstack.dev@gmail.com (email js)
####---> Need to fix the responsiveness of the website for mobile and tablet devices.

####---> Try to automate the content fetcher from google sheets for Projects card with animations

I need to refactor my React portfolio app to load the PROJECTS section dynamically from Google Sheets instead of using hardcoded data.

## Current hardcoded structure:

const PROJECTS = [
"Built and maintain a tool to calculate employee performance using trackers and factor-based scoring.",
"Designed a secure data migration tool to move information from a public server to a local server.",
"Created a questionnaire generation platform and API flow to deliver survey questions to mobile apps.",
];

---

## Google Sheet name:

## projects

## Google Sheet structure:

## project_type | project | description

## Example sheet data:

main | Built and maintain a tool to calculate employee performance using trackers and factor-based scoring. | Nature provides clean air to breathe.
| | Trees help reduce pollution.
| | Rivers supply fresh water for living beings.
| | Forests are home to many animals and birds.

main | Designed a secure data migration tool to move information from a public server to a local server. | Sunlight gives energy to plants and humans.
| | Rain helps crops grow.

small | This is a small project | Nature offers medicinal plants and herbs.
| The beauty of nature brings peace and happiness.

---

Important Requirements:

1. Only rows where project_type = "main" should be shown as project cards in the main UI.
2. Rows with empty project/project_type belong to the previous project block.
3. Every description row should become an item inside the description array.
4. The implementation should support unlimited description rows without code changes.

## Expected final normalized structure:

{
"main": [
{
"project": "Built and maintain a tool to calculate employee performance using trackers and factor-based scoring.",
"description": [
"Nature provides clean air to breathe.",
"Trees help reduce pollution.",
"Rivers supply fresh water for living beings."
]
},
{
"project": "Designed a secure data migration tool to move information from a public server to a local server.",
"description": [
"Sunlight gives energy to plants and humans.",
"Rain helps crops grow."
]
}
],

"small": [
{
"project": "This is a small project",
"description": [
"Nature offers medicinal plants and herbs.",
"The beauty of nature brings peace and happiness."
]
}
]
}

---

Requirements:

1. Fetch all rows from the "projects" sheet using my existing fetchSheetColumns() helper.
2. Create a normalizeProjects() function.
3. Group rows by:
   - project_type
   - project
4. Detect a new project block whenever:
   - project_type has a value
   - OR project has a value
5. Append all related description rows into the description array.
6. Ignore empty descriptions.
7. Replace the hardcoded PROJECTS constant with dynamic state-driven data.
8. Only render "main" projects as cards in the main UI.
9. Add a "View Details" button to every project card.
10. Button styling, colors, hover effects, and UI should dynamically follow the currently selected theme.
11. When user clicks "View Details":
    - open a modal/card/dialog
    - modal title should be the project value
    - modal content should render all description points as a list
12. The modal/card/dialog UI should also dynamically adapt to the selected theme.
13. Add proper open/close state handling.
14. Keep the existing architecture and coding style intact.
15. Add loading and fallback handling if Google Sheets fails.

## Expected Output:

- normalizeProjects() function
- Updated useState logic
- Updated loadData() integration
- Updated return object
- Updated App() destructuring
- Updated JSX for project cards
- Theme-aware View Details button
- Theme-aware modal/dialog/card implementation
- Dynamic description rendering
- Clean scalable implementation

---

## Existing helper already available:

## async function fetchSheetColumns(sheetName)

The implementation should be scalable and support:

- unlimited project categories
- unlimited projects
- unlimited description rows
  without requiring future code changes.

for this requirement the changes all are done, but the UI look is not good, need to update it, and also while I clicks the view detail button, need to open the description in a different card llime a modal with the close option, not below the project card.

####---> Try to automate the content fetcher from google sheets for Skills card with animations
I need to refactor my React portfolio app to load the SKILLS section dynamically from Google Sheets instead of using hardcoded data.

## Current hardcoded structure:

const SKILL_GROUPS = [
{
title: "Back-End",
items: [
"Python",
"Django",
"PostgreSQL",
"REST APIs",
"AWS",
"Java",
"Version Control",
],
},
{
title: "Front-End",
items: [
"React",
"JavaScript",
"HTML",
"CSS",
"Bootstrap",
"Materialize",
"AMCharts",
],
},
];

---

## Google Sheet name:

## skills

## Google Sheet structure:

## Back-End | Front-End | Tools | Soft Skills

## Example sheet data:

Python | React | VS Code | Team Player
Django | JavaScript | PyCharm | Action Planning
PostgreSQL | HTML | Eclipse | Documentation
REST APIs | CSS | Bitbucket | Project Management
AWS | Bootstrap | Git | Customer Experience
Java | Materialize | Google Sheets |
Version Control | AMCharts | |

---

Requirements:

1. Fetch all data from the "skills" sheet using my existing fetchSheetColumns() helper.
2. Dynamically convert every column into:
   {
   title: "Column Name",
   items: ["list of skills"]
   }
3. Ignore empty cells.
4. Ignore completely empty columns.
5. Replace the hardcoded SKILL_GROUPS constant with dynamic state-driven data.
6. The implementation should automatically support:
   - adding new columns
   - removing columns
   - renaming columns
   - adding more skills
     without requiring code changes.

## Expected final normalized structure:

[
{
title: "Back-End",
items: [
"Python",
"Django",
"PostgreSQL",
"REST APIs",
"AWS",
"Java",
"Version Control"
]
},
{
title: "Front-End",
items: [
"React",
"JavaScript",
"HTML",
"CSS",
"Bootstrap",
"Materialize",
"AMCharts"
]
},
{
title: "Tools",
items: [
"VS Code",
"PyCharm",
"Eclipse",
"Bitbucket",
"Git",
"Google Sheets"
]
},
{
title: "Soft Skills",
items: [
"Team Player",
"Action Planning",
"Documentation",
"Project Management",
"Customer Experience"
]
}
]

---

Requirements for implementation:

1. Create a normalizeSkills() function.
2. Use Object.keys(data) dynamically instead of hardcoding column names.
3. Convert every sheet column into a skill group object.
4. Filter empty values from each items array.
5. Add loading and fallback handling if Google Sheets fails.
6. Keep the existing architecture and coding style intact.

## Existing helper already available:

## async function fetchSheetColumns(sheetName)

## Expected output:

- normalizeSkills() function
- Updated useState logic
- Updated loadData() integration
- Updated return object
- Updated App() destructuring
- Updated JSX rendering for skills
- Clean scalable implementation

---

Important:
The implementation should remain fully dynamic and future-proof.
If I later add a new column like:

- DevOps
- Databases
- Cloud
- Testing

it should automatically appear in the UI without any code changes.

####---> AMCharts bottom onhover issue.
I need to fix a hover interaction issue in my React portfolio site related to AMCharts cards.

Context:

- I am using AMCharts inside animated cards.
- There are 3 chart cards displayed in a layout.
- On hover:
  - hovered card expands to 75% width
  - remaining cards shrink to 25%
- The animation is already implemented and mostly works.

Current Issue:

- When the cursor moves near the bottom area of an AMCharts card, the hover state rapidly flickers.
- The card width repeatedly increases and decreases continuously.
- This creates a jitter/flickering effect until the cursor is moved away.
- The issue is especially noticeable around the chart rendering area and lower section of the card.

Expected Behavior:

- Hover expansion should remain stable while the cursor is anywhere inside the card.
- Width transition should happen only once when entering/leaving the card.
- No repeated resize/flickering should happen while hovering.
- AMCharts interactions should not interfere with parent hover detection.

Possible Cause:

- AMCharts internal DOM/canvas/SVG elements may be triggering repeated mouseenter/mouseleave events.
- The width animation may be causing layout recalculations that repeatedly retrigger hover events.

Requirements:

1. Analyze and fix the hover flickering issue.
2. Keep the existing expand/shrink animation behavior.
3. Ensure smooth transitions without repeated width recalculations.
4. Prevent AMCharts internal elements from breaking hover state detection.
5. Make the implementation stable and performant.
6. Ensure compatibility with React component structure.
7. Keep the existing UI design and theme intact.

Potential Fix Areas:

- mouseenter / mouseleave handling
- pointer-events handling
- event bubbling issues
- hover state management
- CSS transition behavior
- flex/grid width recalculation
- throttling/debouncing unnecessary state updates
- using transform scale instead of width where appropriate
- stabilizing parent container dimensions

Please provide:

- Root cause explanation
- Recommended approach
- Updated React hover handling logic
- Updated CSS/animation logic
- Best-practice solution for AMCharts + animated hover cards
- Clean and scalable fix without breaking current animations
