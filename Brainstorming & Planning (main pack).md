Glossary: 'Remove' = remove all recipes for the thing, and all recipes that it can do.
- ## Mod-specific stuff
	- ### Gregtech
		- MAYBE De-tier GT machines and circuits, to an extent
			- Pyanodons has Mark 1 to 5 for most machines, could take a lil inspiration from that.
		- Have machines locked behind science.
			- Also have recipes within machines locked behind science, if possible.
		- Maybe get rid of GT pipes for the most part.
		- Rename GT's research system to something else to avoid confusion
			- Possible names:
				- Analytical System
				- Indagation Implementation
				- Innovation Complex
		- MAYBE restructure the whole mod, if needs be.
		- ULV?
			- 
	- ### Mystical Agriculture \[deprecated]
		- #### MA is not playing nicely with KubeJS - Coremod is being made. 
		- The only source of ores.
		- Higher-tier seeds must be synthesized or spliced from constituents, after researching them.
			- must think about whether synthetization or splicing would be good - maybe a mix of both?
		- Mystical Agriculture's machines & crafting structures have been 'removed'
		- Find uses for the Inferium -> Insanium essences
		- Maybe add a bunch of 'harvested {source-item-here} crop' items as an intermediate between harvesting the crops and getting the essences & seed to replant the crop
			- fuckton of loot table modifications will be needed if i wanna do that with KubeJS
				- (or a coremod that just Mixins to the mod with all the wanted additions/changes)
	- ### Create
		- 'Remove' most functionality and all native sources of RPM/SU
			- definitely keep the logistics side of the mod tho, because I like it, and it fits the Factorio theme.
				- tunnels, funnels & smart chutes will be locked behind basic circuits (and the applicable research thereof)
				- normal chutes will be locked behind Automation research
				- mechanical arms will be available almost right from the get-go
			- [[Kanban#^5ggylw|figure out how to implement a good machine-based source of RPM]]
	- ### Greate (possibly?)
		- Causes a crash currently when placing belts with Flywheel's **Batching** backend enabled instead of the **Instancing** backend (this has been fixed on the main Git repo, will revisit when the devs release a proper update)
		- 'Remove' all but the belts, shafts, gearboxes and small gears.
		- Keep the spouting machine? idk
	- ### AE2
		- Gated late into the pack, behind extreme amounts of research and intermediate components.
		- EXPENSIVE AS FUCK, but still extremely useful.
	- ### Hostile Neural Networks
		- The only source of mob drops (BIG MAYBE)
		- Locked behind advanced bio-engineering research.
	- ### Xnet ^eb43de
		- Mid-game item/fluid/energy/logic transportation
	- ### Pipez ^ea6f54
		- Early-game energy transportation.
		- Probably will disable all other pipes from the mod.
		- Pipe upgrades will be locked behind research.
	- ### Flux Networks ^00de2b
		- Late-game wireless energy transportation
	- ### Computercraft
		- For the smart people.
	- ### Project Red
		- Also for the smart people.
	- ### [[Brainstorming & Planning (coremod)|Gregic Agrifactory Core]]
- ## General
	- ### Heavy focus on being Pyanodons & Krastorio2-like:
		- recursive recipes
		- repurposing byproducts
		- vast processing lines
		- Simple shit like the Create Tunnels will be locked behind basic circuits, which in turn will be locked behind a slew of other research and processes
	- ### Research
		- Possible styles of the research system:  ^7461f9
			- Factorio style:
				- Research items are produced in assemblers.
				- Research items are placed in special researchers that gradually tick up the progress of the selected research quest.
			- Feed the Factory style:
				- Research items are produced in dedicated labs.
				- Research items are directly submitted to quests.
	- ### Bio-Engineering
		- Mystical Agriculture seeds must be Bio-Engineered
			- Special GT or MBD2 machines needed???
		- GMO entities (Possibly ???????)
			- Each one has special drops needed en-mass for progression.
			- Some of them can become **HOSTILE AND DANGEROUS**.
				- Some of them might even become a threat to the world if left alive and alone for long enough.
		- **EXTREME** usage of GT's cleanroom for later bio-engineering recipes.
			- Probably not gonna try and get MBD2 things to be able to detect if they're in a cleanroom
		- [Gleba-style spoilage system](https://factorio.com/blog/post/fff-414) for most organic objects 
			- Every food (or otherwise organic) item will have a 'freshness' timer that ticks down in real time from the moment that the item is created.
				- The only way to slow down or stop the freshness timer will be to store them in a Cold Chest or freezer
					- Cold Chests (singleblock, cannot be made into double chest) will slow the freshness timers of anything in them by 50%, but only when surrounded on 4 or more sides by ice.
					- Freezers (multiblock) will indefinitely halt the timer of anything placed inside them, at the cost of needing constant feed of power & some sort of cryogenic liquid. (TODO: think about what said liquid could be)
			- May be quite tricky to pull off - this is probably wading deep into NBT madness.
				- Items with different NBT data are naturally unstackable with each other (even if they have the same `namespace:item_id`), gonna have to work around this.
				- Possible approach(es):
					- Approach 1: Upon item creation, the item gains NBT containing a Unix timestamp that can then be counted down to internally.
						- Pros: Doesn't require the NBT itself to be updated every second.
						- Cons: Not very malleable after the fact.
					- Approach 2: Upon item creation, the item gains NBT containing the timer itself, which gets updated every second.
						- Pros: Can have the timer easily updated on the fly when attempting to preserve the items.
						- Cons: Would probably start killing TPS really quickly.
					- Approach 3: Upon item creation, the item gains NBT with a ID (or UUID), which then gets appended to a Map (as the key) alongside a Unix timestamp (as the value) of when the item is due to spoil. This value can be updated when the item is preserved, and then removed when the item spoils or is destroyed.
						- Pros: TBD
						- Cons: May start to cause a memory leak if items are destroyed in ways that cannot be reasonably handled or detected - No detection, no removal from the Map.
					- Approach 4: How TFC does it:![[tfcDiscordScreenshot-FoodPreservationSpoilageTimer.png]]
						- Pros:
						- Cons: Rapidly moving items in and out of cold storage may be a bit fucky.
		- May or may not go really 'OH GOD WTF IS THAT' with some of the GMOs
			- Will have to research the rules of Modrinth & Minecraft's EULA to see how far I can go.
	- ### Burner Blocks (EXTREMELY BIG BIG BIG BIIIIG MAYBE)
		- Any block that burns fuel items in order to process a recipe will produce ash with every fuel item burnt. (including normal furnaces)
			- If the ash slot is full, the block stops doing what it does until the ash is cleared.
		- No fuel, no recipe progress.
	- ### may just need to make a coremod for a lot of this deviously ambitious shit
	- ### Dimension-specific content (BIG MAYBE)
		- May or may not have machine recipes be only processable in specific dimensions.
		- If i'm gonna do this, i gotta figure out a good way of gating dimensions to research & progression