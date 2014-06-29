## @konklone's git precommit hook

Catches the slug `DONTCOMMIT` in any `git diff` before I commit something, and then aborts the commit until I resolve it or use `git commit --no-verify`.

For example, if I add this to a Python script:

```python
# DONTCOMMIT
print("Intentionally crashing the script...")
raise Exception("What happens when I crash it")
```

And then I forget I added it, and try to commit these lines, this pre-commit hook will *SAVE THE DAY* and print out:

```bash
$ git commit -m "I hope you stop me from comitting this"
Error: git pre-commit hook forbids committing "DONTCOMMIT" to myscript.py
--------------
To commit anyway, use --no-verify
```

And I will have a second chance at life.

### Using it

Run this for each repo you want to set up the hook:

```bash
./setup.sh /path/to/repo
```

Bear in mind this sets up a **symlink**, so any changes you make to this repo will get made to all repos you've run this script for.

You

### Credits

This is forked from [bobgilmore/githooks](https://github.com/bobgilmore/githooks), who has a much more sophisticated setup than I.

Thanks to [Magnus Holm](https://twitter.com/judofyr) for [suggesting](https://twitter.com/judofyr/status/483321849435389952) I do this.

### License

The comments in [bobgilmore/githooks](https://github.com/bobgilmore/githooks) indicate that work is forked in turn from Henrik Nyh under the MIT License, so mine is [licensed as MIT](LICENSE) as well. If you contribute, you [agree](CONTRIBUTING.md) to license your contributions under the same license.
