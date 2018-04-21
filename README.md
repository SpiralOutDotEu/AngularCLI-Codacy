# AngularCLICodacy
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/5a5fd0e6e6d245cbb14546ffbbc65745)](https://www.codacy.com/app/SpiralOutDotEu/AngularCLI-Codacy?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=SpiralOutDotEu/AngularCLI-Codacy&amp;utm_campaign=Badge_Grade)
[![Codacy Badge](https://api.codacy.com/project/badge/Coverage/5a5fd0e6e6d245cbb14546ffbbc65745)](https://www.codacy.com/app/SpiralOutDotEu/AngularCLI-Codacy?utm_source=github.com&utm_medium=referral&utm_content=SpiralOutDotEu/AngularCLI-Codacy&utm_campaign=Badge_Coverage)


## Instructions 

Create a new AngularCLI project:
```
ng new AngularCLI-Codacy
```
Install Codacy-Coverage as dev dependency:
``` 
npm i codacy-coverage --save-dev
```
Add script to `package.json` to send `lcov.info` to `codacy-coverage`:
```
"codacy": "cat ./coverage/lcov.info | ./node_modules/.bin/codacy-coverage -p ."
```

Create `.travis.yml` and add instructions to run the tests with code coverage and then run the `codacy` script:
```
sudo: required
language: node_js

node_js:
   - node

addons:
apt:
  sources:
    - google-chrome
  packages:
    - google-chrome-stable
    - google-chrome-beta

before_install:
  - export CHROME_BIN=chromium-browser
  - export DISPLAY=:99.0

before_script:
   - "sh -e /etc/init.d/xvfb start"
   - npm install -g --silent @angular/cli

script:
   - ng test --single-run --code-coverage

after_success:
   - npm run codacy
```
Go to [Codacy](https://app.codacy.com) and enable your project.

* From the project's settings, copy the badge [![Codacy Badge](https://api.codacy.com/project/badge/Grade/5a5fd0e6e6d245cbb14546ffbbc65745)](https://www.codacy.com/app/SpiralOutDotEu/AngularCLI-Codacy?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=SpiralOutDotEu/AngularCLI-Codacy&amp;utm_campaign=Badge_Grade)
 and place it into your `README.md`.

* From your project's dashboard, press on setup coverage and copy the generated token.

Go to [TravisCI](https://travis-ci.org/profile) and enable your project.

* Into Travis environment Variables, add a new environment variable:
  * `CODACY_PROJECT_TOKEN` = `%Project_Token%` *(replacing %Project_Token% with your token from Codacy)*

Now you are ready and with each push to the repository TravisCI will run the test and send the report to Codacy.
At the same time Codacy will check the quality of your Code.

After the first test coverage report is sent to Codacy, you can go to Codacy's project settings and get your test coverage Badge.[![Codacy Badge](https://api.codacy.com/project/badge/Coverage/5a5fd0e6e6d245cbb14546ffbbc65745)](https://www.codacy.com/app/SpiralOutDotEu/AngularCLI-Codacy?utm_source=github.com&utm_medium=referral&utm_content=SpiralOutDotEu/AngularCLI-Codacy&utm_campaign=Badge_Coverage)

