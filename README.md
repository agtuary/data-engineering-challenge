# Introduction

For this task, the goal is to match up property sales data, with property geographic data. As these datasets come from different sources, the main way properties are defined and identified is through a legal number/identifier, commonly known as lot and plan (in most states of Australia). The one thing to note with handling this type of data, is that there are no certainties and there are always edge cases to deal with. There are no rules that are 100% set in stone.

In NSW, the identifier is in the following format: `lot/plan`. The way this **mostly** maps to the real world, is a `lot` is a subsection of a `plan`, however the `plan` is the main, singular block of land that is **mostly** mapped to ownership (but not always). Think of a house, this will almost always be a single lot and plan (such as `1/3435456`). If you think about a townhouse, or maybe a commercial block of land that has been split up, it will be a single plan, but multiple lots (such as `3/5439857`, `5/5439857` and so on).

These `lot/plan` can also have additional characters in the, leading to different types/forms of identifiers for either the lot, plan, or both. The following is some of them:

- `3//4537834` (double slashes)
- `3\4537834` (backslash)
- `5/DP453836` (`DP` infront of the plan)
- `5/SP453836` (`SP` infront of the plan)
- `/DP483957` (no lot)
- `1~3/4698304` (alternative form of a lot)
- `1~3//DP456472` (example of multiple differences in one)

`lot/plan`'s can have one or more of the above, at the same time, which makes the parsing problem difficult. The sales dataset and parcels dataset (geographic information) contain columns that both include these `lot/plan`, however sometimes they don't match up just perfectly. In one dataset, you might have `1/DP495945` while in the other you have `1//DP495945` (extra slash). You may also have duplicate rows.

# Task

Match up the sales dataset with the parcels data, by using the `lot/plan` id's. You must write code that will do this automatically, while taking into account the above different types of `lot/plan`s (such as with multiple slashes, etc), producing a resulting json file. The resulting file must have he following structure:

```json
{
    "sales": [
        {
            "row_index": (index of sale row),
            "sale_raw": (dictionary of sale row data),
            "dealing_number": (value from dealing number column),
            "sale_price": (value from price column),
            "contract_date": (value from contract date column),
            "parcels": [
                {
                    "row_index": (index of parcel row),
                    "id": (value from id column),
                    "parcel_raw": (dictionary of parcel row data)
                }
            ]
        },
        ...
    ]
}
```

**Your code will be checked and ran against the entirety of the sales dataset, to check for completeness and robustness.**

Send the resulting code file (either .py or .ipynb) as well as the final json file to matthew@agtuary.com