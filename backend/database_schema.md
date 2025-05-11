# Database Schema Description

## Tables

### 1. **SETTINGS**
Stores information about global settings.
| Column Name     | Type    | Description                                     |
|-----------------|---------|-------------------------------------------------|
| `KEY`            | TEXT | Unique identifier for the setting name. Primary Key. |
| `VALUE`          | TEXT    | Value of the setting.     |

### 2. **CHRISTIANS**
Stores information about Christian (student) players in the game.

| Column Name     | Type    | Description                                     |
|-----------------|---------|-------------------------------------------------|
| `ID`            | INTEGER | Unique identifier for the Christian player. Primary Key. |
| `NAME`          | TEXT    | Name of the Christian player.     |
| `IMAGE`         | TEXT    | Path to the image of the Christian. |
| `IN_JAIL`       | INTEGER | Indicates whether the Christian is in jail. 1 for in jail, 0 for not. |

### 3. **COPS**
Stores information about the Cop (leader) players in the game.

| Column Name     | Type    | Description                                     |
|-----------------|---------|-------------------------------------------------|
| `ID`            | INTEGER | Unique identifier for the Cop player. Primary Key. |
| `NAME`          | TEXT    | Name of the Cop player.          |
| `IMAGE`         | TEXT    | Path to the image of the Cop.  |

### 4. **GAMES**
Stores information about the games being played.

| Column Name     | Type    | Description                                      |
|-----------------|---------|--------------------------------------------------|
| `ID`            | INTEGER | Unique identifier for each game. Primary Key.    |
| `JAIL_START`    | INTEGER | Starting jail time in seconds for captured Christians. |
| `JAIL_INCREMENT`| INTEGER | Increment in jail time in seconds for each capture. Default value is 0.         |
| `JAIL_MAX`      | INTEGER | Maximum allowed jail time in seconds.                       |
| `START_TIME`    | TEXT    | The start time of the game in ISO format.        |
| `END_TIME`      | TEXT    | The end time of the game in ISO format.          |
| `RESULT_CALCULATED`      | INTEGER    | Indicates whether the points have been calculated and entered. 1 for calculated, 0 for not. Default value is 0.          |


### 5. **CAPTURES**
Tracks when a Christian is caught by a Cop and their jail time.

| Column Name        | Type    | Description                                     |
|--------------------|---------|-------------------------------------------------|
| `ID`               | INTEGER | Unique identifier for the capture event. Primary Key. |
| `GAME_ID`          | INTEGER | The game in which the capture occurred. Foreign Key to `GAMES` table. |
| `CHRISTIAN_ID`     | INTEGER | The Christian player who was caught. Foreign Key to `CHRISTIANS` table. |
| `COP_ID`           | INTEGER | The Cop who made the capture. Foreign Key to `COPS` table. |
| `CAPTURE_TIME`     | TEXT    | The timestamp when the capture occurred.        |
| `RELEASE_TIME`     | TEXT    | The timestamp when the Christian is released from jail. |

### 6. **TEAMS**
Stores information about the teams.

| Column Name     | Type    | Description                                     |
|-----------------|---------|-------------------------------------------------|
| `ID`            | INTEGER | Unique identifier for the team. Primary Key.    |
| `NAME`          | TEXT    | Name of the team.                 |

### 7. **GAME_TEAMS**
Links teams to specific games and tracks their performance.

| Column Name     | Type    | Description                                      |
|-----------------|---------|--------------------------------------------------|
| `ID`            | INTEGER | Unique identifier for the game team. Primary Key.|
| `GAME_ID`       | INTEGER | Foreign Key to the `GAMES` table.               |
| `TEAM_ID`       | INTEGER | Foreign Key to the `TEAMS` table.               |
| `POINTS`       | INTEGER | Number of points for the game team. Default value is 0.             |
| `WON`       | INTEGER | Indicates whether the game team won. 1 for won, 0 for not. Default value is 0.              |

### 8. **PLAYER_TEAMS**
Links players to teams (during specific games).

| Column Name     | Type    | Description                                      |
|-----------------|---------|--------------------------------------------------|
| `GAME_TEAM_ID`  | INTEGER | Foreign Key to the `GAME_TEAMS` table. Part of the composite key.           |
| `PLAYER_ID`     | INTEGER | Foreign Key to the `CHRISTIANS` table. Part of the composite key. |
