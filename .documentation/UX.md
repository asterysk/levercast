# Levercast - User Interface Description Document (Celestial Flow)

This document outlines the User Interface (UI) design direction for Levercast, tailored for Soulpreneurs, based on the "Celestial Flow" concept.

## 1. Overall Concept: Celestial Flow

* **Feel:** Expansive, intuitive, calming, inspirational, and slightly mystical. Aims to create a supportive digital environment for content creation.
* **Aesthetic:** Primarily dark mode, utilizing deep cosmic colors, soft glows, and flowing interactions to evoke a sense of calm expansiveness and connection.

## 2. Layout Structure

* **Overall:** A fluid, responsive web application layout adapting smoothly across desktop and mobile screens. Aims for an intuitive feel over rigid boxes.
* **Navigation:** Primary navigation likely via a sleek, dark sidebar (desktop) or collapsed menu/bottom bar (mobile), using clear icons and text with subtle glow effects for active states.
* **Containment:** Content organized using card-like elements with soft, rounded corners. Sections may blend using subtle gradients or dividers aligned with the celestial theme.
* **Spacing:** Generous use of negative space ("cosmic space") enhances clarity and maintains a calm, uncluttered feel.

## 3. Core Components

* **Buttons:** Rounded corners, potentially with subtle deep blue/purple gradient fills or metallic accent borders (silver/gold). Hover/active states feature a soft glow effect. CTAs are distinct but harmonious.
* **Input Fields:** Clean, dark input areas with light text. Rounded corners. Clear focus states, possibly using a subtle border glow in an accent color. Placeholder text is elegant and encouraging.
* **Cards:** Used for posts, drafts, templates, analytics summaries. Dark background (slightly lighter than main background), rounded corners, potentially subtle borders or depth effects.
* **Modals/Pop-ups:** Consistent dark theme with rounded corners for confirmations, settings, editors, etc.
* **Icons:** Clean, minimalist icons rendered in light colors for contrast. May incorporate subtle celestial motifs (stars, crescents, feathers) where contextually appropriate and clear.

## 4. Interaction Patterns

* **Transitions:** Smooth, soft animations and fade effects for page/section transitions, minimizing jarring shifts.
* **Hover Effects:** Subtle glow effects or slight scaling on interactive elements provide clear feedback without being distracting.
* **Feedback:** Clear, unobtrusive visual feedback for actions (saving, publishing, errors) using notifications or state changes.
* **Workflow Focus:** Interactions designed to be intuitive, guiding the user naturally through core tasks (capture -> generate -> preview/edit -> schedule/publish).

## 5. Visual Design Elements & Color Scheme

* **Primary Mode:** Dark mode.
* **Color Palette:** Base of deep blues and purples. Accents of softer teals, pinks, lavenders, silver, or subtle gold. Used for highlights, CTAs, and data visualization.
* **Backgrounds:** Subtle, slow-moving gradients (nebula/night sky) or static dark cosmic textures may be used, ensuring text legibility is paramount.
* **Imagery:** System imagery (placeholders, illustrations) aligns with the mystical/inspirational theme. User images are displayed clearly.

## 6. Mobile, Web App, Desktop Considerations

* **Platform:** Responsive Web Application.
* **Desktop:** Leverages space for potential side-by-side views (e.g., editor/preview), full dashboard visibility, and easy navigation.
* **Mobile:** Adapts to a single-column layout. Collapsible navigation. Appropriately sized touch targets. Dark mode benefits battery life on relevant screens. Key actions remain easily accessible.

## 7. Typography

* **Font:** A clean, elegant, highly readable sans-serif font family (Specific font TBD - e.g., Inter, Lato, Nunito Sans). Potential for a slightly more decorative but readable font for major headings if desired.
* **Hierarchy:** Clear typographic scale using size, weight, and color/opacity variations for headings, body text, labels, etc.
* **Color:** Primarily light colors (white, light grey, soft pastels) for high contrast against dark backgrounds. Accent colors used sparingly for links or emphasis.

## 8. Accessibility

* **Contrast:** Adherence to WCAG AA standards for text/background contrast.
* **Keyboard Navigation:** Fully navigable via keyboard with clear visual focus indicators (e.g., subtle glow).
* **Screen Readers:** Semantic HTML structure and ARIA attributes used where necessary for screen reader compatibility.
* **Target Sizes:** Adequate touch target sizes, especially for mobile.
* **Readability:** Prioritized through clean typography, generous spacing, and non-distracting backgrounds.

## 9. Key Screen Descriptions

* **Dashboard & Idea Input:**
    * Features prominent text input area (image attach option nearby), primary action button ("Generate Posts" / "Save Draft"), potential inspirational greeting, and overview cards for recent drafts/posts. Main navigation is accessible.
* **Preview & Edit:**
    * Displays generated posts in platform-mimicking preview cards (dark theme). Allows inline text editing within previews. Shows adapted image previews. Provides "Publish," "Schedule," and "Save Draft" actions per post or overall. Layout adapts (side-by-side/tabbed) based on screen size.
* **Template Manager:**
    * Lists existing templates as cards with edit/delete actions. Includes a clear button to create new templates. The editor (modal/separate view) provides fields for template name and prompt instructions.
* **Analytics Dashboard:**
    * Presents key metrics (views, likes, comments, shares, etc.) via summary cards and visual charts (lines, bars) using the theme's accent colors. Includes date range selectors and potentially a table view of individual post performance. Focus on clear data visualization.
* **Scheduling View:**
    * Primarily a calendar interface (monthly/weekly) showing scheduled posts as indicators on dates. Allows interaction (hover for details, click for options). Includes controls to navigate dates. Provides modal/panel access to view details and Edit/Reschedule/Unschedule specific posts. A list view alternative may be offered.