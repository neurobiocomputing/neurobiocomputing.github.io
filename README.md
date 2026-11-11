# NeuroBiological Computing 2027

Conference website for **4–6 October 2027**, built with
[jekyll-theme-conference](https://github.com/DigitaleGesellschaft/jekyll-theme-conference)
v5.1.0 and published with GitHub Pages.

The site includes a homepage, program, speakers, participation, venue and travel
pages, and a downloadable calendar event. Unconfirmed information is clearly
marked as **to be announced**.

## Publish on GitHub Pages

1. Commit and push these files to the `main` branch of
   `neurobiocomputing/neurobiocomputing.github.io`.
2. In the repository's **Settings → Pages → Build and deployment**, select
   **GitHub Actions** as the source.
3. The **Build and deploy GitHub Pages** workflow builds and publishes the site.
   If needed, run it manually from the **Actions** tab after enabling Pages.

The published address will be **https://neurobiocomputing.github.io/**.
Pull requests build the site for validation without deploying it.

## Preview locally with conda

Conda manages Ruby, and Bundler installs Jekyll and the conference theme from
the project's `Gemfile`. The instructions below use Windows and Anaconda.

### One-time setup

1. Open **Anaconda Prompt** and create a dedicated environment using
   [conda-forge's Ruby package](https://anaconda.org/conda-forge/ruby):

   ```bat
   conda create --name nbc2027 --channel conda-forge ruby=3.4
   ```

   If you already created `nbc2027`, reuse that environment.

2. Install [Microsoft C++ Build Tools](https://learn.microsoft.com/en-us/cpp/build/building-on-the-command-line).
   Select **Desktop development with C++**, including the **MSVC x64/x86 build
   tools** and a **Windows SDK**. Conda's Windows Ruby uses MSVC to compile
   native gems such as `bigdecimal`; the Ruby package alone does not provide
   this compiler setup.

3. Open **x64 Native Tools Command Prompt for VS** from the Start menu. This
   configures the compiler, headers, and libraries. Run the following commands
   in that prompt; these commands use **Command Prompt syntax**:

   ```bat
   call "%LOCALAPPDATA%\anaconda3\condabin\conda.bat" activate nbc2027
   cd /d "%USERPROFILE%\Documents\GitHub\neurobiocomputing.github.io"

   where ruby
   ruby --version
   where cl
   where nmake

   gem install bundler --version 2.5.22
   bundle install
   ```

   Adjust the Anaconda and repository paths if you installed them elsewhere.
   `where ruby` should list the `nbc2027` environment's Ruby first. Both
   `where cl` and `where nmake` should print paths to the Microsoft build tools.

### Start the preview

In the same activated **x64 Native Tools Command Prompt**, run:

```bat
bundle exec jekyll serve
```

Open **http://localhost:4000**. Jekyll rebuilds the site when source files change.
Press **Ctrl+C** to stop the server. Restart it after editing `_config.yml`.

For later sessions, reopen the x64 Native Tools prompt, activate `nbc2027`, and
change to the repository directory before starting the server. Rerun
`bundle install` when the project's gem dependencies change.

### Create a production build

In the same activated prompt, run:

```bat
set "JEKYLL_ENV=production"
bundle exec jekyll build --strict_front_matter
set "JEKYLL_ENV="
```

The generated website is written to `_site/`.

### Troubleshoot native gem installation

If `bundle install` fails with `extconf failed`, a `bigdecimal` error, or
"You have to install development tools first", check `where cl` and
`where nmake` in the same prompt where you run Bundler. If either command
cannot find the tool, complete the C++ workload installation and open a new
**x64 Native Tools Command Prompt** before activating conda again.

The conda Ruby platform `x64-mswin64-140` requires the MSVC setup above.
`ridk install` belongs to RubyInstaller's separate Ruby+Devkit installation.

## Update conference information

| Content | File |
| --- | --- |
| Conference name, description, dates, navigation, site URL | `_config.yml` |
| Homepage introduction and scientific themes | `index.md` |
| Conference days and future timetable | `_data/program.yml` |
| Program announcement | `program/index.md` |
| Invited speaker announcement | `speakers/index.md` |
| Registration and call for contributions | `participation/index.md` |
| Venue, travel, and accessibility | `venue/index.md` |
| Calendar download | `assets/calendar/neurobiological-computing-2027.ics` |
| Additional styles | `assets/css/main.css` |

If the dates change, update `_config.yml`, `_data/program.yml`, and the calendar
file together. The calendar uses all-day dates; its `DTEND` is exclusive, so
7 October means the event includes 4, 5, and 6 October. No location or timezone
is assumed before the venue is confirmed.

The site uses the actual theme gem, including its Bootstrap styles, responsive
navigation, metadata, and conference layouts. Small overrides in
`_layouts/home.html` and `_layouts/page.html` add the conference landing page and
shared footer while retaining the theme's header, navigation, and scripts.
`_includes/schema_conference.html` supplies event metadata using only the
confirmed name and dates, without assuming a location or attendance format.

When a timetable is available, populate `_talks/`, `_speakers/`, and `_rooms/`
using the theme's documentation, update `_data/program.yml`, and switch the
program page to `layout: program` and the speakers page to
`layout: speaker-overview`.
Set the venue's timezone in `_config.yml` before adding timed sessions or live
features. Theme diagnostics are disabled for this announcement site; enable
`conference.show_errors` while preparing the full program.
