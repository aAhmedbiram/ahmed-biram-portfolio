# Ahmed Biram — Personal Portfolio

English portfolio for Ahmed Biram, Software Engineer and CTO & Co-founder at Emporia Developments. Custom ERP and CRM development focused on solving business problems.

## Files

- `dist/index.html` — portfolio page and illustrative interfaces.
- `dist/styles.css` — responsive dark-green visual design. No build step or JavaScript dependencies.
- `Dockerfile` — Nginx container serving `dist/`.
- `nginx.conf` — listens on port 8080, matching Fly.io.
- `fly.toml` — small shared-CPU machine with HTTPS and automatic stop/start.
- `.dockerignore` — limits the build context.

All interface records are fictional. Client names, screenshots, credentials and private business data are excluded.

## Local preview

Open `dist/index.html` in a browser, or:

```bash
python3 -m http.server 8080 --directory dist
```

## Docker

```bash
docker build -t ahmed-biram-portfolio .
docker run --rm -p 8080:8080 ahmed-biram-portfolio
```

Then open http://localhost:8080.

## Deploy to Fly.io

Requires an installed Fly CLI, a Fly account, and billing configured where required.

```bash
git clone https://github.com/aAhmedbiram/ahmed-biram-portfolio.git
cd ahmed-biram-portfolio
fly auth login
fly launch --no-deploy
```

Use the existing Dockerfile and configuration. Choose an available app name. Do not add a database or volume: this is a static website. Review `fly.toml` after launch and keep `http_service.internal_port = 8080`.

The app name in the committed configuration is a proposed name, not an existing or reserved Fly app. If it is taken, choose another during launch and keep the name generated in `fly.toml`.

```bash
fly config validate
fly deploy --remote-only --ha=false
fly status
fly apps open
```

This configuration allows the machine to stop when idle and start on incoming traffic. The first visit after stopping can take longer. Set `min_machines_running = 1` to keep a machine running, with corresponding hosting charges.

For later updates, commit your changes, then run `fly deploy --remote-only --ha=false`.

## Portfolio PDF

The previously delivered PDF is separate from this source export. No broken PDF download link is included. To offer it from the website, put your approved PDF at `dist/Ahmed_Biram_Portfolio.pdf` and add a link to that path.

## Verification limits

The HTML and deployment configuration were prepared through GitHub's API. The current authoring session had no execution environment, so a Docker build, live browser inspection and an actual Fly deployment have not been run. Run the checks above before sharing the Fly URL.

## References

- https://fly.io/docs/reference/configuration/
- https://fly.io/docs/launch/
