# Assessment Answers

### 1. How to run
This is a pure Vanilla HTML/CSS/JS application. There are no build steps, no package managers, and nothing to install. 
**To run:** Simply open `index.html` in any web browser (Chrome, Safari, Firefox).

### 2. Stack & design choices
**Stack**: Vanilla HTML, CSS, and JavaScript. I chose a vanilla stack to demonstrate fundamental DOM manipulation, state management, and layout skills without relying on heavy frameworks or bundlers.

**Design Choices**:
1. **Sticky First Column on Mobile**: In `style.css`, I gave the `.sticky-col` class `position: sticky; left: 0;`. This preserves the mental model of a "weekly tracker chart" on small screens while allowing users to horizontally swipe through the days without losing track of which row belongs to which habit.
2. **"Today" Column Highlighting**: I added a subtle `--primary-light` background to the entire column representing the current day. This anchors the user visually, allowing them to glance at the tracker and instantly know exactly which column they need to click today, reducing cognitive load.

### 3. Responsive & accessibility
**Responsiveness**: The `.table-responsive` wrapper uses `overflow-x: auto;`. On a 360px phone, the user can swipe left and right to see the weekend, while the habit name stays glued to the left side. On a 1440px laptop, the table naturally expands to fill the central container.
**Accessibility Handled**: The check buttons are actual `<button>` elements, making them natively focusable via the `Tab` key, meaning users can navigate the grid using just their keyboard.
**Accessibility Skipped**: I knowingly skipped adding complex `aria-live` region announcements for screen readers when a habit is checked off or a streak increases. 

### 4. AI usage
- **Tool**: ChatGPT (GPT-4o)
- **Prompt**: *"Write a Javascript function that calculates a current consecutive daily streak given an array of date strings in 'YYYY-MM-DD' format. It should handle if the current day is not checked yet without breaking the streak."*
- **What it gave me**: A function that looped backward from `new Date()` using native JavaScript Date objects.
- **What I changed**: The AI's use of native `Date` objects caused timezone shift bugs when users tracked habits late at night. I refactored the logic to rely strictly on string manipulation (`YYYY-MM-DD`) and date-math without timezone dependencies, ensuring that "yesterday" is calculated predictably regardless of the user's local time.

### 5. Honest gap
The UI feedback when clicking a checkbox is currently instantaneous. Given another day, I would add CSS animations and transitions to make the checkmark pop or scale up smoothly, making the act of completing a habit feel more rewarding and tactile. I would also add an inline-edit feature instead of using `window.prompt()` for renaming habits.

### Defending Scope Choices
* **Start of week**: Monday. The weekend is conceptually the "end" of the week for most users' habits. Grouping the weekend at the right edge gives a satisfying conclusion to the weekly grid.
* **Streak Calculation**: The "current" streak counts up to yesterday if today is unchecked, but includes today if checked. If a user wakes up at 8 AM, they shouldn't see a "0 day streak" just because they haven't completed their evening habit yet. The streak only breaks if *yesterday* was missed.