# ha-octopus-energy-blueprints

Home Assistant blueprints for the [Octopus Energy integration](https://github.com/BottlecapDave/HomeAssistant-OctopusEnergy) by BottlecapDave.

---

## Auto-enrol in Octoplus Saving Sessions

[![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/SiriusSailing/ha-octopus-energy-blueprints/main/blueprints/octopus_energy_auto_enrol_saving_sessions.yaml)

Automatically joins any available **Octoplus Saving Session** events the moment they are announced, and sends push notifications when a session is detected and when enrolment is confirmed.

**How it works**

Triggers whenever the Saving Session events entity changes (i.e. when Octopus publishes a new session) and on Home Assistant startup (to catch any sessions missed while HA was offline). If there are unjoined sessions available, it enrolls in all of them automatically.

Only **standard saving sessions** (where Octopus awards octopoints per kWh reduced) are enrolled. **Free electricity sessions** — where Octopus gives free electricity instead of requesting usage reduction — appear in the same entity but are applied automatically by Octopus and require no enrolment; the blueprint skips them.

Each join is attempted independently — if one fails (e.g. Octopus announces a session before its join window opens), the others still proceed and the automation retries on the next entity update.

**Requirements**
- Octopus Energy integration, installed and configured
- Home Assistant Mobile App integration for push notifications
- An active Octoplus membership

**Inputs**
| Input | Description |
|---|---|
| Saving Session Events Entity | The `event.octoplus_..._saving_session_events` entity for your account |
| Notification Target | Your notify service, e.g. `notify.mobile_app_my_phone` |

---

## Auto-spin Wheel of Fortune

[![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/SiriusSailing/ha-octopus-energy-blueprints/main/blueprints/octopus_energy_wheel_of_fortune.yaml)

Automatically spins the **Wheel of Fortune** whenever spins are available, for electricity or gas.

**How it works**

Triggers when the spins sensor rises above 0 (new spins awarded) and on Home Assistant startup. Spins once per available spin. Optionally records each spin result in an `input_text` helper as a JSON list, keeping the last 10 entries — useful for displaying spin history on a dashboard.

**Tip:** Create two separate automations from this blueprint — one for the electricity sensor and one for the gas sensor.

**Requirements**
- Octopus Energy integration, installed and configured
- An active Octopus Energy account with Wheel of Fortune enabled

**Inputs**
| Input | Description |
|---|---|
| Wheel of Fortune Spins Sensor | The `sensor.octopus_energy_..._wheel_of_fortune_spins_*` entity |
| Win History Helper (optional) | An `input_text` entity to store the last 10 spin results |

---

Community thread: [Octopus Energy blueprints](https://community.home-assistant.io/t/octopus-energy-auto-enrol-in-octoplus-saving-sessions/1018037)
