# watson-assistant-workbench
WAW is a toolkit for maintaining Watson Assistant data in github repository.
It aims at
- structured data-driven approach, with easy diffs visible in GitHub
- easy collaboration among large teams
- improved dialog tree representation resulting in greater readability and easier updates compared to the original WA JSON format
- easy-to-use XML format and tools that make authoring of Watson Conversation workspaces easier using standard text editors
- ability to easily include and combine pieces of dialog together
- full compatibility with the WA JSON workspace format
- easy Continuous Integration - each commit to GitHub runs tests and updates conversation workspace if all succeed
- automatic dialog code generation (go back, abort, etc. - actions needed in each dialog step)
- support for internationalization
- and more :)

It contains a bundle of tools for generating WA workspace from the structure data (and viceversa), testing and uploading (working with the WCS API).

Currently supported conversation version is 2017-02-03 except:
- Fuzzy matching, Folders and Digression are not supported.
- A name of a dialog node still has to be unique as it is used as node ID.
- Missing "slot_in_focus" property.
- Slots are not supported in json to xml conversion scripts.

Scripts use python 3.5, used modules are listed in the [requirements.txt](/requirements.txt) file. To satisfy all requirements run
```
pip install -r requirements.txt
```
For brief summary how to run scripts please see [scripts.md](/scripts.md).

Description of T2C  and xml/csv WAW formats can be found in `doc` folder.

Release notes can be found in [release_notes.md](/release_notes.md).

Instructions on how to use logging can be found in [logging.md](/logging.md).

If you want to run unit tests locally, you first need to install development dependencies from [requirements_dev.txt](/requirements_dev.txt). You can run
```
pip install -r requirements_dev.txt
```

Then set following environment variables
(i.e. run `export VARIABLE_NAME="VARIABLE_VALUE"`)
- `WA_USERNAME` (Watson Assistant username - ALWAYS USE INSTANCE DEDICATED FOR TESTING ONLY! ALL CONTENT WILL BE DELETED DURING TESTING PROCESS!)
- `WA_PASSWORD` (Watson Assistant password)
- `CLOUD_FUNCTIONS_USERNAME` (Cloud Functions username)
- `CLOUD_FUNCTIONS_PASSWORD` (Cloud Functions password)
- `CLOUD_FUNCTIONS_URL` (Cloud Functions namespace - it should contain `https://` at the beginning and `/api/v1/namespaces` at the end)
- `CLOUD_FUNCTIONS_NAMESPACE` (Cloud Functions namespace - don't forget enclosing it in apostrophes if it contains spaces)

The unit tests and app tests can be started with these commands (from the top directory of this repository)
```
PYTHONPATH=./scripts:$PYTHONPATH pytest ci/unit_tests
PYTHONPATH=./scripts:$PYTHONPATH pytest ci/app_tests
```
