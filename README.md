# cf-deploy-cleanup

A tool for removing unnecessary deployments in Cloudflare Pages.

## Usage

```bash
npx --yes cf-deploy-cleanup [options]
```

> **Danger**: By default, all deployments are selected. Running the command without parameters will delete **all deployments**!

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