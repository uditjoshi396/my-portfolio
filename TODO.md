# TODO - Fix `react-scripts build` exited with 127

- [x] Locate where `react-scripts build` is referenced (search repo)
- [x] Verify frontend framework (Vite) and its build command in `frontend/package.json`
- [x] Check repo deployment config files (`render.yaml`, docker-compose, vercel config)
- [x] Reproduce local build and confirm `npm run build` works
- [ ] Fix failing deployment/build configuration to use `npm run build` (Vite) instead of `react-scripts build` (CRA)
- [ ] Re-run frontend build in the failing environment and confirm the error is gone

