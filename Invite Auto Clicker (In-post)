/*
==================================================
Facebook Invite Auto Clicker (In-post)
==================================================

Description:
- This script is designed for the Facebook Invite popup in Meta Business Suite.
- Go to Meta Business Suite and open the Inbox, then the Facebook Comments tab.
- Open a post with reactions, then click the Like/Reaction count to open the Invite popup.
- Scroll down to reveal all available buttons for clicking.
- Keep the Invite popup open and run this script from the browser console.
- Automatically clicks all visible "Invite" buttons.
- Waits 2 seconds after each click to verify success.
- Stops automatically if Facebook temporarily blocks sending more invites.
- Uses a random delay (3–5 seconds) between successful clicks.
- Displays progress and estimated remaining time while running.

Run Environment:
- Browser Developer Console

Dependencies:
- None

How to Run:
1. Open the target Facebook page.
2. Press F12 or Ctrl + Shift + I.
3. Open the Console tab.
4. Paste this script.
5. Press Enter.

Install Command:
# No installation required.

Run Command:
# Paste into the browser console and press Enter.

==================================================
*/


/* ------------------------------------------------------------
 * Configuration
 * ---------------------------------------------------------- */

const INVITE_BUTTON_SELECTOR =
    "span.x1lliihq.x6ikm8r.x10wlt62.x1n2onr6.xlyipyv.xuxw1ft";

const VERIFY_DELAY = 2000;
const MIN_DELAY = 3000;
const MAX_DELAY = 5000;

/* ------------------------------------------------------------
 * State
 * ---------------------------------------------------------- */

let clickCount = 0;

/* ------------------------------------------------------------
 * Returns the first available Invite button.
 * ---------------------------------------------------------- */
function getNextInviteButton() {
    const buttons = document.querySelectorAll(INVITE_BUTTON_SELECTOR);

    for (const button of buttons) {
        if (button.textContent.trim() === "Invite") {
            return button;
        }
    }

    return null;
}

/* ------------------------------------------------------------
 * Generates a random delay.
 * ---------------------------------------------------------- */
function getRandomDelay(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

/* ------------------------------------------------------------
 * Main processing loop.
 * ---------------------------------------------------------- */
function processNextInvite() {
    const button = getNextInviteButton();

    if (!button) {
        console.clear();
        console.log("✅ No Invite buttons found.");
        console.log(`✔ Total successful clicks: ${clickCount}`);

        alert(
            `Invite process completed.\n\nTotal successful clicks: ${clickCount}`
        );

        location.reload();
        return;
    }

    // Scroll button into view.
    button.scrollIntoView({
        behavior: "smooth",
        block: "center",
    });

    // Click button.
    button.click();
    clickCount++;

    console.clear();
    console.log("⏳ Running...");
    console.log(`✔ Successful clicks: ${clickCount}`);

    // Verify whether the button state changed.
    setTimeout(() => {
        if (button.textContent.trim() === "Invite") {
            console.clear();
            console.error("🚨 Invite action appears to be blocked or limited.");
            console.log(`✔ Successful clicks before stop: ${clickCount - 1}`);
            return;
        }

        const delay = getRandomDelay(MIN_DELAY, MAX_DELAY);
        setTimeout(processNextInvite, delay);
    }, VERIFY_DELAY);
}

/* ------------------------------------------------------------
 * Start Script
 * ---------------------------------------------------------- */

console.clear();
console.log("🚀 Facebook Invite Auto Clicker started...");

setTimeout(processNextInvite, 1000);
