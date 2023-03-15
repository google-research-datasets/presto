# PRESTO

*PRESTO: A Multilingual Dataset for Parsing Realistic Task-Oriented Dialogs*

## Introduction

PRESTO is a dataset of over 550K contextual multilingual conversations between humans and virtual assistants. PRESTO contains a diverse array of challenges that occur in real-world NLU tasks such as disfluencies, code-switching, and revisions. It is the only large-scale human generated conversational parsing dataset that provides structured context such as a user's contacts and lists for each example.

The dataset can be downloaded [here](https://storage.googleapis.com/gresearch/presto/presto_v1.zip). This README documents the dataset structure and other important information about the dataset.

## Dataset Structure

PRESTO is published with the following files:
```
├── presto_dataset.jsonl
├── presto_dev.jsonl
├── presto_test.jsonl
├── presto_train.jsonl
└── test_partitions
    ├── de-DE
    │   ├── de-DE_code-mixing
    │   │   └── test.jsonl
    │   ├── de-DE_disfluency
    │   │   └── test.jsonl
    │   ├── de-DE_non_contextual
    │   │   └── test.jsonl
    │   ├── de-DE_no_phenomena
    │   │   └── test.jsonl
    │   ├── de-DE_revisions
    │   │   └── test.jsonl
    │   └── test.jsonl
    ... (more languages)
```

`presto_dataset.jsonl` contains all examples in the dataset. The provided train, dev, and test sets are those used in the paper. Each test partition contains a subset of the examples from the full test set.

Each JSONL file contains a list of examples. An example has the following fields:
- `inputs`: The last utterance in the user's conversation with the virtual assistant. E.g. `Make a movie list`.
- `targets`: The annotated semantic parse of the user's utterance. E.g. `Create_list ( label « movie » )`.
- `metadata`: An object with the following fields:
  - `example_id`: A unique identifier for the example.
  - `locale`: The locale of the conversation. E.g. `en-US`.
  - `split`: The split of the example. One of `train`, `dev`, or `test`.
  - `context`: Whether the example's context was present in the original conversation or added synthetically. One of `human` or `synthetic`.
  - `linguistic_phenomena`: The linguistic phenomenon associated with the example. E.g. `disfluency`. If the example is not associated with any labeled phenomenon, this field is the empty string.
  - `previous_turns`: A list of the previous turns in the conversation, chronologically ordered. Each turn is an object with the following fields:
    - `user_query`: The user's utterance in the turn. E.g. `Add an item to my shopping list`.
    - `response_text`: The virtual assistant's response to the user's utterance. E.g. `What do you want to add?`.
  - `seeded_lists`: A list of the lists present in the user's virtual environment. Each list is an object has the following fields:
    - `name`: The name of the list. E.g. `Shopping`.
    - `items`: A list of the items in the list. E.g. `["milk", "eggs", "bread"]`.
  - `seeded_notes`: A list of the notes present in the user's virtual environment. Each note is an object has the following fields:
    - `name`: The name of the note. E.g. `Workout routine`.
    - `text`: The text of the note. E.g. `10 pushups, 10 situps, 10 squats`.
  - `seeded_contacts`: A list of the contacts present in the user's virtual environment. Each contact is a string containing the name of the contact. E.g. `["John Doe", "Jane Doe"]`.

## Citation

If you use this dataset, please cite the following paper:

```
[Coming soon]
```

## License

PRESTO is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
