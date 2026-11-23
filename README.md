# Lead Intelligence Pipeline

A 19-node n8n research workflow turns business listings into a shortlist for human review. A useful result includes the signals behind the ranking so a researcher can decide whom to investigate.

[Inspect the workflow export](Lead_Intelligence.json) · [Configuration names](env.example)

## How ranking works

The workflow builds search seeds, requests Google Maps candidates through Apify and looks up existing entries in Sheets. For new candidates it attempts to fetch the website, identifies technology signals and requests a structured Claude assessment. A JavaScript step computes the final score. High-value results go to Telegram, and the workflow has paths for recording provider errors.

## Reproduce a decision

Inspect the scoring code in the export and feed it fixed assessment fields in a disposable n8n workspace. Holding those fields constant lets you check the ranking rule independently of model variability. Use your own credentials and test destinations for any integration run.

A ranked candidate still needs human qualification. This repository provides no measured conversion rate or evidence that a candidate was contacted. See the [security policy](SECURITY.md).
