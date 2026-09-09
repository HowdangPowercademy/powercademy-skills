# Preflight — the skill's own onboarding

The user should never have to know a command name or guess what's missing. The
moment they express intent — *"set up ALM"*, *"deploy this to production"* —
run this yourself, in plain language, doing the work for them.

## Posture

- **Do the work, don't prescribe it.** They name environments in plain English;
  you run the commands.
- **Narrate briefly**, and surface any gap with the fix offered.
- **Offer before installing on a customer's machine.**
- **Only the irreducibly-manual stays with the user:** completing a browser
  sign-in, and approvals/licences someone else controls.

**Preferred mechanism:** where the pac CLI's built-in MCP server is available
(see `${PLUGIN_ROOT}/shared/microsoft-refs.md`), use its tools for environment
and solution operations rather than shelling out. Otherwise run the `pac`
commands directly.

## The onboarding sequence

**1. Is the tooling here — and working?**
Check `pac` **functions** (`pac help`), not merely that it resolves — managed
deployments can leave a shim on PATH with no CLI behind it, fixed self-service
with `pac install latest` (**no admin needed**).

**2. Who are you connected as? Lead with the connection card.**
Run `pac auth who` (and `pac auth list` if several profiles exist) and present
user, tenant, environment, profile, plus *"is this the right place?"*. Multiple
cached profiles are normal on consultant machines — list them and let the user
pick (`pac auth select`); offer `pac auth name` to label them per customer.

If not connected, work the **auth ladder** in
`${PLUGIN_ROOT}/shared/microsoft-refs.md`: device code first, interactive
fallback when Conditional Access blocks it, then a policy-exemption request
with the correlation ID. **Never claim "a browser has opened"** — you cannot
see their screen. After any auth change, verify with evidence: re-list and
compare against the *target* tenant.

**3. Map the estate before designing or deploying.**
List environments (`pac env list`) and solutions (`pac solution list`), and
establish **which environments are production**. For ALM work this is not
optional context — it is the subject. Note anything alarming as a finding:
work happening in the Default environment, unmanaged solutions in production,
no dev environment at all.

**4. Which way is this going?**
For a promotion, state source and target explicitly and get confirmation
*before* anything moves. **Say the word "production" out loud** when a
production environment is involved, at the start, not once you're mid-import.

**5. Can you reach Microsoft Learn?**
Confirm a verification route for anything you'd otherwise recall from memory
(see `${PLUGIN_ROOT}/shared/microsoft-refs.md`). Memory is not a route.

## What is never the skill's job

Licences, security roles, DLP policies, admin consent, and **deployment
approvals** live with the user's organisation. When one blocks the work, name
it precisely, say who can resolve it, record it in the process document's
**Open questions**, and don't attempt a workaround. An approval is never
inferred — it is given, explicitly, in the moment.

## Feeding back

A gap this sequence didn't cover is a finding: add it here, and keep the
repo-level `PREREQUISITES.md` in step.
