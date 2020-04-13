# Unofficial documentation to modders - RESEARCH

Unofficial documentation that describes how to read and modify the
research tree present in Workers & Resources.

## Preface

This document uses [Command line description language][1] to describe
structures and formats of directories and configuration files.

Most used tags are:
`<>` - positional argument,
`[]` - optional,
`()` - required,
 `|` - or.

## Files

The research tree is stored in the `research` directory that can be found
in the main games folder (`C:\Program Files (x86)\Steam\steamapps\common\SovietRepublic\media_soviet\research`).

```
research/
├── research.ini
├── tech_1.png
└── tech_2.png
```

Two types of files are stored in this directory. Configuration files, which
are represented by a `research.ini` in which research tree configurations,
i.e., research names, unlocks, and relationships, are stored.

The second type is the icons, which are stored in the PNG format. Names
of these files are not accidental and should correspond to one of the
research names set by the [`$RESEARCH`][1] tag.


## Configuration

Every research has to start with a line `$RESEARCH (name of the research)`,
and end with the line `$RESEARCH_ADD`. The exact order of the technologies
makes no functional difference. It seems that there is no limit to the number
of technologies that can be in the research tree. The tree configuration file
has to end with `ferfer` tag.

```
$RESEARCH chemistry_init

$TYPE_TECHNICAL
$AVAILABLE

$COST 700
$UNLOCK_BUILDING lenin_mausoleum
$UNLOCK_RESEARCH chemistry_1

$NAME 11100
$DESCRIPTION 11101

$RESEARCH_ADD

$RESEARCH chemistry_1

$COST 1400

$UNLOCK_BUILDING crack_den_0
$UNLOCK_BUILDING crack_den_1

$NAME 11102
$DESCRIPTION 11103

$RESEARCH_ADD

ferfer
```

## Tags

### $RESEARCH

- **Designation**:  required
- **Format**: `$RESEARCH (name of the research)`

`$RESEARCH` tag sets the name of the research that is referencable by
the [`$UNLOCK_RESEARCH`][2] tag. It does not set the name that is
visible in the game.

The name argument has influence over which icon will be shown as
a research icon. The game will look for `(name of the research).png` file in
the `research` directory.

### $RESEARCH_ADD

- **Designation**:  required
- **Format**: `$RESEARCH_ADD`

Tag adds research to the research tree and has to be the last tag of the
research definition.

### $TYPE_*

- **Designation**:  required
- **Format**: `$TYPE_TECHNICAL | $TYPE_MEDICAL | $TYPE_POLITICAL`

Research type determines which university can work on the research. The
types are:

- `$TYPE_TECHNICAL` - Technical university,
- `$TYPE_MEDICAL` - Medical university,
- `$TYPE_POLITICAL` - Party HQ.

### $COST

- **Designation**:  required
- **Format**: `$COST (price)`

Cost sets the required amount of human days needed to research the
technology.

### $AVAILABLE

- **Designation**:  optional
- **Format**: `$AVAILABLE`

Optional parameter that makes technology researchable from the start,
i.e., no prerequisite technologies needed.

### $UNLOCK_BUILDING

- **Designation**:  optional
- **Format**: `$UNLOCK_BUILDING (name of the building)`

Defines which buildings are blocked behind the research. The name of
the building argument is not the same for vanilla and workshop buildings.
Format for vanilla buildings is `name_of_the_building`. Format for
workshop buildings is `steam_item_ID/name_of_the_buildings`.

### $UNLOCK_RESEARCH

- **Designation**:  optional
- **Format**: `$UNLOCK_RESEARCH (name of the follow-up research)`

Configures which research will be unlocked for studing. Name of the follow up
research has to be name set by the [`$RESEARCH`][1] tag.

### $NAME

- **Designation**:  optional
- **Format**: `$NAME (Text ID)`

The tag defines the name of the research shown in the game.
`NAME_STR` or another way to add custom names into the game does
not exist right now, which means that technologies with custom names
cannot be created.

### $DESCRIPTION

- **Designation**:  optional
- **Format**: `$DESCRIPTION (Text ID)`

The tag defines a description of the research shown in the game.
`DESCRIPTION_STR` or another way to add custom descriptions into the game does
not exist right now, which means that technologies with custom descriptions
cannot be created.

[1]: #$RESEARCH
[2]: #$UNLOCK_RESEARCH
