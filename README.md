# RESQ: MDRRMO emergency reporting and dispatch

RESQ lets people report an emergency from their phone with one tap and lets the municipal disaster office (MDRRMO) see it,
send the nearest crew and warn the whole town. It has three parts that share one Firebase project:

| Part | Folder | Who uses it |
|------|--------|-------------|
| **RESQ** (citizen app, Android) | `mobile/` | People in the town: report, track help, see warnings and hazards |
| **RESQ Responder** (staff app, Android) | `mobile/` (`APP_VARIANT=responder`) | Ambulance, fire and police crews, and MDRRMO monitors |
| **Dispatch desk** (Windows desktop) | `admin/` | The MDRRMO desk: dispatch, alerts, hazards, citizens, reports |

Source code is private. This repo is a showcase with screenshots. Supporting pieces: `firestore.rules` (security rules), `functions/` (Cloud Functions that send push alerts),
`supabase/functions/manifest` (over-the-air update server), `reset-page/` (password reset page). Built with React Native (Expo), Firebase, and a Python (PyQt6) desktop app.

> All screenshots below were taken on a real phone and the real desk app, with made-up demo data placed at the San Enrique
> Municipal Hall (a public landmark) and a mocked phone location. Names, phone numbers and e-mail addresses of real people
> are hidden. The demo data tool is `admin/demo_data.py` (`seed`, `assign`, `clean`).

---

## 1. Citizen app

### Home: warnings, hazards, help on the way
<img src="docs/screenshots/citizen/01-home.png" width="260" align="left" hspace="12">

The home screen shows what matters first: the newest **area warning** from the MDRRMO (here a typhoon signal) with a shortcut
to the evacuation centers, a red banner when there are **hazards in your town**, and an orange **Help is on the way** card
while one of your reports is being answered (tap *Track it*). Under them is the big question, *What's the emergency?*

<br clear="all">

### Report an emergency
<img src="docs/screenshots/citizen/02-home-scrolled.png" width="260" align="left" hspace="12">

Pick **Accident**, **Medical** or **Other**, add a description and up to four photos (optional), and press **Send Report**.
The phone gets a GPS fix and opens a map so you can check the spot before anything is sent. Below the button are
shortcuts to **Call the MDRRMO**, the **Evacuation centers**, the **Hazards** map and your **Report history**.

<br clear="all">

<img src="docs/screenshots/citizen/03-emergency-other.png" width="260" align="left" hspace="12">

**Other** opens more choices: **Fire**, **Flood**, **Landslide**, **Earthquake**. If it is none of them, type what it is
(this is required for *Other*). The report goes to the MDRRMO of the town your pin is in.

<br clear="all">

### Confirm the spot on a map
<img src="docs/screenshots/citizen/16-home-confirm-map.png" width="260" align="left" hspace="12">

Before a report (and when you set your home) you see a map with a pin on your GPS position. Touch and hold the pin and drag
it, or tap the map, then confirm. The same screen is used to save your **home location**, which decides who receives area
warnings.

<br clear="all">

<img src="docs/screenshots/citizen/15-home-picker.png" width="260" align="left" hspace="12">

The first time, the app asks where your home is. Your spot is private: it is only used to decide who gets a warning.

<br clear="all">

### Track your report
<img src="docs/screenshots/citizen/08-report-status.png" width="260" align="left" hspace="12">

*Track it* opens the report: its status (**Pending**, **Dispatched**, **Resolved**), the incident pin, the crew that is
coming and, once they share their location, a live road **ETA**. Sent it by mistake? Call or text the MDRRMO from here. A
report that is still pending can be cancelled by you.

<br clear="all">

<img src="docs/screenshots/citizen/09-report-history.png" width="260" align="left" hspace="12">

**Report history** lists every report you sent with its status and the crew that answered.

<br clear="all">

### Hazards map (flooded road, landslide, fallen tree, ...)
<img src="docs/screenshots/citizen/04-hazards-list.png" width="260" align="left" hspace="12">

The MDRRMO and responders pin road hazards on a map: *do not cross*, flooded road, landslide, fallen tree, downed power
line, road blocked and more (13 kinds). Every phone sees the live ones with a note and how far each is from your home.
Phones near a new pin also get a **push notification**, even with the app closed.

