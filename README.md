# LoL-Draft: a League of Legends draft dataset for pick/ban recommendation

**LoL-Draft** is a RecBole-format dataset of professional League of Legends drafts (picks and bans in draft
order, sides, winners, patches), updated monthly. It follows the format of
[DOTA-Draft](https://github.com/DeusExMachina1993/Dota-Draft), the Dota 2 dataset introduced in:

> Mohammadnejad, M., Dorrigiv, M., & Yaghmaee, F. (2026). *DOTA-Draft: A Dataset for In-Game Recommendation in
> Multiplayer Online Battle Arenas*. Journal of AI and Data Mining. DOI: 10.22044/jadm.2026.16888.2819

## 📜 Source, licence and attribution

- Match and draft data: [Leaguepedia](https://lol.fandom.com) (Cargo tables `ScoreboardGames`, `PicksAndBansS7`),
  licensed [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/). LoL-Draft is an adaptation of it and is
  released under [CC BY-SA 4.0](LICENSE) (a later version, as CC BY-SA 3.0 allows). `<year>/games.csv` links every
  game to its Leaguepedia page.
- Champion ids and patch data: [Riot Data Dragon](https://developer.riotgames.com/docs/lol#data-dragon).

LoL-Draft isn't endorsed by Riot Games and doesn't reflect the views or opinions of Riot Games or anyone officially
involved in producing or managing Riot Games properties. Riot Games, and all associated properties are trademarks or
registered trademarks of Riot Games, Inc.

<!-- DATASET-STATS:START -->
## 📦 Dataset versions and coverage

Updated monthly from [Leaguepedia](https://lol.fandom.com) (Cargo tables `ScoreboardGames` and `PicksAndBansS7`). Each year has its own folder, in RecBole format:

```
<year>/all_patches/all_patches.inter   all games of that year
<year>/patch_<id>/patch_<id>.inter     one patch (id = major*100 + minor: 1413 = 14.13, 2502 = 25.S1.2)
<year>/games.csv                       match_id -> Leaguepedia game page, teams, sides, tournament, tier
<year>/STATS.md, <year>/stats.json     statistics
```

**Data through:** 2026-08-31 · **Last match:** 2026-08-31 23:25 UTC · **Leaguepedia snapshot:** 2026-10-06 · **Release:** v2026.08

| Year | From | Through | Matches | Interactions | Patches |
|---|---|---|---|---|---|
| [2020](2020/STATS.md) | 2020-01-03 | 2020-12-27 | 9,026 | 180,520 | 924, 1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009, 1010, 1011, 1012, 1013, 1014, 1015, 1016, 1018, 1019, 1020, 1021, 1022, 1023, 1024, 1025 |
| [2021](2021/STATS.md) | 2021-01-02 | 2021-12-26 | 10,782 | 215,640 | 1025, 1101, 1102, 1103, 1104, 1105, 1106, 1107, 1108, 1109, 1110, 1111, 1112, 1113, 1114, 1115, 1116, 1117, 1118, 1119, 1120, 1121, 1122, 1123, 1124 |
| [2022](2022/STATS.md) | 2022-01-10 | 2022-12-27 | 11,475 | 229,500 | 1201, 1202, 1203, 1204, 1205, 1206, 1207, 1208, 1209, 1210, 1211, 1212, 1213, 1214, 1215, 1216, 1217, 1218, 1219, 1220, 1221, 1223 |
| [2023](2023/STATS.md) | 2023-01-06 | 2023-12-31 | 9,797 | 195,940 | 1223, 1301, 1303, 1304, 1305, 1306, 1307, 1308, 1310, 1311, 1312, 1313, 1314, 1315, 1316, 1317, 1318, 1319, 1320, 1321, 1324 |
| [2024](2024/STATS.md) | 2024-01-01 | 2024-12-22 | 11,089 | 221,780 | 1324, 1401, 1402, 1403, 1404, 1405, 1406, 1407, 1408, 1409, 1410, 1411, 1412, 1413, 1414, 1415, 1416, 1417, 1418, 1419, 1420, 1421, 1422, 1423, 1424 |
| [2025](2025/STATS.md) | 2025-01-11 | 2025-12-29 | 11,961 | 239,220 | 2501, 2502, 2503, 2504, 2505, 2506, 2507, 2508, 2509, 2510, 2511, 2512, 2513, 2514, 2515, 2516, 2517, 2518, 2519, 2520, 2521, 2522, 2523, 2524 |
| [2026](2026/STATS.md) | 2026-01-01 | 2026-08-31 | 8,848 | 176,960 | 2524, 2601, 2602, 2603, 2604, 2605, 2606, 2607, 2608, 2609, 2610, 2611, 2612, 2613, 2614, 2615, 2616, 2617 |

Total (schema v1.0 folders): 72,978 matches, 1,459,560 interactions.

**Schema** (same columns as [DOTA-Draft](https://github.com/DeusExMachina1993/Dota-Draft) v2.1, plus three): `user_id` = `<match_id>_<team>` (team 0 = blue, 1 = red), `item_id` = Riot champion id, `label` 1 = pick / 0 = ban, `team_result`, `timestamp` = draft slot, `hero_action` = `champion_<id>_<pick|ban>`, `start_time`, `draft_format`, `first_team` (1 = drafts first), `series_id` and `game_number` (series context, needed for Fearless Draft), `tournament`, `tier` (`primary` = top leagues and international events, `secondary`, `unknown`; from Leaguepedia's tournament level) and `season_phase` (`<year>_1_pre-MSI`, `<year>_2_MSI-to-Worlds`, `<year>_3_Worlds`: groups the ~24 two-week patches of a year into three phases shared by every league). Only games with a complete 20-action draft are kept; showmatch games are dropped. Lower-tier leagues often lack drafts on Leaguepedia, so `tier = primary` is the best-covered subset (see each year's STATS.md).

**Draft formats** (b = ban, P = pick, 1 = team acting first, 2 = the other team):

| Format | Actions | Patches | Order |
|---|---|---|---|
| `td20_10.1` | 20 | 9.24b–26.17 | `b1 b2 b1 b2 b1 b2 P1 P2 P2 P1 P1 P2 b2 b1 b2 b1 P2 P1 P1 P2` |

Machine-readable definitions: [draft_formats.json](draft_formats.json). Patch notes: [patch_notes/](patch_notes) (champion base-stat changes from Riot Data Dragon + link to the official notes).

See [CHANGELOG.md](CHANGELOG.md) for release notes and [STATS.md](STATS.md) for statistics.
<!-- DATASET-STATS:END -->
