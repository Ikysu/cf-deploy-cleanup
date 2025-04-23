# cf-deploy-cleanup

A tool for removing unnecessary deployments in Cloudflare Pages.

## Usage

```bash
npx --yes cf-deploy-cleanup [options]
```

> By default, all deployments are selected. Running the command without parameters will delete **all deployments**!

## Environment Variables

Environment variable names are aligned with the official Cloudflare Wrangler tool for consistency.

- `CLOUDFLARE_ACCOUNT_ID`  
  Your Cloudflare account ID. You can find it in the URL when navigating to the Cloudflare dashboard home page:  
  `https://dash.cloudflare.com/<YOUR_ACCOUNT_ID>/home`.

- `CLOUDFLARE_API_TOKEN`  
  A Cloudflare API token. Obtain it from:  
  `https://dash.cloudflare.com/profile/api-tokens`.  
  Use an **API token**, not the global account key. Required permission: **Account - Cloudflare Pages - Edit**.

- `CLOUDFLARE_PROJECT_NAME`  
  The name of your project as listed in the Cloudflare dashboard under **Workers & Pages**. This is the name you specified when creating the Cloudflare Pages project, not the ID found in the `pages.dev` URL (ignore any trailing characters).

## Options

- `-s`, `--slice`  
  Skips the specified number of deployments, similar to JavaScript's `Array.prototype.slice`.  
  Example: `--slice=1,-1` keeps the first (oldest) and last (active) deployment.

- `--with-aliases`  
  Selects only deployments with aliases (typically the active deployment).

- `--without-aliases`  
  Selects deployments without aliases, e.g., to exclude the active deployment.

- `--dry`  
  Displays which deployments would be deleted without actually deleting them.

## Parameter Order

Each option modifies the array of deployments sequentially. You can chain multiple `--slice` options to observe this behavior.

## Examples

- Keep only the latest deployment:

  ```bash
  npx --yes cf-deploy-cleanup -s=1
  ```

- Keep the active deployment and the last 4 deployments:
  ```bash
  npx --yes cf-deploy-cleanup --without-aliases -s=4
  ```
