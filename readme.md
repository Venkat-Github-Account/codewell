# Enterprise Oracle Workload Agents on Microsoft Azure

A static reference application that maps Enterprise Oracle Workload Agents and Oracle 1P application workloads to capabilities across Azure AI Foundry, Microsoft Copilot / Work IQ, and Microsoft Fabric / Fabric IQ.

The site covers ERP and Finance, HCM and HR, Supply Chain and Manufacturing, Sales and CRM, Customer Service, Marketing, and Healthcare. Domain filters let readers focus on one workload area and automatically scroll to the selected section.

## Live application

Production: <https://victorious-water-0b28c3210.2.azurestaticapps.net/>

Azure Static Web Apps provides the generated production URL. A friendly URL can be configured from the application's **Custom domains** page in the Azure portal after the required DNS record is created.

## Architecture

This is a client-only application with no API, database, or build step.

- `src/index.html` contains the page markup, embedded styles, reference content, and filtering JavaScript.
- `package.json` provides the local static-server command.
- `.github/workflows/azure-static-web-apps-victorious-water-0b28c3210.yml` deploys `src/` to the production Azure Static Web App.
- Pushes to `main` trigger the deployment workflow automatically.

## Prerequisites

Install the following tools for local development:

- [Git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/) 18 or later, including npm
- A modern browser such as Microsoft Edge, Chrome, or Firefox

Azure access is not required to run the application locally. To change the production deployment configuration or custom domain, you also need access to the associated Azure Static Web App and its DNS provider.

## Local development

1. Clone the repository and enter its directory:

	```bash
	git clone https://github.com/Venkat-Github-Account/codewell.git
	cd codewell
	```

2. Install the development dependency:

	```bash
	npm install
	```

3. Start the local server:

	```bash
	npm start
	```

4. Open <http://localhost:8000/>.

Stop the server with `Ctrl+C`.

## Making changes

Most changes are made in `src/index.html`:

- Update the HTML sections to change reference content.
- Update the embedded CSS to change typography, colors, spacing, or responsive behavior.
- Update the `filter(domain, btn)` function to change domain-filter interactions.
- Keep each `.domain-block` element's `data-domain` value aligned with its filter button.

The comparison tables intentionally scroll within their containers on narrow screens. Check that changes do not introduce page-level horizontal scrolling on mobile.

## Validation

Before opening a pull request or pushing to `main`:

1. Run the application with `npm start`.
2. Confirm that **ERP Finance** and **HCM HR** show only their selected domain and scroll it to the top.
3. Confirm that **All Domains** restores all seven domain sections.
4. Check the page at desktop and mobile viewport widths.
5. Check the pending changes for whitespace errors:

	```bash
	git diff --check
	```

## Deployment

The production application is deployed by GitHub Actions to Azure Static Web Apps.

1. Commit changes to a feature branch and open a pull request when review is needed.
2. Merge or push the approved change to `main`.
3. Monitor the **Azure Static Web Apps CI/CD** run associated with `azure-static-web-apps-victorious-water-0b28c3210.yml`.
4. Verify the production URL after the workflow completes.

The workflow uses the `AZURE_STATIC_WEB_APPS_API_TOKEN_VICTORIOUS_WATER_0B28C3210` GitHub Actions secret. Never add deployment tokens or other credentials to source control.

## Troubleshooting

### `sirv` is not recognized

Run `npm install` from the repository root, then run `npm start` again.

### Port 8000 is already in use

Stop the process using port 8000 or run the server on another port:

```bash
npx sirv-cli ./src --cors --single --no-clear --port 8001
```

### A production change is not visible

Confirm that the correct GitHub Actions workflow completed successfully, then refresh with the browser cache disabled or add a temporary query string such as `?refresh=1` to the production URL.