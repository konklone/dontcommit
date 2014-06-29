## @konklone's git precommit hook

Catches the slug `DONTCOMMIT` in any `git diff` before I commit something, and then aborts the commit until I resolve it or use `git commit --no-verify`.

### Credits

This is forked from [bobgilmore/githooks](https://github.com/bobgilmore/githooks), who has a much more sophisticated setup than I.

Thanks to [Magnus Holm](https://twitter.com/judofyr) for [suggesting](https://twitter.com/judofyr/status/483321849435389952) I do this.

### License

The comments in [bobgilmore/githooks](https://github.com/bobgilmore/githooks) indicate that work is forked in turn from Henrik Nyh under the MIT License, so mine is [licensed as MIT](LICENSE) as well. If you contribute, you [agree](CONTRIBUTING.md) to license your contributions under the same license.
