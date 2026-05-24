# Safe PGH Streets - Pittsburgh Bicycle Route Safety Analyzer

An OpenCode skill that analyzes bicycle route safety in Pittsburgh, PA by combining historical crash data and active construction information. Upload a GPX file with turn-by-turn cues and get a detailed safety report for each street on your route.

## What This Tool Does

Before you ride your bike in Pittsburgh, this tool helps you:
- See which streets on your route have had bicycle crashes
- Find out where construction and road closures are happening right now
- Get a safety rating for each street on your route
- Make informed decisions about whether to take that route or choose a safer alternative

**You'll need:**
- A GPX file with turn-by-turn directions from your bike routing app (Ride with GPS, Komoot, Strava, etc.)
- A Windows, Mac, or Linux computer
- An internet connection

**This tool works for:** Pittsburgh and Allegheny County, PA routes only

## What You'll Get in Your Safety Report

- **Safety score for each street** - A rating from 1-10 based on bicycle crash history
- **Construction alerts** - Current road closures and lane reductions along your route
- **Overall route rating** - An average safety score for your entire ride
- **Recommendations** - Suggestions for riding safely

## Where the Data Comes From

This tool uses real data from:
- **Allegheny County crash records** - Historical bicycle crash data for every street
- **City of Pittsburgh DOMI** - Active construction permits and road closures (updated regularly)

---

## Installation

### Step 1: Install OpenCode CLI

OpenCode is a program that lets you talk to an AI assistant in your computer's command window. Follow the instructions for your computer:

#### Windows

1. Click the Windows Start button and type "PowerShell"
2. Right-click on "Windows PowerShell" and select "Run as administrator"
3. Copy this command and paste it into the PowerShell window:
   ```powershell
   irm https://install.opencode.so/install.ps1 | iex
   ```
