# Helix Bridge - ALM to Perforce Job Creator

## Overview
A web app that connects Helix ALM (TestTrack) to Perforce (P4). It fetches issues from the ALM REST API and creates Perforce jobs populated with the ALM issue number and URL.

## Architecture
- **Frontend**: React + TypeScript + Vite + shadcn/ui + TanStack Query
- **Backend**: Express.js API routes
- **No database** - stateless; all data comes from Helix ALM and Perforce

## Configuration (env vars)
| Variable | Value |
|---|---|
| ALM_API_URL | https://jquesta0725/api/v1 |
| ALM_PROJECT | Holtec Integration |
| ALM_USERNAME | Administrator |
| ALM_PASSWORD | (secret) |
| P4_PORT | ssl:jquesta0725:1666 |
| P4_USER | jeniq |
| P4_PASSWORD | (secret) |
| P4_BINARY | /home/runner/p4 |
| P4_JOB_FIELD_ALM_ID | ALM_ID |
| P4_JOB_FIELD_ALM_URL | ALM_URL |

## Key Features
- Fetch and list ALM issues from "Holtec Integration" project
- Search/filter issues by number, title, or status
- Select an issue to auto-populate job fields
- Create a Perforce job with:
  - Description field from issue summary
  - ALM_ID field = issue number
  - ALM_URL field = issue URL

## P4 Setup
- p4 binary downloaded to `/home/runner/p4`
- Connects via SSL to jquesta0725:1666
- Trusts SSL fingerprint automatically
- Uses `echo password | p4 login` pattern for auth

## API Endpoints
- `GET /api/alm/issues` - Fetch all issues from Helix ALM
- `POST /api/p4/job` - Create a P4 job from an ALM issue
- `GET /api/p4/jobs` - List recent P4 jobs
