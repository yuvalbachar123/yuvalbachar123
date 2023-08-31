#------------------------SETTINGS------------------------

variables:

#! --- GUI BACKGROUND FRAME
	{frame} = gray stained glass pane

options:

#! --- SKRIPT PREFIX
  p: &7[&b&lCrates&7]

#! --- CRATE DENY MESSAGE
  denymsg: &cYou are not holding any keys for this crate!

#! --- FULL INVENTORY MESSAGE
  fullinvmsg: &cYour inventory is full!

#! --- REGION NAME
  region: crates

#! --- Crate Key Lore
  keylore: &7[&e!&7] Rightclick a crate to use.

#! --- Crate Key Names
  iron: &f&lIron &7Crate Key
  gold: &6&lGold &7Crate Key
  diamond: &b&lDiamond &7Crate Keyzo

#------------------------SETTINGS------------------------

#------------------------WARPS------------------------

command /setcrates:
    permission: op
    trigger:
        set {crates.loc} to location of block at location of player
        set {crates.loc}'s yaw to player's yaw
        set {crates.loc}'s pitch to player's pitch
        send "{@p}: &fCrate location has been set to &6%{crates.loc}%" to player

command /crates:
  trigger:
    send "{@p}: &fTeleporting to Crates..." to player
    teleport player to {crates.loc}

#------------------------WARPS------------------------

#------------------------VIEW CRATES------------------------

on leftclick:
	if event-block is iron block:
		cancel event
		viewCrate(player, "iron")
	if event-block is gold block:
		cancel event
		viewCrate(player, "gold")
	if event-block is diamond block:
		cancel event
		viewCrate(player, "diamond")


