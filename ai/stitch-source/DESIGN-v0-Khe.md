# DESIGN.md: Khe (study planner)
## Overview
Khe is an Android study planner for university students who also work evening
shifts that change every week. The interface is calm, flat and quick to scan:
each visit lasts under a minute and is usually one-handed. Material 3, light
theme only, phone layout at 360x800 dp. All UI text is in Vietnamese.
## Colors
- primary #2251D9 (modern blue): the single main button per screen, selected tab, study sessions
- onPrimary #FFFFFF
- primaryContainer #DBE6FF: study session cards, selected chips
- onPrimaryContainer #0B2466
- secondary #8A4B2D (terracotta): work shifts only
- onSecondary #FFFFFF
- secondaryContainer #FFDBCC: work shift cards
- onSecondaryContainer #3A1707
- surface #F8FAFD (cool off-white): screen background
- surfaceContainer #EDF1F7: deadline cards, navigation bar, text fields
- onSurface #171A1F: primary text
- onSurfaceVariant #444A54: secondary text, unselected icons
- outline #717885: borders and dividers only, never text
- error #B3261E, onError #FFFFFF: validation errors and delete actions only
- errorContainer #F9DEDC, onErrorContainer #5F1410: "Quá hạn" label
- warningContainer #FFE9B8, onWarningContainer #5C3A00: "Sắp đến hạn" label, conflicting sessions
- successContainer #D6EFDB, onSuccessContainer #0F4221: "Đã nộp" label
## Typography
Font family: Be Vietnam Pro.
- headlineSmall 24/32 semibold: top-level screen titles
- titleLarge 20/28 semibold: app bar titles on nested screens, dialog titles
- titleMedium 16/24 semibold: card titles, day group headers
- bodyLarge 16/24 regular: main content, text field input
- bodyMedium 14/20 regular: times, course names, supporting text
- labelLarge 14/20 semibold: buttons, chips
- labelMedium 12/16 medium: navigation labels and short status labels only
Body text is never smaller than 14sp. Times and dates use tabular figures.
## Layout
- 4dp grid. Screen margins 16dp. Card padding 16dp. 12dp between cards. 24dp between sections.
- Every touch target is at least 48x48dp. List rows are at least 64dp tall.
- Primary action: one full-width filled button, 56dp tall, fixed at the bottom of nested screens.
- Schedules are vertical lists grouped by day. Never a week grid or month calendar.
- Long content scrolls vertically; the bottom button bar and navigation bar stay fixed.
## Elevation
Flat. Cards have no shadow and are separated from the background by fill color.
Only the navigation bar, the fixed bottom button bar, snackbars and dialogs are elevated.
## Shapes
- 8dp: chips and status labels
- 12dp: cards and text fields
- 16dp: the highlighted card on the Today screen
- 28dp: dialogs
- fully rounded: buttons
## Components
- Buttons: filled (main action, one per screen), tonal (secondary action), text (cancel, undo). Delete buttons use the error color. Labels start with a verb and name the result, e.g. "Lưu deadline", "Dời sang 20:30", "Thử lại".
- Text fields: outlined, 56dp tall, label always visible above the field. Error message directly under the field with an error icon. Dates and times use pickers.
- Cards: three types with the same structure. Study session: primaryContainer with a book icon. Work shift: secondaryContainer with a briefcase icon. Deadline: surfaceContainer with a status label and a progress bar.
- Status labels: always an icon plus text ("Quá hạn", "Hôm nay", "Còn 2 ngày", "Đã nộp"). Never color alone.
- Bottom navigation bar: 4 destinations, each with icon and label: Hôm nay, Kế hoạch, Deadline, Ca làm. Hidden on nested screens.
- App bar: top-level screens have a large left-aligned title and no back button. Nested screens have a back button, a title and at most one action.
- Dialogs: only when data would be lost. Title is a question, two buttons, the safe button on the left.
- Snackbar: shown after every undoable action, above the navigation bar, with a "Hoàn tác" action.
- Empty state: one 64dp outlined icon, one sentence, one button.
- Error state: what happened, a plain-language cause, a "Thử lại" button. No technical error codes.
- Icons: Material Symbols, outlined, 24dp.
## Do's and Don'ts
- Do keep one filled primary button per screen.
- Do place the main action in the lower half of the screen.
- Do tell study sessions and work shifts apart by icon and label as well as color.
- Don't use gradients, glassmorphism, heavy shadows, photos or multi-color illustrations.
- Don't add streaks, badges, points or any gamification.
- Don't use red for anything except errors and delete actions.
- Don't use exclamation marks or emoji in UI text.
- Don't design a dark theme, login screen or profile screen.
