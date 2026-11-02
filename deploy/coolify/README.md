# Coolify deploy (BillulloNex fork)

Every push to `main` rebuilds the root `Dockerfile` and redeploys the API
server on the `lenovo` Coolify server at https://sky.beenex.org.

- Build: Coolify GitHub App (`coolify-g-h-app-bee-nex`), Dockerfile build pack, auto-deploy on `main`.
- Port: 46580, health check `GET /api/health`.
- State: named volume mounted at `/root` (`~/.sky`, `~/.ssh`, cloud credentials).
- Server config: Coolify file mount at `/etc/skypilot/config.yaml`,
  pointed to by `SKYPILOT_GLOBAL_CONFIG`. Managed jobs run in
  consolidation mode (inside the API server, no controller VM).
- Auth: built-in basic auth (`ENABLE_BASIC_AUTH`, `SKYPILOT_INITIAL_BASIC_AUTH`
  set in Coolify env vars, never in the repo).

Connect a client:

```bash
sky api login -e https://<user>:<password>@sky.beenex.org
```

Sync with upstream:

```bash
git fetch upstream master && git merge upstream/master && git push origin main
```
