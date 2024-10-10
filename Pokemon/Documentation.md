# Data Sources

## 1. Pokemon.csv

Document with basic data's Pokémon: Name, Numeber, Generation, Types and Stats.

### Fields Description

- `ID`: For joins and also is the number of the Pokémon, corresponding to their National Dex number.
- `Name`: The name of the Pokémon (e.g., Pikachu, Bulbasaur).
- `Form`: Indicates if the Pokémon has more than one form (not used in this version).
- `Type1`: The primary type of the Pokémon (e.g., Fire, Water, Grass).
- `Type2`: - The secondary type of the Pokémon, if applicable (e.g., Flying, Ice). If the Pokémon has only one type, this field is empty.
- `Total`: The sum of all base stats for the Pokémon (HP, Attack, Defense, Sp. Atk, Sp. Def, Speed).
- `HP`: The base **Health Points** stat of the Pokémon.
- `Attack`: The base **Attack** stat, which determines the power of physical moves.
- `Defense`: The base **Defense** stat, which reduces damage from physical moves.
- `Sp. Atk`: The base **Special Attack** stat, which determines the power of special moves.
- `Sp. Def`: The base **Special Defense** stat, which reduces damage from special moves.
- `Speed`: The base **Speed** stat, which determines the order of moves in battle.
- `Generation`: The generation in which the Pokémon was introduced (e.g., Generation I, Generation V).

## 2. pokedex_description.csv

For the pokedex description inclusion of each Pokémon, extracted with the script in the Extraction section.

### Fields Description

- `ID`: The number of the Pokémon.
- `Description`: The pokedex description of each Pokémon.

## 3. pokemon_species.csv

Mainly used for the chain evolution calculation of each Pokémon.

## Fields Description

- `id`: Unique identifier for the Pokémon, corresponding to their National Dex number.
- `identifier`: The name of the Pokémon (e.g., Bulbasaur, not used in this version).
- `generation_id`: The generation in which the Pokémon was introduced (e.g., 1 for Generation I).
- `evolves_from_species_id`: ID of the Pokémon from which this species evolves, if applicable.
- `evolution_chain_id`: Identifier for the evolution chain to which this species belongs.
- `capture_rate`: Base rate determining how easy it is to capture this Pokémon.
- `is_baby`: Boolean indicating if the species is a baby Pokémon (not used in this version).
- `has_gender_differences`: Boolean indicating if there are visual differences between genders (not used in this version).
- `mega_evolution`: Boolean indicating if the species has a Mega Evolution (not used in this version).
- `is_legendary`: Boolean indicating if the species is considered Legendary (not used in this version).
- `is_mythical`: Boolean indicating if the species is classified as Mythical (not used in this version).
- `order`: Numerical order of the Pokémon in the National Pokédex, including regional or alternate forms.

## 4. pokemon_types.csv

For indicate each Pokémon's types in the same column, even for Pokémon with two types.

### Fields Description

- `pokemon_id`: Unique identifier for the Pokémon, corresponding to their National Dex number.
- `type_id`: Id for the Pokémon's types.
- `slot`: Indicate if is the main or the second Pokémon's type (in case of has two).

## 5. type_efficacy.csv

For calculate the damage between all Pokémon´s types.

### Fields Description

- `damage_type_id`: Pokémon's type that inflicts damage.
- `target_type_id`: Pokémon's type that recive damage.
- `damage_factor`: Percentage of attack effectiveness.

## 6. types_names.csv

Indicate type names, for join with the pokemon_types and type_efficacy tables.

### Fields Description

- `type_id`: Unique identifier for the type.
- `local_languaje`: Languaje of the name, only in english for this project.
- `name`: Name of the type.

# Joins

![Alt text](https://github.com/TalexJuarezProject/Tableau-proyects/blob/main/Pokemon/Data/Schema_joins.png)

- `Pokemon.ID` *--* `pokedex_description.ID`
- `Pokemon.ID` *--* `pokedex_species.id`
- `Pokemon.ID` *--* `pokedex_types.pokemon_id`
- `pokedex_species.evolves_from_species_id` *--* `evo_from_second.id`
- `pokedex_species.evolves_from_species_id` *--* `evo_to_second.evolves_from_species_id`
- `pokemon_types.type_id` *--* `type_efficacy.target_type_id`

#### Logic table "pokedex_species" formed for 3 tables
For add Pokémon, Evolves to and Evolves from in the same row. This complete the evolution chain for chains of only one, two, or Pokémon in the middle of chains of three Pokemón.

![Alt text](https://github.com/TalexJuarezProject/Tableau-proyects/blob/main/Pokemon/Data/Schema_ev_from_to.png)

- `pokedex_species.evolves_from_species_id` *--* `pokedex_species.id` (for calculate "Evolves from")
- `pokedex_species.id` *--* `pokedex_species.evolves_from_species_id` (for calculate "Evolves to")


#### Logic table "evo from second" and logic table "evo to second"
For add the first and last evolution in chains of three Pokemón, inclusive for the firt and the last Pokémon in the chain.
- `pokedex_species.evolves_from_species_id` *--* `pokedex_species.id` (for calculate "Evolves from")
- `pokedex_species.id` *--* `pokedex_species.evolves_from_species_id` (for calculate "Evolves to")

The logic tables `pokemon_types` and `type_efficacy` have the natural join with `types_names`.


# Some calculated fields

- Damage

For the calculation of the damage received, considering the interaction between type inclusive when the pokemon who receives the damage has two types.

```
IF COUNTD([Name1])=1 
    THEN 
        AVG([Damage Factor (Type Efficacy.Csv1)])
    ELSE
        MIN([Damage Factor (Type Efficacy.Csv1)])*MAX([Damage Factor (Type Efficacy.Csv1)])/100
END
```


- Immune to, Resistant to, Super resistant to, Weak to, Super Weak to.

This calculated fiels are a simple clasification of the diferent attack effectiveness. E.g.:

```
IF [Damage]>25 AND [Damage]<100 THEN 1 ELSE 0 END
```

