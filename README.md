# Diataxis

[Vale](https://vale.sh) styles for the four kinds of documentation in
[Diátaxis](https://diataxis.fr): tutorials, how-to guides, reference, and
explanation. Each kind has its own rules, drawn from what the framework says
each one is for, so a page is checked against the job it claims to do.

The framework's central claim is that the four kinds fail when they mix: a
tutorial that explains, a how-to guide that teaches, reference that advises,
explanation that instructs. The rules look for exactly those slips.

## Install

Requires Vale 3.23.0 or later.

Vale doesn't know which kind a page is, so the config says, one folder per
kind, which is how Diátaxis-shaped documentation is usually laid out:

```ini
StylesPath = styles
Packages = https://github.com/jdkato/diataxis/releases/latest/download/Diataxis.zip

[tutorials/*.md]
BasedOnStyles = Tutorial

[how-to/*.md]
BasedOnStyles = HowTo

[reference/*.md]
BasedOnStyles = Reference

[explanation/*.md]
BasedOnStyles = Explanation
```

```console
$ vale sync
```

| Style | The page is for | What it checks |
| ----- | --------------- | -------------- |
| `Tutorial` | Learning by doing | Opens by saying what the learner will build, and says "we". Numbered steps. No choices offered, no explanation of why, and the learner is told what they will see. |
| `HowTo` | Reaching a goal | Named for the goal, "How to ..." or "Deploying ...", and opens by saying what it shows. Numbered steps written as commands. No teaching, no explaining, and the full list of options left to the reference. |
| `Reference` | Looking something up | Describes without advising: no "you should", no "we recommend"; a warning, "you must not", is allowed. Neutral: no "simply", "unfortunately", "obviously". States rather than narrates, and shows at least one example. |
| `Explanation` | Understanding | Answers why somewhere. No steps to run, and no tables of every option, which are reference. |

Every rule file starts with a comment saying what it checks and links to
the page of the framework it follows.

## Tuning

Levels and limits are settings:

```ini
[explanation/*.md]
BasedOnStyles = Explanation
Explanation.Reference[max] = 12
Tutorial.Options = suggestion
```

## Development

`./test.sh` runs each rule's own cases with `vale test --coverage`, then
checks one page per kind in `fixtures/` against the golden files in
`testdata/` and requires the rewrites in `fixtures/clean/` to pass clean.
`./test.sh -u` rewrites the golden files.

## License

MIT. The rules follow Diátaxis, by Daniele Procida, published under CC
BY-SA 4.0; see [NOTICE](NOTICE).
