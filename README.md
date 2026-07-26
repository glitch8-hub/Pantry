# PantryPantry Ledger, standalone
Same app, running outside Claude. Your pantry, recipes, and buy list live in
this browser's localStorage on your device. Nothing is sent anywhere except the
recipe and photo requests you make.
Files:
index.html is the whole app, CSS and JavaScript included. Nothing to build.
manifest.webmanifest, icon-192.png, icon-512.png make it installable.
sw.js caches the app so it opens with no signal.
Putting it online
localStorage and the service worker both want a real https address, so a hosted
copy behaves better than a file opened from your downloads folder. GitHub Pages
is free and takes a few minutes.
Make a new repository, public or private, called something like pantry.
Upload all six files to the root of it. On a phone: Add file, then Upload
files, then commit.
Settings, then Pages. Under Build and deployment set Source to
"Deploy from a branch", branch main, folder / (root). Save.
Wait a minute, then open https://<your-username>.github.io/pantry/.
Note that GitHub Pages sites are public even from a private repo on the free
plan, so treat the URL as guessable. There is nothing sensitive in the files.
Your pantry data never leaves your phone, and your API key is not in these
files.
Putting it on your home screen
Open the address in Chrome on Android, then the three dot menu, then Add to home
screen or Install app. On iPhone use Safari, then Share, then Add to Home
Screen. It opens without browser chrome and keeps its own data.
The API key
Recipe ideas, photo reading, and sorting a pasted inventory all call Claude, so
the app needs a key. Typing your pantry in by hand works without one.
Get a key at console.anthropic.com, under API keys. It needs a small amount
of credit on the account, separate from a Claude subscription.
Open the app, tap "add key" at the bottom, paste it, save.
The key is kept in localStorage on your device. The app sends it straight to
Anthropic with the anthropic-dangerous-direct-browser-access header, which is
their opt-in for calls made from a page rather than a server. That header is
fine for a personal app holding your own key, and would not be fine for a site
shipping somebody else's. Do not paste your key into the files or commit it.
Rough costs: a bulk paste of a couple hundred lines runs a handful of small
requests, and a recipe is two. Cents rather than dollars, but watch the console
if you paste a lot.
The buy list
It saves on its own, separately from the pantry, so ticks survive closing the
app mid-shop and a pantry problem cannot take the list down with it.
"Send list" copies a link with the list packed into it. Text that link to
whoever is shopping and it opens on their phone, in their installed copy if they
have one, with the items ready to tick. Their ticks stay on their phone. It is a
handoff, not live sync, so for two people ticking the same list at once use the
"copy for keep" button and a shared Google Keep checklist instead.
Moving your existing pantry across
In the Claude version, tap "back up" at the bottom and copy the text. In this
version, tap "restore", paste it, then "load it". The two use the same format.
Do the same thing in reverse now and then. A backup pasted into a note is the
only copy that survives clearing your browser data.
Changing it later
index.html is a bundled build, so it is not meant to be edited by hand. The
readable source is the .jsx file from the conversation this came from. Ask
Claude for changes there and rebuild, or paste the source into a new
conversation.
