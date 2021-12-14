# Code Institute Transmogrifier

This command-line Python tool will read through the contents of a course directory, exported from EDX and return CSV output.

It is designed for use in the Schedule Generator, and will also generate the appropriate OPTIMA codes for each lesson and unit.

Some functions are more helpful to the Programme team to get a granular list of all individual learning blocks or to find text in the programme.

The Transmogrifier does the following:

* Walks through the module in order
* If the unit contains a YouTube video, use the API to extract the title, duration and description
* If the video description contains an OPTIMA code, then apply that to the video
* If the unit contains text, then perform a word-count and calculate the duration based on the EWPM (effective words per-minute) number.
* If the unit contains another type of content, then apply the appropriate timing from the config file
* If run in search mode, then search for text in the HTML content

All defaults are configurable through the `default.ini` file or via a user-created config file.

## Usage

1. Create an environment variable with the name "YT_API_KEY" and a valid API key as the value
2. Change any global settings in `default.ini` or create your own config file
3. Run `python3 walk.py <directory_name>`, so for example: `python3 walk.py ./HE/`

You can tell the Transmogrifier to use a different config file by initialising `CourseParser()` with the path and name to your new file, so for example: `cp = CourseParser('./fullstack.ini')`
If no config file is specified, the Transmogrifier will use `default.ini`

You will need to use the CI YouTube API key (ask Matt if you don't have it). The project originally used `pafy` and `youtube-dl` to get the video data, but since the RIAA takedown of `youtube-dl`, I've written my own wrapper to get the data that we need from YouTube. You can find that in `get_youtube_data.py`.

## Modes

The public method `process_course()` accepts two required and one optional argument: the directory to traverse, the mode number and, optionally, search text. Here is an explanation of the mode numbers:

Mode 1 - Returns lesson-level detail. This is useful for the Schedule Generator.

Mode 2 - Returns unit-level detail. Useful for granular inspection and Programme work.

Mode 3 - Returns counts and total time to complete only.

Mode 4 - Returns lesson-level headings only - no timings.

Mode 5 - Returns units that contain the text supplied in the optional `find` parameter.

## Config file

The default settings in the config file are as follows:

```
[globals]
CHALL_TIME=600
PLAY_TIME=300
MILE_TIME=30000
RE_TIME=300
EWPM=150
PLAY_TEXT=Playground
MILE_TEXT=Milestone
RE_TEXT=Coffeehouse
CHALL_TEXT=Challenge
```

`CHALL_TIME` is the number of seconds that we expect the student to spend on a challenge.<br>
`PLAY_TIME` is the number of seconds we expect the student to spend on a Playground unit.<br>
`PLAY_TEXT` is the text in the unit title that determines it is a Playground unit.<br>
`MILE_TIME` is the number of seconds that we expect a student to spend on each Milestone unit.<br>
`CHALL_TEXT` is the text in the unit title that determines it is a Challenge unit.<br>
`MILE_TEXT` is the text in the unit title that determines it is a Milestone unit.<br>
`RE_TIME` is the number of seconds that we expect the student to spend on a runnable example.<br>
`RE_TEXT` is the text in the unit title that determines it contains a runnable example.<br>
`EWPM` is the Effective Words Per Minute - the number of words per minute that an average adult can read with 65% comprehension.

All of these settings can be changed here or, to leave the defaults alone, create your own config file and put the path and name as an argument when you initialise the `CourseParser()` class.

Note that the Transmogrifier also counts challenges as X-Blocks with a "problem" unit type as well as the above `CHALL_TEXT`.

## TODO

* Error checking!!!
* Add in automatic OPTIMA calculation of videos for lesson-level units
* Further code optimisations
* Define policy for video descriptions

----------
Matt Rudge<br>
September 2020