function viewCrate(p: player, crate: text):

	if {_crate} is "iron":
		open virtual chest inventory with size 3 named "&f&lIron&7 Crate" to {_p}
		format gui slot 0 and 1 and 2 and 3 and 4 and 5 and 6 and 7 and 8 and 9 and 17 and 18 and 19 and 20 and 21 and 23 and 24 and 25 and 26 of {_p} with {frame} named "&6"
		format gui slot 10 of {_p} with paper named "&a&l$500" with lore "" and "&7Chance:" and "&7[&a33%%&7]"
		format gui slot 11 of {_p} with paper named "&a&l$1000" with lore "" and "&7Chance:" and "&7[&a25%%&7]"
		format gui slot 12 of {_p} with iron ingot named "&r&l1 Iron Ingot" with lore "" and "&7Chance:" and "&7[&e20%%&7]"
		format gui slot 13 of {_p} with paper named "&a&l$3000" with lore "" and "&7Chance:" and "&7[&e15%%&7]"
		format gui slot 14 of {_p} with tripwire hook named "&72x {@iron}" with lore "" and "&7Chance:" and "&7[&c5%%&7]"
		format gui slot 15 of {_p} with tripwire hook named "{@gold}" with lore "" and "&7Chance:" and "&7[&c1.99%%&7]"
		format gui slot 16 of {_p} with nametag named "&f&lIron &7Rank" with lore "" and "&7Chance:" and "&7[&c0.01%%&7]"
		format gui slot 22 of {_p} with barrier named "&4Close" to run:
			close {_p}'s inventory
	if {_crate} is "gold":
		open virtual chest inventory with size 3 named "&6&lGold&7 Crate" to {_p}
		format gui slot 0 and 1 and 2 and 3 and 4 and 5 and 6 and 7 and 8 and 9 and 17 and 18 and 19 and 20 and 21 and 23 and 24 and 25 and 26 of {_p} with {frame} named "&6"
		format gui slot 10 of {_p} with paper named "&a&l$3500" with lore "" and "&7Chance:" and "&7[&a33%%&7]"
		format gui slot 11 of {_p} with paper named "&a&l$4000" with lore "" and "&7Chance:" and "&7[&a25%%&7]"
		format gui slot 12 of {_p} with paper named "&a&l$6500" with lore "" and "&7Chance:" and "&7[&e20%%&7]"
		format gui slot 13 of {_p} with gold ingot named "&6&l1 Gold Ingot" with lore "" and "&7Chance:" and "&7[&e15%%&7]"
		format gui slot 14 of {_p} with tripwire hook named "&72x {@gold}" with lore "" and "&7Chance:" and "&7[&c5%%&7]"
		format gui slot 15 of {_p} with tripwire hook named "{@diamond}" with lore "" and "&7Chance:" and "&7[&c1.99%%&7]"
		format gui slot 16 of {_p} with nametag named "&6&lGold &7Rank" with lore "" and "&7Chance:" and "&7[&c0.01%%&7]"
		format gui slot 22 of {_p} with barrier named "&4Close" to run:
			close {_p}'s inventory
	if {_crate} is "diamond":
		open virtual chest inventory with size 3 named "&b&lDiamond&7 Crate" to {_p}
		format gui slot 0 and 1 and 2 and 3 and 4 and 5 and 6 and 7 and 8 and 9 and 17 and 18 and 19 and 20 and 21 and 23 and 24 and 25 and 26 of {_p} with {frame} named "&6"
		format gui slot 10 of {_p} with paper named "&a&l$6000" with lore "" and "&7Chance:" and "&7[&a33%%&7]"
		format gui slot 11 of {_p} with paper named "&a&l$7000" with lore "" and "&7Chance:" and "&7[&a25%%&7]"
		format gui slot 12 of {_p} with diamond named "&b&l1 Diamond" with lore "" and "&7Chance:" and "&7[&e20%%&7]"
		format gui slot 13 of {_p} with paper named "&a&l$9000" with lore "" and "&7Chance:" and "&7[&e15%%&7]"
		format gui slot 14 of {_p} with tripwire hook named "&72x {@diamond}" with lore "" and "&7Chance:" and "&7[&c5%%&7]"
		format gui slot 15 of {_p} with diamond block named "&b&l1 Diamond Block" with lore "" and "&7Chance:" and "&7[&c1.99%%&7]"
		format gui slot 16 of {_p} with nametag named "&b&lDiamond &7Rank" with lore "" and "&7Chance:" and "&7[&c0.01%%&7]"
		format gui slot 22 of {_p} with barrier named "&4Close" to run:
			close {_p}'s inventory

#------------------------VIEW CRATES------------------------

#------------------------OPEN CRATES------------------------

on rightclick:
  if "%region at clicked block%" contains "{@region}":
    if clicked block is iron block:
      if player is holding tripwire hook named "{@iron}" with lore "" and "{@keylore}":
        if inventory of player doesn't have enough space for 1 of blue shulker box:
          send "{@p}: {@fullinvmsg}" to player
          play sound "ENTITY_VILLAGER_NO" at volume 100 and pitch 1 for player
        else:
          cancel event
          remove 1 of tripwire hook named "{@iron}" with lore "" and "{@keylore}" from player's inventory
          openCrate(player, "iron")
      else:
        send "{@p}: {@denymsg}" to player
        play sound "ENTITY_VILLAGER_NO" at volume 100 and pitch 1 for player
    if clicked block is gold block:
      if player is holding tripwire hook named "{@gold}" with lore "" and "{@keylore}":
        if inventory of player doesn't have enough space for 1 of blue shulker box:
          send "{@p}: {@fullinvmsg}" to player
          play sound "ENTITY_VILLAGER_NO" at volume 100 and pitch 1 for player
        else:
          cancel event
          remove 1 of tripwire hook named "{@gold}" with lore "" and "{@keylore}" from player's inventory
          openCrate(player, "gold")
      else:
        send "{@p}: {@denymsg}" to player
        play sound "ENTITY_VILLAGER_NO" at volume 100 and pitch 1 for player
    if clicked block is diamond block:
      if player is holding tripwire hook named "{@diamond}" with lore "" and "{@keylore}":
        if inventory of player doesn't have enough space for 1 of blue shulker box:
          send "{@p}: {@fullinvmsg}" to player
          play sound "ENTITY_VILLAGER_NO" at volume 100 and pitch 1 for player
        else:
          cancel event
          remove 1 of tripwire hook named "{@diamond}" with lore "" and "{@keylore}" from player's inventory
          openCrate(player, "diamond")
      else:
        send "{@p}: {@denymsg}" to player
        play sound "ENTITY_VILLAGER_NO" at volume 100 and pitch 1 for player