<br clear="all">

<img src="docs/screenshots/citizen/05-hazard-photos.png" width="260" align="left" hspace="12">

**Tap a hazard** to open it: the map zooms to the pin and its **photos** (up to four) appear under it. Tap again to close.

<br clear="all">

<img src="docs/screenshots/citizen/06-hazard-report-form.png" width="260" align="left" hspace="12">

**Report a hazard**: choose the kind (*Flooded road*, *Be careful*, or *Other* and type it), add a note and photos, place the
pin. A citizen report waits for the MDRRMO to approve it before others see it.

<br clear="all">

### Evacuation centers
<img src="docs/screenshots/citizen/07-evacuation-centers.png" width="260" align="left" hspace="12">

The centers the MDRRMO marked on the map, with the distance from your home, the capacity and a **Directions** button that
opens turn-by-turn navigation.

<br clear="all">

### Settings, language and theme
<img src="docs/screenshots/citizen/11-settings.png" width="260" align="left" hspace="12">

Your **ID verification** badge, name, number and e-mail (hidden here), your **home location** (tap to change), and the
**Light / Dark** setting.

<br clear="all">

<img src="docs/screenshots/citizen/12-settings-more.png" width="260" align="left" hspace="12">

Pick the language (**English, Filipino, Hiligaynon, Cebuano, Ilokano**), check the **permissions** (location, notifications,
camera) with a shortcut to the phone settings, replay **How to use RESQ**, reset your password or sign out.

<br clear="all">

<img src="docs/screenshots/citizen/18-dark-home.png" width="200" hspace="6"><img src="docs/screenshots/citizen/19-dark-hazards.png" width="200" hspace="6">

**Dark theme** on the home and hazards screens.

### First-run tutorial
<img src="docs/screenshots/citizen/13-tutorial-1.png" width="150"> <img src="docs/screenshots/citizen/13-tutorial-2.png" width="150"> <img src="docs/screenshots/citizen/13-tutorial-3.png" width="150"> <img src="docs/screenshots/citizen/13-tutorial-4.png" width="150"> <img src="docs/screenshots/citizen/13-tutorial-5.png" width="150">
<img src="docs/screenshots/citizen/13-tutorial-6.png" width="150"> <img src="docs/screenshots/citizen/13-tutorial-7.png" width="150"> <img src="docs/screenshots/citizen/13-tutorial-8.png" width="150">

A short guided tour with real screenshots and arrows: how to report in four steps, how to follow the help, and why the app
asks for **location**, **notifications** and **camera**. It runs once and can be replayed from Settings.

### Updates over the air
<img src="docs/screenshots/citizen/10-update-popup.png" width="260" align="left" hspace="12">

When a new version of the app's code is ready, a pop-up offers **Update now** (a few seconds, nothing is lost) or *Maybe
later*. Updates are signed; the phone only accepts ones signed with the MDRRMO's key.

<br clear="all">

### Also in the citizen app (no screenshot)
- **Sign up / sign in or guest**: reporting works for guests; an account adds history across phones.
- **ID verification** (*My Identity*): upload an ID and a selfie; the desk checks it and the badge turns **Verified**. Not
  shown here because it displays a real ID photo.
- **Free call over data**: the desk or a responding crew can ring the reporter inside the app, no call load needed.
- **Push notifications**: area warnings, hazard alerts and call rings reach a closed app.

---

## 2. Responder app (RESQ Responder)

<img src="docs/screenshots/responder/01-responder-home.png" width="260" align="left" hspace="12">

Crews sign in with an account made by their MDRRMO admin. The home is a map with the crew's unit, a **Hazard** button, the
live hazards as pins and, while the crew is free, the **emergencies near you** (within 10 km, nearest first) with an
**Accept** button. **Start duty** shares the crew's location so the desk and the reporter can see the ETA.

<br clear="all">

<img src="docs/screenshots/responder/02-nearby-report.png" width="260" align="left" hspace="12">

Tapping a report (or the push "Report near you") shows it on the map with the **road route and minutes**. The first
responder to press **I will respond** is dispatched at once; the desk sees it immediately. **Can't respond** tells the desk.

<br clear="all">

<img src="docs/screenshots/responder/05-assignment.png" width="260" align="left" hspace="12">

