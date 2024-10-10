# Data Sources

## 1. Pokemon.csv

Document with basic data's Pokémon: Name, Numeber, Generation, Types and Stats.

### Fields Description

- ID: For joins and also is the number of the Pokémon
- Name: The name of the Pokémon (e.g., Pikachu, Bulbasaur).
- Form: Indicates if the Pokémon has more than one form (not used in this version).
- Type1: The primary type of the Pokémon (e.g., Fire, Water, Grass).
- Type2: - The secondary type of the Pokémon, if applicable (e.g., Flying, Ice). If the Pokémon has only one type, this field is empty.
- Total: The sum of all base stats for the Pokémon (HP, Attack, Defense, Sp. Atk, Sp. Def, Speed).
- HP: The base **Health Points** stat of the Pokémon.
- Attack: The base **Attack** stat, which determines the power of physical moves.
- Defense: The base **Defense** stat, which reduces damage from physical moves.
- Sp. Atk: The base **Special Attack** stat, which determines the power of special moves.
- Sp. Def: The base **Special Defense** stat, which reduces damage from special moves.
- Speed: The base **Speed** stat, which determines the order of moves in battle.
- Generation: The generation in which the Pokémon was introduced (e.g., Generation I, Generation V).


## 2. pokedex_description.csv

For the pokedex description inclusion of each Pokémon.

### Fields Description

- ID: The number of the Pokémon.
- Description: The pokedex description of each Pokémon.

## 3. pokemon_species.csv

# Pokémon Database Documentation

Mainly used for the chain evolution calculation of each Pokémon.

## Fields Description

- `id`:
- A unique identifier for each Pokémon, typically corresponding to their National Dex number.

### 2. `name`:
- The name of the Pokémon (e.g., Pikachu, Bulbasaur).

### 3. `form`:
- Indicates if the Pokémon has an alternate form (e.g., Mega Evolution, regional variants). If empty, the Pokémon has only one form.

### 4. `type1`:
- The primary type of the Pokémon (e.g., Fire, Water).

### 5. `type2`:
- The secondary type of the Pokémon, if applicable. It may be empty for single-type Pokémon.

### 6. `total`:
- The total base stats for the Pokémon (sum of HP, Attack, Defense, Sp. Atk, Sp. Def, and Speed).

### 7. `hp`:
- Base **Health Points** stat, representing the Pokémon's durability.

### 8. `attack`:
- Base **Attack** stat, affecting the power of physical moves.

### 9. `defense`:
- Base **Defense** stat, reducing damage from physical moves.

### 10. `sp_atk`:
- Base **Special Attack** stat, affecting the power of special moves.

### 11. `sp_def`:
- Base **Special Defense** stat, reducing damage from special moves.

### 12. `speed`:
- Base **Speed** stat, determining the order of turns in battle.

### 13. `generation`:
- Indicates the generation in which the Pokémon was introduced (e.g., Generation I, Generation VI).