function openCrate(p: player, crate: text):

	if {_crate} is "iron":
		wait 5 ticks
		set {_random} to a random integer from 0 to 10000
		if {_random} is 0:
			send "" to {_p}
			send "{@p}: &aYou won the &f&lIron &7Rank&a!" to {_p}
			send "" to {_p}
			play sound "UI_TOAST_CHALLENGE_COMPLETE" at volume 50 and pitch 1 for {_p}
			broadcast "{@p}: &a%{_p}% got &f&lIron &7Rank&a in a crate!"
			if {_p} has permission "group.iron":
				send "" to {_p}
				send "{@p}: &cYou already have this rank!" to {_p}
				send "{@p}: &7You have been awarded &a$10000&7 instead!" to {_p}
				send "" to {_p}
				add 10000 to {balance.tot::%{_p}%}
			else:
				make console execute command "/lp user %{_p}% permission set group.iron true"
		if {_random} is between 1 and 200:
			send "" to {_p}
			send "{@p}: &aYou won a {@gold}&a!" to {_p}
			send "" to {_p}
			give {_p} 1 of tripwire hook named "{@gold}" with lore "" and "{@keylore}"
			play sound "ENTITY_PLAYER_LEVELUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 201 and 700:
			send "" to {_p}
			send "{@p}: &aYou won 2x {@iron}&a!" to {_p}
			send "" to {_p}
			give {_p} 2 of tripwire hook named "{@iron}" with lore "" and "{@keylore}"
			play sound "ENTITY_PLAYER_LEVELUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 701 and 2200:
			send "" to {_p}
			send "{@p}: &aYou won $3000!" to {_p}
			send "" to {_p}
			add 3000 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 2201 and 4200:
			send "" to {_p}
			send "{@p}: &aYou won &f1 Iron Ingot&a!" to {_p}
			send "" to {_p}
			give {_p} 1 iron ingot
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 4201 and 6700:
			send "" to {_p}
			send "{@p}: &aYou won $1000!" to {_p}
			send "" to {_p}
			add 1000 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 6701 and 10000:
			send "" to {_p}
			send "{@p}: &aYou won $500!" to {_p}
			send "" to {_p}
			add 500 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
	if {_crate} is "gold":
		wait 5 ticks
		set {_random} to a random integer from 0 to 10000
		if {_random} is 0:
			send "" to {_p}
			send "{@p}: &aYou won the &6&lGold &7Rank&a!" to {_p}
			send "" to {_p}
			play sound "UI_TOAST_CHALLENGE_COMPLETE" at volume 50 and pitch 1 for {_p}
			broadcast "{@p}: &a%{_p}% got &6&lGold &7Rank&a in a crate!"
			if {_p} has permission "group.gold":
				send "" to {_p}
				send "{@p}: &cYou already have this tag!" to {_p}
				send "{@p}: &7You have been awarded &a$50000&7 instead!" to {_p}
				send "" to {_p}
				add 50000 to {balance.tot::%{_p}%}
			else:
				make console execute command "/lp user %{_p}% permission set group.gold true"
		if {_random} is between 1 and 200:
			send "" to {_p}
			send "{@p}: &aYou won a {@diamond}&a!" to {_p}
			send "" to {_p}
			give {_p} 1 of tripwire hook named "{@diamond}" with lore "" and "{@keylore}"
			play sound "ENTITY_PLAYER_LEVELUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 201 and 700:
			send "" to {_p}
			send "{@p}: &aYou won 2x {@gold}&a!" to {_p}
			send "" to {_p}
			give {_p} 2 of tripwire hook named "{@gold}" with lore "" and "{@keylore}"
			play sound "ENTITY_PLAYER_LEVELUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 701 and 2200:
			send "" to {_p}
			send "{@p}: &aYou won &61 Gold Ingot&a!" to {_p}
			send "" to {_p}
			give {_p} 1 of gold ingot
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 2201 and 4200:
			send "" to {_p}
			send "{@p}: &aYou won $6500!" to {_p}
			send "" to {_p}
			add 6500 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 4201 and 6700:
			send "" to {_p}
			send "{@p}: &aYou won $4000!" to {_p}
			send "" to {_p}
			add 4000 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 6701 and 10000:
			send "" to {_p}
			send "{@p}: &aYou won $3500!" to {_p}
			send "" to {_p}
			add 3500 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
	if {_crate} is "diamond":
		wait 5 ticks
		set {_random} to a random integer from 0 to 10000
		if {_random} is 0:
			send "" to {_p}
			send "{@p}: &aYou won the &b&lDiamond &7Rank&a!" to {_p}
			send "" to {_p}
			play sound "UI_TOAST_CHALLENGE_COMPLETE" at volume 50 and pitch 1 for {_p}
			broadcast "{@p}: &a%{_p}% got &b&lDiamond &7Rank&a in a crate!"
			if {_p} has permission "group.diamond":
				send "" to {_p}
				send "{@p}: &cYou already have this tag!" to {_p}
				send "{@p}: &7You have been awarded &a$75000&7 instead!" to {_p}
				send "" to {_p}
				add 75000 to {balance.tot::%{_p}%}
			else:
				make console execute command "/lp user %{_p}% permission set group.diamond true"
		if {_random} is between 1 and 200:
			send "" to {_p}
			send "{@p}: &aYou won a &b1 Diamond Block&a!" to {_p}
			send "" to {_p}
			give {_p} 1 diamond block
			play sound "ENTITY_PLAYER_LEVELUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 201 and 700:
			send "" to {_p}
			send "{@p}: &aYou won 2x {@diamond}&a!" to {_p}
			send "" to {_p}
			give {_p} 2 of tripwire hook named "{@diamond}" with lore "" and "{@keylore}"
			play sound "ENTITY_PLAYER_LEVELUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 701 and 2200:
			send "" to {_p}
			send "{@p}: &aYou won $9000!" to {_p}
			send "" to {_p}
			add 9000 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 2201 and 4200:
			send "" to {_p}
			send "{@p}: &aYou won &b1 diamond&a!" to {_p}
			send "" to {_p}
			give {_p} 1 diamond
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 4201 and 6700:
			send "" to {_p}
			send "{@p}: &aYou won $7000!" to {_p}
			send "" to {_p}
			add 7000 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}
		if {_random} is between 6701 and 10000:
			send "" to {_p}
			send "{@p}: &aYou won $6000!" to {_p}
			send "" to {_p}
			add 6000 to {balance.tot::%{_p}%}
			play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for {_p}

