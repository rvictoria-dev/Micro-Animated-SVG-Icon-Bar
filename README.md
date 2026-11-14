# Micro-Animated SVG Icon Bar

### ₊⊹ About

This navigation bar transforms the mundane act of switching tabs into a tactile event. By embedding the animation logic directly into the SVG structure, create a system that feels organic, responsive, and deeply crafted. It is not just about showing the user where they are; it is about rewarding them for arriving there.

https://github.com/user-attachments/assets/b7397bf0-eae3-4e93-9229-e25748c189f7

---

### ★ Features

- Bar with four SVG icons: alarm, clock, timer, and stopwatch
- The active icon is highlighted in a light color, and the others appear darker
- Each icon has its own micro-animation when clicked:
  - **Alarm:** the bells ring
  - **Clock:** the hand makes a full rotation
  - **Timer:** the hourglass rotates halfway and the sand falls
  - **Stopwatch:** the top button is pressed and the hand rotates
- A light-colored circle pulses and expands around the button when it receives focus
- Minimalist design with a grayish-beige background

---

### .ᐟ.ᐟ How It Works

- **Structure:** The `nav` element has four buttons, and each one contains a `span` with the name (`.visually-hidden`) and an SVG drawn directly in the HTML. The strokes use `stroke=“currentColor”`, so the icon's color comes from the CSS.

- **Centered at zero:** All SVGs use `viewBox=“-50 -50 100 100”`, which places the point `(0, 0)` at the center of the icon. By default, SVG element transformations rotate around this point, so the rotation of the hands and the timer occurs around the center without any extra `transform-origin`.

- **Active item:** JavaScript listens for clicks on each button, removes the `active` class from all of them, and adds it only to the clicked button. This is what causes the color change: buttons without `.active` turn dark gray (`hsl(0, 0%, 35%)`), and the active button inherits the light color of the `body`.

- **Class-based animation:** Each animation exists only within a selector such as `button.active .rotate`. When a button gains the `active` class, its icon’s animation begins, and when it loses it, the icon returns to its initial state.

- **One animation per icon:**
   - **Alarm:** The `.jiggle` group wobbles between `-8deg` and `8deg` four times, and since the center is at `(0, 0)`, the bells rotate around the clock.
   - **Clock:** The hand (`.rotate`) rotates a full `360deg`.
   - **Timer:** the `.half-rotate` group rotates `180deg`. Then, the `.fall` property shifts the sand rectangle, and the `clip-path` shows only the part inside the hourglass, giving the impression that the sand is falling.
   - **Stopwatch:** The top button (`.push`) moves down `5px` and returns, and the hand rotates like on the clock.

- **Sequence with delay:** The `animation` is written in short notation (`0.8s 0.3s ...`), where the second time value is the delay. The icon waits `0.3s` to start, and the sand fall waits `1s` to occur after the hourglass flips. The `forwards` property keeps the icon in its final position.

- **Focus pulse:** The `button::before` is a light-colored circle with `scale(0)`. When the button receives focus (`:focus`), the `pulse` animation scales the circle up to `scale(2)` while the opacity drops to zero, creating a ripple around the icon.

- **Accessibility:** The text on each button is hidden from view but remains accessible to screen readers, since the icon alone does not indicate what the button does.

---

### ⚙️ Tech Stack

- **HTML5**
- **CSS3**
- **JavaScript (vanilla)**

---

### 🖿 Project structure

```
micro-animated-SVG-icon-bar/
├── index.html
├── style.css
├── script.js
└── README.md
```

---

### 📖 What i learned

- **HTML:** Draw icons directly in HTML using inline SVG, with `circle`, `path`, and groups (`g`)
- **SVG:** Use `viewBox=“-50 -50 100 100”` to center the point `(0, 0)` and rotate elements around it without `transform-origin`
- **SVG:** `stroke=“currentColor”` so the icon inherits its color from CSS
- **SVG:** `clip-path` to show only the part of the sand that’s inside the hourglass

- **CSS:** create micro-animations with `@keyframes` and `transform` (`rotate`, `translateY`)
- **CSS:** Use the shorthand form of `animation` with duration and delay so that animations play in sequence
- **CSS:** `animation-fill-mode: forwards` to keep the element in its final position
- **CSS:** create a pulse effect using a `::before` pseudo-element and `scale`
- **CSS:** hide text from view while keeping it accessible to screen readers using the `.visually-hidden` class

- **JavaScript:** Iterate through the buttons using `querySelectorAll` and `forEach`
- **JavaScript:** Move the `active` class from one button to another using `classList.add` and `classList.remove`, and let CSS handle the animation
