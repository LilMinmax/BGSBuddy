# BGSBuddy

BGS buddy is a simple application for generating an Elite Dangerous Back Ground Situation Reports.

# Situation Report

Generates a situation report based on the faction entered into the settings while omitting any systems added to the "offlimits" list.

![Sample Report](https://github.com/EricJFisher/BGSBuddy/blob/master/SampleReport.PNG)

## Critical Reports
 - Systems where you are in conflict
 - Systems where you are in retreat
 - Systems where data is stale (over 2 ticks old)

## Warning Reports
 - Systems where you're in danger of triggering conflict that won't gain you any assets (within 10% influence)
 - Systems where data is stale (hasn't been updated since most recent tick)
 - Systems where you're nearing expansion (more than 65% influence)
 - Systems you're nearing retreat (less than 7.5% influence)
 
## Opportunity Reports
 - Systems where you are near a conflict that can gain you a new asset (within 10% influence)
 - Systems that aren't on your "off limits" list that you aren't the controlling faction
 - Systems where another faction is in retreat

## Controlled Systems
 - Systems you control including all assets present in that system

## Partially Controlled Systems
 - Systems you are the controlling faction, but do not control all assets in the system

# Expansion Planner

Generates an expansion report for planning expansions. This includes most likely places for an expasion to reach based on current data.

Note: Expansion planner will omit any systems containing the controlling faction of the system entered as the system to expand from. (this is NOT based on the faction you entered in Settings)

![Sample Report](https://github.com/EricJFisher/BGSBuddy/blob/master/expansionplanner.png)

## Space Available

 - Systems in range of the expanding system with less than 7 factions present making them available to expand into without requiring an invasion.

## Invasion Targets

 - Systems in range of the expanding system ordered by lowest influence of a "non-native" faction to highest making them available as targets for invasion if no systems have space available.
 
## FAQ
 - Does this tool save any files to my hard drive? Yes, it creates a directory `BGSBuddy` in your `Documents` folder. The file placed here `Settings.txt` contains basic application settings such as your faction name and what systems are on your offlimits list.
 - It seems to take quite a while to update the report, what gives? I am leveraging both the EliteBGS API and the EDDB API, unfortunately I have no control over these third party services so when generating the report it's not as simple as making a call and parsing the data... Assuming data is at least older than the last tick there is 1 call for the faction info, a second call to get when the most recent tick happened, then 2 calls for every system who's information is older than the most recent tick. This can be A LOT of calls. I'm hoping EliteBGS stream lines this into a singular call later, but at this time we're stuck waiting on every single one of these calls completing... which can take upwards of 30 seconds.
 - How do I update the off limits systems? Click on the "Settings" button below the title. *Note: the value is comma seperated without leading or following spaces, I'll make this less cumbersome later Ex `Sol,Lave,Brestla`*
 - How do I use this? Open it, then click on "settings" and enter your faction name and any systems you want omitted from the report, then "Save and Close", then press "Update". The report is regenerated anytime you reopen the application.
 - Do you accept pull requests? Yes, submit it and as long as it's desirable functionality (from my perspective, sorry) I'll check it out and bring it in! (I'm pretty open to support so long as it aligns with the intention of the application which is to be able to quickly get a glimpse at your immediate BGS situation) EliteBGS and Inara already cover historical information well.
 - Why is the code so bad? Check the Code Situation section, I just hacked this together with no intention of it being a thing, and well... it's a thing now I guess... so yeah... my bad... I'll work on it.

## Code situation

I've decided to open source it to share with others, however; it was a proof of concept hack job so the code is not up to the quality it should be, I will correct this over time, but just advising it's a bit of an untestable mess atm, you've been warned.
