# Achievement
Simple achievements script for SA-MP.

# Usage:

```Pawn
#include <a_samp>
#include "achievement"

new
	Achievement:NadeKingMaster,
	Achievement:NadeKingExpert,
	Achievement:NadeKingNovice,
	Achievement:TheFirstRuleIs;

main() {
	NadeKingMaster = DefineAchievement("Nade King Master", "Kill 50 players with grenades.", 50);
	NadeKingExpert = DefineAchievement("Nade King Expert", "Kill 30 players with grenades.", 30);
	NadeKingNovice = DefineAchievement("Nade King Novice", "Kill 10 players with grenades.", 10, NadeKingExpert, NadeKingMaster);
	TheFirstRuleIs = DefineAchievement("The First Rule Is...", "Kill 20 players with bare hands.", 20);
}

public OnPlayerDeath(playerid, killerid, reason) {
	if (killerid != INVALID_PLAYER_ID) {
		if (reason == WEAPON_GRENADE)
			GivePlayerAchievement(killerid, NadeKingNovice, 1);

		if (!reason)
			GivePlayerAchievement(killerid, TheFirstRuleIs, 1);
	}
	return 1;
}

public OnPlayerUnlockAchievement(playerid, Achievement:achievementid) {
	if (achievementid == NadeKingNovice || achievementid == NadeKingExpert || achievementid == NadeKingMaster)
		GivePlayerMoney(playerid, 4250);

	if (achievementid == TheFirstRuleIs)
		GivePlayerMoney(playerid, 500);

	return 1;
}
```