#------------------------OPEN CRATES------------------------

#------------------------GIVE KEY COMMAND------------------------

command /key [<text>] [<player>] [<text>] [<number>]:
	permission: key.give
	permission message: "&7[&bKEYS&7]: &cYou don't have permission to do this!"
	trigger:
		if arg 1 is "list":
			send "" to player
			send "&7-------[&b&lKeys&7]-------" to player
			send " &7» &fIron" to player
			send " &7» &6Gold" to player
			send " &7» &bDiamond" to player
			send "" to player
			send "&7 /key give <player> <key> <amount>" to player
			send "&7-------[&b&lKeys&7]-------" to player
			send "" to player
		if arg 1 is not set:
			send "" to player
			send "{@p}: &c/key [list/give] <player> <key> <amount>" to player
			send "" to player
		if arg 1 is "give":
			if arg 2 is set:
				if arg 3 is "iron":
					if arg 4 is set:
						give arg-2 arg-4 of tripwire hook named "{@iron}" with lore "" and "{@keylore}"
						send "{@p}: &a%player% &7gave you &b%arg-4%&7 of {@iron}!" to arg-2
						send "{@p}: &7You gave &b%arg-4%&7 of {@iron} to &a%arg-2%&7!" to player
						play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for player
						play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for arg-2
					if arg 4 is not set:
						make player execute "key"
				if arg 3 is "gold":
					if arg 4 is set:
						give arg-2 arg-4 of tripwire hook named "{@gold}" with lore "" and "{@keylore}"
						send "{@p}: &a%player% &7gave you &b%arg-4%&7 of {@gold}!" to arg-2
						send "{@p}: &7You gave &b%arg-4%&7 of {@gold} to &a%arg-2%&7!" to player
						play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for player
						play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for arg-2
					if arg 4 is not set:
						make player execute "key"
				if arg 3 is "diamond":
					if arg 4 is set:
						give arg-2 arg-4 of tripwire hook named "{@diamond}" with lore "" and "{@keylore}"
						send "{@p}: &a%player% &7gave you &b%arg-4%&7 of {@diamond}!" to arg-2
						send "{@p}: &7You gave &b%arg-4%&7 of {@diamond} to &a%arg-2%&7!" to player
						play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for player
						play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for arg-2
					if arg 4 is not set:
						make player execute "key"
				if arg 3 is not set:
					make player execute "key"
			if arg 2 is not set:
				make player execute "key"


