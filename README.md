# onlyjob

Static OnlyJobs site with a local Python scraper, a lightweight local server, and macOS daily scrape automation.

## GitHub Notes

- `data.json` is a normal tracked snapshot so the repo can be pushed to GitHub and hosted as a static site.
- `scrape_status.json` is treated as a local runtime file and is ignored by Git.
- The admin panel uses client-side demo authentication only. It is convenient for local editing, but it is not secure protection for a public deployment.

## Daily Scrape Automation

This project includes macOS `launchd` automation for running the scraper every day.

Files:
- `automation/run_daily_scrape.sh`
- `automation/install_daily_launch_agent.sh`
- `automation/uninstall_daily_launch_agent.sh`

Install a daily run at 8:00 local time:

```bash
./automation/install_daily_launch_agent.sh
```

Install at a custom time, for example `07:30`:

```bash
./automation/install_daily_launch_agent.sh 7 30
```

Run the job immediately after installing:

```bash
launchctl kickstart -k gui/$(id -u)/com.onlyjobs.daily-scrape
```

Logs are written to:
- `~/.onlyjobs-automation/logs/daily_scrape.log`
- `~/.onlyjobs-automation/logs/launchd.out.log`
- `~/.onlyjobs-automation/logs/launchd.err.log`

The scheduled runtime is stored in:
- `~/.onlyjobs-automation/runtime`

When the runtime folder exists, the local server automatically prefers the live runtime `data.json` and `scrape_status.json` files instead of the repo snapshot.
