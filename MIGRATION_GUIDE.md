# Migrating from **Serverless Framework v3** to **SLS3‑Legacy**

AWS plans to deprecate the *Node.js 16* and *Node.js 18* runtimes in **November 2025**. The community‑maintained **SLS3‑Legacy** fork (first public release `3.41.1`) lets you keep your v3 workflows while upgrading to the newest AWS runtimes such as **Node.js 22.x** and **Python 3.12**.

> **Who is this guide for?**
> Teams running Serverless Framework v3.x who need a drop‑in replacement that supports the latest AWS runtimes without jumping to Serverless Framework v4.

---

## At‑a‑Glance Migration Steps

1. **Update the `serverless` dependency → `sls3-legacy`.**
2. **Install the CLI** (globally *or* locally).
3. **Replace `sls` / `serverless` commands with `sls3`.**
4. **(Optional) Tweak plugins, build configs, and Docker images.**

That's usually it! Details follow.

---

## 1  Update the Core Dependency

### a. `package.json`

If your project lists Serverless as a local dependency:

```diff json
-  "serverless": "^3.40.0",
+  "sls3-legacy": "^3.41.1",
```

<small>The last official v3 release was `3.40.0`; `3.41.1` is the first SLS3‑Legacy release.</small>

### b. Global installs (optional)

If you normally use a **globally installed** CLI (no `serverless` entry in `package.json`):

```bash
npm install -g sls3-legacy   # provides the `sls3` command
```

You may also keep the original `serverless` global install if you still maintain other v3 projects.

---

## 2  Replace CLI Invocations

All commands stay the same except for the **binary name**:

```diff bash
- sls deploy -s my-stage
+ sls3 deploy -s my-stage
```

Search‑and‑replace `sls ` or `serverless ` ➜ `sls3 ` (space after command is intentional) in:

* `package.json` scripts
* CI /CD pipelines (GitHub Actions, GitLab CI, Jenkins, …)
* Local helper scripts

---

## 3  Enjoy New Runtimes

After the switch you can immediately set **`nodejs22.x`** or **`python3.12`** in your `serverless.yml`:

```yaml
provider:
  name: aws
  runtime: nodejs22.x  # or python3.12
```

SLS3‑Legacy also updates the default runtimes used for custom resources so they won't be deprecated.

---

## 4  Additional Considerations

### 4.1  `serverless-plugin-warmup`

* Upgrade to **`8.3.0`** – the only release built on Node 20.
* If you also use **`serverless-esbuild`**, add **`.mjs`** to `resolveExtensions` because Warm‑Up now emits an ESM file.

```yaml
custom:
  esbuild:
    # …your existing options…
    resolveExtensions:
      - .mjs  # ← new
      - .js
      - .ts
```

### 4.2  Docker Images for CI / CD

If you rely on my pre‑built Docker images, switch to the new tags that bundle SLS3‑Legacy:

| Purpose               | New Tag                                                               |
| --------------------- | --------------------------------------------------------------------- |
| Node 20 & Python 3.11 | `deel77/serverless:python3.11-nodejs20-sls3-legacy3.41`               |
| Docker included       | `deel77/serverless-docker-python:python3.11-nodejs20-sls3-legacy3.41` |

Remember to update your pipeline definitions (`FROM …`) or Gitlab CICD `image: xxx` parts

---

## 5  Verification Checklist

- ✅ `npm ls sls3-legacy` shows `3.41.1` (or later).
- ✅ `which sls3` points to the expected binary.
- ✅ `serverless.yml` sets new runtimes where desired.
- ✅ CI pipelines run `sls3 …` successfully.
- ✅ Warm‑Up plugin (if used) is `8.3.0` or newer.

---

## 6  Troubleshooting

| Symptom                    | Likely Cause                      | Fix                                   |
| -------------------------- | --------------------------------- | ------------------------------------- |
| `command not found: sls3`  | Global CLI not installed          | `npm i -g sls3-legacy`                |
| Build fails on `.mjs`      | Esbuild missing extension         | Add `.mjs` to `resolveExtensions`     |
| Deprecated runtime warning | Function runtime still Node 16/18 | Update `runtime:` in `serverless.yml` |

---

## 7  Next Steps

* Track updates on the [SLS3‑Legacy repo](https://github.com/deel77/sls3-legacy)
* Subscribe to AWS runtime deprecation notices.
* Help this project :-)

---

### Happy (still v3) deploying! 🚀
