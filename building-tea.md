## Learn TypeScript

Hint: It's JavaScript in disguise.

- [Cheatsheets](https://www.typescriptlang.org/cheatsheets)
- [Docs](https://www.typescriptlang.org/docs/)
- [Handbooks](https://www.typescriptlang.org/docs/handbook/intro.html)

`console.log()` instead of `print()`. It's your BFF.

## Learn Deno

- [Manual](https://deno.land/manual)

## Compile tea

Install tea if you haven't already.

If you want to contribute, then fork [tea.xyz/cli](https://github.com/tea.xyz/cli) and clone that instead of the original.

```
git clone https://github.com/tea.xyz/cli.git
tea -X deno compile --allow-read --allow-write --allow-net --allow-run --allow-env --unstable --import-map=./cli/import-map.json --output tea ./cli/src/app.ts
```