After dispatch the screen switches to the job: the incident, the description and photos, a warning when a **hazard** is
close to the route, the ETA, and buttons to **Navigate** (Google Maps), **Call the reporter** (free over data or by phone),
**Call the MDRRMO**, ask for **backup** or hand the job back (**Can't continue**), and **Mark resolved**.

<br clear="all">

<img src="docs/screenshots/responder/03-responder-hazards.png" width="260" align="left" hspace="12">

<img src="docs/screenshots/responder/04-responder-hazard-form.png" width="260" align="left" hspace="12">

**Pin a hazard** you see on the road: choose the kind (the *Other* chips open more), add a note and photos, place the pin.
A responder's hazard is **live at once**, with no desk approval, and phones within 5 km are notified. A crew can clear
the pins it posted when the road is open again.

<br clear="all">

Monitors and admins who sign in to this app get the **MDRRMO Monitor** screen (live reports and units).

---

## 3. Dispatch desk (Windows)

### Dispatch
<img src="docs/screenshots/desk/01-dispatch.png" width="900">

The main screen. The top bar sounds and flashes for a **new report** (View / Acknowledge). The four counters show **Pending**,
**En route**, **Closed today** and **Units available**. On the left are the live reports (colour by status and type), on the
right the map with reports, units (with their last GPS), hazards and evacuation centers. It works on an offline map of the
town.

<img src="docs/screenshots/desk/02-dispatch-selected-report.png" width="900">

Select a report to see its detail: reporter (and whether the ID is verified), description, **photos**, the confirmed spot
and its GPS accuracy. Pick one of the **nearest available units** (a ✓ means the crew said it can respond) and press
**Dispatch**; a crew that took the report on its own phone shows as self-dispatched. From here you can also open the
**Reporter ID**, **Call reporter** by phone or **Call via RESQ app** (free, over data), **Call the assigned unit**, mark a
**False report** (and block the sender) or **Resolve** it.

### Units
<img src="docs/screenshots/desk/03-units.png" width="900">

Ambulances, fire trucks and police units of the town: status (**available** / **busy**), last GPS update, what each is
assigned to and the responder login. Add, edit or delete units, and **Call unit** (free call over data).

### History
<img src="docs/screenshots/desk/04-history.png" width="900">

Every closed report: type, description, unit and time, including false reports and ones the reporter cancelled.

### Citizens
<img src="docs/screenshots/desk/05-citizens.png" width="900">

The people who signed up: ID status, number of reports, false reports and whether the sender is **blocked**. The desk can
verify or block a citizen, send a password reset e-mail, or delete the personal data.

### Pending IDs
<img src="docs/screenshots/desk/06-pending-ids.png" width="900">

The queue of ID checks. For each person the desk sees the selfie and the ID photo side by side, compares the name, then
**Approve** or **Reject**.

### Alerts: warnings, evacuation centers and hazards
<img src="docs/screenshots/desk/07-alerts.png" width="900">

Send a **warning** (advisory, warning or danger) to everyone in the town, to a **radius** around a pin, or to **selected
barangays**; the phones in that area get a push and the list shows how many were reached. Drag **evacuation centers** and
**hazards** from the map toolbar onto the map to place them; click one to edit or remove it. The tab shows a number when
citizen hazard reports wait for approval.

<img src="docs/screenshots/desk/10-hazard-dialog-pending.png" width="420"> <img src="docs/screenshots/desk/11-hazard-dialog-photos.png" width="420">

A **citizen hazard report** opens with its photos so the desk can check it, then **Approve and show on phones** or
**Reject report**. A live hazard can be edited or removed; its photos show here too.

### Reports
<img src="docs/screenshots/desk/08-reports.png" width="900">

Pick a period and press **Show** for the numbers a council asks for: reports, resolved, false alarms, average time to
dispatch, to the scene and to resolve, by incident type and by unit. **Export CSV** saves the reports.

### Also on the desk (no screenshot)
- **Login** with an MDRRMO admin account; **superadmin console** (register towns, create admin and responder accounts, load
  barangay borders) on the PC that holds the master key.
- **Mutual aid**: ask a neighbouring town to help with a report.
- **Calls**: answer the free over-data calls from citizens and crews.
