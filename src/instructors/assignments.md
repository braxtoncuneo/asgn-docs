# Managing Assignments

## Controlling Assignment Accessibility/Visibility

The accessibility of an assignment can be changed via the **`enable`** and **`disable`** sub-commands:

![](./img/enable.png)

Likewise, whether or not an assignment is visible in the course's summary can be changed via the **`publish`** and **`unpublish`** sub-commands:

![](./img/publish.png)

Of course, these properties may also be directly changed by changing the respective assignment's **`info.toml`** files.

## Setting Open/Close/Due Dates

The due/open/close dates of an assignment can be set through the **`set_due`**/**`set_open`**/**`set_close`** sub-commands.
These sub-commands can accept a date in **`yyyy-mm-dd`** format, with the submission time defaulting to **`23:59:59`**, or an explicit time-of-day may be established with the longer **`yyyy-mm-ddThh-mm-ss`** format.

![](./img/dates.png)


## Score Updates

The scores publicly displayed to members of a course may only be evaluated by the course's instructor.
This is done to reduce the possibility of tampering, if competition gets heated.

To evaluate and update the scores of a particular assignment, use the **`update_scores`** sub-command.
To update all scores across all assignments, there is the **`update_all_scores`**.
Only submissions made after the most recent score update get re-evaluated by the next score update.
If students wish to "re-roll" their score, in cases of randomization, they would need to re-submit the assignment.

To prevent rounding errors from causing repeated re-evaluations of the same submission, any submissions made within 1 second of a previously evaluated submission (for the same student) are not considered for re-evaluation.
Of course, outside of agressive "re-rolling", this is not likely to be relevant.


## Automating Score Updates

If you plan to use scores heavily in your course, you and your students will likely desire quick feedback between someone running the `submit` sub-command and seeing an update in the published rankings.

Out of the box, `asgn` does not provide automated ranking updates.
However, you can easily establish ranking updates with `crontab`.

To do so, open your `crontab` file with this command:

```console
crontab -e
```

Once it has been opened, add in the appropriate `update_ranks`/`update_all_ranks` command, prepended with an appropriate periodicity [according to the `cron` format](https://www.man7.org/linux/man-pages/man5/crontab.5.html).
Here's an example `crontab` file snippet, with two different periodic ranking updates:

```
# Update all rankings on an hourly basis, appending stdout/stderr to a log file
0 * * * * my_course update_all_scores &>> ~/ranking_log
# Update the rankings of assignment "hackathon" on a minute-by-minute basis, but don't log any output
* * * * * my_course update_scores hackathon
```

If you plan on accumulating logs from score updates, keep in mind that quite a bit of text can accumulate over time.
If you only care about recent log messages, consider adding another cron job that clears the log at the start of each day.

