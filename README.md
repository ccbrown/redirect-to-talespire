# redirect-to-talespire

This repo has a simple HTML redirect to TaleSpire for the purpose of using [TaleSpire dice URLs](https://bouncyrock.com/news/articles/talespire-update-dice-urls) where custom URI handlers aren't supported (namely [Google Sheets](https://support.google.com/docs/answer/3093313?hl=en)).

Opening up dice.html via a URL like this will redirect to TaleSpire:

> https://ccbrown.github.io/redirect-to-talespire/dice.html#Fireball:2d6

## Google Sheets

The best way to use this in Google Sheets is to create a [custom function](https://developers.google.com/apps-script/guides/sheets/functions) that assembles the URL:

```javascript
function DICEURL(dice, label) {
  if (label) {
    return "https://ccbrown.github.io/redirect-to-talespire/dice.html#" + encodeURIComponent(label) + ":" + dice;
  } else {
    return "https://ccbrown.github.io/redirect-to-talespire/dice.html#" + dice;
  }
}
```

Then you can use formulas like this in your cells:

```
=HYPERLINK(DICEURL("d20" & TEXT(AA20+AC20, "+0;-0;0"), "Initiative"), AA20+AC20)
```

To get started quickly, you can clone the [sheet here](https://docs.google.com/spreadsheets/d/14cHDNLSUFVO-MO70jnn3N_ESSs6flK8tZBKosK_FHu0/edit?usp=sharing).
