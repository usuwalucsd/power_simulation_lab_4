# Simulation Lab 4: power and sample size planning

Fourth simulation lab for **PSYC 201A** (UC San Diego), accompanying the
sampling chapter of [Experimentology](https://experimentology.io/) (Ch. 10) and
the sample size planning practicum. In Lab 2 you built power curves for an
effect you chose yourself. Here you will see what goes wrong when you have to
guess that effect, and then write the sample size justification for your own
project. When you are done you will have:

- Computed power and required sample size with the `pwr` package, and checked
  the formulas against simulation
- Seen how publication bias inflates published effects, and what that does to a
  replication powered on them
- Seen why a small pilot can't tell you your effect size
- Tested the "2.5 × the original sample" rule for replications (small telescopes)
- Run a sensitivity analysis for a fixed sample, and written a justification
  whose numbers come from your code
- Explored the trade-off between more people and more trials
- Computed effect sizes from raw data and from the statistics a paper reports,
  and seen how uncertain a single study's effect size is
- Made a power curve and a sample size justification for your project

The running example is the tea experiment from Labs 2 and 3, until Part 3, when
we move to a plain two-group study so that effects are in units of Cohen's d.

> **Before you start:** finish
> [Simulation Lab 2](https://github.com/psyc-201/inference_simulations_lab_2) and
> [Simulation Lab 3](https://github.com/psyc-201/reliability_simulation_exercises).
> This lab needs the tidyverse and one new package, `pwr`. The optional bonus
> also uses `lme4`, `lmerTest`, and `simr`.

---

## Part 1. Make your own copy

Same steps as in getting-started-with-r:

1. At the top of [this repository's GitHub page](https://github.com/psyc-201/power_simulation_lab_4),
   click the green **Use this template** button, then **Create a new repository**.
2. Owner: **your own account**. Name it `power_simulation_lab_4`, leave
   it **Public**, and click **Create repository**.
3. On *your* copy, click **Code** → **Open with GitHub Desktop** → **Clone**.

Step-by-step version:
[github-desktop.md](https://github.com/psyc-201/getting-started-with-r/blob/main/docs/github-desktop.md).

## Part 2. Open the project

**Double-click `power_simulation_lab_4.Rproj`** to open RStudio inside the
project, then open `ch10_power_simulations.qmd` from the Files pane and put your
name in the `author:` line. Run `install.packages("pwr")` once.

## Part 3. Work through the lab

Run one chunk at a time with the green arrow, top to bottom. Later parts use
functions defined in Parts 2 and 3, so run those chunks first. Fill in each
`___`.

| Part | What you do |
|---|---|
| 1. Probing your intuitions | Guess the power of five studies, then check with `pwr` |
| 2. Same answer, two ways | Compare `pwr` to simulation |
| 3. The published effect | Simulate a biased literature, then power replications on it |
| 4. The pilot | Write your own simulation of powering on a pilot |
| 5. Small telescopes | Find d33 and test the 2.5× rule |
| 6. Fixed samples | Sensitivity analysis, smallest effect of interest, and a justification paragraph |
| 7. People or trials | Trade participants for trials on a fixed budget |
| 8. Getting an effect size | Cohen's d by hand, d_z vs. d_av, converting reported statistics, and a CI on d |
| 9. Your project | Power analysis, power curve, and justification for your study |
| Bonus | Power for a mixed model by simulation, by hand and with `simr` (optional) |

**Short on time?** Do Parts 1, 3, 6, and 9, plus Part 8 if your paper doesn't
report an effect size. Run the chunks in Part 2 that define the functions
first, because Parts 3 and 8 use them. Two of the options in Part 9 build on
parts you'd skip: safeguard power uses `d_ci()` from Part 8d, and the 2.5×
rule comes from Part 5.

`error: true` is set at the top of the file, so **Render works even while
chunks are unfinished**: the unfinished chunks show their error in red.

`ch10_power_simulations_solutions.qmd` is the answer key. Try each part first.

## Part 4. Commit, push, and submit

Commit as you go. When you are finished, render once more, commit with a
message like `Finish power lab`, **Push origin**, and submit your repository
link on Canvas with your Part 9 power curve figure and paragraph (the end of
Part 9 says how to save the figure). Rendered `.html` files are ignored by
git, so only your `.qmd` is pushed. Your Part 9 paragraph goes into the Power
Analysis section of your own project report.

## What is in this repository

```
power_simulation_lab_4/
├── power_simulation_lab_4.Rproj          open this to start work
├── ch10_power_simulations.qmd            the lab
└── ch10_power_simulations_solutions.qmd  answer key
```

There is no `data/` folder: you make all the data yourself.

## Stuck?

1. **Setup errors** (package not found, RStudio not in the project): see
   [troubleshooting.md](https://github.com/psyc-201/getting-started-with-r/blob/main/docs/troubleshooting.md).
2. **`could not find function "pwr.t.test"`:** run `install.packages("pwr")`
   once, then run the `library()` chunk.
3. **Your required N looks half as big as it should:** `n` in `pwr.t.test()` is
   per group. Multiply by two for the total.
4. **`could not find function "simulate_study"`** (or `n_for_80`,
   `estimate_power`, `make_tea_data`): run the chunks in Parts 2 and 3 that define them.
5. **`uniroot` error from `pwr.t.test()`:** the effect size is at or very near
   zero, so no sample size can reach your target power.
6. **Your numbers differ from the solutions:** expected, unless you render from
   scratch. Every rerun of a chunk draws new random numbers.
7. **Some chunks are slow.** Let them finish.
8. Still stuck? Post the **exact** error message in the course forum.

## Resources

- [Experimentology, Ch. 10: Sampling](https://experimentology.io/): the course textbook
- [`pwr` package documentation](https://cran.r-project.org/package=pwr)
- [G\*Power](https://www.psychologie.hhu.de/arbeitsgruppen/allgemeine-psychologie-und-arbeitspsychologie/gpower): the point-and-click version
- Lakens, D. (2022). [Sample size justification](https://doi.org/10.1525/collabra.33267). *Collabra: Psychology*.
