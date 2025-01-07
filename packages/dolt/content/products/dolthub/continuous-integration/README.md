# DoltHub/DoltLab Continuous Integration (CI)

DoltHub and DoltLab support continuous integration (CI) testing which allow you to validate changes before you commit them on your primary branch.&#x20;

Continuous integration (CI) testing originated as a software development best practice where automated tests run against incoming code changes pushed by software developers who are collaborating on a code repository. 

If a developer pushes changes that fail to pass the automated tests, the proposed changes are rejected. This practice ensures that only valid, high quality changes get committed on the primary build branch, resulting in fewer bugs, and higher developer productivity.

Dolt's revolutionary technology that marries Git and MySql now allows for CI testing on data and is supported on both DoltHub and DoltLab. In the same way the proposed code changes undergo automated tests to ensure they're valid, proposed data changes on a DoltHub or DoltLab database can also undergo automated tests to assert their validity.

The following sections will introduce you to how CI works with Dolt, DoltHub and DoltLab and help you setup CI testing for your own databases.

# CI starts with Dolt

CI configuration for a DoltHub or DoltLab database is stored in the database itself. At the time of this writing, in order to add CI configuration to a DoltHub or DoltLab database, you will need to have a local Dolt client version >= [v1.46.0]() and will have to clone a copy of the the database. In order to configure CI on the database, you will use Dolt's CI CLI commands.

## Dolt CI Commands

The primary interface for creating and editing CI configuration in a Dolt database is via the `dolt ci` CLI command. These commands aim to simplify CI configuration in Dolt, so that users do not need to manually interact with the underlying CI tables directly. They provide the ability to create, read, edit, and delete CI configuration the Dolt calls _workflows_.

The `dolt ci` commands as of Dolt v1.46.0 are:

- [dolt ci init](). This command creates internal database tables used to store continuous integration configuration.
- [dolt ci destroy](). This command drops all database tables used to store continuous integration configuration.
- [dolt ci import](). This command will import a Dolt continuous integration workflow file into the database.
- [dolt ci export](). This command will export a Dolt continuous integration workflow by name.
- [dolt ci ls](). This command lists existing Dolt continuous integration workflows by name.
- [dolt ci remove](). This command removes a Dolt continuous integration workflow by name.

## Workflows
