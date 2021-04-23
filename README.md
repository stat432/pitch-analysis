# Classifying MLB Pitches

This repository contains the files necessary to get started with the Classifying MLB Pitches data set created for analysis in STAT 432 at the University of Illinois at Urbana-Champaign.

## Files and Directories

- `README.md`: The file that you are reading that describes the analysis and data provided.
- `analysis.Rmd`: A **template** R Markdown file to be used for reporting the results of your analysis.
- `data/pitches_2019_regular_**.csv`: A dataset containing pitches with complete data from a particular month of the 2019 regular season.
- `data/pitches_2019_post.csv`: A dataset containing pitches with complete data from the 2019 post season.
- `pitches-analysis.Rproj`: An RStudio project file.

## Source and Documentation

The data stored in the `data` folder was scrapped using the [`baseballr`](https://billpetti.github.io/baseballr/) package written by [Bill Petti](https://billpetti.github.io/). This package allows for easy querying of [Statcast](https://en.wikipedia.org/wiki/Statcast) and [PITCH f/x](https://en.wikipedia.org/wiki/PITCHf/x) data as provided by [Baseball Savant](https://baseballsavant.mlb.com/).

- [Documentation: Statcast CSV Documentation](https://baseballsavant.mlb.com/csv-docs)
- [Documentation: MLB Pitch Types](http://m.mlb.com/glossary/pitch-types)

## Analysis Goal

The goal of this analysis is to create a pitch classifier. Want to see how well you would do as a human pitch classifier? Try this game:

- [MLB Guess The Pitch Game](https://baseballsavant.mlb.com/games/pitch-type-guess)

Unless you are a baseball expert, you will probably find it difficult to score well.

What determines a pitch type? Here is a primer on the various pitch types seen in Major League Baseball:

- [Identifying Pitch Types: A Fan's Guide](https://www.mlb.com/news/identifying-pitch-types-a-fan-s-guide)

What you'll notice is that what determines a pitch type is generally how the ball is gripped, and how the pitcher releases the ball from their hands. So the best way to determine pitch type would be to simply ask the pitcher! Without doing that, because that would take too much time and the game already moves too slowly, pitch type is generally inferred based on what the pitch looks like as it moves from the pitcher towards the batter, especially with respect to how fast, how much spin, and how much it moves left-to-right and up-and-down. Veteran baseball fans will be able to identify pitch type by simply observing the pitch, but even then, humans will make mistakes, and humans are a costly way to perform data entry.

Suppose instead that we could train a machine to detect pitch type. That's what we'll do! In the future, there will likely be deep learning computer vision approaches that can learn the pitch type by watching video of the games. But without using the raw video data, MLB already records a wealth of data on each pitch, through the use of

- [Statcast](https://en.wikipedia.org/wiki/Statcast)
- [PITCH f/x](https://en.wikipedia.org/wiki/PITCHf/x)

Essentially, we have access to data related to speed, spin, movement, and positioning of each pitch. See the documentation above. Our job is to create a data product that will take in this information, and read out a pitch type. This could be used to:

- Automatically record pitch types
- Verify and augment human labeled pitch types
- Fill in missing pitch type data

In other words, this could be a helpful tool in a larger data pipeline used by baseball organizations. You might even notice that while watching an MLB game, that the pitch type is shown on the broadcast immediately after the pitch is thrown. This suggests they already have this sort of pipeline developed.

## Additional Context

Why would we want to do this? You might realize that there isn't much to gain from knowing pitch types during a game. (That is, unless you knew them ahead of time.) But, baseball is an incredibly data-driven sport. Many teams have large analytics divisions. If nothing else, having good pitch type data will help with future analyses. So in some sense, we are doing a data analysis to ensure data quality for future analyses. As an aside, the baseball analytics world contains several Illini alumni including:

- [Ehsan Bokhari](https://www.mlb.com/astros/team/front-office/ehsan-bokhari) - Formerly a visiting professor with the Statistics department who shared an office with David and was a part of the original conversations leading to the creation of STAT 432.
- [Charlie Young](https://stat.illinois.edu/news/2020-05-14/deck-charlie-young-statistics-major-heads-major-leagues) - A former STAT 432 student!

You are given a large number of variables to consider, but also note that more are available in the raw data. Something to keep in mind is that not all variables available to you are appropriate to use, or at least your should consider if they are relevant. For example, the date of the game probably should not influence the type of pitch. And even it was shown to be predictive, we should be suspicious of this. We don't expect you to have full understanding of baseball and be able to determine the appropriateness of each variable, but we'd like you to give this some thought.

Two datasets are available to you:

- `data/pitches_2019_regular.csv`: A dataset containing pitches with complete data from the 2020 regular season. (This dataset is created within the `analysis.Rmd` file.)
- `data/pitches_2019_post.csv`: A dataset containing pitches with complete data from the 2020 post season.

You might consider (but are not required to) think about using these datasets as follows:

- Use `pitches_2019_regular` as a training dataset.
- Use `pitches_2019_post` as a test dataset.

The `pitches_2020_missing` can be ignored if you like, but, consider using your resulting model to make predictions for these pitches that are missing a pitch type. How confident are you in your predictions?

## Additional Notes

Some modification to the possible pitch types was done during data processing. These were to mostly to remove extremely rare pitch types such as [knuckleballs](https://en.wikipedia.org/wiki/Knuckleball).

If you are interested in work with this type of data, you will be interested in resources such as:

- The [`baseballr`](https://billpetti.github.io/baseballr/) package
- [Baseball Savant](https://baseballsavant.mlb.com/)
- [Lahman Baseball Database](https://lahman.r-forge.r-project.org/)
