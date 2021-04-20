# Gulag API documentation (v3.2.5) - by Jakatebel
  * [Unauthorized Endpoints](#unauthorized-no-api-key-required)
    * [Users](#users)
      * [User count](#user-count)
      * [User information & stats](#user-information-and-stats)
      * [User status](#user-status)
      * [User scores](#user-scores)
      * [User most played maps](#user-most-played-maps)
    * [Beatmaps](#beatmaps)
      * [Beatmap information](#beatmap-information)
      * [Beatmap scores](#beatmap-scores)
      * [Beatmap score info](#beatmap-score-info)
      * [Beatmap replay](#beatmap-replay)
    * [Multiplayer](#multiplayer)
      * [Multiplayer match](#multiplayer-match)
      <br>
  * [Authorized Endpoints](#authorized-requires-valid-api-key-passed-as-authorization-header)
    * [Beatmaps](#beatmaps-1)
      * [Calculate PP](#calculate-pp)
    * [Users](#users-1)
      * [Set Avatar](#set-avatar)
      <br>
  * [TODO](#todo)
  
# Unauthorized Endpoints (no api key required)

## Users

### User count

#### Description:<br>
Get total registered users and online user count.<br>
Returns total registered & online player counts.

#### URL
```
/api/get_player_count
```

#### Parameters
`None` - This endpoint does not require parameters.

#### Response
```json
{
  "online": 1,
  "total": 12
}
```
#### Notes
It does not count the bot as a user.

-----------------------------------------

### User information and stats

#### Description:<br>
Get player account information<br>
Returns info or stats for a given player.

#### URL
```
/api/get_player_info
```

#### Parameters
* Required id or name<br>
`id` = The users id<br>
`name` = The user's name

* Required scope<br>
`scope` = <all/stats/info>
  * `info` - Returns user info
  * `stats` - Returns user stats
  * `all` - Returns everything

#### Examples:
```md
https://.../api/get_player_info?id=3&scope=info
https://.../api/get_player_info?name=User&scope=all
```

#### Response (scope: `info`)
```json
{
  "id": 3,
  "name": "User",
  "safe_name": "user",
  "priv": 31879,
  "country": "it",
  "silence_end": 0
}
```


#### Response (scope: `all`)
```json
{
  "id": 3,
  "name": "User",
  "safe_name": "user",
  "priv": 31879,
  "country": "it",
  "silence_end": 0,
  "tscore_vn_std": 310287722,
  "tscore_vn_taiko": 0,
  "tscore_vn_catch": 10128,
  "tscore_vn_mania": 189246577,
  "tscore_rx_std": 22446060,
  "tscore_rx_taiko": 0,
  "tscore_rx_catch": 0,
  "tscore_ap_std": 0,
  "rscore_vn_std": 198156251,
  "rscore_vn_taiko": 0,
  "rscore_vn_catch": 0,
  "rscore_vn_mania": 99527289,
  "rscore_rx_std": 14065180,
  "rscore_rx_taiko": 0,
  "rscore_rx_catch": 0,
  "rscore_ap_std": 0,
  "pp_vn_std": 1703,
  "pp_vn_taiko": 0,
  "pp_vn_catch": 0,
  "pp_vn_mania": 5688,
  "pp_rx_std": 3893,
  "pp_rx_taiko": 0,
  "pp_rx_catch": 0,
  "pp_ap_std": 0,
  "plays_vn_std": 289,
  "plays_vn_taiko": 0,
  "plays_vn_catch": 1,
  "plays_vn_mania": 600,
  "plays_rx_std": 196,
  "plays_rx_taiko": 0,
  "plays_rx_catch": 0,
  "plays_ap_std": 0,
  "playtime_vn_std": 18315,
  "playtime_vn_taiko": 0,
  "playtime_vn_catch": 21,
  "playtime_vn_mania": 43354,
  "playtime_rx_std": 17775,
  "playtime_rx_taiko": 0,
  "playtime_rx_catch": 0,
  "playtime_ap_std": 0,
  "acc_vn_std": 89.709,
  "acc_vn_taiko": 0,
  "acc_vn_catch": 0,
  "acc_vn_mania": 95.077,
  "acc_rx_std": 96.694,
  "acc_rx_taiko": 0,
  "acc_rx_catch": 0,
  "acc_ap_std": 0,
  "maxcombo_vn_std": 842,
  "maxcombo_vn_taiko": 0,
  "maxcombo_vn_catch": 13,
  "maxcombo_vn_mania": 4810,
  "maxcombo_rx_std": 4938,
  "maxcombo_rx_taiko": 0,
  "maxcombo_rx_catch": 0,
  "maxcombo_ap_std": 0
}
```

-----------------------------------------
  
### User status

#### Description:<br>
Get a player's current status.<br>
Returns a player's current status, if online.

#### URL
```
/api/get_player_status
```

#### Parameters
* Required id or name<br>
`id` = The users id<br>
`name` = The user's name

#### Examples:
```md
https://.../api/get_player_status?id=3
https://.../api/get_player_status?name=User
```

#### Response (offline example)
```json
{ "online": false }
```

#### Response (online idle example)
```json
{
  "online": true,
  "login_time": 1618882598.054161,
  "status": {
    "action": 0,
    "info_text": "",
    "mode": 4,
    "mods": 200,
    "beatmap": null
  }
}
```

#### Response (online example spectating/watching)
```json
{
  "online": true,
  "login_time": 1618882598.054161,
  "status": {
    "action": 6,
    "info_text": "User 2 play BLANKFIELD - Goodbye [Intense]",
    "mode": 4,
    "mods": 200,
    "beatmap": {
      "md5": "4a4bc3bdb6d951512db592994b08cfc7",
      "id": 1172819,
      "set_id": 553906,
      "artist": "BLANKFIELD",
      "title": "Goodbye",
      "version": "Intense",
      "creator": "Kyubey",
      "last_update": "2017-02-25T12:56:50",
      "total_length": 289,
      "max_combo": 2516,
      "status": 2,
      "plays": 7,
      "passes": 3,
      "mode": 0,
      "bpm": 104.5,
      "cs": 4,
      "od": 10,
      "ar": 10,
      "hp": 4.7,
      "diff": 8.356
    }
  }
}
```
#### Notes
`mods` - Will return only client mods! If status is watching it will not return the spectated user's mods.<br>
`mode` - Will return `4` if `mode` is unknown.<br>
`status` - Will be set only when a user is online.

-----------------------------------------
  
### User scores

#### Description:<br>
Get a list of scores for a given user.<br>
Returns a list of best or recent scores for a given player.

#### URL
```
/api/get_player_scores
```

#### Parameters
* Required id or name<br>
`id` = The users id<br>
`name` = The user's name

* Required sort<br>
`sort` = <best/recent>
  * `best` - Returns user's best scores
  * `recent` - Returns user's recent scores
* Required mods<br>
`mods` = <vn/rx/ap>
  * `vn` - Vanilla
  * `rx` - Relax
  * `ap` - Autopilot
* Required mode<br>
`mode` = <std/taiko/catch/mania>

#### Example
```md
https://.../api/get_player_scores?id=3&sort=recent&mods=vn&mode=mania
```

#### Response
```json
{
  "limit": 299,
  "scores": [
    {
      "acc": 100,
      "ar": 5,
      "artist": "Various Artist",
      "bpm": 122,
      "client_flags": 0,
      "creator": "NikoSek",
      "cs": 4,
      "diff": 3.042,
      "frozen": 1,
      "grade": "X",
      "hp": 8,
      "id": 1886,
      "last_update": "Sat, 01 Sep 2018 03:53:21 GMT",
      "map_md5": "944eaa26bc1957e396d97ec88881707d",
      "maps.id": 1755777,
      "maps.max_combo": 0,
      "maps.mode": 3,
      "maps.status": 2,
      "max_combo": 585,
      "md5": "944eaa26bc1957e396d97ec88881707d",
      "mode": 3,
      "mods": 0,
      "n100": 0,
      "n300": 48,
      "n50": 0,
      "ngeki": 289,
      "nkatu": 0,
      "nmiss": 0,
      "od": 8,
      "passes": 4,
      "perfect": 1,
      "play_time": "Mon, 19 Apr 2021 19:16:43 GMT",
      "plays": 5,
      "pp": 82.449,
      "score": 995549,
      "server": "osu!",
      "set_id": 838659,
      "status": 2,
      "time_elapsed": 42058,
      "title": "The 4k wea trash pack",
      "total_length": 37,
      "userid": 3,
      "version": "OH YEAH MR KRABS"
    }, { ... }
  ]
}
```
#### Notes
It does not count the bot as a user.
  
-----------------------------------------
  
### User most played maps

#### Description:<br>
Get a list of the most played maps by a user.<br>
Returns a list of maps most played by a given player.

#### URL
```
/api/get_player_most_played
```

#### Parameters
* Required id or name<br>
`id` = The users id<br>
`name` = The user's name

#### Example
```md
https://.../api/get_player_most_played?id=3
```

#### Response
```json
. . .
```

## Beatmaps

### Beatmap information

#### Description:<br>
Get information about a given beatmap by it's id or md5 hash.<br>
Returns information about a given beatmap.

#### URL
```
/api/get_map_info
```

#### Parameters
* Required beatmap id or beatmap md5<br>
`id` = The beatmap's id<br>
`md5` = The beatmap's md5 hash

#### Example
```md
https://.../api/get_map_info?id=1172819
https://.../api/get_map_info?md5=4a4bc3bdb6d951512db592994b08cfc7
```

#### Response
```json
{
  "md5": "4a4bc3bdb6d951512db592994b08cfc7",
  "id": 1172819,
  "set_id": 553906,
  "artist": "BLANKFIELD",
  "title": "Goodbye",
  "version": "Intense",
  "creator": "Kyubey",
  "last_update": "2017-02-25T12:56:50",
  "total_length": 289,
  "max_combo": 2516,
  "status": 2,
  "plays": 7,
  "passes": 3,
  "mode": 0,
  "bpm": 104.5,
  "cs": 4,
  "od": 10,
  "ar": 10,
  "hp": 4.7,
  "diff": 8.356
}
```

-----------------------------------------

### Beatmap scores

#### Description:<br>
Get scores for a given beatmap, mode and mods<br>
Returns the best scores for a given beatmap & mode.

#### URL
```
/api/get_map_scores
```

#### Parameters
* Required beatmap id or beatmap md5<br>
`id` = The beatmap's id<br>
`md5` = The beatmap's md5 hash

* Required scope<br>
`scope` = <best/recent>
  * `best` - Returns beatmap's best scores
  * `recent` - Returns beatmap's recent scores

* Optional mode<br>
`mode` = `(0-7), explained below`

#### Modes
```md
0 - Standard
1 - Taiko
2 - Catch
3 - Mania

4 - Relax Standard
5 - Relax Taiko
6 - Relax Catch

7 - Autopilot Standard
```

#### Examples:
```md
https://.../api/get_map_scores?id=1172819&scope=recent
https://.../api/get_map_scores?id=1172819&scope=best&mode=4
```

#### Response
```json
[
  {
    "map_md5": "4a4bc3bdb6d951512db592994b08cfc7",
    "score": 625250,
    "pp": 445.184,
    "acc": 99.361,
    "max_combo": 1941,
    "mods": 128,
    "n300": 1887,
    "n100": 17,
    "n50": 1,
    "nmiss": 0,
    "ngeki": 296,
    "nkatu": 15,
    "grade": "S",
    "status": 2,
    "mode": 0,
    "play_time": "2021-04-05T13:40:02",
    "time_elapsed": 323012,
    "userid": 9,
    "perfect": 0
  }, { ... }
]
```

-----------------------------------------

### Beatmap score info

#### Description:<br>
Get beatmap score information by score id.<br>
Returns information about a given score.

#### URL
```
/api/get_score_info
```

#### Parameters
* Required score id<br>
`id` = The score's id

#### Example
```md
https://.../api/get_score_info?id=1731
```

#### Response
```json
{
  "map_md5": "a53a591e8ee0e4cf66a20a070968b194",
  "score": 546250,
  "pp": 159.304,
  "acc": 94.104,
  "max_combo": 139,
  "mods": 0,
  "n300": 135,
  "n100": 10,
  "n50": 0,
  "nmiss": 2,
  "ngeki": 24,
  "nkatu": 4,
  "grade": "A",
  "status": 2,
  "mode": 0,
  "play_time": "2021-04-15T01:59:26",
  "time_elapsed": 38539,
  "perfect": 0
}
```

-----------------------------------------

### Beatmap replay

#### Description:<br>
Get beatmap replay by id.<br>
Returns the file for a given replay (with or without headers).

#### URL
```
/api/get_replay
```

#### Parameters
* Required score/replay id<br>
`id` = The score/replay's id
* Optionally disable headers
`include_headers` = `true/false, default: true` - Include hits and score headers, dev option.

#### Examples:
```md
https://.../api/get_replay?id=1731
https://.../api/get_replay?id=1731&include_headers=false
```

#### Response
```json
Returns the replay file.
Returns the replay file without headers for the hits and score.
```

## Multiplayer

### Multiplayer Match

#### Description:<br>
Get information about a (CURRENTLY ACTIVE) multiplayer match.<br>
Returns information for a given multiplayer match.

#### URL
```
/api/get_match
```

#### Parameters
* Required current match id<br>
`id` = The multi lobby's id

#### Examples:
```md
https://.../api/get_match?id=0
```

#### Response
```json
{
  "name": "User's game",
  "mode": 0,
  "mods": 0,
  "seed": 2600202,
  "host": {
    "id": 3,
    "name": "User"
  },
  "refs": [
    {
      "id": 3,
      "name": "User"
    }
  ],
  "in_progress": false,
  "is_scrimming": false,
  "map": {
    "id": 962880,
    "md5": "a48b273b2d4ee9e297ee333f7d216f8f",
    "name": "TRUE - Hiryuu no Kishi [Knight's Dance]"
  },
  "active_slots": {
    "0": {
      "loaded": false,
      "mods": 0,
      "player": {
        "id": 3,
        "name": "User"
      },
      "skipped": false,
      "status": 4,
      "team": 0
    },
    "1": {
      "loaded": false,
      "mods": 0,
      "player": {
        "id": 5,
        "name": "User 2"
      },
      "skipped": false,
      "status": 16,
      "team": 0
    }
  }
}
```

-----------------------------------------

## Authorized (requires valid api key, passed as 'Authorization' header)
```
NOTE: authenticated handlers may also have privilege requirements!
```

## Beatmaps

#### Calculate PP
```md
GET /api/calculate_pp
  calculate & return pp for a given beatmap.
```

## Users

#### Set Avatar
```md
POST/PUT /api/set_avatar
  Update the api token holder's avatar to a given file.
```

-----------------------------------------

## TODO
<pre>
GET /api/get_friends
  return a list of the player's friends.
  
POST/PUT /api/set_player_info
  update user information (updates whatever received).
</pre>
