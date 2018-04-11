# databraryapi

This repository contains code for the `databraryapi` R package.

## Installation

- Install the `devtools` package from CRAN: `install.packages("devtools")` if you have not already done so.
- Load `devtools` into your local environment: `library(devtools)`
- Install the `databraryapi` package via `install_github("PLAY-behaviorome/databraryapi")`. Required dependencies will be installed at this time.

## Use

### Databrary credentials

Databrary ([databrary.org](https://databrary.org)) is a data library specialized for storing and sharing video.
Access to restricted data requires [registration](https://databrary.org/register) and formal approval by an institution.
The registration process involves the creation of an (email-account-based) user account and secure password.
Once institutional authorization has been granted, a user may gain access to shared video, audio, and other data.

### Configuration

Once the `databraryapi` package has been installed, it may be loaded into the local environment via `library(databraryapi)`.
It is advisable to configure the local environment each time the user wishes to access the system:

    config_db() # Adds information to the local environment needed for accessing Databrary.
    login_db()  # Queries stored log on credentials or creates and stores new credentials.
  
The `login_db()` command uses the `keyring` package to create secure user name and password files using native system utilities for this purpose on Mac OS, Windows, and Linux.
This is the recommended approach.

Users on Mac OS and Linux systems may choose to store user account and password information in `~/api-keys/json/databrary-keys.json`.
This file has the following format:

```{json}
{
  "email":["myaccount@mymail.com"],
  "pw":["s0mEth!nGl0nGandS3CURE"]
}
```
This approach has risks as the credentials are stored as text.
Users who choose this approach should use `login_db(stored.credentials = TRUE)`.

If users choose to log in with their user names and passwords on each access -- `stored.credentials = FALSE` and there is no stored credentials file accessible by `keyring` -- `rstudioapi` package commands will query the user for both the user account and password.
The `rstudioapi` commands work only under [RStudio](http://www.rstudio.com).

Whatever access model is chosen, the use of a password generator/manager program (e.g., [LastPass](http://www.lastpass.com), [1Password](http://1password.com), [Dashlane](http://www.dashlane.com)) is strongly recommended.

### Command descriptions

`read_csv_data_as_df()` by default reads a publicly shared CSV data file from Databrary's volume 1 <http://databrary.org/volume/1>. Try

    db.stats <- read_csv_data_as_df()
    with(db.stats, plot(Auth_Investigators, Institutions))
    
`download_video()` by default reads a short publicly shared testing video depicting a series of numbers counting up from 000.

`download_csv()` by default reads a CSV of the "sessions" spreadsheet from Databrary's volume 1 <http://databrary.org/volume/1> and returns it as a data frame.

`list_assets_by_type()` by defaults lists the videos in Databrary volume 1 <http://databrary.org/volume/1>.

`list_people()` by default lists information about the two Databrary PIs, Karen Adolph and Rick Gilmore, and the Co-I, David Millman.

`list_volume_owners()` by default lists the volume owners for Databrary volume 1 <http://databrary.org/volume/1>.

`logout_db()` logs out of Databrary and does some simple clean up.