4. Press Enter and wait for it to finish
5. Close PowerShell and open it again (you don't need administrator this time)
6. Type this command to check if it worked:
   ```powershell
   opencode --version
   ```
7. If you see a version number, it worked!

#### macOS

1. Click the magnifying glass in the top-right corner (Spotlight Search)
2. Type "Terminal" and press Enter
3. Copy this command and paste it into Terminal:
   ```bash
   curl -fsSL https://install.opencode.so/install.sh | sh
   ```
4. Press Enter and wait for it to finish
5. Close Terminal and open it again
6. Type this command to check if it worked:
   ```bash
   opencode --version
   ```
7. If you see a version number, it worked!

#### Linux

1. Open your terminal application
2. Copy this command and paste it:
   ```bash
   curl -fsSL https://install.opencode.so/install.sh | sh
   ```
3. Press Enter and wait for it to finish
4. Close your terminal and open it again
5. Type this command to check if it worked:
   ```bash
   opencode --version
   ```
6. If you see a version number, it worked!

### Step 2: Install the Safe PGH Streets Skill

The "skill" is a set of instructions that teaches OpenCode how to analyze bike routes.

#### Windows Instructions

1. Press `Windows Key + R` on your keyboard
2. Type `%USERPROFILE%` and press Enter - this opens your user folder
3. Look for a folder called `.opencode` (note the dot at the beginning)
   - **Don't see it?** That's okay - you need to create it:
     - Right-click in the empty space → New → Folder
     - Name it `.opencode` (with the dot)
4. Open the `.opencode` folder
5. Create a new folder inside called `skills`
6. Open the `skills` folder
7. Create a new folder inside called `safe-pgh-streets`
8. Download the `SKILL.md` file from this repository
9. Put the `SKILL.md` file inside the `safe-pgh-streets` folder

**Your final path should look like:**
`C:\Users\YourName\.opencode\skills\safe-pgh-streets\SKILL.md`

#### macOS Instructions

1. Open Finder
2. Press `Command + Shift + G` on your keyboard
3. Type `~/.opencode` and press Enter
   - **Don't see the folder?** You need to create it:
     - Press `Command + Shift + .` to show hidden files
     - Create a new folder called `.opencode` in your home folder
4. Inside `.opencode`, create a folder called `skills`
5. Inside `skills`, create a folder called `safe-pgh-streets`
6. Download the `SKILL.md` file from this repository
7. Put the `SKILL.md` file inside the `safe-pgh-streets` folder

**Your final path should look like:**
`/Users/YourName/.opencode/skills/safe-pgh-streets/SKILL.md`

#### Linux Instructions

1. Open your file manager
2. Go to your home folder
3. Press `Ctrl + H` to show hidden files
4. Look for a folder called `.opencode`
   - **Don't see it?** Create a new folder called `.opencode`
5. Inside `.opencode`, create a folder called `skills`
6. Inside `skills`, create a folder called `safe-pgh-streets`
7. Download the `SKILL.md` file from this repository
8. Put the `SKILL.md` file inside the `safe-pgh-streets` folder

**Your final path should look like:**
`/home/yourname/.opencode/skills/safe-pgh-streets/SKILL.md`

### Step 3: Configure MCP Servers

MCP servers are where the crash data and construction information come from. You need to tell OpenCode where to find them.

#### Windows Instructions

1. Press `Windows Key + R` on your keyboard
2. Type `%USERPROFILE%\.opencode` and press Enter
3. Right-click in the empty space → New → Text Document
4. Name it `mcp.json` (make sure it ends with .json, not .txt)
   - **Tip:** If you can't see file extensions, click View → File name extensions
5. Right-click on `mcp.json` and open it with Notepad
6. Copy and paste this text into the file:

```json
{
  "mcpServers": {
    "safe-pgh-streets": {
      "url": "https://safe-pgh-streets-mcp.brubernator.link/mcp"
    },
    "domi-obstruction": {
      "url": "https://domi-obstruction-mcp.brubernator.link/mcp"
    }
  }
}
```

7. Save the file and close Notepad

#### macOS Instructions

1. Press `Command + Space` and type "TextEdit", then press Enter
2. Click Format → Make Plain Text
3. Copy and paste this text:

```json
{
  "mcpServers": {
    "safe-pgh-streets": {
      "url": "https://safe-pgh-streets-mcp.brubernator.link/mcp"
    },
    "domi-obstruction": {
      "url": "https://domi-obstruction-mcp.brubernator.link/mcp"
    }
  }
}
```

4. Click File → Save
5. For the save location, press `Command + Shift + G`
6. Type `~/.opencode` and press Enter
7. Name the file `mcp.json`
8. Click Save

#### Linux Instructions

1. Open your text editor (gedit, nano, or any text editor)
2. Copy and paste this text:

```json
{
  "mcpServers": {
    "safe-pgh-streets": {
      "url": "https://safe-pgh-streets-mcp.brubernator.link/mcp"
    },
    "domi-obstruction": {
      "url": "https://domi-obstruction-mcp.brubernator.link/mcp"
    }
  }
}
```

3. Save the file as `mcp.json` in your home folder at: `~/.opencode/mcp.json`

---

## Usage

### Where to Save Your GPX File

Before you can check your route, you need to save your GPX file somewhere easy to find.

**Best Option: Save to Your Documents Folder**

1. Export your route as a GPX file from your bike app (Ride with GPS, Komoot, etc.)
2. Save it to your Documents folder
3. Give it a simple name without spaces, like: `my-bike-route.gpx`

**Example locations:**
- Windows: `C:\Users\YourName\Documents\my-bike-route.gpx`
- Mac: `/Users/YourName/Documents/my-bike-route.gpx`
- Linux: `/home/yourname/Documents/my-bike-route.gpx`

### How to Check Your Route Safety

#### Windows Instructions

1. Click the Windows Start button and type "PowerShell"
2. Click on "Windows PowerShell" to open it
3. Type this command to go to your Documents folder:
   ```powershell
   cd Documents
   ```
4. Press Enter
5. Type this command to start OpenCode:
   ```powershell
   opencode agent
   ```
6. Press Enter
7. When OpenCode is ready, type your question with the @ symbol before your filename:
   ```
   @my-bike-route.gpx Check the safety of this route
   ```
8. Press Enter and wait for your safety report!

#### macOS Instructions

1. Press `Command + Space` and type "Terminal"
2. Press Enter to open Terminal
3. Type this command to go to your Documents folder:
   ```bash
   cd Documents
   ```
4. Press Enter
5. Type this command to start OpenCode:
   ```bash
   opencode agent
   ```
6. Press Enter
7. When OpenCode is ready, type your question with the @ symbol before your filename:
   ```
   @my-bike-route.gpx Check the safety of this route
   ```
8. Press Enter and wait for your safety report!

#### Linux Instructions

1. Open your Terminal application
2. Type this command to go to your Documents folder:
   ```bash
   cd Documents
   ```
3. Press Enter
4. Type this command to start OpenCode:
   ```bash
   opencode agent
   ```
5. Press Enter
6. When OpenCode is ready, type your question with the @ symbol before your filename:
   ```
   @my-bike-route.gpx Check the safety of this route
   ```
7. Press Enter and wait for your safety report!

### Other Ways to Ask

You can ask OpenCode in different ways:
- `@my-bike-route.gpx Is this route safe to ride?`
- `@my-bike-route.gpx Check for crashes and construction`
- `@my-bike-route.gpx Analyze this Pittsburgh cycling route`
- `@my-bike-route.gpx Give me a safety report`

### What You'll See

After you ask, OpenCode will:
1. Read your GPX file
2. Look up crash data for each street on your route
3. Check for active construction zones
4. Create a detailed safety report showing:
   - Which streets have the most crashes
   - Where construction is happening
   - An overall safety rating for your route
   - Recommendations for riding safely

### GPX File Requirements (Detailed)

**What makes a GPX file work with this tool:**

✅ **Yes - These work:**
- Files from routing apps with "turn-by-turn" or "cue sheet" option enabled
- Routes you planned (not recorded while riding)
- Files that have street names embedded in them

❌ **No - These don't work:**
- GPS tracks you recorded while actually riding (these only have coordinates, no street names)
- Simple route lines without turn instructions
- Files from fitness trackers that only log your path

**How to check if your GPX file will work:**

The easiest way: Try it! If OpenCode says "no street names found," you need to re-export your route with turn-by-turn directions enabled.

**Where your GPX file comes from matters:**
- **Planned a route** in Ride with GPS, Komoot, or Strava? ✅ Should work (if exported correctly)
- **Recorded a ride** with your bike computer or phone? ❌ Won't work
- **Someone sent you** their route file? ✅ Might work (depends how they exported it)

**Pittsburgh/Allegheny County only:**
This tool only has data for routes in the Pittsburgh area. Routes in other cities won't return any crash or construction data.

### Example: What It Looks Like

Here's what you'll see when you use OpenCode:

```
C:\Users\YourName\Documents> opencode agent

OpenCode is starting...

You: @strip-district-route.gpx Check the safety of this route

OpenCode: I'll analyze your Pittsburgh bike route for safety...

[A few moments later, you'll see a detailed report with:]

🚲 Pittsburgh Bike Route Safety Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Route: Penn Ave → Liberty Ave → Smallman St
Total Streets Analyzed: 8

⚠️ Active Construction:
- Penn Avenue has a lane closure until June 30

📊 Street Safety Ratings:
- Penn Ave: 3/10 (12 crashes, high risk)
- Liberty Ave: 7/10 (3 crashes, moderate risk)
- Smallman St: 10/10 (no crashes, safe)

🏆 Overall Route Safety: 6.7/10 - Moderate Risk
Recommendation: Ride with care, especially on Penn Ave
```

---

## Sample Output

The skill generates a structured safety report:

```markdown
### 🚲 Pittsburgh Bike Route Safety Report

**Route**: Penn Ave → Liberty Ave → Smallman St
**Total Streets Analyzed**: 8
**Report Generated**: May 23, 2026

---

### ⚠️ Active Construction & Obstructions

**Penn Avenue** (4500-4600 block)
- Type: Lane Closure
- Duration: May 15 - June 30, 2026
- Note: Eastbound lane reduced to one lane

**No other active obstructions found**

---

### 📊 Per-Street Crash Safety Ratings

| Street        | Crashes | Severity          | Safety Rating |
|---------------|---------|-------------------|---------------|
| Penn Ave      | 12      | 2 fatal, 4 injury | 3/10          |
| Liberty Ave   | 3       | 0 fatal, 3 injury | 7/10          |
| Smallman St   | 0       | None              | 10/10         |

---

### 🏆 Overall Route Rating

**Overall Route Safety: 6.7 / 10** — ⚠️ Moderate Risk — ride with care
```

---

## Troubleshooting

### Problem: "OpenCode command not found"

**What it means:** OpenCode didn't install correctly or your computer can't find it.

**How to fix:**
1. Close your PowerShell or Terminal window completely
2. Open a new PowerShell or Terminal window
3. Try typing `opencode --version` again
4. If it still doesn't work, repeat Step 1 of the installation instructions

### Problem: "File not found" or Can't Find Your GPX File

**What it means:** OpenCode can't see your GPX file where you said it was.

**How to fix:**

**Option 1: Make sure you're in the right folder**
1. When you open PowerShell or Terminal, type:
   - Windows: `cd Documents` and press Enter
   - Mac/Linux: `cd Documents` and press Enter
2. Now start OpenCode: `opencode agent`
3. Use just the filename: `@my-bike-route.gpx`

**Option 2: Check your file is really there**
- Open your Documents folder in Windows Explorer (Windows) or Finder (Mac)
- Look for your GPX file
- Make sure the name matches exactly what you typed (including the .gpx ending)

**Option 3: Use a simpler filename**
- If your file has spaces in the name, rename it
- Change "my bike route.gpx" to "my-bike-route.gpx"
- Avoid special characters like !@#$%^&*

### Problem: "No street names found in GPX"

**What it means:** Your GPX file doesn't have the turn-by-turn directions needed for this tool.

**How to fix:**
1. Go back to your routing app (Ride with GPS, Komoot, Strava, etc.)
2. When exporting your route:
   - Look for an option like "Include turn-by-turn cues"
   - Or "Include cue sheet"
   - Or "Include waypoints"
3. Make sure that option is checked/enabled
4. Export the GPX file again
5. Save it to your Documents folder
6. Try again with OpenCode

**Important:** GPX files from recorded rides (where you actually rode and tracked it) usually won't work. You need a planned route with turn-by-turn directions.

### Problem: "Skill not found"

**What it means:** OpenCode can't find the Safe PGH Streets skill you installed.

**How to fix:**
1. Go back to Step 2 of the installation instructions
2. Make sure you created all the folders correctly:
   - `.opencode` folder
   - `skills` folder inside `.opencode`
   - `safe-pgh-streets` folder inside `skills`
3. Make sure the `SKILL.md` file is inside the `safe-pgh-streets` folder
4. The full path should be: `.opencode/skills/safe-pgh-streets/SKILL.md`

### Problem: "MCP server unreachable"

**What it means:** OpenCode can't connect to the servers that have the crash and construction data.

**How to fix:**
1. Check that you're connected to the internet
2. Make sure you completed Step 3 (Configure MCP Servers)
3. Check that the `mcp.json` file is in the right place: `.opencode/mcp.json`
4. Try again in a few minutes (the server might be temporarily down)

### Problem: "No data available"

**What it means:** Your route might be outside Pittsburgh or the street doesn't have crash data.

**What this means:**
- This tool only works for routes in Pittsburgh and Allegheny County, PA
- If your route is elsewhere, it won't have data
- Some streets might not have any crash records (which is good news!)

---

## Contributing

If you'd like to help improve this tool, you're welcome to suggest changes or report problems! Just open an issue on this repository.

### For Developers

If you want to modify how the skill works:

1. Open the `SKILL.md` file in any text editor
2. Make your changes
3. Save the file
4. Test it by using OpenCode with a GPX file

---

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

This means you're free to:
- Use this tool for any purpose
- Modify the code however you want
- Share it with others
- Use it in commercial projects

The only requirement is that you include the original copyright notice.

---

## Acknowledgments

- **Data Sources**: Allegheny County crash data, City of Pittsburgh DOMI permits
- **MCP Servers**: Hosted by brubernator.link
- **OpenCode Platform**: Built with OpenCode Skills framework

---

## Important Safety Information

**Please read this carefully:**

This tool shows you historical data and current construction information, but it cannot guarantee your safety. Here's what you need to know:

- **Past crashes don't predict the future** - A street with no crashes in the past could still be dangerous today
- **Construction info might be outdated** - Permit dates can change, and new construction starts all the time
- **You still need to use good judgment** - Even a "safe" street requires you to ride carefully and follow traffic laws
- **Always wear a helmet and use lights** - Basic safety gear is essential no matter what route you take
- **Check conditions before you ride** - Weather, traffic, and visibility can change everything

**This tool is meant to help you make informed decisions, not to replace common sense and safe cycling practices.**

Think of it like a weather forecast: It gives you useful information, but you still need to look outside and decide what to wear!