command /keyall [<text>] [<number>]:
	permission: key.all
	permission message: "&7[&bKEYS&7]: &cYou don't have permission to do this!"
	trigger:
		if arg 1 is "list":
			send "" to player
			send "&7-------[&b&lKeys&7]-------" to player
			send " &7» &f&lIron" to player
			send " &7» &6&lGold" to player
			send " &7» &b&lDiamond" to player
			send "" to player
			send "&7 /keyall <key> <amount>" to player
			send "&7-------[&b&lKeys&7]-------" to player
			send "" to player
		if arg 1 is not set:
			send "" to player
			send "{@p}: &c/keyall <key> <amount>" to player
			send "" to player
		if arg 1 is "iron":
			if arg 2 is set:
				send "{@p}: &7You gave &b%arg-2%&7 of {@iron} to &aall players&7!" to player
				loop all players:
					give loop-player arg-2 of tripwire hook named "{@iron}" with lore "" and "{@keylore}"
					send "{@p}: &a%player% &7gave you &b%arg-2%&7 of {@iron}!" to loop-player
					play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for player
					play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for loop-player
			if arg 2 is not set:
				make player execute "keyall"
		if arg 1 is "gold":
			if arg 2 is set:
				send "{@p}: &7You gave &b%arg-2%&7 of {@gold} to &aall players&7!" to player
				loop all players:
					give loop-player arg-2 of tripwire hook named "{@gold}" with lore "" and "{@keylore}"
					send "{@p}: &a%player% &7gave you &b%arg-2%&7 of {@gold}!" to loop-player
					play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for player
					play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for loop-player
			if arg 2 is not set:
				make player execute "keyall"
		if arg 1 is "diamond":
			if arg 2 is set:
				send "{@p}: &7You gave &b%arg-2%&7 of {@diamond} to &aall players&7!" to player
				loop all players:
					give loop-player arg-2 of tripwire hook named "{@diamond}" with lore "" and "{@keylore}"
					send "{@p}: &a%player% &7gave you &b%arg-2%&7 of {@diamond}!" to loop-player
					play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for player
					play sound "ENTITY_EXPERIENCE_ORB_PICKUP" at volume 100 and pitch 1 for loop-player
			if arg 2 is not set:
				make player execute "keyall"

#------------------------GIVE KEY COMMAND------------------------
