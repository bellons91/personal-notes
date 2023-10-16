---
tags: git, dotnet
---

# How to Use Husky.NET Pre-commit hooks

If you need to run operations before completing a Git Commit, you must rely on Git Hooks.

I've already described how to use [Husky with NPM](https://www.code4it.dev/blog/conventional-commit-with-githooks/), but here I'm gonna use [Husky.NET](https://alirezanet.github.io/Husky.Net/), the version of Husky created for .NET applications.

## Install the tool

The tool must be installed in the root folder of the solution.

To install the tool globally, you have to run

```cmd
dotnet new tool-manifest
dotnet tool install Husky
```

and, to add it to an existing .NET application, you must run

```cmd
dotnet husky install
```

Finally, you can add a new hook by running, for example,

```cmd
dotnet husky add pre-commit -c "echo 'Husky.Net is awesome!'"
git add .husky/pre-commit
```

This fill create a new file, _pre-commit_, in your project. The content, here, is pretty useless: you should customize that script.

## Create custom scripts

To customize the script, open the file located at `.husky/pre-commit` (the file has no extensions).

Here you can add whatever you want.

My personal file just compiles the code, formats the text (using `dotnet format` with the rules defined in the .editorconfig file), and then runs all the tests.

```cmd
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

echo 'Building code'
dotnet build

echo 'Formatting code'
dotnet format
git add .

echo 'Running tests'
dotnet test
```

Then, add it to Git, and you are ready to go.

## Skip git hooks

To trigger the hook, just run `git commit -m "message"`. **Before** completing the commit, the hook will run all the commands. **If one of them fails, the whole commit operation is aborted**.

There are cases when you have to skip the validation. For example, if you have integration tests that rely on an external source that is currently offline. In that case, some tests will fail, and you won't be able to commit your code until the external system comes back.

You can skip the commit validation by adding the `--no-verify` flag:

```cmd
git commit -m "my message" --no-verify
```

## Related notes

[[how-to-use-editorconfig]]

## External references

🔗 [Husky.Net](https://alirezanet.github.io/Husky.Net/)
