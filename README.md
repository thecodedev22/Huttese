# Huttese

A powerful, Huttese-inspired interactive fiction engine for creating branching narrative games. Write stories using simple commands in a language that would make Jabba proud!

## Features

- **Interactive Storytelling** - Create complex branching narratives with multiple paths
- **Programming Logic** - Variables, counters, flags, timers, and math operations
- **Save System** - Multiple save slots with full state persistence
- **Rich Text Effects** - Formatting, delays, sound effects, and screen clearing
- **Developer Tools** - Debug mode, error handling, and comprehensive logging
- **Modular Stories** - Include system for splitting large stories into multiple files
- **Randomization** - Probability-based choices and random variables

## Quick Start

1. **Install Python 3.6+**
2. **Download `hutt.py`**
3. **Create a story file** (see example below)
4. **Run your story:**
   ```bash
   python hutt.py mystory.hutt
   ```

## Basic Story Format

Stories are written in plain text files with special Huttese commands:

```
start:
jee-jee Welcome to the cantina, traveler!
jee-jee The music is loud and the air is thick with smoke.

set credits 50
take blaster

kee credits >= 10 buy_drink
nova leave_cantina

buy_drink:
jee-jee You order a blue milk. It costs 10 credits.
sub credits 10
bolla start

leave_cantina:
jee-jee You step out into the desert night.
👉
```

## Command Reference

### Scene Management
- `scene_name:` - Start a new scene
- `👉` or `The End` - End the story
- `bolla scene_name` - Call another scene (like a function)

### Text & Narrative
- `jee-jee text` - Display narrative text
- `bold text` - **Bold formatting**
- `italic text` - *Italic formatting*
- `delay 2.5` - Pause for 2.5 seconds
- `clear` - Clear the screen
- `huttdance` - Jabba dances!

### Variables & Math
- `set variable value` - Set a variable
- `set health player_max_health + 50` - Math expressions
- `add variable amount` - Increment variable
- `sub variable amount` - Decrement variable  
- `mult variable amount` - Multiply variable
- `random variable min max` - Random number
- `{variable}` - Insert variable value in text

### Inventory System
- `take item_name` - Add item to inventory
- `drop item_name` - Remove specific item
- `drop_all` - Clear entire inventory

### Counters & Flags
- `count counter_name` - Increment a counter
- `reset_count counter_name` - Reset counter to 0
- `flag flag_name` - Set a flag
- `unflag flag_name` - Remove a flag

### Timers ⏰
- `timer timer_name 30` - Set timer for 30 seconds
- `if timer timer_name scene` - Check if timer expired

### Branching & Conditions
- `kee condition target_scene` - Conditional branch
- `nova target_scene` - Else/default branch
- `if variable == value target_scene` - Variable comparison
- `if has item_name target_scene` - Check inventory
- `if flag flag_name target_scene` - Check flag
- `if count counter >= 5 target_scene` - Check counter
- `if probability 25 target_scene` - 25% chance

### Comparison Operators
- `==` - Equal to
- `!=` - Not equal to  
- `>` - Greater than
- `<` - Less than
- `>=` - Greater than or equal
- `<=` - Less than or equal
- `contains` - String contains

### Save & Load System 💾
- `save slot_name` - Save game state
- `load slot_name` - Load game state

### Audio & Effects 🎵
- `sound effect_name` - Play sound effect
- `music track_name` - Play background music

### Development Tools 🔧
- `include other_file.hutt` - Include another story file
- `# comment` - Add comments (ignored)
- `debug` - Show current game state

## Player Commands

While playing, users can type these commands:
- `help` - Show available commands
- `status` - View game state (variables, inventory, flags)
- `history` - Show recently visited scenes
- `log` - Display story event log
- `save slot_name` - Save to specific slot
- `load slot_name` - Load from specific slot  
- `quit` - Exit the game

## Example Story

```hutt
# The Great Hutt Adventure
# A demo story showing off engine features

start:
jee-jee You wake up in Jabba's palace...
jee-jee Your health is {health} and you have {credits} credits.

set health 100
set credits 25
random luck 1 10

kee luck >= 7 lucky_start
kee credits >= 20 rich_start  
nova poor_start

lucky_start:
jee-jee You feel lucky today!
flag lucky_day
take lucky_charm
bolla throne_room

rich_start:
jee-jee Your pockets jingle with coins.
bolla marketplace

poor_start:  
jee-jee You're broke, but determined.
count poor_choices
bolla servant_quarters

throne_room:
jee-jee Jabba sits on his massive throne, eyeing you suspiciously.
sound jabba_laugh

timer audience 10
kee has lucky_charm impress_jabba
if timer audience disappointed_jabba
nova grovel_before_jabba

impress_jabba:
jee-jee Your lucky charm catches Jabba's attention!
jee-jee bold "Ho ho ho!" laughs the great Hutt.
add credits 100
bolla victory

disappointed_jabba:
jee-jee Jabba grows impatient with your silence.
sub health 25
nova dungeon

victory:
jee-jee You have impressed the mighty Jabba!
save victory_save
👉

# Include additional story files
include palace_dungeon.hutt
include marketplace.hutt
```

## Command Line Options

```bash
# Basic usage
python hutt.py story.hutt

# Enable debug mode
python hutt.py story.hutt --debug

# Debug mode shows:
# - Parsing information
# - Scene transitions
# - Variable changes
# - Error details
```

## Advanced Features

### Modular Stories
Split large stories across multiple files:

```hutt
# main.hutt
start:
jee-jee Welcome to the main story!
include chapter1.hutt
include chapter2.hutt
```

### Complex Conditions
Combine multiple condition types:

```hutt
temple_entrance:
kee has key_card && credits >= 50 enter_temple
kee flag temple_member enter_as_member
if count visit_attempts >= 3 desperate_entry
nova turned_away
```

### Dynamic Text
Use variables in your narrative:

```hutt
status_report:
jee-jee Health: {health}/100
jee-jee Credits: {credits}
jee-jee You have visited {count} locations.
```

## Tips & Best Practices

1. **Use descriptive scene names** - `dark_alley` not `scene3`
2. **Test all paths** - Use debug mode to verify branches work
3. **Save frequently during development** - Use the save system to test different paths
4. **Comment your complex logic** - Future you will thank you
5. **Use includes for organization** - Split large stories into logical files
6. **Plan your variables** - Decide on naming conventions early

## Error Handling

The engine includes comprehensive error handling:
- Line numbers for parsing errors
- Graceful handling of missing scenes
- Invalid condition checking
- File not found errors

Enable debug mode (`--debug`) to see detailed error information.

## File Extensions

While any text file works, we recommend:
- `.hutt` - Main story files
- `.txt` - Simple story files
- Use UTF-8 encoding for special characters

## Contributing

This engine is designed to be hackable! Some ideas for extensions:
- Sound system integration
- Graphics/image support  
- Network multiplayer
- Story compilation tools
- Visual story editors

## License

Feel free to use, modify, and distribute.

May the Force be with you, and may Jabba smile upon your stories!

---

*"Kee younglings know not the power of the Hutt tongue!" - Ancient Tatooine Proverb*
