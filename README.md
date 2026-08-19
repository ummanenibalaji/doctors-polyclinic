# Doctor's & Doctor's Polyclinic & Diagnostic Centre

Patient-facing website and front-desk console for a two-branch neighbourhood
polyclinic in north-west Hyderabad (Bachupally and Madeenaguda / Hafeezpet).

**Live:** https://ummanenibalaji.github.io/doctors-polyclinic/

## What's here

`index.html` — the entire site, self-contained. No build step, no bundler, no
dependencies. The only network request is Google Fonts, and the type falls back
cleanly without it. Open it directly or serve it from anything.

## What it does

- **Booking** in four steps, each its own route so back and refresh work:
  branch and speciality → consultant and day → time → patient details and OTP.
  Taken slots stay visible but disabled, the held slot expires after five
  minutes with a visible countdown, and confirmation issues a token number.
- **Specialities** (14) and **consultants** (18), filterable by speciality and branch.
- **Diagnostics** — searchable test catalogue with prices and turnaround times.
- **Day care** — what is walk-in and what needs a booking.
- **Branches**, **patient portal** (OTP sign-in, no password, no account).
- **Staff console** at `#/staff` — today's queue, one-click status, walk-in entry
  in three fields, full keyboard operation, and an owner insights view.

## Design

Warm ivory ground, deep emerald, brass. Fraunces for display, Plus Jakarta Sans
for body, IBM Plex Mono for the token and appointment number. Contrast is
measured rather than eyeballed: ink on ivory 14.8:1, emerald on ivory 8.5:1, and
the worst text-over-canvas case 5.98:1.

A single persistent canvas sits behind the whole site and re-poses itself per
route — an orbital cloud on home, an ordered grid on specialities, two clusters
on doctors, a vertical column on diagnostics, a ribbon that advances with the
booking steps, and on confirmation it releases and settles as the token lands.
Real 3D positions with perspective projection and depth sorting, drawn to 2D
canvas. It degrades to a static composition under `prefers-reduced-motion`, on
low-core devices, and with save-data on; motion can also be switched off from
the footer. The staff console never mounts it.

Responsive from 360px. On phones the branch chip and emergency call sit in a
fixed thumb bar.

## Status

Front end only. There is no server attached: the consultant roster, prices,
slot availability and phone numbers are **sample data**, and anything typed into
a form stays in the browser and is never transmitted. Wiring it to the real
Express and PostgreSQL API means replacing the data layer with calls to
`available_slots`, `branch_day_queue`, `book_appointment` and
`cancel_appointment`.
