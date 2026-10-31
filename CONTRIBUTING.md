# Contributing

Thank you for helping improve Altdown.

## Kinds of change

The specification says the format is small on purpose: later versions should clarify the text,
not add to the format. Proposals are handled with that in mind.

| Kind | Example | Where it goes |
| --- | --- | --- |
| Editorial | A typo, an unclear sentence, a broken link | Pull request against the current draft, merged by the editor |
| Clarification | A rule that two readers interpret differently | Issue first, then a pull request once the meaning is agreed |
| New capability | A new front matter field or index member | An `x-` field or `_` member first, as described under "Extending Altdown". Promotion into the specification is considered only after real use |

## How to propose a change

1. Check the open issues and discussions for the same topic.
2. Open an issue that quotes the section you are discussing and says what you expect it to say.
3. For wording changes, open a pull request that edits `spec/<version>.md` directly. Keep each pull request to one topic.

## Versions

- A draft may change in any way until it is marked final.
- A final version is frozen. Its file is not edited again, except to fix typos that do not change meaning.
- Each change that ships is listed in [CHANGELOG.md](CHANGELOG.md).

## License of contributions

By contributing, you agree that your contribution is published under the same license as the
specification, [CC BY-SA 4.0](LICENSE).
