# Movement Builders Portal

This is a [living document](https://en.wikipedia.org/wiki/Living_document), subject to any necessary changes throughout the life of the project.

## What's this about?

A tool to streamline the process of contacting recruits and taking in data during conversations based on predetermined scripts.

## Terminology

**Hub**: The Google Sheet currently being used to track potential recruits' information as well as volunteer assignment. (probably used for other things I don't know about yet as well)

**Server**: A web service that will have access to the hub and other essential tooling in order to provide helpful services to staff and volunteers.

**Admin**: A privileged user on the server. Ideally, this will consist of staff, and potentially highly trusted volunteers as staff sees fit.

**Recruit**: A person who is interested in potentially volunteering with either JD or a candidate's campaign.

**Volunteer**: A person who has signed up to volunteer and is scheduled to take one or more recruit calls.

**Shift**: A block of time when volunteers will be handling calls to/from recruits.

**Script**: A predefined conversation flow that a volunteer should follow when speaking with recruits.

## First Iteration System

### Initial Setup

- The server will be granted access to the hub via the [Google Oauth 2.0](https://developers.google.com/identity/protocols/oauth2) token exchange protocol.

### Pre-shift Setup

The following will need to be done prior to each scheduled shift.

- Volunteers need to be pre-assigned recruits. Initially this will have to be done manually via the hub by assigning the volunteer's email address to recruit records.
  - If you need to rearrange assignments, you can do so in the hub, but you and the on-shift volunteers will need to reload data.
- The script must be completed and validated by an admin ahead of a given shift. In this first round, updating the script during an active shift will not be supported.
- Recruit data from the hub will need to be pulled. This will consist of an admin clicking a button to load the data from the hub to the server. The admin may be required to reauthenticate to Google if the refresh token has expired.
  - Data will be persisted using [Redis hosted with Upstash](https://upstash.com/)
  - The data can be loaded again at any time, but beware that a version history will not be kept, at least in this initial phase - whenever you load data, if existing data matches by email address, the new data will overwrite.
  - Email addresses must be unique between recruit records for matching to work properly. Errors may be experienced if two or more recruits in the hub have the same email address.

### Shift Flow

- A volunteer will authenticate, and then they will see their assigned recruits.
  - At any point during a shift, a volunteer can refresh their list of assigned recruits by reloading the browser tab.
- When the volunteer clicks on a recruit's name, this will trigger the script flow. They will follow the prompts, clicking the appropriate buttons or inputting data as the script defines.
- At the end of the script, the volunteer will click a save button to persist the data.

### Post-shift

- Data collected during a shift can be downloaded in CSV or JSON format when a shift is complete. Technically you could download during a shift, but you may get incomplete data.

## Future State

These are some features I think could be useful at some point in the future, but this will be an ongoing conversation to establish priorities and goals for the project.

- Live data refresh so admins don't have to click a button to reload every time something changes.
- The script editor will need continuous improvements in the early stages at least. It will not be perfect in round one.
- Replace the hub with something more user friendly for admins.
- Scheduling tool integration so volunteers can be automatically assigned recruits.

## Technical Contributor Skills

The best engineers I have worked with are generalists who enjoy a good challenge through problem solving and tenacity. The most important qualities a contributor could have:

- Curiosity
- Perseverance
- Commitment
  - They should be able to prioritize and keep their word when they say they can get something done.

These are some ideal technical skills, but none of these are necessarily required. With some intelligence and prior technical experience, all of this can be learned in the course of working on the project.

- [Go](https://go.dev/)
- Databases, specifically [Redis](https://redis.io/)
- HTML
- CSS

## Ideal Project Staffing

- 2+ devs/engineers
- 1+ UI/UX designers
- 1+ project manager/coordinator
