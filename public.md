# Index
- [Authentication](#authentication)
- [API Route](#api-route)
- [Special Codes](#special-codes)
    - [Match status codes](#match-status-codes)
    - [Demo status codes](#demo-status-codes)
    - [Team side codes](#team-side-codes)
- [Version](#version)
- [Players](#players)
- [Profile](#profile)
- [Community](#community)
- [Matches](#matches)
- [Scoreboard](#scoreboard)
- [Server](#server)
- [Servers](#servers)

## Authentication
SQLMatches uses BasicAuth for authentication with the API key being the password.

## API Route
``https://sqlmatches.com/api``

SQLMatches routing requires it to always end in a back slash ('/').

## Special Codes
### Match status codes
- ``0`` = Finished
- ``1`` = Live

### Demo status codes
- ``0`` = No demo
- ``1`` = Processing
- ``2`` = Ready for download
- ``3`` = Too large
- ``4`` = Expired

### Team side codes
- ``0`` = CT
- ``1`` = T

---

## Version
- ``GET - /version/{major:int}/{minor:int}/{patch:int}/``
    - E.g. ``/version/1/0/0/``
### Status 200
```json
{
    "data": "Amazing version message",
    "error": false
}
```
### Status 500
```json
{
    "data": null,
    "error": "Invalid version"
}
```

---

## Players
- ``GET - /players/``
    - Payload
        - search, string, not required
        - page, int, not required
        - desc, bool, not required
### Status 200
```json
{
  "data": [
    {
      "name": "Doggy",
      "steam_id": "76561198050395665",
      "kills": 36,
      "headshots": 16,
      "assists": 6,
      "deaths": 20
    },
    {
      "name": "Ward",
      "steam_id": "76561198077228213",
      "kills": 36,
      "headshots": 16,
      "assists": 6,
      "deaths": 20
    }
  ],
  "error": false
}
```
---

## Profile
- ``GET - /profile/{steam_id}/``
    - E.g. ``/profile/76561198077228213/``
### Status 200
```json
{
    "data": {
        "name": "Ward",
        "steam_id": "76561198077228213",
        "kills": 36,
        "headshots": 16,
        "assists": 6,
        "deaths": 20,
        "kdr": 1.8,
        "hs_percentage": 44.44,
        "hit_percentage": 76.5,
        "shots_fired": 400,
        "shots_hit": 306,
        "mvps": 10,
        "timestamp": "01/21/2021-12:26:21"
    },
    "error": false
}
```
### Status 500
```json
{
    "data": null,
    "error": "Invalid Steam ID"
}
```

---

## Community
- ``GET - /community/public/``
### Status 200
```json
{
    "data": {
        "community_name": "TestLeague",
        "owner_id": "76561198077228213",
        "disabled": false,
        "timestamp": "01/21/2021-12:26:21",
        "banned": false,
        "allow_api_access": true
    },
    "error": false
}
```
- ``GET - /community/exists/``
### Status 200
```json
{
    "data": {
        "taken": true
    },
    "error": false
}
```

---

## Matches
- ``POST - /matches/``
    - Payload
        - search, string, not required
        - page, int, not required
        - desc, bool, not required
        - require_scoreboard, bool, not required by default True
            - If no scoreboard exists for the match, it won't be returned.
### Status 200
```json
{
    "data": [
        {
            "match_id": "c10310d5-1b17-4a71-a351-024cc55551fd",
            "timestamp": "01/21/2021-12:26:21",
            "status": 0,
            "demo_status": 0,
            "map": "de_mirage",
            "team_1_name": "Ward",
            "team_2_name": "Doggy",
            "team_1_score": 16,
            "team_2_score": 8,
            "team_1_side": 0,
            "team_2_side": 1,
            "cover_image": "https://sqlmatches.com/api/maps/mirage.jpg",
            "community_name": "TestLeague"
        }
    ],
    "error": false
}
```

---

## Scoreboard
- ``GET - /match/{match_id}/``
    - E.g. ``/match/c10310d5-1b17-4a71-a351-024cc55551fd/``
### Status 200
```json
{
    "data": {
        "match_id": "c10310d5-1b17-4a71-a351-024cc55551fd",
        "timestamp": "01/21/2021-12:26:21",
        "status": 0,
        "demo_status": 0,
        "map": "de_mirage",
        "team_1_name": "Ward",
        "team_2_name": "Doggy",
        "team_1_score": 16,
        "team_2_score": 8,
        "team_1_side": 0,
        "team_2_side": 1,
        "cover_image": "https://sqlmatches.com/api/maps/mirage.jpg",
        "community_name": "TestLeague",
        "team_1": [
            {
                "steam_id": "76561198077228213",
                "name": "Weeb",
                "team": 0,
                "alive": true,
                "ping": 69,
                "kills": 36,
                "headshots": 16,
                "assists": 6,
                "deaths": 20,
                "shots_fired": 400,
                "shots_hit": 306,
                "mvps": 10,
                "score": 130,
                "disconnected": false
            }
        ],
        "team_2": [
            {
                "steam_id": "76561198050395665",
                "name": "Furry",
                "team": 1,
                "alive": true,
                "ping": 69,
                "kills": 36,
                "headshots": 16,
                "assists": 6,
                "deaths": 20,
                "shots_fired": 400,
                "shots_hit": 306,
                "mvps": 10,
                "score": 130,
                "disconnected": false
            }
        ]
    },
    "error": false
}
```

---

## Server
- ``GET - /server/{ip:str}/{port:int}/``
    - E.g. ``/server/54.37.244.193/27919/``
### Status 200
```json
{
    "data": {
        "community_name": "TestLeague",
        "name": "Ward Dev",
        "players": 0,
        "max_players": 12,
        "ip": "54.37.244.193",
        "port": 27919,
        "map": "de_mirage",
        "cover_image": "https://sqlmatches.com/api/maps/mirage.jpg"
    },
    "error": false
}
```

---

## Servers
- ``GET - /servers/``
### Status 200
```json
{
    "data": [
        {
            "community_name": "TestLeague",
            "name": "Ward Dev",
            "players": 0,
            "max_players": 12,
            "ip": "54.37.244.193",
            "port": 27919,
            "map": "de_mirage",
            "cover_image": "https://sqlmatches.com/api/maps/mirage.jpg"
        }
    ],
    "error": false
}
```