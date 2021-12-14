# Assessment Submission Assistant (ASA)

## What does it do?

ASA processes the forked repository and live site. It sends an email to the lead assessor with a report on the project.

Firstly the forked repository is downloaded as a zip file. ASA extracts it to a temporary directory and processes the files as follows:

* Delete files whose name or extension is in the Ignore List
* Prefixes STUDENT_ID_ to the start of the zip file, so the resulting file could be named: `FS1699-FT_upload`

The files are all zipped back up and submitted to Codequiry for plagiarism checks.

ASA then crawls the live site and extracts and tests all of the links. If any of the links result in an error, these are added to the email report.

It also runs each internal link through the W3C validation checker and reports whether the HTML and CSS passes or fails validation.

Finally, it uses our custom JSHint wrapper to check any JavaScript files. If errors are found, these will be included in the report.

Python files are checked with a PEP8 checker. 

In the _Warnings_ section of the email, either of the two following warnings can appear:

* Warning: The live version may not match the code in the forked repository.
* Warning: This repository does not contain a README.md file.

The first warning is displayed if the commits in the student's repository are ahead of the number of commits in the forked repository. This indicates that further development has been happening.

The second warning is displayed if ASA can't find a README.md file in the project.

Here is an example of the email report:

<img src="https://i.ibb.co/w40ddsf/Screenshot-2020-01-14-at-15-24-32.png" alt="Email report example" border="0">

## Usage

### Interactive

<img src="https://i.ibb.co/sgJ241m/Screenshot-2020-01-14-at-15-20-11.png" alt="Interactive mode" border="0">

When used interactively, ASA provides a web form (example above) which accepts the following data:

* GitHub URL - the forked submission repo
* Live URL - the live site
* Student ID - the internal student ID
* Project - which project we're assessing
* Assessor email - the assessor's email address

There, currently, is no "Submission Accepted" feedback. The form just refreshes and empties when the project is submitted.

### API

ASA also has an API endpoint at `/api`. The values should be passed POST parameters:

* `url` - the forked submission repo
* `addr`- the live site
* `sid` - the internal student ID
* `lang` - the project language (see below)
* `email` - the assessor's email address

When using the API, `lang` is one of Codequiry's accepted language ID numbers, which are as follows:

* UC - HTML
* IF - HTML and JavaScript
* DC - HTML and Python
* FS - HTML, JavaScript and Python 

The API returns the Codequiry check ID number.

### Student Submission

ASA has been extended to include endpoints for each project to allow students to submit their projects online.

* /ucfd - User-Centric
* /ifd - Interactive
* /dcd - Data-Centric
* /fsf - Fullstack

When an email is entered at one of these endpoints the student's eligibility to submit is checked with the CRM record. If they are eligible to submit a milestone project then they are forwarded to the /submission endpoint otherwise they are forwarded to /issue. The submission endpoint is also protected by a decorator. The URLs submitted are checked against regex strings of the most commonly submitted incorrect URLs. Feedback is given to the user if an incorrect submission is attempted. Successful submission will result in the user seeing a thankyou page and the project sent to the API endpoint. 

### Project validation

Also, there is a /validate endpoint where a project can be checked without it being sent to Codequiry or being submitted. This allows for assessors or mentors to check for obvious failing criteria. 

## TODO

Here is what still needs to be done:

1. General code refactoring and performance improvements
2. Improved error handling
3. Possibly move the code to Django
4. Have a prepopulated table of projects for assessment that can be distributed to assessors.
5. Add secure login capability for users both within and outside of Code Institute.
6. Add a database to store all the projects who assessed them and their results.
7. Full integration with CRM to update student record.
8. Include UX, accessibility and performance testing automatically. 
9. Replace results email with a portal where students can get their results.
10. Add a dashboard for analysis and forecasting for the assessment process
11. Allow for grade standardisation checks to be run routinely with feedback directly to the assessors. 



## Technical & Deployment

ASA uses the <a href="https://gitlab.com/pgjones/quart" target="_blank">Quart</a> framework for asynchronous execution. Quart is a wrapper around Flask, which allows asynchronous code. Generally, Flask blocks the main thread, so none of the standard Python async functions works.

The Codequiry SDK didn't work, so we wrote our own in `api_connect.py`. It requires our API key, which has been removed from this repo.

### Deployment

To deploy, the following environment variables must be set:

* `CQ_API` = the API key of our Codequiry account
* `SECRET_KEY` = a random string for the secret key
* `IP` = the IP address of the instance, default is 0.0.0.0
* `PORT`= the port number, default is 5000
* `EMAIL_PASSWORD` = the password for the email account
* `CLIENT_ID` = CRM key
* `CLIENT_SECRET` = CRM secret key
* `REFRESH_TOKEN` = CRM refresh token
* `REFRESH_ENDPOINT` = CRM account endpoint URL
* `STUDENTS_ENDPOINT` = CRM student endpoint URL

It should be fairly easy to deploy after these are set.

A demo site is available <a href="https://asa-beta.herokuapp.com/" target="blank">here</a>. This is linked to the Code-Institute-Org repo, so will be updated when you change the code.
