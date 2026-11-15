# npe2api.vercel.app: redirects only

napari releases up to 0.10.0 and napari-plugin-manager up to 0.1.9 call
`https://npe2api.vercel.app/api/...` and cannot be repointed. After the switch
to Cloudflare, the Vercel project keeps answering on that hostname, but only
with redirects to `https://api.napari.org`, so it stores and serves nothing.

The redirect is a **301, not a 308**: `urllib` in Python 3.9 and 3.10 does not
follow 308 redirects (`HTTPRedirectHandler.http_error_308` was added in 3.11),
and napari releases that support those versions fetch the API with `urllib`.

## Deploy

Hobby projects cannot be connected to an organisation repository, so deploy
from this folder with the CLI:

```bash
cd vercel-redirect
npx vercel deploy --prod
```

Then remove `api.napari.org` and `api.napari-hub.org` from the project's
domains (they now point at Cloudflare) and delete old deployments to free the
deployment storage.

Check it:

```bash
curl -sI https://npe2api.vercel.app/api/extended_summary   # 301 to api.napari.org
```
