# pallor

pallor is yet another syntax highlighting color scheme. Why another color scheme? Because color schemes are *really really* subjective and eventually I'm sure everyone tries to make their own (unless they find one that they think is perfect already). This is my attempt to do so. After some amount of messing around with other schemes, I now use pallor exclusively.

Several samples are shown in [SAMPLES.md](SAMPLES.md), but here's a good one from C, which is basically my number one priority for any theme.
![C](samples/C.png)

## Design

pallor is a dark low-constrast color scheme with an especially pale background (`#383838`). In this regard, it is heavily derivative of [zenburn](http://slinky.imukuppi.org/zenburnpage/). If you like zenburn's "alien fruit salad" feel, you might also find pallor appealing. Where zenburn has a lot of yellows and oranges, I generally prefer a lot of blues and greens, so pallor's look is slightly cooler in temperature. See [COLORS.md](COLORS.md) for more details on the pallor colors.

pallor aims for as few colors as possible (as of writing, there are only five non-gray foreground colors). This ensures that the colors are easy to distinguish. One of the things I didn't like about zenburn was that there were a lot of colors that were really similar. If they weren't side by side, I wouldn't have been able to tell them apart, so the distinction between them became meaningless. pallor tries to make this a complete non-issue.

It makes as little use of bold/italic as possible, since your preferred font might not have that face (especially bitmap fonts). It also makes minimal use of background coloring - this type of highlighting stands out in the extreme and I think it should be used *very* sparingly. As of writing, the only scope that uses background highlighting is `invalid`.

## How to use

If you use an editor that is compatible with TextMate's `.tmTheme` format, just drop [pallor.tmTheme](pallor.tmTheme) into your editor. Unfortunately, I don't have any other syntax highlighting formats; ports are welcome.

If you want to edit pallor's colors, the basic process is simple. Edit [colors.json](colors.json) to change the colors you don't like. You can add new highlight colors under the `colors` object, and then refer to them in the various keys below (each key corresponds to a group of scopes in the template). This lets you define a color once and refer to it many times. The values above the `colors` object tend to only get used once (various shades of gray, and special background highlights), so they aren't bound to any convenient names.

Make sure that all the keys correspond to valid values (including the name and uuid). If they don't then `<no value>` will be left in their place, and the angle brackets will give an XML parsing error. Then use [jgtr](https://github.com/tummychow/jgtr) to compile the template like so:

```bash
$ jgtr -t pallor.tmTheme.tmpl.plist -d colors.json -o pallor.tmTheme
```

If you want to edit pallor's structure (ie what color corresponds to what scopes), you'll need to edit the raw plist (which is an awful experience), or acquire a means of converting json to plist. I use [SerializedDataConverter](https://github.com/facelessuser/SerializedDataConverter). You'll want to work with either [pallor.tmTheme.tmpl.plist](pallor.tmTheme.tmpl.plist) or [pallor.tmTheme.tmpl.json](pallor.tmTheme.tmpl.json). Once you've edited the plist to your heart's content (or edited the JSON and converted it back to plist), invoke jgtr as above to generate the new theme.

I use [pandoc](http://johnmacfarlane.net/pandoc) to write stuff, so I've also included an experimental [CSS file](pandoc.css) for highlighting pandoc-generated HTML. A [template](pandoc.tmpl.css) is also provided, so you can regenerate the CSS after changing the colors. I haven't tested this, so let me know if stuff doesn't work. I also have a [CSS file](coderay.css) for CodeRay-generated HTML with optional table-based line numbers (which I use in [lannoc](https://github.com/tummychow/lannoc)), and a matching [template](coderay.tmpl.css).

## Languages and scopes

pallor has first-class support for a handful of TextMate grammars: [C Improved](https://github.com/abusalimov/SublimeCImproved), [GoSublime](https://github.com/DisposaBoy/GoSublime) and [Markdown Extended](https://github.com/jonschlinkert/sublime-markdown-extended). Those happen to be the languages I use, so I care a lot about supporting them. (Notice how none of those grammars are TextMate defaults, they're all improved in some way.)

I also have some behavior specialized for the standard TextMate JSON grammar, so that keys are highlighted differently from values. See the [credits](#credits) for where I got the idea for JSON, it's a real hell of a hack. I'm particularly concerned about its stability, so if your JSON is coming out all blue, you should open an issue ASAP. Right now I think it goes 7 or 8 nested objects deep, which is good enough for me. Honestly the problem is with the TextMate JSON grammar, but I can't be bothered to learn and fix that right now.

If highlighting is less granular than you'd like in a language that you use, PRs are welcome. If highlighting is BORKED in a language (ie this element falls under this group of stuff, yet it's being highlighted under a different group), issues are *strongly* encouraged. I care about my theme breaking stuff - who knows, someday I'll be programming in that language. However, the problem might be with the TextMate grammar, and not with pallor. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Credits

zenburn for being the best theme I've ever seen (that wasn't written by myself). If I couldn't write my own, I'd use this for the rest of my life and never look back. (Runner-up: Tomorrow Night Eighties.) Many of the colors in pallor are taken straight out of zenburn (and rounded off to be divisible by 8 because yay pretty numbers).

[base16](https://github.com/chriskempson/base16) for the idea of using templates to build themes. This lets you separate colors from the scopes they apply to. In fact, the base16-builder script was what inspired me to write jgtr.

[Neon](https://github.com/MattDMo/Neon-color-scheme) for a lot of the scopes used in pallor, particularly the [hack](https://github.com/MattDMo/Neon-color-scheme/blob/master/Neon.tmTheme#L1139) to highlight JSON keys. Since TextMate grammars can define arbitrary scopes, the burden is on theme maintainers to include support to highlight those scopes, so thanks for taking away a lot of the grunt work in finding out what scopes I cared about.

## License

MIT/expat, see [LICENSE.md](LICENSE.md).
